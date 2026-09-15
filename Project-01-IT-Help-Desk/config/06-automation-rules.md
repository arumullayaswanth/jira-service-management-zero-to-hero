# 06 — Automation Rules

Reference for [DEPLOY.md Part 10](../DEPLOY.md#part-10--build-the-automation-rules).

Every rule is `WHEN → IF → THEN`.

⚠️ Free plan: 100 rule runs per month per site. These 8 rules are lightweight, but watch the usage page. ([Jira plans](https://www.atlassian.com/software/jira/guides/more/jira-editions)) *Content was rephrased for compliance with licensing restrictions.*

---

## Rule 1 — Auto set priority from impact

| | |
| --- | --- |
| **Trigger** | Work item created |
| **Condition** | Work item fields condition → `Impact Level` |
| **Action** | Edit work item → `Priority` |

| If Impact Level = | Then Priority = |
| --- | --- |
| Whole office | Highest |
| My team | High |
| Only me | Medium |

Use an **If/else block** if your plan has it, otherwise three separate rules.

Overrides (separate rules, run after):

| Request type | Priority |
| --- | --- |
| Password Reset, VPN Issue | High |
| Laptop Request, Software Installation | Low |

---

## Rule 2 — Auto-assign by request type

| | |
| --- | --- |
| **Trigger** | Work item created |
| **Condition** | Request Type is one of … |
| **Action** | Assign work item |

| Sub-rule | Request types | Assignee |
| --- | --- | --- |
| 2a | Laptop Issue, Laptop Request, Wi-Fi Issue | agent2 |
| 2b | Access Request, Password Reset, Software Installation | agent3 |
| 2c | Email Issue, VPN Issue, General IT Support | you |

**Better option:** Assign work item → *Balanced workload* → role `Service Desk Team`. Spreads load instead of hard-coding people who go on holiday.

---

## Rule 3 — Welcome comment

| | |
| --- | --- |
| **Trigger** | Work item created |
| **Condition** | *(none)* |
| **Action** | Comment on work item — **Share with customer** |

```text
Hi {{reporter.displayName}},

Thanks for contacting the Nimbus IT Help Desk 👋

We've logged your request as {{issue.key}}.
Priority: {{issue.priority.name}}
We'll respond within our target time for this priority.

Track it here: {{issue.url.customer}}

— Nimbus IT
```

---

## Rule 4 — Auto start work on agent comment

| | |
| --- | --- |
| **Trigger** | Work item commented |
| **Condition 1** | User condition → user is in role `Service Desk Team` |
| **Condition 2** | Work item fields → Status equals `Open` |
| **Action** | Transition work item → `In Progress` |

Fixes the most common agent habit: replying but never moving the status.

---

## Rule 5 — Customer replied, resume work

| | |
| --- | --- |
| **Trigger** | Work item commented |
| **Condition 1** | User condition → user is `Reporter` |
| **Condition 2** | Status equals `Waiting for Customer` |
| **Action 1** | Transition work item → `In Progress` |
| **Action 2** | Comment (internal): `Customer replied at {{now}} — please review.` |

Without this rule, customer replies sit in a paused status forever and the SLA never resumes.

---

## Rule 6 — Escalate before SLA breach

| | |
| --- | --- |
| **Trigger** | SLA threshold breached → `Time to resolution` → **will breach in 30 minutes** |
| **Action 1** | Edit work item → add label `sla-at-risk` |
| **Action 2** | Comment (internal): `⚠️ SLA breaches in 30 minutes. {{issue.key}} — {{issue.summary}}` |
| **Action 3** | Send email → project lead → `SLA risk: {{issue.key}}` |

Escalate **before** the breach, not after. After is just a report of failure.

---

## Rule 7 — Auto-close resolved after 3 days

| | |
| --- | --- |
| **Trigger** | Scheduled → daily |
| **JQL** | `project = ITHD AND status = Resolved AND updated <= -3d` |
| **Action 1** | Comment (public): closing notice |
| **Action 2** | Transition work item → `Closed` |

---

## Rule 8 — Nudge silent customers

| | |
| --- | --- |
| **Trigger** | Scheduled → daily |
| **JQL** | `project = ITHD AND status = "Waiting for Customer" AND updated <= -5d` |
| **Action** | Comment (public): reminder + 2-day warning |

Optional companion rule at `-7d` → transition to Closed with Resolution `Won't Do`.

---

## Smart values you will actually use

| Smart value | Result |
| --- | --- |
| `{{issue.key}}` | ITHD-42 |
| `{{issue.summary}}` | Laptop won't boot |
| `{{issue.priority.name}}` | High |
| `{{issue.status.name}}` | In Progress |
| `{{issue.assignee.displayName}}` | Agent name |
| `{{reporter.displayName}}` | Customer name |
| `{{reporter.emailAddress}}` | Customer email |
| `{{issue.url.customer}}` | Portal link (give this to customers) |
| `{{issue.url}}` | Agent link (internal only) |
| `{{issue.Impact Level}}` | Custom field value by name |
| `{{now}}` | Current timestamp |
| `{{now.plusDays(3)}}` | Date maths |
| `{{issue.created.format("dd MMM yyyy")}}` | Formatted date |

---

## Debugging automation

Open the rule → **Audit log**. It tells you the truth.

| Audit message | Meaning | Fix |
| --- | --- | --- |
| `No actions performed` | A condition failed | Check field values and exact spelling |
| `Error editing work item` | Actor lacks permission | Set actor to `Automation for Jira` |
| Rule not listed at all | Rule is off, or trigger never fired | Toggle it on; verify the trigger |
| `Transition not valid` | The workflow has no such transition from the current status | Add the transition in the workflow |

**Rules do not trigger themselves by default.** If you genuinely need rule A to fire rule B, enable *Allow rule trigger* in rule B's details — but be careful, this is how infinite loops and blown run quotas happen.

---

## Run order

Multiple rules on `Work item created` run in parallel, not in a guaranteed order. If Rule 2 needs the priority that Rule 1 sets, don't split them — put both actions in one rule, sequentially.

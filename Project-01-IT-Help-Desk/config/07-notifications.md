# 07 — Notifications & Comment Visibility

Reference for [DEPLOY.md](../DEPLOY.md). Configure in **Project settings → Notifications** (customer notifications) and **⚙️ → Issues → Notification schemes** (internal).

---

## The single most important concept

There are **two kinds of comment**:

| Comment type | Customer sees it? | Use for |
| --- | --- | --- |
| **Share with customer** (public) | ✅ Yes, in portal + email | Anything you want the requester to read |
| **Internal note** | ❌ No, agents only | Diagnosis, blame, vendor notes, passwords-adjacent chatter |

🚨 **Test this before you go live.** Log in as a customer and confirm internal notes are invisible. Getting this wrong means leaking internal conversation to employees.

---

## Customer notifications

| Event | Who gets email | Default | Keep it? |
| --- | --- | --- | --- |
| Request created | Reporter | On | ✅ Yes |
| Public comment added | Reporter + participants | On | ✅ Yes |
| Request resolved | Reporter | On | ✅ Yes |
| Approval required | Approver | On | ✅ Yes |
| Approval completed | Reporter | On | ✅ Yes |
| Request reopened | Reporter | On | ✅ Yes |
| Participant added | New participant | On | ✅ Yes |
| Organization added | Org members | Off | Optional |
| Internal comment | — | Never | ❌ Must stay off |

---

## Agent notifications

| Event | Who | Notes |
| --- | --- | --- |
| Issue assigned | Assignee | Essential |
| Comment added (any) | Assignee, watchers | Can get noisy |
| SLA at risk | Assignee + lead | Via Automation Rule 6 |
| Approval granted | Assignee | So they know to start work |
| Priority changed | Assignee | Useful when automation escalates |

---

## Recommended email templates

Customise the wording in **Project settings → Notifications → Customer notifications**, then edit each template.

**Request created**
```text
Subject: [{{issue.key}}] We got your request

Hi {{reporter.displayName}},

We've received your request: {{issue.summary}}
Reference: {{issue.key}}

Track it here: {{issue.url.customer}}

— Nimbus IT Help Desk
```

**Request resolved**
```text
Subject: [{{issue.key}}] Resolved

Hi {{reporter.displayName}},

We've resolved: {{issue.summary}}
Resolution: {{issue.resolution.name}}

Still broken? Just reply and we'll reopen it.

— Nimbus IT Help Desk
```

---

## Notification hygiene

| Do | Don't |
| --- | --- |
| Put the ticket key in every subject line | Send a mail on every field change |
| Include the customer portal URL, not the agent URL | Notify the whole team on every comment |
| Tell the customer what happens next | Leave "Issue updated" notifications on for agents |
| Keep resolution emails short | Send internal notes to customers, ever |

**Why the URL matters:** `{{issue.url}}` sends customers to the agent view, where they get an access-denied error. Always use `{{issue.url.customer}}` in customer-facing messages.

---

## Free plan email caps

Free and trial Jira Cloud sites cap outbound automation email in a rolling 24-hour window. If your test emails stop arriving, you probably hit the cap — wait it out rather than debugging config. ([automation service limits](https://support.atlassian.com/cloud-automation/docs/automation-service-limits/)) *Content was rephrased for compliance with licensing restrictions.*

---

## Testing checklist

- [ ] Customer gets a "created" email
- [ ] Customer gets an email for a public comment
- [ ] Customer gets **nothing** for an internal note
- [ ] Approver gets an approval-request email with working buttons
- [ ] Agent gets an email when a ticket is assigned to them
- [ ] Resolved email arrives and shows the resolution
- [ ] Every customer email link opens the **portal**, not the agent view

# 03 — Workflow

Reference for [DEPLOY.md Part 6](../DEPLOY.md#part-6--build-the-workflow).

---

## Standard workflow (non-approval request types)

```text
   (create)
      │
      ▼
   ┌──────┐   Start work   ┌─────────────┐
   │ OPEN │──────────────► │ IN PROGRESS │
   └──┬───┘                └──┬───────▲──┘
      │                       │       │
      │ Resolve               │ Need  │ Customer
      │                       │ info  │ replied
      │                       ▼       │
      │            ┌──────────────────┴───┐
      │            │ WAITING FOR CUSTOMER │
      │            └──────────────────────┘
      │                       │
      │                       │ Resolve
      ▼                       ▼
   ┌──────────┐
   │ RESOLVED │
   └────┬─────┘
        │ Close        ┌── Reopen ──┐
        ▼              │            │
   ┌──────────┐        │            │
   │  CLOSED  │────────┘            │
   └──────────┘                     │
        └── Reopen ─► IN PROGRESS ◄─┘
```

---

## Statuses

| Status | Category | SLA behaviour | Meaning |
| --- | --- | --- | --- |
| Open | To Do | Both SLAs running | Logged, nobody working yet |
| In Progress | In Progress | Both SLAs running | Agent actively working |
| Waiting for Customer | In Progress | **Both SLAs paused** | Blocked on the customer |
| Pending Approval | To Do | **Resolution SLA paused** | Blocked on a manager |
| Resolved | Done | Resolution SLA stopped | Fixed, awaiting confirmation |
| Closed | Done | All SLAs stopped | Finished |

Getting the **category** right matters more than the name — SLAs, queues (`statusCategory != Done`) and reports all key off it.

---

## Transitions

| # | Name | From | To | Notes |
| --- | --- | --- | --- | --- |
| 1 | Create | — | Open | Default for non-approval types |
| 2 | Create | — | Pending Approval | For the 3 approval types |
| 3 | Start work | Open | In Progress | Also fired by Automation Rule 4 |
| 4 | Need info | In Progress | Waiting for Customer | Agent asks a question |
| 5 | Customer replied | Waiting for Customer | In Progress | Fired by Automation Rule 5 |
| 6 | Resolve | In Progress | Resolved | Requires Resolution |
| 7 | Resolve | Open | Resolved | Quick fixes |
| 8 | Close | Resolved | Closed | Fired by Automation Rule 7 |
| 9 | Reopen | Resolved | In Progress | Clears Resolution |
| 10 | Reopen | Closed | In Progress | Clears Resolution |
| 11 | Cancel | Open | Closed | Resolution = Won't Do |
| 12 | Approve | Pending Approval | In Progress | Approval outcome |
| 13 | Decline | Pending Approval | Closed | Approval outcome |

---

## Rules on transitions

| Transition | Rule type | Rule |
| --- | --- | --- |
| Resolve | Validator / screen | Resolution must be set |
| Resolve | Post function | Set `Resolved` date |
| Close | Post function | Nothing extra needed |
| Reopen | Post function | **Clear** the `Resolution` field |
| Cancel | Post function | Set Resolution = `Won't Do` |
| Start work | Condition | Only Service Desk Team (agents) |

**Why Reopen must clear Resolution:** a ticket that is back In Progress but still carries `Done` as its resolution will pollute every report and make your resolution-rate look better than it is.

---

## Resolution values to use

| Resolution | When |
| --- | --- |
| Done | Fixed properly |
| Duplicate | Same as another ticket — link it |
| Won't Do | Rejected, cancelled, or declined approval |
| Cannot Reproduce | Couldn't recreate the problem |
| Answered | Question answered, nothing to fix |

---

## Team-managed vs company-managed

| | Team-managed | Company-managed |
| --- | --- | --- |
| Workflow editing | Simple, per-project | Full editor, shareable |
| Validators / post functions | Limited | Full |
| Transition screens | Not available | Available |
| Recommended for this project | Fine for learning | Better if you want full control |

If you are on a team-managed project and can't add validators, that's expected. Use Automation Rule 4/5 for status hygiene instead, and rely on the ticket view for Resolution.

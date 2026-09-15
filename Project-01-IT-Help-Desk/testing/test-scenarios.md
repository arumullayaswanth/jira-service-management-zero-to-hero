# Test Scenarios

Reference for [DEPLOY.md Part 13](../DEPLOY.md#part-13--test-everything).

## Setup

Two browser windows:

| Window | Logged in as | Role |
| --- | --- | --- |
| **A** | you | Agent / admin |
| **B** | `you+emp1@gmail.com` (incognito) | Customer |

---

## Test 1 — Customer can submit a request

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window B: open the portal URL | Portal loads, branded "Nimbus IT Help Desk" |
| 2 | 3 categories visible | Hardware / Software & Accounts / Access & Other |
| 3 | Click **Password Reset** | Form opens with your custom questions |
| 4 | Fill it in and submit | Confirmation page with a ticket key like `ITHD-1` |
| 5 | Window A: open queue `1. New Requests` | Ticket is there |

**Fails if:** portal won't load → check Customer permissions. Form shows generic fields only → your fields aren't on the request form.

---

## Test 2 — Automation fires on create

Wait ~30 seconds after Test 1, then open the ticket in Window A.

| Check | Expected |
| --- | --- |
| Priority | Set automatically (High for Password Reset) |
| Assignee | Set automatically (agent3) |
| Comments | A public welcome comment exists |
| Customer name in comment | Real name, not `{{reporter.displayName}}` |

**Fails if:** nothing happened → Project settings → Automation → open the rule → **Audit log**. Smart value showing as literal text → you typed it into the wrong field type.

---

## Test 3 — SLA starts

| Check | Expected |
| --- | --- |
| Right panel on the ticket | Two SLA timers visible |
| Time to first response | Counting down (2h for High) |
| Time to resolution | Counting down (8h for High) |

**Fails if:** no timer → no SLA goal matched. Add an empty-JQL catch-all goal as the **last** goal.

---

## Test 4 — Agent public comment stops the first-response SLA

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window A: add a comment, choose **Share with customer** | Comment posts |
| 2 | Check the SLA panel | *Time to first response* shows ✅ met |
| 3 | Window B: refresh the ticket in the portal | Comment is visible |
| 4 | Check `you+emp1@gmail.com` inbox | Email arrived with the comment |
| 5 | Check the link in that email | Opens the **portal**, not an access-denied page |

**Fails at step 5:** your notification template uses `{{issue.url}}` instead of `{{issue.url.customer}}`.

---

## Test 5 — SLA pauses on Waiting for Customer

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window A: transition to **Waiting for Customer** | Status changes |
| 2 | Check *Time to resolution* | Shows as **paused** |
| 3 | Note the remaining time | e.g. `7h 42m` |
| 4 | Wait 2 minutes, refresh | Remaining time **unchanged** |

**Fails if:** clock keeps running → the SLA pause condition doesn't match your status name exactly. Check capitalisation.

---

## Test 6 — Customer reply resumes work

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window B: add a comment on the ticket in the portal | Comment posts |
| 2 | Window A: refresh after ~30s | Status is back to **In Progress** |
| 3 | Check comments | Internal note: "Customer replied at …" |
| 4 | Check the SLA | Resumed from where it paused |

**Fails if:** status didn't change → Automation Rule 5. Check the user condition is `Reporter` and the status condition matches.

---

## Test 7 — Internal comments are invisible to customers 🚨

**This is the most important test in the whole project.**

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window A: add a comment as **Internal note** with text `INTERNAL TEST — do not show` | Comment posts, shown with the internal styling |
| 2 | Window B: refresh the ticket in the portal | ❌ The internal text is **not** there |
| 3 | Check `you+emp1@gmail.com` inbox | ❌ No email about it |

**If the customer can see it, stop everything and fix comment visibility before doing anything else.** You are leaking internal conversation to employees.

---

## Test 8 — Approval flow

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window B: submit **Software Installation**, set Approver = `you+manager1@gmail.com` | Ticket created |
| 2 | Window A: check the status | **Pending Approval** |
| 3 | Check the *Time to resolution* SLA | **Paused** |
| 4 | Check `you+manager1@gmail.com` inbox | Approval request email arrived |
| 5 | Open the link in that email | Portal shows **Approve** / **Decline** buttons |
| 6 | Click **Approve** | Ticket moves to **In Progress** |
| 7 | Check the SLA | Resumed |
| 8 | Check the requester's inbox | Notified that it was approved |

**Fails at step 4/5:** the Approver field is empty, or the approver isn't a customer/agent on the project.

---

## Test 9 — Resolve and close

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window A: transition to **Resolved** | Asked for a Resolution |
| 2 | Set Resolution = `Done`, add a public comment | Saves |
| 3 | Check *Time to resolution* | Stopped, shows met or breached |
| 4 | Check queues 1–5 | Ticket has left all active queues |
| 5 | Window B: check the portal | Ticket shows as Resolved |
| 6 | Check the customer inbox | "Resolved" email arrived |
| 7 | Window A: **Reopen** the ticket | Status In Progress, **Resolution is now empty** |

**Fails at step 7:** the Reopen transition has no "clear Resolution" post function.

---

## Test 10 — Knowledge base deflection

| Step | Action | Expected |
| --- | --- | --- |
| 1 | Window B: portal → **Password Reset** | Form opens |
| 2 | Type `password` in the summary field | Suggested articles appear |
| 3 | Click an article | It opens and is readable |
| 4 | Try `vpn` on the VPN Issue form | VPN article suggested |

**Fails if:** no articles → space not linked, or the article has no matching labels, or the space isn't viewable by customers.

---

## Results table

| # | Test | Pass | Notes |
| --- | --- | :---: | --- |
| 1 | Customer can submit | ☐ | |
| 2 | Automation on create | ☐ | |
| 3 | SLA starts | ☐ | |
| 4 | Public comment + first response SLA | ☐ | |
| 5 | SLA pauses | ☐ | |
| 6 | Customer reply resumes | ☐ | |
| 7 | **Internal comments hidden** | ☐ | 🚨 blocker if it fails |
| 8 | Approval flow | ☐ | |
| 9 | Resolve / close / reopen | ☐ | |
| 10 | KB deflection | ☐ | |

---

## Extra tests if you want to push further

| Test | How |
| --- | --- |
| Email channel | Send a mail to `ithd@yoursite.atlassian.net` → ticket appears |
| Organization visibility | emp1 shares a ticket with Nimbus - Sales; another Sales member can see it |
| SLA breach | Create a ticket, set an SLA goal to `1m`, wait → it goes red and Rule 6 fires |
| Auto-close | Resolve a ticket, edit Rule 7's JQL to `-0d`, run it manually → it closes |
| Agent seat limit | Try inviting a 4th agent → Free plan blocks it. Good thing to see once. |

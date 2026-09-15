# 05 — SLAs

Reference for [DEPLOY.md Part 8](../DEPLOY.md#part-8--build-the-slas).

---

## Calendars

| Calendar | Hours | Used for |
| --- | --- | --- |
| **Nimbus Business Hours** | Mon–Fri 09:00–18:00 | High / Medium / Low priority |
| **24/7 Calendar** (built-in) | Always | Highest priority only |

A `4h` goal on business hours submitted Friday 17:00 is not due until Monday 12:00. That is the point of calendars — don't measure your team against hours nobody was working.

---

## SLA 1 — Time to First Response

| Setting | Value |
| --- | --- |
| **Begin** | Work item created |
| **Pause on** | Status = Waiting for Customer |
| **Stop** | Comment: For customers (public comment by an agent) |

**Goals — order is critical:**

| Order | JQL | Goal | Calendar |
| --- | --- | --- | --- |
| 1 | `priority = Highest` | 30m | 24/7 |
| 2 | `priority = High` | 2h | Business Hours |
| 3 | `priority = Medium` | 4h | Business Hours |
| 4 | `priority = Low` | 8h | Business Hours |
| 5 | *(empty)* | 8h | Business Hours |

---

## SLA 2 — Time to Resolution

| Setting | Value |
| --- | --- |
| **Begin** | Work item created |
| **Pause on** | Status = Waiting for Customer, Status = Pending Approval |
| **Stop** | Status = Resolved, Status = Closed, Resolution = Set |

**Goals:**

| Order | JQL | Goal | Calendar |
| --- | --- | --- | --- |
| 1 | `priority = Highest` | 4h | 24/7 |
| 2 | `priority = High` | 8h | Business Hours |
| 3 | `priority = Medium` | 24h | Business Hours |
| 4 | `priority = Low` | 40h | Business Hours |
| 5 | *(empty)* | 24h | Business Hours |

---

## SLA 3 — Time Waiting for Support

Measures how long the customer has been ignored since their last message.

| Setting | Value |
| --- | --- |
| **Begin** | Work item created; Comment: For customers *by customer* |
| **Pause on** | *(nothing)* |
| **Stop** | Comment: For customers *by agent* |
| **Goal** | *(empty JQL)* → 4h, Business Hours |

---

## Priority matrix — how Priority gets decided

Priority is not chosen by the customer. It is derived:

| Impact ↓ / Urgency → | Low urgency | Medium urgency | High urgency |
| --- | --- | --- | --- |
| **Whole office** | High | Highest | Highest |
| **My team** | Medium | High | High |
| **Only me** | Low | Medium | Medium |

Automation Rule 1 implements a simplified version of this using the `Impact Level` field:

| Impact Level | Priority |
| --- | --- |
| Whole office | Highest |
| My team | High |
| Only me | Medium |

Plus overrides by request type:

| Request type | Priority override |
| --- | --- |
| Password Reset | High (people cannot work at all) |
| VPN Issue | High |
| Laptop Request | Low (it's a purchase, not an outage) |
| Software Installation | Low |

---

## SLA targets summary

| Priority | First response | Resolution | Clock |
| --- | --- | --- | --- |
| 🔴 Highest | 30 min | 4 hours | 24/7 |
| 🟠 High | 2 hours | 8 hours | Business |
| 🟡 Medium | 4 hours | 24 hours | Business |
| 🟢 Low | 8 hours | 40 hours | Business |

---

## The 5 SLA mistakes beginners make

1. **Catch-all goal placed first.** Jira uses the first matching goal, so an empty-JQL goal at the top swallows every ticket. Put it last, always.
2. **No catch-all at all.** Tickets that match nothing show no timer. Always have a final empty-JQL goal.
3. **Forgetting to pause.** Without a pause on Waiting for Customer, your SLA punishes you for the customer's silence.
4. **Wrong status name.** `Waiting For Customer` ≠ `Waiting for Customer`. Copy-paste the exact status.
5. **Business hours on critical tickets.** A P1 at 2am should not wait until 09:00. Use the 24/7 calendar for Highest.

---

## Verifying an SLA

1. Create a ticket → timer visible with a countdown
2. Move to Waiting for Customer → timer shows paused
3. Move back → timer resumes from where it stopped
4. Add a public agent comment → First Response shows met ✅
5. Resolve → Resolution SLA stops

If step 1 shows nothing, your goals don't match. Add the empty-JQL catch-all.

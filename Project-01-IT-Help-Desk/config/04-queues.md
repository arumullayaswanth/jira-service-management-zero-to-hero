# 04 — Queues

Reference for [DEPLOY.md Part 7](../DEPLOY.md#part-7--build-the-queues).

Copy the JQL exactly. Replace `ITHD` only if you used a different project key.

---

## 1. New Requests

Everything nobody has touched yet. Agents start their day here.

```jql
project = ITHD AND status = "Open" ORDER BY created ASC
```

Columns: `Key`, `Summary`, `Request Type`, `Reporter`, `Created`, `Time to first response`

---

## 2. Unassigned

Tickets with no owner, in any active status. Nothing should live here for long.

```jql
project = ITHD AND assignee IS EMPTY AND statusCategory != Done ORDER BY created ASC
```

Columns: `Key`, `Summary`, `Priority`, `Request Type`, `Created`

---

## 3. My Open Tickets

Each agent sees only their own work. `currentUser()` makes one queue work for everybody.

```jql
project = ITHD AND assignee = currentUser() AND statusCategory != Done ORDER BY priority DESC, created ASC
```

Columns: `Key`, `Summary`, `Status`, `Priority`, `Time to resolution`

---

## 4. High & Critical

```jql
project = ITHD AND priority IN (Highest, High) AND statusCategory != Done ORDER BY created ASC
```

Columns: `Key`, `Summary`, `Priority`, `Assignee`, `Time to resolution`

---

## 5. Waiting for Customer

Sorted oldest-updated first, so forgotten tickets float to the top.

```jql
project = ITHD AND status = "Waiting for Customer" ORDER BY updated ASC
```

Columns: `Key`, `Summary`, `Reporter`, `Updated`, `Assignee`

---

## 6. SLA Breached

```jql
project = ITHD AND ("Time to resolution" = breached() OR "Time to first response" = breached()) AND statusCategory != Done ORDER BY created ASC
```

Columns: `Key`, `Summary`, `Priority`, `Assignee`, `Time to resolution`

⚠️ This queue errors until the SLAs from Part 8 exist.

---

## Optional extras

**At risk (breaching soon)**
```jql
project = ITHD AND "Time to resolution" = everBreached() AND statusCategory != Done
```

**Pending approval**
```jql
project = ITHD AND status = "Pending Approval" ORDER BY created ASC
```

**Sales department only** (organization-based routing)
```jql
project = ITHD AND organizations = "Nimbus - Sales" AND statusCategory != Done
```

**Untouched for 2 days**
```jql
project = ITHD AND statusCategory != Done AND updated <= -2d ORDER BY updated ASC
```

---

## JQL cheat sheet

| Piece | Meaning |
| --- | --- |
| `project = ITHD` | Only this project |
| `statusCategory != Done` | Any ticket still alive (better than listing statuses) |
| `assignee IS EMPTY` | Nobody owns it |
| `assignee = currentUser()` | Whoever is looking at the queue |
| `priority IN (Highest, High)` | Multiple values |
| `updated <= -2d` | Not touched in 2 days |
| `created >= startOfMonth()` | This month |
| `"Time to resolution" = breached()` | SLA already blown |
| `= everBreached()` | Blown at any point, even if recovered |
| `ORDER BY created ASC` | Oldest first — the fair way to work a queue |

---

## Two rules for good queues

1. **Order matters.** Agents work top to bottom. Put New Requests first.
2. **No ticket should be invisible.** Every active ticket should appear in at least one queue, or it will be forgotten. Test this by comparing your queue totals against `project = ITHD AND statusCategory != Done`.

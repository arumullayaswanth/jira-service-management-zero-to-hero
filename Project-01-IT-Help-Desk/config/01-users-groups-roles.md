# 01 — Users, Groups, Roles, Organizations

Reference tables for [DEPLOY.md Part 3](../DEPLOY.md#part-3--add-users-groups-and-organizations).

---

## Agents (max 3 on the Free plan)

| Name | Email | Project role | Handles |
| --- | --- | --- | --- |
| You | `you@gmail.com` | Administrator + Service Desk Team | Everything, email, VPN, general |
| Agent 2 | `you+agent2@gmail.com` | Service Desk Team | Laptops, Wi-Fi, hardware |
| Agent 3 | `you+agent3@gmail.com` | Service Desk Team | Access, passwords, software |

> Agents consume paid seats. Customers do not.

---

## Customers (unlimited, free)

| Name | Email | Organization | Role in tests |
| --- | --- | --- | --- |
| Priya Sharma | `you+emp1@gmail.com` | Nimbus - Sales | Normal requester |
| Rahul Verma | `you+emp2@gmail.com` | Nimbus - Finance | Second requester |
| Anita Desai | `you+manager1@gmail.com` | Nimbus - Engineering | Approver |

---

## Organizations

| Organization | Members | Why it exists |
| --- | --- | --- |
| Nimbus - Sales | emp1 | Department reporting + shared ticket visibility |
| Nimbus - Finance | emp2 | Department reporting |
| Nimbus - Engineering | manager1 | Approver group |

---

## Project roles explained

| Role | Can do |
| --- | --- |
| **Administrator** | Change every project setting: workflows, SLAs, automation, fields |
| **Service Desk Team** | Work tickets: comment, transition, assign, close. This is "agent". |
| **Service Desk Customer** | Raise and view own requests through the portal only |
| **Member** (Jira software role) | Not used in this project |

---

## Permission checklist

| Setting | Where | Value for this project |
| --- | --- | --- |
| Who can raise requests | Project settings → Customer permissions | Customers added to this project |
| Share with organization | Project settings → Customer permissions | Yes |
| Public signup | Site → Product access | Off (lab safety) |
| Anonymous access to portal | Project settings → Customer permissions | Off |

---

## Test email trick

If your real mailbox is `you@gmail.com`, all of these arrive in the same inbox but are separate identities to Jira:

```text
you+agent2@gmail.com
you+agent3@gmail.com
you+emp1@gmail.com
you+emp2@gmail.com
you+manager1@gmail.com
```

Works on Gmail and Outlook. Lets you test the whole flow with one mailbox.

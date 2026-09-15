# 🟢 PROJECT 1 — IT Help Desk

**Level:** Beginner
**Time to build:** 6–8 hours (can be split over a weekend)
**Cost:** 🟢 FREE (Jira Service Management Free plan + Confluence Free plan)

---

## 📖 What Is This Project?

We are building a **real internal IT Help Desk** for a fake company called **Nimbus Corp**.

Employees of Nimbus Corp will be able to:

* Open a website (the **Portal**)
* Pick what is broken (Laptop, Wi-Fi, VPN, Password…)
* Fill a small form
* Submit a ticket
* Get email updates
* Read help articles to fix things themselves

The IT team will be able to:

* See tickets in organised **Queues**
* Get tickets **auto-assigned**
* See a **countdown timer (SLA)** on every ticket
* **Approve** software and hardware requests
* Move tickets through a proper **Workflow**
* Let **Automation** do the boring work

---

## 🗺️ The Big Picture

```text
        EMPLOYEE (Customer)
                |
                ▼
         HELP CENTER  (website)
                |
                ▼
        PORTAL: "Nimbus IT Help Desk"
                |
      +---------+---------+
      |         |         |
      ▼         ▼         ▼
  Hardware   Software   Access
  requests   requests   requests
      |         |         |
      +---------+---------+
                |
                ▼
            REQUEST TYPE
                |
                ▼
              FORM
                |
                ▼
             TICKET
                |
      +---------+---------+
      |         |         |
      ▼         ▼         ▼
   QUEUE      SLA     AUTOMATION
      |         |         |
      +---------+---------+
                |
                ▼
           IT AGENT
                |
                ▼
            WORKFLOW
   Open → In Progress → Waiting for Customer
        → Resolved → Closed
                |
                ▼
         KNOWLEDGE BASE
```

---

## 📂 What Is In This Folder

| File / Folder | What it is |
| --- | --- |
| **DEPLOY.md** | 👈 **START HERE.** Step-by-step build guide. Every single click. |
| `config/01-users-groups-roles.md` | Copy-paste table of users, groups, roles, organizations |
| `config/02-request-types.md` | All 9 request types + their fields |
| `config/03-workflow.md` | Statuses, transitions, rules |
| `config/04-queues.md` | 6 queues + exact JQL to paste |
| `config/05-slas.md` | SLA metrics, goals, JQL, calendar |
| `config/06-automation-rules.md` | 8 automation rules, trigger → condition → action |
| `config/07-notifications.md` | Who gets emailed, when |
| `knowledge-base/` | 6 ready-to-paste help articles |
| `testing/test-scenarios.md` | 10 tests to prove it works |
| `api/` | Optional: create a ticket with the REST API |

---

## ✅ What "Done" Looks Like

At the end you can show someone this:

1. A real URL like `https://yourname.atlassian.net/servicedesk/customer/portal/1`
2. A branded portal with 3 categories and 9 request types
3. A ticket that auto-assigns itself and starts an SLA timer
4. An approval that must be granted before software is installed
5. A knowledge base article that appears while the customer is typing
6. A dashboard with ticket counts and SLA performance

---

## ⚠️ Before You Start

* You need an **email address** you can receive mail on.
* Use a **second email** (or a `+` alias like `you+customer@gmail.com`) to play the role of the *employee/customer*. This is how you test properly.
* You do **not** need a credit card for the Free plan.
* Free plan = **3 agents max**, **2 GB storage**, **100 automation runs/month per site**. That is plenty for this project. ([Jira plans](https://www.atlassian.com/software/jira/guides/more/jira-editions), [Service Collection licensing](https://www.atlassian.com/licensing/service-collection)) *Content was rephrased for compliance with licensing restrictions.*

---

👉 **Now open [DEPLOY.md](./DEPLOY.md) and follow it top to bottom. Do not skip.**

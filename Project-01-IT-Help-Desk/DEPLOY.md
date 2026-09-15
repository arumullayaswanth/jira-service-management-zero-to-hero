# 🚀 DEPLOY.md — Build the IT Help Desk, Step By Step

> **Read me like a recipe.** Do one step. Tick the box. Go to the next step.
> If a screen looks different, look for the same *words* — Atlassian moves buttons around but the words stay.

**Company we are pretending to be:** Nimbus Corp
**What we are building:** The internal IT Help Desk
**Total steps:** 10 parts, 78 small steps

---

## 🧭 Table of Contents

| Part | What you will do | Time |
| --- | --- | --- |
| [Part 0](#part-0--words-you-must-know) | Learn 12 words (5 min of reading, saves you hours) | 5 min |
| [Part 1](#part-1--create-your-atlassian-account) | Create the account + site | 15 min |
| [Part 2](#part-2--create-the-service-project) | Create the IT Help Desk project | 10 min |
| [Part 3](#part-3--add-users-groups-and-organizations) | Agents, customers, organizations | 30 min |
| [Part 4](#part-4--build-the-9-request-types) | The things people can ask for | 60 min |
| [Part 5](#part-5--build-the-forms-and-fields) | The questions on each request | 45 min |
| [Part 6](#part-6--build-the-workflow) | Open → In Progress → … → Closed | 45 min |
| [Part 7](#part-7--build-the-queues) | Agent to-do lists | 30 min |
| [Part 8](#part-8--build-the-slas) | Countdown timers | 40 min |
| [Part 9](#part-9--build-approvals) | "Manager must say yes" | 30 min |
| [Part 10](#part-10--build-the-automation-rules) | Robots do the boring work | 60 min |
| [Part 11](#part-11--build-the-knowledge-base) | Self-help articles | 40 min |
| [Part 12](#part-12--brand-the-portal) | Make it look like a real company | 20 min |
| [Part 13](#part-13--test-everything) | Prove it works | 40 min |
| [Part 14](#part-14--build-a-dashboard) | Charts for your boss | 20 min |

---

# PART 0 — Words You Must Know

Read this once. These 12 words are 90% of Jira Service Management.

| Word | Kid-simple meaning |
| --- | --- |
| **Site** | Your own Jira on the internet. Looks like `nimbus-yourname.atlassian.net`. |
| **Product** | An app on your site. We use *Jira Service Management* (JSM) and *Confluence*. |
| **Project** | One help desk. Ours is called "IT Help Desk". |
| **Agent** | A person who *fixes* tickets. Costs money (3 free). |
| **Customer** | A person who *asks* for help. **Always free, unlimited.** |
| **Portal** | The pretty website customers use to ask for help. |
| **Help Center** | The front page that lists all portals. |
| **Request Type** | One thing a customer can ask for, e.g. "VPN Issue". |
| **Issue / Ticket** | One actual request from one person. |
| **Workflow** | The list of statuses a ticket walks through. |
| **Queue** | A filtered to-do list for agents. |
| **SLA** | A countdown timer, e.g. "reply within 4 hours". |
| **Automation** | If *this* happens, then do *that*. A robot. |

🧠 **The one rule beginners get wrong:**
Agents cost money. Customers are free. So *never* invite an employee as an agent unless they fix tickets.

- [ ] I read Part 0

---

# PART 1 — Create Your Atlassian Account

### Step 1.1 — Open the signup page

Go to 👉 <https://www.atlassian.com/software/jira/service-management/free>

Click the big **Get it free** button.

### Step 1.2 — Sign up

* Use **Google/Microsoft sign-in** (fastest) or an email + password.
* Use an email you can actually open. You will get real mail here.

### Step 1.3 — Name your site

You will be asked for a site name. Type something unique:

```text
nimbus-<your-first-name>
```

Example: `nimbus-yaswanth`

Your site URL becomes:

```text
https://nimbus-yaswanth.atlassian.net
```

📌 **Write this URL down.** You will use it 100 times.

### Step 1.4 — Pick the products

When asked which products you want, tick:

* ✅ **Jira Service Management**
* ✅ **Confluence** (free — we need it for the Knowledge Base in Part 11)

If Confluence is not offered now, don't panic. We add it in Part 11.

### Step 1.5 — Skip the setup wizard questions

Atlassian will ask "what is your team size / what do you do". Answer anything. It changes nothing important.

### Step 1.6 — Confirm you are on the Free plan

1. Click the ⚙️ **gear icon** (top right) → **Billing**
2. Open **Manage subscriptions**
3. You should see **Jira Service Management — Free**

If it says *Trial of Standard/Premium*, that's OK too — it becomes Free after the trial. Just know that some fancy features will disappear later. Everything in this project works on Free.

- [ ] Part 1 done. I can open my site URL and see Jira.

---

# PART 2 — Create the Service Project

### Step 2.1 — Start a new project

1. Top-left, click **Projects** → **Create project**
2. If you see product choices, choose **Service management**

### Step 2.2 — Pick the template

Choose the template called **IT service management**.

> Why? It gives you incident/change/problem types for free later. If you only see "Basic service desk", that is fine too.

Click **Use template** → **Next**.

### Step 2.3 — Name it

| Field | What to type |
| --- | --- |
| Name | `IT Help Desk` |
| Key | `ITHD` |

⚠️ **The key `ITHD` is permanent.** Every ticket will be named `ITHD-1`, `ITHD-2`, … Type it carefully.

Click **Next** → **Create project**.

### Step 2.4 — Find your two most important URLs

**Agent view** (where you work):

```text
https://YOUR-SITE.atlassian.net/jira/servicedesk/projects/ITHD/queues
```

**Customer portal** (where employees ask):

1. In the project, left sidebar → **Project settings**
2. Click **Portal settings**
3. Copy the link shown. It looks like:

```text
https://YOUR-SITE.atlassian.net/servicedesk/customer/portal/1
```

📌 **Write both URLs down.**

### Step 2.5 — Look around (2 minutes)

Click each item in the left sidebar just to see it:

* **Queues** — agent to-do lists
* **Work items / Issues** — all tickets
* **Customers** — people who can ask
* **Reports** — charts
* **Project settings** — where we do all the building

- [ ] Part 2 done. I have my portal URL and my agent URL.

---

# PART 3 — Add Users, Groups and Organizations

We need people. On the Free plan you get **3 agents**. We will use all 3.

### Step 3.1 — Understand who we are creating

```text
AGENTS (3 max on Free — these fix tickets)
├── You                → Admin + Agent  (Service Desk Team)
├── agent2@...         → Agent          (Hardware Team)
└── agent3@...         → Agent          (Access Team)

CUSTOMERS (unlimited, free — these ask for help)
├── employee1@...      → Sales dept
├── employee2@...      → Finance dept
└── manager1@...       → Approver

ORGANIZATIONS (groups of customers)
├── Nimbus - Sales
├── Nimbus - Finance
└── Nimbus - Engineering
```

💡 **Trick for getting free test emails:** if your email is `you@gmail.com`, then `you+agent2@gmail.com`, `you+emp1@gmail.com` all arrive in your same inbox but Jira thinks they are different people. Gmail and Outlook both support this.

### Step 3.2 — Add agents

1. **Project settings** → **People** (or **Access**)
2. Click **Add people**
3. Type `you+agent2@gmail.com`
4. Role: choose **Service Desk Team**
5. Click **Add**
6. Repeat for `you+agent3@gmail.com`

> **Service Desk Team** = agent. Can see tickets, comment, transition, close.

### Step 3.3 — Add customers

1. Left sidebar → **Customers**
2. Click **Add customers**
3. Paste these, one per line:

```text
you+emp1@gmail.com
you+emp2@gmail.com
you+manager1@gmail.com
```

4. Click **Add**

> Customers do **not** consume an agent seat. Add 500 if you like.

### Step 3.4 — Create organizations

1. Still in **Customers**, click the **Organizations** tab (or ⚙️ → **Organizations**)
2. Click **Create organization**
3. Name: `Nimbus - Sales` → Create
4. Repeat for `Nimbus - Finance` and `Nimbus - Engineering`

### Step 3.5 — Put customers into organizations

1. Click **Nimbus - Sales**
2. Click **Add customers**
3. Add `you+emp1@gmail.com`
4. Go back → open **Nimbus - Finance** → add `you+emp2@gmail.com`
5. Open **Nimbus - Engineering** → add `you+manager1@gmail.com`

### Step 3.6 — Why organizations matter

Because of organizations you can later:

* Route Sales tickets to one team
* Let everyone in Sales **see each other's tickets** (shared visibility)
* Report per department

### Step 3.7 — Check the customer permission setting

1. **Project settings** → **Customer permissions**
2. Set **Who can raise requests?** → **Customers added to this project** (safer for a lab)
3. Set **Can customers share requests with their organization?** → **Yes**

- [ ] Part 3 done. I have 3 agents, 3 customers, 3 organizations.

📄 Full reference table: [`config/01-users-groups-roles.md`](./config/01-users-groups-roles.md)

---

# PART 4 — Build the 9 Request Types

A **request type** is one thing a customer can ask for. We build 9, grouped into 3 categories.

### Step 4.1 — The plan

```text
PORTAL: Nimbus IT Help Desk
│
├── 🖥️  HARDWARE
│    ├── 1. Laptop Issue
│    ├── 2. Laptop Request
│    └── 3. Wi-Fi Issue
│
├── 💾  SOFTWARE & ACCOUNTS
│    ├── 4. Software Installation
│    ├── 5. Password Reset
│    ├── 6. Email Issue
│    └── 7. VPN Issue
│
└── 🔐  ACCESS & OTHER
     ├── 8. Access Request
     └── 9. General IT Support
```

### Step 4.2 — Create the 3 portal groups first

1. **Project settings** → **Request types**
2. Look for **Portal groups** (sometimes a tab, sometimes a left panel)
3. Click **Add group** three times and name them:

```text
Hardware
Software & Accounts
Access & Other
```

4. Drag them into that order.

### Step 4.3 — Delete the sample request types

The template gave you some samples like "Get IT help". Delete or hide the ones you don't want so your portal looks clean.

* Hover a request type → **⋯** → **Delete** (or untick its portal group to hide it)

> Keep at least one until you have created your own, otherwise the portal shows an error.

### Step 4.4 — Create request type #1

1. **Project settings** → **Request types** → **Create request type**
2. Fill it in:

| Field | Value |
| --- | --- |
| Name | `Laptop Issue` |
| Description | `My laptop is broken, slow, or won't start.` |
| Icon | pick a laptop icon |
| Work type / Issue type | `Service Request` |
| Portal group | `Hardware` |

3. Click **Create**

### Step 4.5 — Create the other 8

Repeat Step 4.4 exactly, using this table:

| # | Name | Customer-facing description | Issue type | Portal group |
| --- | --- | --- | --- | --- |
| 1 | Laptop Issue | My laptop is broken, slow, or won't start. | Service Request | Hardware |
| 2 | Laptop Request | I need a new or replacement laptop. | Service Request with Approvals | Hardware |
| 3 | Wi-Fi Issue | I can't connect to office Wi-Fi. | Service Request | Hardware |
| 4 | Software Installation | I need software installed on my machine. | Service Request with Approvals | Software & Accounts |
| 5 | Password Reset | I forgot my password or I'm locked out. | Service Request | Software & Accounts |
| 6 | Email Issue | I can't send or receive email. | Service Request | Software & Accounts |
| 7 | VPN Issue | I can't connect to the VPN. | Service Request | Software & Accounts |
| 8 | Access Request | I need access to a system, folder, or app. | Service Request with Approvals | Access & Other |
| 9 | General IT Support | Something else — I'll explain. | Service Request | Access & Other |

⚠️ **Important:** #2, #4 and #8 use **Service Request with Approvals**. That issue type already has an approval step in its workflow. This saves you a lot of pain in Part 9.

If your template did not create "Service Request with Approvals":
* Use plain `Service Request` for now
* We will add the approval status manually in Part 9

### Step 4.6 — Check the portal

Open your portal URL in a **private/incognito window** (so you see it as a customer would... you will need to log in as a customer, we do that properly in Part 13).

You should see 3 groups and 9 tiles.

- [ ] Part 4 done. 9 request types live in 3 groups.

📄 Full reference: [`config/02-request-types.md`](./config/02-request-types.md)

---

# PART 5 — Build the Forms and Fields

Right now every request just asks "Summary" and "Description". That is lazy. Let's ask smart questions.

### Step 5.1 — Understand the 3 kinds of field

| Kind | Meaning |
| --- | --- |
| **Built-in** | Already exists: Summary, Description, Attachment, Priority |
| **Custom field** | You create it: "Laptop Asset Tag" |
| **Hidden with preset value** | Customer never sees it, but it gets filled automatically |

### Step 5.2 — Create the custom fields

Go to ⚙️ **Settings** (top right, site admin) → **Issues** → **Custom fields** → **Create custom field**.

Create these 8:

| Field name | Type | Options / notes |
| --- | --- | --- |
| `Asset Tag` | Text field (single line) | e.g. NB-1042 |
| `Impact Level` | Select list (single choice) | `Only me` / `My team` / `Whole office` |
| `Software Name` | Text field (single line) | |
| `Business Justification` | Paragraph (multi-line text) | |
| `System / Application` | Select list (single choice) | `Payroll` / `CRM` / `Shared Drive` / `Jira` / `VPN` / `Other` |
| `Access Level` | Select list (single choice) | `Read only` / `Read + Write` / `Admin` |
| `Manager Email` | Text field (single line) | |
| `Location` | Select list (single choice) | `HQ Floor 1` / `HQ Floor 2` / `Remote` |

For each one, after creating it you must **associate it with a screen**. When Jira asks, tick the screens for your `ITHD` project. If you skip this, the field will not appear anywhere.

### Step 5.3 — Add fields to each request type

1. **Project settings** → **Request types**
2. Click a request type, e.g. **Laptop Issue**
3. Open the **Request form** tab
4. Click **Add a field**, pick a field, then set:
   * **Display name** — rewrite it in plain English for the customer
   * **Required** — on/off
   * **Field help** — a hint under the box

Use this table:

#### 1. Laptop Issue
| Field | Shown to customer as | Required |
| --- | --- | --- |
| Summary | `What's wrong?` | ✅ |
| Description | `Tell us more — when did it start?` | ✅ |
| Asset Tag | `Laptop asset tag (sticker on the bottom)` | ❌ |
| Impact Level | `Who is affected?` | ✅ |
| Location | `Where are you?` | ✅ |
| Attachment | `Add a photo or screenshot` | ❌ |

#### 2. Laptop Request
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `What do you need?` | ✅ |
| Description | `Why do you need a new laptop?` | ✅ |
| Business Justification | `Business justification` | ✅ |
| Manager Email | `Your manager's email` | ✅ |
| Location | `Delivery location` | ✅ |

#### 3. Wi-Fi Issue
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `Describe the Wi-Fi problem` | ✅ |
| Description | `What have you already tried?` | ✅ |
| Location | `Which floor / office?` | ✅ |
| Impact Level | `Is anyone else affected?` | ✅ |

#### 4. Software Installation
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `Which software?` | ✅ |
| Software Name | `Exact software name and version` | ✅ |
| Business Justification | `Why do you need it?` | ✅ |
| Manager Email | `Your manager's email` | ✅ |
| Asset Tag | `Which machine? (asset tag)` | ❌ |

#### 5. Password Reset
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `Which account is locked?` | ✅ |
| System / Application | `Which system?` | ✅ |
| Description | `Any error message you see` | ❌ |

#### 6. Email Issue
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `Describe the email problem` | ✅ |
| Description | `Sending, receiving, or both?` | ✅ |
| Attachment | `Screenshot of the error` | ❌ |

#### 7. VPN Issue
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `Describe the VPN problem` | ✅ |
| Description | `Error message + what you tried` | ✅ |
| Location | `Where are you connecting from?` | ✅ |

#### 8. Access Request
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `What access do you need?` | ✅ |
| System / Application | `Which system?` | ✅ |
| Access Level | `What level of access?` | ✅ |
| Business Justification | `Why do you need this access?` | ✅ |
| Manager Email | `Approving manager's email` | ✅ |

#### 9. General IT Support
| Field | Shown as | Required |
| --- | --- | --- |
| Summary | `One-line summary` | ✅ |
| Description | `Explain in detail` | ✅ |
| Impact Level | `How many people are affected?` | ✅ |
| Attachment | `Anything that helps` | ❌ |

### Step 5.4 — Hide Priority from customers

Customers **always** pick "Highest". Don't let them.

1. In each request form, if `Priority` is showing → remove it from the visible fields
2. Instead we will set Priority automatically in Part 10 using automation

### Step 5.5 — Optional: conditional fields (Forms)

Some plans give you the **Forms** builder, which can show a question only when another answer is chosen (e.g. show "Which floor?" only if Location = HQ).

1. In a request type, look for the **Forms** tab
2. Create a form, drag questions in
3. Select a question → **Add condition**

If you don't see Forms, skip it. Not needed for Project 1.

- [ ] Part 5 done. Every request asks the right questions.

---

# PART 6 — Build the Workflow

The workflow is the path a ticket walks. We want exactly this:

```text
        ┌─────────┐
        │  OPEN   │  ← ticket is created here
        └────┬────┘
             │ Start work
             ▼
      ┌──────────────┐
      │ IN PROGRESS  │
      └───┬──────┬───┘
          │      │ Need info from customer
          │      ▼
          │  ┌──────────────────────┐
          │  │ WAITING FOR CUSTOMER │
          │  └──────┬───────────────┘
          │         │ Customer replied
          │◄────────┘
          │ Resolve
          ▼
     ┌──────────┐
     │ RESOLVED │
     └────┬─────┘
          │ Close          ▲
          ▼                │ Reopen
     ┌──────────┐──────────┘
     │  CLOSED  │
     └──────────┘
```

### Step 6.1 — Find the workflow

1. **Project settings** → **Workflows**
2. You will see a workflow attached to your issue types
3. Click the ✏️ **pencil / Edit** icon

> ⚠️ If it says the workflow is **shared** with other projects, Jira will offer to make a copy. **Say yes / create a draft.** Never edit a shared system workflow.

### Step 6.2 — Understand statuses vs transitions

| Thing | Meaning |
| --- | --- |
| **Status** | A box. Where the ticket *is*. |
| **Transition** | An arrow. How it *moves*. |
| **Category** | The colour: To Do (grey), In Progress (blue), Done (green) |

### Step 6.3 — Create the 5 statuses

In the workflow editor, add statuses. For each, set the category correctly — **this matters for SLAs and reports.**

| Status | Category | Why |
| --- | --- | --- |
| `Open` | To Do (grey) | Nobody working yet |
| `In Progress` | In Progress (blue) | Agent is working |
| `Waiting for Customer` | In Progress (blue) | We're blocked, SLA should pause |
| `Resolved` | Done (green) | Fixed, waiting for confirmation |
| `Closed` | Done (green) | Finished forever |

To add a status: click **+ Add status**, type the name, choose the category.

### Step 6.4 — Create the transitions

Draw these arrows. In the editor you usually drag from one status to another, or click **Add transition**.

| # | Transition name | From | To |
| --- | --- | --- | --- |
| 1 | *(Create)* | — | Open |
| 2 | Start work | Open | In Progress |
| 3 | Need info | In Progress | Waiting for Customer |
| 4 | Customer replied | Waiting for Customer | In Progress |
| 5 | Resolve | In Progress | Resolved |
| 6 | Resolve | Open | Resolved |
| 7 | Close | Resolved | Closed |
| 8 | Reopen | Closed | In Progress |
| 9 | Reopen | Resolved | In Progress |
| 10 | Cancel | Open | Closed |

💡 Transition #6 exists because sometimes a quick ticket gets fixed instantly without ever being "In Progress".

### Step 6.5 — Add a required Resolution on Close

We want every closed ticket to say *how* it was fixed.

1. Click the **Close** transition
2. Open its **Rules** / **Post functions** / **Validators** area
3. Add a **screen** to the transition that asks for **Resolution** and a comment
   * If you can't add a screen (team-managed project), instead make sure the `Resolution` field is on the ticket view and fill it manually — automation in Part 10 will remind agents.

### Step 6.6 — Make Reopen clear the resolution

1. Click the **Reopen** transition
2. Add a **post function** → **Clear field value** → `Resolution`

> Why? A reopened ticket is not resolved any more. Reports will lie if you skip this.

### Step 6.7 — Publish

Click **Publish** / **Save**. Confirm.

### Step 6.8 — Verify

1. Go to **Queues** → open any ticket (or create a test one with the **Create** button)
2. Click the status dropdown
3. You should see the correct next steps only — from `Open` you should be able to go to *In Progress*, *Resolved*, *Closed*, and nothing weird.

- [ ] Part 6 done. My workflow has 5 statuses and correct arrows.

📄 Full reference: [`config/03-workflow.md`](./config/03-workflow.md)

---

# PART 7 — Build the Queues

A queue is a saved filter. Agents live here all day.

### Step 7.1 — Where to go

**Project settings** → **Queues** (or click **Queues** in the sidebar, then **Manage queues** / the ⚙️ icon).

Delete the sample queues you don't want.

### Step 7.2 — Create queue 1: New Requests

1. Click **Create queue** / **New queue**
2. Name: `1. New Requests`
3. Switch the filter editor to **JQL** (look for "Advanced" or "Switch to JQL")
4. Paste:

```jql
project = ITHD AND status = "Open" ORDER BY created ASC
```

5. Columns to show: `Key`, `Summary`, `Request Type`, `Reporter`, `Created`, `Time to first response`
6. Save

### Step 7.3 — Create the other 5 queues

Same process. Copy each JQL exactly.

**2. Unassigned**
```jql
project = ITHD AND assignee IS EMPTY AND statusCategory != Done ORDER BY created ASC
```

**3. My Open Tickets**
```jql
project = ITHD AND assignee = currentUser() AND statusCategory != Done ORDER BY priority DESC, created ASC
```

**4. High & Critical**
```jql
project = ITHD AND priority IN (Highest, High) AND statusCategory != Done ORDER BY created ASC
```

**5. Waiting for Customer**
```jql
project = ITHD AND status = "Waiting for Customer" ORDER BY updated ASC
```

**6. SLA Breached**
```jql
project = ITHD AND ("Time to resolution" = breached() OR "Time to first response" = breached()) AND statusCategory != Done ORDER BY created ASC
```

⚠️ Queue 6 will error until Part 8 creates the SLAs. Build the SLAs first, then come back — or build it now and fix it after.

### Step 7.4 — Order them

Drag so the order is 1 → 6. Agents read top to bottom, so **New Requests** must be first.

### Step 7.5 — Understand queue vs filter

Queues are shared with the whole team and are always visible in the sidebar. A personal filter is just yours. Queues = team workflow.

- [ ] Part 7 done. 6 queues, correct order.

📄 Full reference: [`config/04-queues.md`](./config/04-queues.md)

---

# PART 8 — Build the SLAs

An SLA is a **countdown clock**. It answers: "are we being fast enough?"

### Step 8.1 — The 3 parts of every SLA

```text
1. START   → when does the clock start ticking?
2. PAUSE   → when does it freeze?  (e.g. waiting for the customer)
3. STOP    → when does it stop forever?
        +
4. GOAL    → how long is allowed, and for which tickets (JQL)
        +
5. CALENDAR→ do weekends count?
```

### Step 8.2 — Create the business hours calendar

1. **Project settings** → **SLAs**
2. Find **Calendars** (or **Manage calendars**)
3. Create a calendar named `Nimbus Business Hours`
4. Working hours: **Mon–Fri, 09:00 → 18:00**
5. Add holidays if you want (e.g. 1 Jan)
6. Save

Also keep the built-in **24/7 Calendar** — we use it for critical tickets.

### Step 8.3 — Create SLA 1: Time to First Response

1. **Project settings** → **SLAs** → **Create SLA**
2. Name: `Time to first response`

**Begin:**
* `Work item created` / `Issue created`

**Pause on:**
* Status = `Waiting for Customer`

**Stop:**
* `Comment: For customers` added (public comment by an agent)

**Goals** — add them in this exact order (Jira reads top to bottom and uses the **first match**):

| Order | JQL | Goal | Calendar |
| --- | --- | --- | --- |
| 1 | `priority = Highest` | `30m` | 24/7 Calendar |
| 2 | `priority = High` | `2h` | Nimbus Business Hours |
| 3 | `priority = Medium` | `4h` | Nimbus Business Hours |
| 4 | `priority = Low` | `8h` | Nimbus Business Hours |
| 5 | *(leave JQL empty = everything else)* | `8h` | Nimbus Business Hours |

3. Save

🧠 **The #1 SLA mistake:** putting the "everything else" goal at the top. Then it matches every ticket and your priority goals never run. Always put the catch-all **last**.

### Step 8.4 — Create SLA 2: Time to Resolution

Name: `Time to resolution`

**Begin:**
* `Work item created`

**Pause on:**
* Status = `Waiting for Customer`
* Status = `Pending Approval` (if you have it)

**Stop:**
* `Status: Resolved`
* `Status: Closed`
* `Resolution: Set`

**Goals:**

| Order | JQL | Goal | Calendar |
| --- | --- | --- | --- |
| 1 | `priority = Highest` | `4h` | 24/7 Calendar |
| 2 | `priority = High` | `8h` | Nimbus Business Hours |
| 3 | `priority = Medium` | `24h` | Nimbus Business Hours |
| 4 | `priority = Low` | `40h` | Nimbus Business Hours |
| 5 | *(empty)* | `24h` | Nimbus Business Hours |

### Step 8.5 — Create SLA 3: Time Waiting for Support (optional but nice)

Name: `Time waiting for support`

* **Begin:** Comment: For customers *by customer*, and Work item created
* **Pause:** never
* **Stop:** Comment: For customers *by agent*
* **Goal:** empty JQL → `4h`, Nimbus Business Hours

This measures "how long has the customer been ignored". Great for coaching agents.

### Step 8.6 — Verify

1. Create a test ticket (**Create** button in the agent view)
2. Open it
3. On the right panel you should see a **countdown**, e.g. `3h 58m remaining`
4. Move it to **Waiting for Customer** → the clock should show as **paused**
5. Move it back → it resumes
6. Add a public comment → *Time to first response* should show **✅ met**

### Step 8.7 — Fix queue 6

Go back to Part 7 queue **6. SLA Breached** and save the JQL now that the SLA names exist.

- [ ] Part 8 done. Tickets show countdown timers that pause correctly.

📄 Full reference: [`config/05-slas.md`](./config/05-slas.md)

---

# PART 9 — Build Approvals

Some things need a manager to say **yes** before IT does the work:

* Laptop Request (costs money)
* Software Installation (costs a licence)
* Access Request (security risk)

### Step 9.1 — How approvals actually work

```text
Customer submits
       ▼
  PENDING APPROVAL   ← ticket waits here, agent does nothing
       ▼
 Approver gets email + portal link
       │
   ┌───┴────┐
   ▼        ▼
APPROVE   DECLINE
   │        │
   ▼        ▼
In Progress  Closed (Declined)
```

The key pieces:
1. A **status** in the workflow (`Pending Approval`)
2. An **approval step** attached to that status
3. A field that says **who** approves

### Step 9.2 — Add the Pending Approval status

1. **Project settings** → **Workflows** → edit the workflow used by *Laptop Request / Software Installation / Access Request*
2. Add status `Pending Approval` → category **To Do**
3. Add transitions:

| Transition | From | To |
| --- | --- | --- |
| *(Create)* | — | Pending Approval |
| Approve | Pending Approval | In Progress |
| Decline | Pending Approval | Closed |
| Cancel | Pending Approval | Closed |

4. Make `Pending Approval` the **first status after create** for these three request types.

> If you used the **Service Request with Approvals** issue type in Part 4, this status already exists. Just check the transitions.

### Step 9.3 — Create the approver field

Approvals need to know *who* approves. Two options:

**Option A (simplest — fixed approvers):**
Pick specific users as approvers in the approval config. Good for a lab.

**Option B (real world — customer names their manager):**
1. ⚙️ **Settings** → **Issues** → **Custom fields** → **Create custom field**
2. Type: **User picker (single user)**
3. Name: `Approver`
4. Add it to your screens
5. Add it to the request forms for the 3 approval request types

⚠️ Note: the `Manager Email` text field from Part 5 is for humans to read. Approvals need a real **user picker** field, not text. Keep both.

### Step 9.4 — Configure the approval step

1. In the workflow editor, click the **Pending Approval** status
2. Find **Approvals** → **Add approval**
3. Configure:

| Setting | Value |
| --- | --- |
| Approvers from | `Approver` field (Option B) or *specific users* (Option A) |
| How many approvals needed | `1` |
| Transition when approved | `Approve` → In Progress |
| Transition when declined | `Decline` → Closed |

4. Save and **Publish** the workflow

### Step 9.5 — Make the approver a customer

The approver must be able to log into the portal.

1. **Customers** → make sure `you+manager1@gmail.com` is listed
2. If your approver is an agent, that also works

### Step 9.6 — Pause the SLA during approval

Go back to **Project settings** → **SLAs** → `Time to resolution` → add to **Pause on**: status `Pending Approval`.

> Why? It is not IT's fault the manager went to lunch. Don't let approvals breach your SLA.

### Step 9.7 — Test it

1. Open the portal as `you+emp1@gmail.com`
2. Submit **Software Installation**, set Approver = `you+manager1@gmail.com`
3. Check the manager's inbox — there should be an approval email
4. Click the link → portal shows **Approve** / **Decline** buttons
5. Click **Approve**
6. Ticket should jump to **In Progress**

- [ ] Part 9 done. Approvals block work until a manager says yes.

---

# PART 10 — Build the Automation Rules

Automation = robots. This is where the help desk starts to feel magic.

### Step 10.1 — Where to go

**Project settings** → **Automation** (or ⚙️ → **System** → **Automation rules**).

Every rule has the same 3 pieces:

```text
WHEN (trigger)   →   IF (condition)   →   THEN (action)
```

⚠️ **Free plan limit:** 100 rule runs per month per site. Our 8 rules are cheap, but don't leave a runaway rule looping. ([Jira plans](https://www.atlassian.com/software/jira/guides/more/jira-editions)) *Content was rephrased for compliance with licensing restrictions.*

---

### Rule 1 — Set priority automatically

**Why:** customers can't be trusted with Priority, so we compute it.

1. **Create rule**
2. **Trigger:** `Work item created`
3. **Add condition** → **Work item fields condition**:
   * Field: `Impact Level`
   * Condition: `equals`
   * Value: `Whole office`
4. **Add action** → **Edit work item** → set `Priority` = `Highest`
5. Now add a **branch-free alternative** using more rules, or use **If/else block**:

| If Impact Level = | Set Priority = |
| --- | --- |
| Whole office | Highest |
| My team | High |
| Only me | Medium |

6. Name it: `1 - Auto set priority from impact`
7. **Turn it on**

💡 If your plan has **If/else blocks**, do it in one rule. If not, make 3 small rules.

---

### Rule 2 — Auto-assign by request type

**Why:** nobody should have to pick up tickets manually.

1. **Trigger:** `Work item created`
2. **Condition** → **Work item fields condition** → `Request Type` is one of `Laptop Issue`, `Laptop Request`, `Wi-Fi Issue`
3. **Action** → **Assign work item** → to `you+agent2@gmail.com`
4. Name: `2a - Route hardware to Hardware team`

Repeat for:

| Rule | Request types | Assign to |
| --- | --- | --- |
| 2a | Laptop Issue, Laptop Request, Wi-Fi Issue | agent2 (Hardware) |
| 2b | Access Request, Password Reset, Software Installation | agent3 (Access) |
| 2c | Email Issue, VPN Issue, General IT Support | you (Service Desk) |

**Better alternative if available:** action → **Assign work item** → *Balanced workload* → pick the project role **Service Desk Team**. This spreads tickets evenly.

---

### Rule 3 — Welcome comment to the customer

1. **Trigger:** `Work item created`
2. **Action** → **Comment on work item** → choose **Share with customer** (public!)
3. Body:

```text
Hi {{reporter.displayName}},

Thanks for contacting the Nimbus IT Help Desk 👋

We've logged your request as {{issue.key}}.
Priority: {{issue.priority.name}}
We'll respond within our target time for this priority.

You can track it here: {{issue.url.customer}}

— Nimbus IT
```

4. Name: `3 - Send welcome comment`

🧠 Those `{{...}}` things are **smart values** — placeholders Jira fills in. Learn these 6:

| Smart value | Becomes |
| --- | --- |
| `{{issue.key}}` | ITHD-42 |
| `{{issue.summary}}` | The ticket title |
| `{{reporter.displayName}}` | Priya Sharma |
| `{{issue.priority.name}}` | High |
| `{{issue.url.customer}}` | The portal link |
| `{{now}}` | Right now, as a date |

---

### Rule 4 — Move to In Progress on first agent comment

**Why:** agents forget to change status.

1. **Trigger:** `Work item commented`
2. **Condition** → **User condition** → user is in role `Service Desk Team`
3. **Condition** → **Work item fields condition** → `Status` equals `Open`
4. **Action** → **Transition work item** → to `In Progress`
5. Name: `4 - Auto start work on agent comment`

---

### Rule 5 — Customer replies → back to In Progress

1. **Trigger:** `Work item commented`
2. **Condition** → **User condition** → user is `Reporter`
3. **Condition** → `Status` equals `Waiting for Customer`
4. **Actions:**
   * **Transition work item** → `In Progress`
   * **Add comment (internal)**: `Customer replied at {{now}} — please review.`
5. Name: `5 - Customer replied, resume work`

---

### Rule 6 — Escalate when SLA is nearly breached

1. **Trigger:** `SLA threshold breached`
   * SLA: `Time to resolution`
   * Condition: **will breach in** `30 minutes`
2. **Actions:**
   * **Edit work item** → add label `sla-at-risk`
   * **Add comment (internal)**: `⚠️ SLA breaches in 30 minutes. {{issue.key}} — {{issue.summary}}`
   * **Send email** → to the project lead → subject `SLA risk: {{issue.key}}`
3. Name: `6 - Escalate before SLA breach`

---

### Rule 7 — Auto-close resolved tickets after 3 days

1. **Trigger:** `Scheduled` → run **daily**
2. Tick **run a JQL search** and paste:

```jql
project = ITHD AND status = Resolved AND updated <= -3d
```

3. **Actions:**
   * **Comment (public)**: `This request has been resolved for 3 days, so we're closing it. Reply any time to reopen.`
   * **Transition work item** → `Closed`
4. Name: `7 - Auto-close resolved after 3 days`

---

### Rule 8 — Nudge the customer, then close abandoned tickets

1. **Trigger:** `Scheduled` → daily
2. JQL:

```jql
project = ITHD AND status = "Waiting for Customer" AND updated <= -5d
```

3. **Actions:**
   * **Comment (public)**: `Just checking in — we still need your reply on {{issue.key}}. We'll close this in 2 days if we don't hear back.`
4. Name: `8 - Nudge silent customers`

Optional second rule with `updated <= -7d` that transitions to `Closed` with resolution `Won't Do`.

---

### Step 10.2 — Verify automation

1. Create a ticket from the portal
2. Within ~30 seconds it should have: a priority, an assignee, and a welcome comment
3. If nothing happened → **Project settings** → **Automation** → open the rule → **Audit log**. It tells you exactly why it did or didn't run.

🔧 **The 4 reasons automation "doesn't work":**
1. The rule is **off** (toggle at the top)
2. The **actor** lacks permission → set the rule actor to `Automation for Jira` or an admin
3. A **condition** didn't match (audit log says "no actions performed")
4. The rule ignores its own changes — by default rules don't trigger themselves. That's on purpose.

- [ ] Part 10 done. 8 rules live and passing their audit logs.

📄 Full reference: [`config/06-automation-rules.md`](./config/06-automation-rules.md)

---

# PART 11 — Build the Knowledge Base

Goal: the customer fixes their own problem and **never creates a ticket**. That is called **request deflection** and it is the cheapest win in IT.

### Step 11.1 — Get Confluence (free)

1. ⚙️ **Settings** → **Billing** → **Discover more products** (or the app switcher grid, top-left)
2. Add **Confluence** → choose **Free**
3. Wait ~1 minute for it to provision

### Step 11.2 — Create the space

1. Open Confluence
2. **Create space** → **Blank space**
3. Name: `Nimbus IT Knowledge Base`
4. Key: `ITKB`

### Step 11.3 — Create the page structure

Create these as parent pages inside the space:

```text
Nimbus IT Knowledge Base
├── 💻 Laptop & Hardware
├── 🔐 Passwords & Accounts
├── 🌐 Network & VPN
├── 📧 Email
└── 💾 Software
```

### Step 11.4 — Write the 6 articles

Copy the ready-made content from the `knowledge-base/` folder in this repo:

| Article | File to copy from | Put under |
| --- | --- | --- |
| How to Reset Your Password | `knowledge-base/01-password-reset.md` | Passwords & Accounts |
| Fix VPN Connection Problems | `knowledge-base/02-vpn-troubleshooting.md` | Network & VPN |
| Fix Wi-Fi Connection Problems | `knowledge-base/03-wifi-troubleshooting.md` | Network & VPN |
| My Laptop Is Slow | `knowledge-base/04-laptop-slow.md` | Laptop & Hardware |
| Fix Email Not Sending or Receiving | `knowledge-base/05-email-issues.md` | Email |
| How to Request Software | `knowledge-base/06-request-software.md` | Software |

**Write every article in this shape** — it's what makes a KB useful:

```text
1. Title = the problem in the customer's words
   ✅ "I can't connect to VPN"
   ❌ "VPN Client Remediation Procedure"
2. Who this is for (1 line)
3. Try this first (the 3 fixes that solve 80% of cases)
4. Step-by-step, numbered
5. Still broken? → link to the portal request type
```

### Step 11.5 — Link the space to your project

1. Back in Jira → **Project settings** → **Knowledge base**
2. Click **Link Confluence space**
3. Pick `Nimbus IT Knowledge Base`
4. Choose **Anyone can view articles** (so customers who aren't logged in can read them)

### Step 11.6 — Connect articles to request types

1. **Project settings** → **Knowledge base**
2. For each request type, add the label or search term that surfaces the right articles

Add these labels to your Confluence pages so matching works:

| Article | Confluence labels |
| --- | --- |
| Password Reset | `password`, `login`, `locked-out`, `mfa` |
| VPN | `vpn`, `remote`, `connection` |
| Wi-Fi | `wifi`, `wireless`, `network` |
| Laptop Slow | `laptop`, `slow`, `performance` |
| Email | `email`, `outlook`, `mail` |
| Request Software | `software`, `install`, `licence` |

### Step 11.7 — Verify deflection

1. Open the portal as a customer
2. Click **Password Reset**
3. Start typing `password` in the summary box
4. 👀 Articles should appear beside/below the form

That popup is the whole point. Every time someone reads it instead of submitting, you saved an agent 15 minutes.

- [ ] Part 11 done. 6 articles live and surfacing in the portal.

---

# PART 12 — Brand the Portal

Right now the portal says "IT Help Desk" in Atlassian blue. Let's make it look like Nimbus Corp.

### Step 12.1 — Portal name and intro

1. **Project settings** → **Portal settings**
2. Set:

| Field | Value |
| --- | --- |
| Name | `Nimbus IT Help Desk` |
| Intro text | `Need IT help? Pick a category below. For urgent outages call the IT hotline on x4357.` |

3. Upload a logo (any square PNG, 48×48 or bigger)

### Step 12.2 — Help Center branding (site-wide)

1. ⚙️ **Settings** → **Products** → **Jira Service Management** → **Configuration**, or from the Help Center click **Edit Help Center appearance**
2. Set:
   * Help Center name: `Nimbus Corp Service Portal`
   * Banner image
   * Banner text colour
   * Primary highlight colour — pick your brand colour

### Step 12.3 — Announcement banner

Add a banner customers see on every visit:

```text
📢 Planned maintenance Saturday 22:00–23:00. VPN may drop briefly.
```

Set it in **Portal settings** → announcement, and site-wide in the Help Center config.

### Step 12.4 — Check request type order

Drag your request types so the **most common ones are first**. Real usage order for an IT desk:

```text
1. Password Reset       ← always #1
2. Laptop Issue
3. Wi-Fi Issue
4. VPN Issue
5. Software Installation
6. Access Request
7. Email Issue
8. Laptop Request
9. General IT Support
```

### Step 12.5 — Turn on the email channel (optional, powerful)

1. **Project settings** → **Email requests** / **Channels**
2. You get a free address like `ithd@yoursite.atlassian.net`
3. Set the default request type for emailed tickets → `General IT Support`
4. Send a test email to it → a ticket should appear in ~1 minute

Now employees can create tickets *without even opening the portal*.

- [ ] Part 12 done. Portal looks like a real company service desk.

---

# PART 13 — Test Everything

Do not skip this. This is where you find the 5 things you configured wrong.

### Step 13.1 — Set up to test properly

Open **two browsers** (or one normal + one incognito):

| Window | Logged in as | Purpose |
| --- | --- | --- |
| A | you (admin/agent) | Agent view |
| B | `you+emp1@gmail.com` | Customer portal |

To log in as the customer: open the portal URL in window B, click **sign up / log in**, use the invite email that Jira sent to `you+emp1@gmail.com`.

### Step 13.2 — Run the 10 tests

Full details in [`testing/test-scenarios.md`](./testing/test-scenarios.md). Quick version:

| # | Test | Pass looks like |
| --- | --- | --- |
| 1 | Customer submits Password Reset | Ticket appears in `1. New Requests` |
| 2 | Automation fires | Priority set, assignee set, welcome comment posted |
| 3 | SLA starts | Countdown visible on the ticket |
| 4 | Agent public comment | Customer gets email; *First response* SLA met |
| 5 | Waiting for Customer | SLA clock pauses |
| 6 | Customer replies | Status flips back to In Progress automatically |
| 7 | Internal comment | Customer **cannot** see it in the portal |
| 8 | Approval flow | Software Installation waits, manager approves, ticket moves on |
| 9 | Resolve → Close | Resolution required; ticket leaves active queues |
| 10 | KB deflection | Typing "password" shows the article |

### Step 13.3 — The internal-comment test is the most important one

Log in as the customer and look at the ticket. If you can see the internal note, your comment visibility is wrong and you have just leaked internal chat to an employee. Fix it before anything else.

- [ ] Part 13 done. All 10 tests pass.

---

# PART 14 — Build a Dashboard

### Step 14.1 — Create it

1. Top nav → **Dashboards** → **Create dashboard**
2. Name: `Nimbus IT Help Desk — Overview`
3. Layout: two columns

### Step 14.2 — Add these gadgets

| Gadget | Configure with |
| --- | --- |
| **Filter Results** | `project = ITHD AND statusCategory != Done ORDER BY created ASC` — title "Open tickets" |
| **Pie Chart** | Project ITHD, group by `Request Type` |
| **Pie Chart** | Project ITHD, group by `Priority` |
| **Created vs Resolved Chart** | Project ITHD, last 30 days |
| **Average Age Chart** | Project ITHD |
| **Two Dimensional Filter Statistics** | Filter: ITHD open. X = `Assignee`, Y = `Status` |

### Step 14.3 — Use the built-in reports too

Left sidebar → **Reports**. You get SLA-aware reports for free:

* **Created vs Resolved** — are we keeping up?
* **Time to resolution** — are we hitting SLA?
* **SLA success rate** — the number your boss asks for
* **Workload** — who is drowning?

- [ ] Part 14 done. I have a dashboard.

---

# 🏁 You Are Finished

You built:

```text
✅ A live Atlassian site
✅ A JSM service project (ITHD)
✅ 3 agents, 3 customers, 3 organizations
✅ 9 request types in 3 portal groups
✅ 8 custom fields on tailored forms
✅ A 6-status workflow with proper transitions
✅ 6 agent queues
✅ 3 SLAs with priority goals + business hours + pause rules
✅ Approval flow for money/security requests
✅ 8 automation rules
✅ A Confluence knowledge base with 6 articles, deflecting tickets
✅ A branded portal + email channel
✅ 10 passing tests
✅ A reporting dashboard
```

## 🎤 How to talk about this in an interview

> "I built an internal IT help desk in Jira Service Management. Nine request types across three portal groups, each with a tailored form. Tickets are auto-prioritised from a business-impact field rather than letting customers self-select priority, then routed to the right team by request type. SLAs are priority-based against a business-hours calendar, and they pause while we're waiting on the customer or on an approval, so the clock only runs when the work is actually ours. Money and access requests go through a manager approval gate. Eight automation rules handle assignment, status hygiene, SLA escalation, and auto-closure. A linked Confluence knowledge base deflects the common password and VPN requests at the point of submission."

That paragraph is the whole point of Project 1.

## 🧹 Optional: keep your site tidy

If you want to keep this site for Projects 2–8 (recommended), leave everything. If you want to reset:

* Don't delete the site — you'd lose your URL
* Instead archive the project: **Project settings** → **Details** → **Move to trash**

## ➡️ Next

**Project 2 — Employee Service Management.** We take everything here and expand it to HR, Finance, Facilities and Security, with department-based routing and multiple service catalogs.

---

# 🆘 Troubleshooting

| Problem | Cause | Fix |
| --- | --- | --- |
| Customer can't see the portal | Not added as a customer, or permissions too tight | **Customer permissions** → allow, and add them under **Customers** |
| "You don't have access to this project" | You invited them as an agent but have no seats left | Free plan = 3 agents. Remove one, or add them as a customer instead |
| Custom field doesn't appear | Not associated with a screen | ⚙️ → Issues → Custom fields → your field → **Screens** → tick the ITHD screens |
| SLA shows no countdown | No goal matched the ticket | Add a catch-all goal with **empty JQL** as the **last** goal |
| SLA never pauses | Pause condition uses the wrong status name | Status names must match exactly, including capital letters |
| Automation didn't run | Rule off / condition failed / no permission | Open the rule → **Audit log**. It states the reason |
| Automation ran but changed nothing | Actor lacks permission | Set rule actor to `Automation for Jira` |
| Approval buttons missing | Approver field empty, or approver isn't a customer/agent | Fill the `Approver` user-picker field; add them as a customer |
| Emails not arriving | Notification off, or Free-plan email cap hit | **Project settings** → Notifications. Free/trial sites cap outbound automation email per 24h ([automation limits](https://support.atlassian.com/cloud-automation/docs/automation-service-limits/)) |
| Can't edit the workflow | It's a shared system workflow | Let Jira create a **copy/draft**, edit that, then publish |
| Queue JQL error | SLA or field name doesn't exist yet | Build SLAs (Part 8) first, then save the queue |
| KB articles don't show in portal | Space not linked, or permissions restricted | **Project settings** → Knowledge base → link space, allow public viewing |

---

*Sources: [Jira plan comparison](https://www.atlassian.com/software/jira/guides/more/jira-editions), [JSM agent licensing](https://support.atlassian.com/jira-service-management-cloud/docs/overview-of-jira-cloud-products/), [automation service limits](https://support.atlassian.com/cloud-automation/docs/automation-service-limits/). Content was rephrased for compliance with licensing restrictions.*

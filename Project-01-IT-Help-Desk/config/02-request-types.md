# 02 — Request Types & Fields

Reference for [DEPLOY.md Part 4](../DEPLOY.md#part-4--build-the-9-request-types) and [Part 5](../DEPLOY.md#part-5--build-the-forms-and-fields).

---

## Portal layout

```text
Nimbus IT Help Desk
├── Hardware
│   ├── Laptop Issue
│   ├── Laptop Request           🔒 needs approval
│   └── Wi-Fi Issue
├── Software & Accounts
│   ├── Software Installation    🔒 needs approval
│   ├── Password Reset
│   ├── Email Issue
│   └── VPN Issue
└── Access & Other
    ├── Access Request           🔒 needs approval
    └── General IT Support
```

---

## Master table

| # | Request type | Issue type | Group | Approval | Default priority | Team |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Laptop Issue | Service Request | Hardware | No | Medium | Hardware |
| 2 | Laptop Request | Service Request with Approvals | Hardware | Yes | Low | Hardware |
| 3 | Wi-Fi Issue | Service Request | Hardware | No | Medium | Hardware |
| 4 | Software Installation | Service Request with Approvals | Software & Accounts | Yes | Low | Access |
| 5 | Password Reset | Service Request | Software & Accounts | No | High | Access |
| 6 | Email Issue | Service Request | Software & Accounts | No | Medium | Service Desk |
| 7 | VPN Issue | Service Request | Software & Accounts | No | High | Service Desk |
| 8 | Access Request | Service Request with Approvals | Access & Other | Yes | Medium | Access |
| 9 | General IT Support | Service Request | Access & Other | No | Medium | Service Desk |

---

## Custom fields to create

| Field | Type | Options |
| --- | --- | --- |
| Asset Tag | Text (single line) | — |
| Impact Level | Select (single) | Only me / My team / Whole office |
| Software Name | Text (single line) | — |
| Business Justification | Paragraph | — |
| System / Application | Select (single) | Payroll / CRM / Shared Drive / Jira / VPN / Other |
| Access Level | Select (single) | Read only / Read + Write / Admin |
| Manager Email | Text (single line) | — |
| Location | Select (single) | HQ Floor 1 / HQ Floor 2 / Remote |
| Approver | User picker (single) | — (needed for real approvals) |

⚠️ After creating each field, associate it with the ITHD screens or it will never appear.

---

## Field-to-request-type matrix

`R` = required, `O` = optional, `–` = not on the form

| Field | Laptop Issue | Laptop Req | Wi-Fi | Software Inst | Password | Email | VPN | Access Req | General |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Summary | R | R | R | R | R | R | R | R | R |
| Description | R | R | R | O | O | R | R | O | R |
| Attachment | O | – | O | O | – | O | O | – | O |
| Asset Tag | O | – | – | O | – | – | – | – | – |
| Impact Level | R | – | R | – | – | – | – | – | R |
| Location | R | R | R | – | – | – | R | – | – |
| Software Name | – | – | – | R | – | – | – | – | – |
| Business Justification | – | R | – | R | – | – | – | R | – |
| Manager Email | – | R | – | R | – | – | – | R | – |
| System / Application | – | – | – | – | R | – | – | R | – |
| Access Level | – | – | – | – | – | – | – | R | – |
| Approver | – | R | – | R | – | – | – | R | – |
| Priority | hidden | hidden | hidden | hidden | hidden | hidden | hidden | hidden | hidden |

**Priority is hidden from every form on purpose.** Automation Rule 1 sets it from Impact Level and request type. Customers who pick their own priority always pick the highest one.

---

## Customer-facing wording

Never show a customer a field label like `Impact Level`. Rewrite it as a question:

| Internal name | What the customer reads |
| --- | --- |
| Summary | What's wrong? |
| Description | Tell us more — when did it start? |
| Impact Level | Who is affected? |
| Asset Tag | Laptop asset tag (sticker on the bottom) |
| Business Justification | Why do you need this? |
| System / Application | Which system? |
| Access Level | What level of access? |
| Manager Email | Your manager's email |
| Location | Where are you? |

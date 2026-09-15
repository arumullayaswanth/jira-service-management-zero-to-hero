# Optional — Create a Ticket With the REST API

Not required for Project 1. Do this if you want a preview of Project 7.

---

## Step 1 — Create an API token

1. Go to <https://id.atlassian.com/manage-profile/security/api-tokens>
2. Click **Create API token**
3. Label it `jsm-lab`
4. **Copy it now.** You cannot see it again.

🔒 Treat the token like a password. Don't commit it to git, don't paste it in chat, don't put it in a screenshot.

---

## Step 2 — Store it as an environment variable

Never put the token in a script file.

**Windows CMD:**
```cmd
set JIRA_EMAIL=you@gmail.com
set JIRA_TOKEN=paste-your-token-here
set JIRA_SITE=https://nimbus-yourname.atlassian.net
```

**PowerShell:**
```powershell
$env:JIRA_EMAIL="you@gmail.com"
$env:JIRA_TOKEN="paste-your-token-here"
$env:JIRA_SITE="https://nimbus-yourname.atlassian.net"
```

These last only for the current terminal session, which is what you want for a lab.

---

## Step 3 — Find your service desk ID and request type IDs

```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" \
  -H "Accept: application/json" \
  "$JIRA_SITE/rest/servicedeskapi/servicedesk"
```

Note the `id` for IT Help Desk (usually `1`).

Then list request types:

```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" \
  -H "Accept: application/json" \
  "$JIRA_SITE/rest/servicedeskapi/servicedesk/1/requesttype"
```

Note the `id` of the request type you want.

---

## Step 4 — Create a request

```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  --data '{
    "serviceDeskId": "1",
    "requestTypeId": "10",
    "requestFieldValues": {
      "summary": "Created via REST API",
      "description": "This ticket was created by a script, not a human."
    }
  }' \
  "$JIRA_SITE/rest/servicedeskapi/request"
```

The response contains the new issue key. Check your `1. New Requests` queue — it should be there, and your automation rules should have fired on it exactly like a portal ticket.

---

## Other useful calls

**Get one request**
```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" \
  "$JIRA_SITE/rest/servicedeskapi/request/ITHD-1"
```

**Add a public comment**
```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" -X POST \
  -H "Content-Type: application/json" \
  --data '{"body":"Comment from the API","public":true}' \
  "$JIRA_SITE/rest/servicedeskapi/request/ITHD-1/comment"
```

**Search with JQL**
```bash
curl -u "$JIRA_EMAIL:$JIRA_TOKEN" \
  -G --data-urlencode 'jql=project=ITHD AND statusCategory != Done' \
  "$JIRA_SITE/rest/api/3/search"
```

---

## Two APIs, and why it matters

| API | Path | Use it for |
| --- | --- | --- |
| **Service Desk API** | `/rest/servicedeskapi/...` | Customer-facing: requests, portal comments, approvals, organizations |
| **Jira Platform API** | `/rest/api/3/...` | Agent-side: issues, fields, transitions, JQL search |

Use the Service Desk API when you want the ticket to behave like a real customer request — it respects request types and public/internal comment visibility. Use the platform API for bulk agent operations and searching.

---

## Common errors

| Status | Meaning | Fix |
| --- | --- | --- |
| 401 | Bad credentials | Use your **email + API token**, not your password |
| 403 | No permission | Your account isn't an agent on that project |
| 404 | Wrong ID or wrong site URL | Re-check the service desk ID and site URL |
| 400 | Bad payload | A required field is missing — the response names it |

---

## Next

Project 7 goes much deeper: webhooks, CI/CD triggers, automated incident creation from monitoring alerts, and API-driven change management.

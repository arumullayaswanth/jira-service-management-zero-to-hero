# Fix Email Not Sending or Receiving

**Labels:** `email` `outlook` `mail` `mailbox`
**Category:** Email

---

## Who this is for

Email won't send, won't arrive, or your mail app keeps asking for a password.

---

## Try this first

1. **Check webmail in a browser.** Sign in to your mail on the web. If email works there, the problem is your desktop app, not your mailbox. That's a much smaller problem.
2. **Restart the mail app** — fully quit it, don't just close the window.
3. **Check you're online.** Open any website.

---

## Email won't send / stuck in Outbox

1. **Check the recipient address for typos.** One wrong character and it silently fails.
2. **Check the attachment size.** Over 25 MB usually gets rejected. Share a cloud link instead.
3. **Look in your Outbox.** If messages are piling up there, the app can't reach the server — usually a password or connection problem.
4. **Work offline mode:** in Outlook, check the **Send/Receive** tab and make sure **Work Offline** is not enabled. This catches people surprisingly often.

---

## Email not arriving

1. **Check Junk / Spam.** Always check here first.
2. **Check your rules.** A rule you set up months ago may be filing mail into a folder you never open.
   * Outlook: File → Manage Rules & Alerts
3. **Check if your mailbox is full.** A full mailbox silently rejects incoming mail.
4. **Ask the sender for the bounce message.** If they got a delivery failure, the text of it tells us exactly what's wrong. Ask them to forward it to you.

---

## It keeps asking for my password

1. Your password probably changed recently. Enter the current one.
2. Approve the MFA prompt on your phone.
3. If it asks again immediately after you enter the correct password, the saved credential is corrupted. Raise a ticket — we need to clear the credential store, and the exact steps differ per machine.

---

## Calendar invites are wrong or missing

1. Check your time zone: it should match your actual location.
2. Refresh the calendar view, or restart the app.
3. If a meeting shows at the wrong hour for only *some* attendees, it's a time-zone mismatch. Note who sees what — it helps us pinpoint it.

---

## Mailbox is full

1. Empty Deleted Items / Trash.
2. Sort by size and delete the biggest messages — usually old attachments.
3. Empty the Junk folder.
4. Need more space permanently? Raise a ticket and say how much you have and how fast you fill it.

---

## Still stuck?

👉 Raise an **Email Issue** request in the portal.

Tell us:
* Is it sending, receiving, or both?
* Does webmail in a browser work?
* The exact error message (screenshot is best)
* Which app and which device
* If a specific message failed: the recipient and the time you sent it

**Target response:** 4 hours during business hours.

# Fix VPN Connection Problems

**Labels:** `vpn` `remote` `connection` `work-from-home`
**Category:** Network & VPN

---

## Who this is for

The VPN won't connect, or it connects and then drops, or you're connected but company sites still don't load.

---

## Try this first

These three fix most VPN problems:

1. **Check your normal internet works.** Open any public website *without* the VPN. If that fails, the problem is your home Wi-Fi, not the VPN.
2. **Fully quit and reopen the VPN client.** Not just the window — quit it from the system tray / menu bar so the background process restarts.
3. **Restart your laptop.** Genuinely fixes a large share of VPN adapter problems.

---

## "Authentication failed"

1. Your VPN password is your normal work password. If you changed it recently, use the new one.
2. Check the username format. Some clients want `you@nimbus.com`, others want just `you`.
3. Approve the MFA prompt on your phone — VPN logins usually need it, and the prompt often arrives a few seconds late.
4. Three wrong attempts locks the account for 15 minutes. Wait it out rather than retrying.

---

## "Connection timed out" or it never finishes connecting

1. **Switch networks.** Try your phone's hotspot. If the VPN works on the hotspot, your home router or ISP is blocking it.
2. **Hotel or café Wi-Fi?** You usually have to open a browser and accept their terms page before anything else works.
3. **Try the other gateway.** Most clients let you pick a region — switch to a different one.
4. **Turn off other VPNs.** A personal VPN running at the same time will fight with the work one.

---

## Connected, but company sites don't load

This is usually DNS.

1. Disconnect and reconnect the VPN.
2. Flush your DNS cache:
   * **Windows:** open Command Prompt and run `ipconfig /flushdns`
   * **Mac:** open Terminal and run `sudo dscacheutil -flushcache`
3. Try the site's IP address if you know it. If the IP works but the name doesn't, it's definitely DNS — tell us that, it saves us 20 minutes.

---

## Keeps disconnecting every few minutes

1. Move closer to your Wi-Fi router, or plug in with a cable.
2. Switch your Wi-Fi to the 5 GHz band if you have both.
3. Close bandwidth-heavy apps — cloud backup and video calls both starve the VPN tunnel.
4. If it drops at exactly the same interval every time, note that interval. It points at a session timeout and it's a strong clue for us.

---

## Still stuck?

👉 Raise a **VPN Issue** request in the portal.

Tell us:
* The exact error message (a screenshot is ideal)
* Where you're connecting from — home, office, hotel, hotspot
* Whether the internet works without the VPN
* Whether it ever connects, or fails every time

**Target response:** 2 hours during business hours.

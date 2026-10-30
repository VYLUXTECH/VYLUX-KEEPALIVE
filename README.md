# VYLUX-KEEPALIVE
Free Render spin-down prevention. Pings every 5 min (public repo -> unlimited free Actions minutes):
- Target A: backend on Render (keeps the WhatsApp/Baileys session connected)
- Target B: frontend on Vercel

URLs are stored as repo secrets (PING_URL / PING_URL2), not in code.
`heartbeat.yml` makes a weekly commit so GitHub's 60-day inactivity auto-disable never turns the cron off.

Why not inside VYLUX-ADMIN: that repo is private, and private-repo Actions burn the 2,000 free minutes/month (~8,600 runs/mo at 5-min cadence) - a public repo uses zero minutes.

## PanelBot free-tier watchdog (panelbot-renew.yml)
Every 8 h this repo also checks the PanelBot dashboard (session alive? expiry date?) and attempts a
renewal POST for paid categories. Free categories cannot be renewed (panel rejects with
"Panel gratis tidak dapat diperpanjang") and only allow ONE active free panel - so free-tier
continuity is handled by a box-local watcher instead:

    /root/.aichatapi/panelbot_keepalive.py   (cron hourly, drives local Chrome over CDP)
      - healthy? -> exit 0
      - renewal attempt (paid path) -> free: rejected
      - create fresh Free server (Bot Development / Node.js) once the single free slot frees up
      - when the old panel still holds the slot: logs "slot_conflict", retries next run
      - panel is auto-deleted 1 day after expiry, so the hourly cadence keeps downtime ~< 1 h

Secrets never live in code:
    GitHub repo secrets : PANELBOT_BASE_URL, PANELBOT_SERVER_PATH, PANELBOT_RENEW_PATH, PANELBOT_COOKIES
    box-local env file  : /root/.aichatapi/panelbot.env (chmod 600)
State/log on the box: /root/.aichatapi/panelbot_state.json, panelbot_keepalive.log

# VYLUX-KEEPALIVE
Free Render spin-down prevention. Pings every 5 min (public repo → unlimited free Actions minutes):
- `https://jayo.vyluxtech.com/` (Render backend — keeps the WhatsApp/Baileys session connected)
- `https://top.vyluxtech.com/` (Vercel frontend)

`heartbeat.yml` makes a weekly commit so GitHub's 60-day inactivity auto-disable never turns the cron off.

Why not inside VYLUX-ADMIN: that repo is private, and private-repo Actions burn the 2000 free minutes/month (~8,600 runs/mo at 5-min cadence) — a public repo uses zero minutes.

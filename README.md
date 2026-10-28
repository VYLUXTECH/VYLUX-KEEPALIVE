# VYLUX-KEEPALIVE
Free Render spin-down prevention. Pings every 5 min (public repo -> unlimited free Actions minutes):
- Target A: backend on Render (keeps the WhatsApp/Baileys session connected)
- Target B: frontend on Vercel

URLs are stored as repo secrets (PING_URL / PING_URL2), not in code.
`heartbeat.yml` makes a weekly commit so GitHub's 60-day inactivity auto-disable never turns the cron off.

Why not inside VYLUX-ADMIN: that repo is private, and private-repo Actions burn the 2,000 free minutes/month (~8,600 runs/mo at 5-min cadence) - a public repo uses zero minutes.

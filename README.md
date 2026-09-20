# TaqOptionKe

Real-time digit trading platform. Node.js backend, single-file frontend, Postgres persistence, Telegram bot for withdrawal approvals.

## Deploy

1. Free Postgres at https://neon.tech → copy connection string ending with `?sslmode=require`
2. Push this repo to GitHub
3. Render → New Web Service → connect repo
   - Environment: Node
   - Build: npm install
   - Start: node server.js
   - Free tier
4. Add env vars (see the table in your deploy guide)
5. Open https://your-app.onrender.com/healthz — must show `"storage":"postgres"` and `"telegram":"yes"`

## Telegram bot setup

1. @BotFather → /newbot → get token
2. Send any message to your bot
3. Visit https://api.telegram.org/bot<TOKEN>/getUpdates → copy chat id
4. Add to Render env: TELEGRAM_BOT_TOKEN, TELEGRAM_CHAT_ID
5. Redeploy — webhook auto-registers on boot
6. Your phone will buzz with ✅/❌ buttons on every withdrawal request

## Health check

GET /healthz — returns uptime, storage, users, feature flags.

## Storage

| DATABASE_URL | Behaviour |
|---|---|
| Set | Postgres — users persist |
| Empty | JSON file — wiped on restart |

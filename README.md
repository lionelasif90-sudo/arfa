# —͞ᗩᴀʀғᴀ Telegram Bot

Customized version of the uploaded modular Telegram group-management bot.

## Before deployment
1. Create a Telegram bot with `@BotFather`.
2. Set its display name to `—͞ᗩᴀʀғᴀ` and choose an available username ending in `bot`.
3. Keep the bot token private. Never post it in chats, screenshots, GitHub, or this README.
4. Get your numeric Telegram user ID for `OWNER_ID`.
5. Create a PostgreSQL database. This project initializes its SQL modules at startup, so `DATABASE_URL` is required.

## Deploy on Render
This project uses Telegram long polling, so deploy it as a **Background Worker**, not a Web Service.

### Option A: Render Blueprint
1. Upload this project to a private GitHub repository.
2. In Render, choose **New → Blueprint** and connect that repository.
3. Render reads `render.yaml` and creates the worker service.
4. In the service Environment settings, fill in:
   - `TOKEN`: token from BotFather
   - `OWNER_ID`: your numeric Telegram user ID
   - `OWNER_USERNAME`: your Telegram username without `@`
   - `DATABASE_URL`: PostgreSQL **Internal Database URL** (database in the same Render region)
5. Deploy and inspect the worker logs.

### Option B: Manual worker
- Runtime: Python
- Build command: `pip install -r requirements.txt`
- Start command: `python -m tg_bot`
- Service type: Background Worker
- Environment variables: `ENV=1`, `TOKEN`, `OWNER_ID`, `OWNER_USERNAME`, `DATABASE_URL`

Do not set `WEBHOOK`; the bot uses long polling.

## Notes
- Render Background Workers and managed PostgreSQL may require a paid plan. Check current pricing before creating resources.
- Keep the worker and PostgreSQL database in the same Render region and use the database's Internal URL.
- Never share the bot token. If exposed, revoke it with BotFather and generate a new one.
- The original project uses older dependencies. If Render reports an error, share the log with secrets removed.
- The Telegram profile display name is changed in BotFather; changing source text does not change the Telegram profile name.

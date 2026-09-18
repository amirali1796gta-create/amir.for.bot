# Telegram Config Shop Bot

A Telegram configuration-shop bot built with Python, aiogram 3, and SQLite.

## Files

- `bot.py` — main bot source
- `requirements.txt` — Python dependencies
- `.env.example` — environment-variable template
- `render.yaml` — Render worker deployment template
- `.gitignore` — prevents secrets and local SQLite databases from being committed

## Run locally

1. Create a virtual environment.
2. Install dependencies:

   `pip install -r requirements.txt`

3. Copy `.env.example` to `.env` and set your values.
4. Export/load those variables in your environment.
5. Start:

   `python bot.py`

The bot creates `config_shop.db` automatically on first run.

## Important before publishing/forking

The original source contained a Telegram bot token and a local proxy address. This fork-ready version removes the hard-coded token and reads it from `BOT_TOKEN`.

**Do not commit `.env` or any `*.db` file.**

If the original token was ever exposed publicly, revoke it in BotFather and generate a new one.

## Render

This repository is configured as a **worker** because the bot uses Telegram long polling (`start_polling`).

Set these environment variables in Render:

- `BOT_TOKEN`
- `SUPER_ADMIN_ID`
- `REQUIRED_CHANNEL`
- `CHANNEL_LINK`
- `PROXY_URL` (normally empty)

### SQLite persistence

`config_shop.db` is local SQLite storage. A normal ephemeral cloud filesystem can lose the database when the service is recreated/redeployed. For production use, attach persistent storage or migrate the database to a managed database.

## Forking

After pushing this folder to GitHub, another person can fork it, set the environment variables, install dependencies, and run the bot without editing secrets into the source code.

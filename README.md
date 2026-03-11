# TutorsLink Discord Bot

A Discord.js v14 bot for matching tutors with students, managing tickets, mod-mail, and tutor ads.

---

## Required Environment Variables

Set these in your hosting provider's **Environment Variables** panel — **do not paste them into the startup command**.

Variables marked ✅ are checked at startup — the bot will refuse to start if they are missing.
Variables marked ⚠️ are not checked at startup but are required for specific features to work correctly; the bot will start without them but those features will fail at runtime.

| Variable | Status | Description |
|---|---|---|
| `BOT_TOKEN` | ✅ startup check | Discord bot token (Discord Developer Portal → App → Bot → Token) |
| `GUILD_ID` | ✅ startup check | Your Discord server (guild) ID |
| `STAFF_ROLE_ID` | ✅ startup check | Role ID(s) for staff, comma-separated (no spaces: `id1,id2`) |
| `FIND_A_TUTOR_CHANNEL_ID` | ✅ startup check | Channel ID for the main find-a-tutor channel |
| `TUTORS_FEED_CHANNEL_ID` | ✅ startup check | Channel ID for the tutors feed |
| `TUTOR_CHAT_CHANNEL_ID` | ⚠️ used at runtime | Channel ID for tutor chat |
| `TUTOR_POLICIES_CHANNEL_ID` | ⚠️ used at runtime | Channel ID for tutor policies |
| `TICKET_CATEGORY_ID` | ⚠️ used at runtime | Category ID for ticket channels |
| `TRANSCRIPTS_CHANNEL_ID` | ⚠️ used at runtime | Channel ID for ticket transcripts (has a built-in fallback ID) |
| `MODMAIL_CATEGORY_ID` | ⚠️ used at runtime | Category ID for mod-mail threads |
| `MODMAIL_TRANSCRIPTS_CHANNEL_ID` | ⚠️ used at runtime | Channel ID for mod-mail transcripts |
| `STAFF_CHAT_ID` | ⚠️ used at runtime | Channel ID for staff chat (error/alert notifications) |
| `BUMP_CHANNEL_ID` | optional | Channel ID to listen for bump messages (listens everywhere if unset) |
| `ADS_CHANNEL_ID` | optional | Channel ID for the ads sync source |
| `ARCHIVED_ADS_CHANNEL_ID` | optional | Channel ID for archived ads |
| `SYNC_SECRET` | optional | Shared secret for the ad-sync webhook endpoint |
| `SYNC_WEBHOOK_URL` | optional | Webhook URL used by the ad-sync worker |
| `SERVER_HOST` | optional | IP/hostname shown in certain embeds |

---

## ⚠️ Do NOT put secrets in the startup command

A startup command like this **leaks your token**:

```bash
# BAD — token is visible in logs, process lists, and hosting-panel history
export BOT_TOKEN='your-token-here'; node /home/container/index.js
```

Instead, set `BOT_TOKEN` (and all other IDs) in your hosting provider's **Environment Variables** panel, then use a clean startup command:

```bash
node /home/container/index.js
```

If you accidentally exposed a token (posted it in chat, a startup command, or anywhere else), **reset it immediately**:
1. Go to [Discord Developer Portal](https://discord.com/developers/applications) → your app → **Bot** → **Reset Token**
2. Update the new token in your hosting panel's environment variables
3. Restart the bot

---

## How to verify the bot is in your guild

After starting the bot, look for this line in the console/log output:

```
Bot is in guild: YourServerName (123456789012345678)
```

If you see:

```
Bot is NOT in guild (or lacks access): 123456789012345678 — re-invite via Discord Developer Portal OAuth2 URL
```

Then the bot has been kicked or was never added. Re-invite it using the **OAuth2 URL Generator** in the Discord Developer Portal (Scopes: `bot`, `applications.commands`; required permissions: Administrator or the specific permissions your bot needs).

---

## Starting the bot

```bash
node /home/container/index.js
```

Dependencies are installed automatically by the hosting panel via `npm install` if a `package.json` is present.

---

## Migration script

To migrate existing ads to category channels:

```bash
# Dry-run (skip ads that already have a category message)
node scripts/migrateAds.js

# Re-post all ads (even those already migrated)
node scripts/migrateAds.js --force
```

Requires the same environment variables as the main bot (`BOT_TOKEN`, `GUILD_ID`, `FIND_A_TUTOR_CHANNEL_ID`).

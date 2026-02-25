# Quasar News — Rubric Settings Mini App

A Telegram Mini App for managing news feed subscriptions inside [@QuasarNews_bot](https://t.me/QuasarNews_bot).

## What it does

Users open this interface inside Telegram, toggle the news categories they want to follow, and hit save. The selection is sent back to the bot, which then delivers news only from the chosen categories.

## Categories

| Key | Label |
|---|---|
| `recipes` | Recipes from The Guardian |
| `science` | Science & Technology |
| `movies` | Movies & TV Series |
| `fashion` | Fashion & Beauty |
| `travel` | Travel |
| `psychology` | Psychology |
| `politics` | Politics |
| `celebrity_news` | Celebrity News |

## How it works

1. The bot opens this Mini App via a web app button, optionally passing current subscriptions as a URL param: `?subs=recipes,science,travel`
2. The user toggles categories on or off
3. On save, the app calls `tg.sendData()` with a JSON payload:

```json
{
  "action": "update_subscriptions",
  "subscriptions": ["recipes", "science", "travel"]
}
```

4. The bot receives the payload via `web_app_data` update and updates the user's subscription list

## Stack

- Vanilla HTML / CSS / JavaScript
- [Telegram Web App API](https://core.telegram.org/bots/webapps)

## Bot

[@QuasarNews_bot](https://t.me/QuasarNews_bot)

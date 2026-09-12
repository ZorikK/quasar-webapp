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
| `photo_of_day` | Photo of the Day |

Politics is no longer an active user-facing category. The legacy Politics sources remain available only for manual/internal use and are not shown in the Mini App.

## Delivery schedule

The scheduler uses server time (UTC).

| Time | Content |
|---|---|
| 07:00 | Recipes from The Guardian |
| 09:00 | Science & Technology — The Guardian |
| 11:00 | Psychology — best fresh item from NYT + The Guardian, with legacy fallback |
| 14:00 | Fashion & Beauty — The Guardian |
| 15:00 | Travel — The Guardian |
| 16:00 | Movie recommendation |
| 16:10 | TV series recommendation |
| 18:00 | Science & Technology — The New York Times |
| 19:00 | Photo of the Day — The Guardian |

For Kyiv during UTC+3, these correspond to 10:00, 12:00, 14:00, 17:00, 18:00, 19:00, 19:10, 21:00 and 22:00 respectively.

Photo of the Day uses a dedicated non-political editorial filter. Politics, war, terrorism, protests, military content, violent breaking-news imagery and related geopolitical topics are excluded. Priority is given to animals and wildlife, culture and art, urban life and architecture, design and fashion, followed by neutral visual stories from science, nature and human-interest topics.

Psychology is a single daily category. The bot combines fresh candidates from The New York Times and The Guardian, selects the strongest available item regardless of source, and falls back to the legacy psychology library only when no suitable fresh article is available.

## How it works

1. The bot opens this Mini App via a web app button, optionally passing current subscriptions as a URL param: `?subs=recipes,science,travel`
2. The user toggles categories on or off.
3. On save, the app calls `tg.sendData()` with a JSON payload:

```json
{
  "action": "update_subscriptions",
  "subscriptions": ["recipes", "science", "travel", "photo_of_day"]
}
```

4. The bot receives the payload via `web_app_data` update and updates the user's subscription list.

## Stack

- Vanilla HTML / CSS / JavaScript
- [Telegram Web App API](https://core.telegram.org/bots/webapps)

## Bot

[@QuasarNews_bot](https://t.me/QuasarNews_bot)

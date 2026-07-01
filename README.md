# Hermes Agent — Telegram Multi-Bot & Rich Messages

Модификации исходников Hermes Agent для поддержки:
- **Multi-Telegram bot**: до 20 слотов (telegram, telegram2, …, telegram20)
- **Rich Messages**: официальный Bot API rich_message параметр + MarkdownV2 fallback
- **Dynamic Platform**: Platform("telegramN") — идентично-стабильные псевдочлены enum

## Файлы

| Файл | Назначение |
|------|-----------|
| config.py | gateway/config.py — Platform enum, multi-slot helpers, env scanning |
| platforms.py | hermes_cli/platforms.py — platform info для telegram2…telegram20 |
| adapter.py | plugins/platforms/telegram/adapter.py — plugin регистрация слотов |
| telegram.py | gateway/platforms/telegram.py — полный Telegram adapter (rich messages + multi-bot) |
| base.py | gateway/platforms/base.py — базовый адаптер с rich_message edit |

## Ключевые изменения

### Multi-Telegram (config.py)
- is_telegram_platform(platform) — проверка Telegram-слота
- telegram_env_prefix(platform) — префикс env для слота
- Platform enum: псевдочлены telegram2…telegram20
- Env: TELEGRAM2_BOT_TOKEN…TELEGRAM20_BOT_TOKEN
- Plugin: авторегистрация 20 слотов

### Rich Messages (telegram.py)
- RICH_MESSAGE_MAX_CHARS = 32768
- _rich_messages_enabled из extra.rich_messages
- _rich_message_payload() для Bot API rich_message
- editMessageText с rich_message параметром
- MarkdownV2 fallback + _escape_mdv2()

## Лицензия
Исходный код Hermes Agent — собственность Nous Research.
Модификации распространяются на тех же условиях.

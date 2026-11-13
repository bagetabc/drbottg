# DearTG Admin Bot

Отдельный Python Telegram-бот для администрирования внутренних активов DearTG через защищённый API.

## Возможности

- `/users` — список последних аккаунтов и баланс.
- `/user ID` — активы аккаунта.
- `/stars ID AMOUNT [reason]` — начислить внутренние DearTG Stars.
- `/username ID USERNAME` — закрепить юзернейм.
- `/number_add +15551234567` — добавить запись виртуального номера в пул.
- `/number_assign USER_ID NUMBER_ID` — назначить номер аккаунту.
- `/nft ID TITLE [description]` — выдать коллекционную карточку.

Бот использует Telegram long polling: входящий публичный порт и webhook не нужны.

## Запуск на Windows 10/11

Открой PowerShell в папке проекта:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt

$env:DEARTG_BOT_TOKEN = "ТОКЕН_ОТ_BOTFATHER"
$env:DEARTG_API_URL = "http://127.0.0.1:8080"
$env:DEARTG_ADMIN_TOKEN = "ТОТ_ЖЕ_СЕКРЕТ_ЧТО_У_API"
$env:DEARTG_BOT_ADMIN_IDS = "ТВОЙ_TELEGRAM_NUMERIC_ID"

python bot.py
```

Сначала запусти DearTG API. Значение `DEARTG_ADMIN_TOKEN` должно совпадать с секретом, заданным серверу. Для нескольких администраторов укажи числовые Telegram ID через запятую.

## Настройки

| Переменная | Назначение |
|---|---|
| `DEARTG_BOT_TOKEN` | Токен от BotFather |
| `DEARTG_API_URL` | Адрес DearTG API |
| `DEARTG_ADMIN_TOKEN` | Секрет административного API |
| `DEARTG_BOT_ADMIN_IDS` | Разрешённые числовые Telegram ID |

Не добавляй токены в исходники, GitHub или ZIP. Храни их только в переменных окружения.

## Безопасность и ограничения

- Команды доступны только ID из `DEARTG_BOT_ADMIN_IDS`.
- Используется отдельный заголовок `X-Admin-Token` для API.
- Запускай только один экземпляр бота на один токен Telegram.
- Stars — внутренняя валюта DearTG, не Telegram Stars.
- Номера — записи инвентаря; бот не предоставляет SMS или телефонную связь.
- NFT — внутренние off-chain карточки, не блокчейн-NFT.

## CI

GitHub Actions проверяет синтаксис Python и компиляцию файла бота при push и pull request в `main`.

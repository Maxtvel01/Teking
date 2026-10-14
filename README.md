# TEKING — ИИ-консультант по подбору ПК

Чат-консультант, который собирает ПК из позиций каталога с ценами и ссылками. Без звонков.

## Быстрый старт

```bash
cp .env.example .env   # прописать LLM_API_KEY
pip install -r requirements.txt
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000
# открыть http://localhost:8000
```

Или через Docker: `docker build -t teking . && docker run -p 8000:8000 --env-file .env teking`

## ИИ-модель чата

По умолчанию — **Kimi K2.6** (Moonshot AI, OpenAI-compatible, работает из РФ):
- $0.95 вход / $4.00 выход за 1M токенов; кэшированный ввод $0.16.
- Минимальное пополнение $1; есть стартовый бонус $5 при пополнении $5.
- Ориентировочная стоимость диалога с консультантом: ~1–3 ₽ за сессию → **сотни диалогов за $1–5/мес**.

Получить ключ: https://platform.kimi.ai (LLM_BASE_URL=https://api.moonshot.ai/v1).

Альтернативы (провайдер подменяется в .env, интерфейс OpenAI-compatible):
- **GigaChat** (Сбер) — есть бесплатный тариф, оплата в рублях, работает в РФ.
- **YandexGPT** (Яндекс Облако) — yandexgpt-lite, копеечный, российский.
- Любая OpenAI-compatible модель.

## Структура

- `backend/` — FastAPI: `/api/chat`, CRUD каталога, импорт, история цен
- `frontend/` — чат, каталог, админка `/admin` (Basic Auth: логин `admin`, пароль из `.env` → `ADMIN_PASSWORD`; запись в API защищена тем же паролем)
- `scripts/parser_daily.py` — ежедневный парсер в файл, см. `scripts/PARSER.md`
- ИИ: Kimi (kimi-k2.6) или DeepSeek — настройка в `.env`, см. комментарии в `.env.example`
- `data/` — seed-каталог (демо-цены, заменить реальными) и системный промт
- `backend/parser_ozon_ym.py` — парсер Ozon/ЯМ (опционально, fallback)

## Важно

Данные каталога в `data/catalog_seed.json` — демонстрационные. Перед публикацией
заполните реальными товарами (админка или `POST /api/import`). Вопросы гарантии/
доставки/оплаты промт направляет на `HUMAN_SUPPORT_LINK`.

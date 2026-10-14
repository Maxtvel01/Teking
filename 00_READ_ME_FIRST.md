# TEKING — актуальная сборка проекта (15.10.2026)

## Что уже сделано (статус)

- ✅ Сайт запущен на сервере (VPS Hostkey 185.149.145.147, Docker-контейнер `teking`, Caddy + HTTPS)
- ✅ Дизайн «бордо» обновлён: анимации GSAP + Lenis, частицы tsParticles в шапке
- ✅ Чат в мессендингерском формате: сообщения сверху, поле ввода снизу, скролл мышью листает чат
- ✅ Каталог: 757 реальных позиций (Ситилинк/DNS), загружены через админку импортом JSON
- ✅ ИИ подключён: **Yandex AI Studio, модель DeepSeek 4 Flash** (через OpenAI-совместимый API)
- ✅ Группировка токенов: в запрос уходит срез каталога 2–9 тыс. токенов (не весь каталог)
- ✅ Парсер `scripts/parser_daily.py` — парсит DNS/Ситилинк, чистит чужие категории

## Структура папки

```
Teking12.10/
├── 00_READ_ME_FIRST.md      ← этот файл
├── AI_PROMPT.md             ← как устроен и настраивается ИИ-консультант
├── DESIGN.md                ← дизайн: палитра, структура, как править
├── PARSER.md                ← парсер каталога
├── SERVER.md                ← сервер: обновление, команды, бэкапы
├── TODO_CHECKLIST.md        ← чек-лист
└── app/                     ← ВЕСЬ код сайта (заливать на сервер целиком)
    ├── backend/             ← FastAPI: чат, каталог, импорт (main.py, config.py, models.py, ...)
    ├── frontend/            ← index.html, admin.html, css/, js/ (+ js/vendor — GSAP/Lenis/tsParticles)
    ├── data/                ← system_prompt.txt («характер» бота), catalog_seed.json
    ├── scripts/             ← parser_daily.py + PARSER.md
    ├── Dockerfile, requirements.txt
```

## Где что менять

| Хочу поменять... | Файл |
|---|---|
| Цвета, стили | `app/frontend/css/style.css` (переменные в `:root`) |
| Тексты, структура страницы | `app/frontend/index.html` |
| Поведение ИИ | `app/data/system_prompt.txt` |
| Товары | админка сайта (/static/admin.html), импорт JSON |
| Модель ИИ / ключ | `.env` на сервере (`/root/app/.env`) |

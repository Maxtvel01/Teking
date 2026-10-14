# SERVER — сервер и обновление сайта

## Сервер

- Hostkey VPS: 2 vCPU / 2 ГБ RAM, ~560 ₽/мес
- IP: `185.149.145.147`, Ubuntu 24.04
- Сайт: Docker-контейнер `teking` (порт 8000), HTTPS через Caddy

## Адреса

| Что | Адрес |
|---|---|
| Сайт | `http://185.149.145.147:8000` (и по домену, если привязан) |
| Админка | `http://185.149.145.147:8000/static/admin.html` |

SSH: `ssh root@185.149.145.147`

## Настройки (.env на сервере, /root/app/.env)

- `LLM_API_KEY=` — ключ Yandex Cloud (вводить только на сервере!)
- `LLM_BASE_URL=https://ai.api.cloud.yandex.net/v1`
- `LLM_AUTH=Api-Key`
- `LLM_PROJECT=` — id каталога Yandex Cloud
- `LLM_MODEL=gpt://<id>/deepseek-v4-flash/latest`
- `LLM_BUILD_PER_CATEGORY=15`
- `ADMIN_PASSWORD=` — пароль админки

После правки `.env`: `docker restart teking`.

## Команды (на сервере)

```bash
docker ps / docker logs teking / docker restart teking / docker stats teking
```

## Как обновить сайт после правок на компьютере

Замена отдельных файлов (самый частый случай):

```powershell
# с компьютера, PowerShell:
scp "<путь к файлу>" root@185.149.145.147:/root/app/<путь>
```
```bash
# на сервере:
docker cp /root/app/<путь> teking:/app/<путь>
docker restart teking
```

Обновление всего frontend сразу:

```powershell
scp -r "C:\Users\MVEliseev\Desktop\Teking1210\TEKING12.10\app\frontend" root@185.149.145.147:/root/app/
```
```bash
docker cp /root/app/frontend/. teking:/app/frontend/
docker restart teking
```

В браузере — Ctrl+F5.

## Бэкапы

```bash
mkdir -p /root/backups
docker cp teking:/app/teking.db /root/backups/teking-$(date +%F).db
```

База (весь каталог) живёт в `teking.db` ВНУТРИ контейнера — бэкапить обязательно перед импортом нового каталога!

## Если сайт «упал»

```bash
docker logs teking --tail 50
docker restart teking
```

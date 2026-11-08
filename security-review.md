# Проверка по чек-листу

- **PASS — Dockerfile: USER не root.** `Dockerfile:11` — `USER node`.
- **PASS — Dockerfile: chown папки тома выполнен до USER.** `Dockerfile:8` — `chown node:node /data`; `Dockerfile:11` — переключение на `node`.
- **PASS — compose.yaml: порт компьютера привязан к localhost.** `compose.yaml:9` — перед портом хоста указан `127.0.0.1:`.
- **PASS — секреты не заданы через ENV, ARG или environment; файл секрета исключён.** В `Dockerfile` и `compose.yaml` таких объявлений нет; подключение Compose secret: `compose.yaml:12–13, 24–26`; исключение файла: `.dockerignore:3`.
- **НЕ УДАЛОСЬ ПРОВЕРИТЬ — критические (C) уязвимости в Scout.** `report/scout.txt:1` сообщает, что Scout не установлен и проверка не выполнена. Scout не запускался; файл только прочитан.
- **PASS — workflow использует secrets.NAME для логина и токена.** `.github/workflows/build.yml:21–22`.

## Решения

- Пункт 4, Scout — принято: Scout на этом компьютере не установлен, проверка уязвимостей не сделана. Перед следующим выпуском поставить Scout и снять `report/scout.txt` заново; в этот выпуск правок нет.
- Пункты 1, 2, 3, 5 — согласен, сверил с файлами: `USER node` и `chown node:node /data` выше него в Dockerfile, `127.0.0.1:8080:3000` в compose.yaml, `api_token.txt` в .dockerignore и секрет через `secrets`, `secrets.DOCKERHUB_USERNAME` и `secrets.DOCKERHUB_TOKEN` в build.yml.

# LinkedIn Desk

Приложение для разбора LinkedIn-постов (iPhone, Safari и Telegram WebApp). Отдельно от приложения рилсов.

- Страница: `index.html` (один файл, без сборки). Данные: `data.gz.bin` (gzip + AES-GCM), картинки: `img/<sha256>.bin`.
- Ключ в ссылке `#k=...`, без него ничего не читается. Ссылка: `/usr/bin/python3 ~/Projects/linkedin-engine/app_sync.py --link`.
- Данные собирает `~/Projects/linkedin-engine/app_sync.py` из `linkedin-engine/data/posts.json` (+ today.json, stats.json), коммитит и пушит только при изменениях.
- Кнопки шлют действие зашифрованным issue «li-action» в этот репозиторий (если в конфиге есть gh_token), иначе через Telegram (sendData или ссылка на бота).
- Хук `.githooks/pre-commit` (включён через `git config core.hooksPath .githooks`) не даёт закоммитить страницу со сломанным скриптом.
- При каждом изменении страницы поднимай `APP_VER` в index.html: старые копии сами перезагрузятся.
- Проверка: `node ~/Projects/linkedin-engine/tools/app_smoke.js "<ссылка с ключом>" [папка для скриншотов]`.

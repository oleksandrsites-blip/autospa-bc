# Нотатки для ШІ-помічника

- Реальний клієнтський сайт детейлінг-студії, зроблений на основі шаблону з репозиторію detailingrv (портфоліо — окремо, його не чіпаємо).
- Дані — у `site.json`, дизайн — у `template.html`. Після будь-якої правки: `python3 build.py site.json --out index.html`. `index.html` руками не редагувати.
- Хостинг: Cloudflare Pages на акаунті клієнта, збірка `bash tools/cf-build.sh` → `public/`. Деплої безкоштовні, пушити можна скільки завгодно.
- Форма: `functions/api/estimate.js` → `lib/estimate-core.mjs` → Telegram. Токен і chat_id лише в змінних Cloudflare (TELEGRAM_BOT_TOKEN, TELEGRAM_CHAT_ID), ніколи в коді.
- Netlify не використовуємо.
- Не вигадувати реальні дані клієнта (контакти, адреси, відгуки, ціни) — ставити заглушку й питати.
- Список того, що ще треба замінити під клієнта, — у README.md.

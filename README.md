# Сайт детейлінг-студії (клієнт)

Сайт на базі шаблону detailingrv. Хостинг — Cloudflare Pages, заявки з форми — у Telegram.

## Як влаштовано
| Файл / папка | Що це |
|---|---|
| `site.json` | **Усі дані сайту**: назва, тексти, послуги, ціни, контакти, FAQ, відгуки, до/після. Майже всі правки — тут. |
| `template.html` | Дизайн і верстка (HTML + CSS + JS). Чіпати, коли міняємо вигляд. |
| `build.py` | Збирає `index.html` з `template.html` + `site.json`. |
| `index.html` | Готовий сайт. **Не редагувати руками** — він перезаписується збіркою. |
| `images/photos/` | Фото сайту (WebP/AVIF у кількох розмірах). |
| `images/before-after/<категорія>/` | Пари до/після: `before.webp`, `after.webp` (+ `-800` версії). |
| `images/brand/` | Лого, фавікон, OG-картинка для прев'ю в месенджерах (`og.jpg`, 1200×630). |
| `functions/api/estimate.js` + `lib/estimate-core.mjs` | Відправка заявки з фото в Telegram. |
| `tools/` | Збірка для Cloudflare, оптимізація фото, шаблон OG-картинки. |
| `_src/` | Оригінали фото клієнта (не потрапляють у GitHub). |

## Після правок
```
python3 build.py site.json --out index.html
```
Потім коміт і push — Cloudflare сам оновить сайт за ~1 хв.

## Нові фото
Оригінали клади в `_src/`, оптимізація: `python3 tools/optimize-images.py photos` або `pairs`.

## Cloudflare Pages (акаунт клієнта)
- Workers & Pages → Create → Continue to Pages → Connect to Git → цей репозиторій
- Production branch: `main`, Framework: None
- Build command: `bash tools/cf-build.sh`, Build output directory: `public`
- Settings → Variables and Secrets: `TELEGRAM_BOT_TOKEN` (Secret), `TELEGRAM_CHAT_ID` → Retry deployment

## Що замінити під клієнта (зараз стоять дані демо detailingrv)
- [ ] `site.json`: назва, місто, тексти, послуги й ціни, контакти, соцмережі, години роботи, `site_url`
- [ ] прибрати з `site.json` плашку «Концепт-проєкт для портфоліо» (це вже реальний бізнес)
- [ ] фото героя, послуг і пари до/після → реальні роботи клієнта
- [ ] лого й фавікон (`images/brand/`), OG-картинка
- [ ] `404.html`, `robots.txt`, `sitemap.xml` — назва й адреса сайту
- [ ] Telegram-бот і chat_id клієнта — у змінних Cloudflare (не в коді)

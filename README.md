Published mirror for static hosting: https://github.com/srazumnii/anviva-website

# Anviva website

Статический маркетинговый сайт для **Anviva DocGen** (Google Workspace Editor Add-on): лендинг, политика конфиденциальности, Limited Use, условия использования и поддержка.

Сборка не нужна — достаточно выложить содержимое этой папки на любой static host и привязать домен `anviva.ru`.

## Содержимое

| Файл | Назначение |
|------|------------|
| `index.html` | Лендинг (RU) |
| `index-en.html` | Homepage (EN, OAuth Branding / Google review) |
| `privacy.html` | Политика конфиденциальности (RU) |
| `privacy-en.html` | Privacy Policy (EN, Marketplace / OAuth) |
| `limited-use.html` | Limited Use (RU) |
| `limited-use-en.html` | Limited Use (EN, OAuth / GWM) |
| `terms.html` | Условия использования (RU) |
| `terms-en.html` | Terms of Service (EN, Marketplace) |
| `support.html` | Поддержка и FAQ (RU) |
| `support-en.html` | Support and FAQ (EN) |
| `css/site.css` | Общие стили |
| `assets/anviva-icon.svg` | Иконка бренда |
| `assets/anviva-logo.svg` | Логотип-слово |
| `assets/marketplace/` | PNG-иконки для Marketplace / OAuth (32, 128, 512) |

## URL для Google OAuth / Marketplace

| Поле | URL |
|------|-----|
| Homepage (OAuth Branding) | `https://anviva.ru/index-en.html` |
| Homepage (RU) | `https://anviva.ru/` |
| Privacy policy | `https://anviva.ru/privacy-en.html` (EN; RU: `https://anviva.ru/privacy.html`) |
| Limited Use | `https://anviva.ru/limited-use-en.html` (EN; RU: `https://anviva.ru/limited-use.html`) |
| Terms of Service | `https://anviva.ru/terms-en.html` (EN, for Google review; RU: `https://anviva.ru/terms.html`) |
| Support | `https://anviva.ru/support-en.html` (EN; RU: `https://anviva.ru/support.html`) |

Опциональные pretty-path редиректы: `/privacy` → `privacy.html`, `/terms` → `terms.html`, `/support` → `support.html`.

Authorized domain: `anviva.ru`.

## Деплой (prod = Timeweb ← GitHub)

**Как устроено сейчас:** хостинг **Timeweb** смотрит в этот репозиторий
[`srazumnii/anviva-website`](https://github.com/srazumnii/anviva-website) на GitHub
и автоматически выкладывает изменения на **`https://anviva.ru`**.

| Шаг | Действие |
|-----|----------|
| 1 | Править HTML/CSS **в этом репо** (корень = document root сайта) |
| 2 | `git push` в `main` на GitHub |
| 3 | Дождаться деплоя Timeweb (обычно минуты) |
| 4 | Проверить live URL (например `https://anviva.ru/privacy-en.html`) |

**Не нужно:** SSH на VPS, ручной `scp`/`rsync`, GitHub Pages, Netlify.  
Черновик тех же страниц может жить в monorepo `docGeneration/website/` — **публикуется только** push в `anviva-website`.

### Локальная проверка

```bash
npx --yes serve .
# или
python -m http.server 8080
```

## Контакты на сайте

Поддержка: **support@anviva.ru**.

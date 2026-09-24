Published mirror for static hosting: https://github.com/srazumnii/anviva-website

# Anviva website

Статический маркетинговый сайт для **Anviva DocGen** (Google Workspace Editor Add-on): лендинг, политика конфиденциальности, Limited Use, условия использования и поддержка.

Сборка не нужна — достаточно выложить содержимое этой папки на любой static host и привязать домен `anviva.ru`.

## Содержимое

| Файл | Назначение |
|------|------------|
| `index.html` | Лендинг |
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
| Homepage | `https://anviva.ru/` или `https://anviva.ru/index.html` |
| Privacy policy | `https://anviva.ru/privacy-en.html` (EN; RU: `https://anviva.ru/privacy.html`) |
| Limited Use | `https://anviva.ru/limited-use-en.html` (EN; RU: `https://anviva.ru/limited-use.html`) |
| Terms of Service | `https://anviva.ru/terms-en.html` (EN, for Google review; RU: `https://anviva.ru/terms.html`) |
| Support | `https://anviva.ru/support-en.html` (EN; RU: `https://anviva.ru/support.html`) |

Опциональные pretty-path редиректы: `/privacy` → `privacy.html`, `/terms` → `terms.html`, `/support` → `support.html`.

Authorized domain: `anviva.ru`.

## Деплой

### 1. Обычный static host / nginx

Скопируйте **содержимое** `website/` в document root (например `/var/www/anviva.ru/`):

```nginx
server {
  listen 80;
  server_name anviva.ru www.anviva.ru;
  root /var/www/anviva.ru;
  index index.html;

  location / {
    try_files $uri $uri/ =404;
  }

  # optional pretty paths
  location = /privacy { return 301 /privacy.html; }
  location = /limited-use { return 301 /limited-use.html; }
  location = /terms { return 301 /terms.html; }
  location = /support { return 301 /support.html; }
}
```

Дальше — TLS (Let's Encrypt / certbot) и DNS A/AAAA (или CNAME) на сервер.

### 2. Netlify

1. В Netlify: **Add new site → Deploy manually** или подключите репозиторий.
2. Publish directory: `website` (если деплой из корня monorepo).
3. Domain management → добавьте `anviva.ru` и следуйте DNS-подсказкам Netlify.

`netlify.toml` (опционально, в корне репо):

```toml
[build]
  publish = "website"
```

### 3. GitHub Pages

Вариант A — отдельный branch `gh-pages` только с файлами из `website/`.

Вариант B — Actions: собрать артефакт из папки `website` и опубликовать.

В настройках Pages укажите custom domain `anviva.ru` и добавьте DNS-запись `CNAME` / A по инструкции GitHub. Файл `CNAME` с содержимым `anviva.ru` можно положить внутрь `website/` при публикации.

### 4. Локальная проверка

```bash
# из корня репозитория
npx --yes serve website
# или
python -m http.server -d website 8080
```

Откройте `http://localhost:3000` (или порт serve/http.server).

## Контакты на сайте

Поддержка: **support@anviva.ru**.

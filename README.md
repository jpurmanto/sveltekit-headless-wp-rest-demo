Work in progress. 👨‍💻

![Screenshot current status, headline and two posts displayed, one with featured image](screenshot.jpg?raw=true)

## Local setup

### SvelteKit frontend

Currently via local (host computer) npm, could be maybe added to DDEV as well:

```bash
npm install
npm run dev -- --open
```

### WordPress backend

This demo also ships an optional WordPress Demo Site in the `wp-backend/`-folder, installed with [DDEV + bedrock](https://ddev.readthedocs.io/en/latest/users/quickstart/#wordpress).

```
# Install DDEV on your local machine:
# https://ddev.readthedocs.io/en/latest/users/install/ddev-installation/

cd wp-backend/
ddev start && ddev composer install
ddev exec cp .env.example .env
# import example database snapshot
ddev snapshot restore --latest
# copy some assets for demo purposes
ddev exec "rsync -avz --mkpath .upload-examples/uploads/ web/app/uploads/"
```

https://sveltekit-pico-headless-wp.ddev.site/wp-admin/
User: admin
PW: !jIO\*D^^XtAF9N4x9Z

### General

## TODOs

- [ ] Host and deploy via ploi.io + Hetzner, https://dev.to/mandrasch/host-sveltekit-apps-with-ssr-support-via-ploiio-on-hetzner-cloud-1cpa
  - [ ] Add .env example
  - [ ] https://dev.to/danawoodman/storing-environment-variables-in-sveltekit-2of3
  - [ ] https://sveltekit-pico-headless-wp.mandrasch.dev/
- [ ] Add post detail page with gutenberg styles, see: https://github.com/mandrasch/sveltekit-wp-bs5
- [ ] Add header and footer
- [ ] Add acf fields, custom post type + search filter in sveltekit
- [ ] Add gmaps (or similiar)
- [ ] Add forms example - submit via REST API
- [ ] Add forms captcha
- [ ] Add cookie / 2 click privacy solution for embeds, see: https://github.com/mandrasch/wie-steht-es-um-das-klima-so
- [ ] Add sitemap
- [ ] Add search?

## How was this created?

### Frontend

```bash
# Frontend - SvelteKit
npm create svelte@latest frontend
cd frontend
npm install

npm i @picocss/pico
# Add picocss - https://joyofcode.xyz/using-pico-css-with-svelte
npm i -D sass
npm i -D svelte-preprocess
```

### Backend

```
# Backend - WordPress with bedrock
# https://ddev.readthedocs.io/en/stable/users/quickstart/#wordpress -> bedrock
mkdir wp-backend
cd wp-backend
ddev config --project-type=wordpress --docroot=web --create-docroot
ddev start
ddev composer create roots/bedrock
# create .env
# install via browser
ddev launch
# Copy ACF pro into /web/app/plugins/, activate
ddev wp plugin activate advanced-custom-fields-pro
# Headless Mode plugin https://wordpress.org/plugins/headless-mode/
ddev composer require "wpackagist-plugin/headless-mode":"0.4.0"

# save database snapshot for easy demo setup
ddev snapshot
```

## License

My own work (mostly config stuff) is availabe as CC0 / Public Domain.

In this repository ACF pro is included for demo purposes. ACF pro is licensed as GPLv2 (https://www.gnu.org/licenses/gpl-2.0.html). Please support the developers by purchasing a license.

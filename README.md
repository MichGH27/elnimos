# Elnimo's Place Resort UI — index.php in the project root

This ZIP is the same **UI-only Grandoria-inspired prototype**, reorganized so that `index.php` stays in the project root while all redesigned secondary PHP pages, CSS, JS, and shared PHP includes live in a dedicated `landing-page/` subfolder.

## Placement inside an existing XAMPP project

Copy `index.php` and the entire `landing-page/` folder into `C:\xampp\htdocs\elnimos_resort\` (back up the original `index.php` first). DO NOT replace your original production booking, login, registration, or other app files outside the **UI folder**.

```text
elnimos_resort/
    index.php
    landing-page/
        about.php  rates.php  services.php  gallery.php
        offers.php  events.php  reviews.php  location.php
        contact.php  book.php
        includes/header.php
        includes/footer.php
        includes/data.php
        assets/css/style.css
        assets/js/main.js
        assets/img/fallback-*.svg
    uploads/   (existing optional site photos)
    config/    (your existing app, untouched)
```

Start Apache and open: http://localhost/elnimos_resort/index.php

Pages: `http://localhost/elnimos_resort/landing-page/about.php`, `.../landing-page/reviews.php`, etc.

## What was changed to support the new folder layout

- All page URLs use a single `page_url()` helper in `landing-page/includes/data.php`. It resolves to a root `index.php` or `landing-page/{slug}.php` based on which page is being viewed.
- The shared header loads CSS, JS, logo image, and all navigation from paths valid on BOTH the root and nested pages.
- The shared footer, breadcrumbs, homepage links and dynamic package cards use the same URLs.
- The `photo()` helper finds optional existing resort images under the project-root `uploads/` folder, and emits correct browser-relative URLs.
- JavaScript reads an asset base path from the page so its bundled image fallbacks work on the homepage and subpages.

## Scope and caveats

This is **design/UI only**: there are no database connections, real bookings, payments, user accounts or live review/promo feeds. `landing-page/book.php` is an independent illustrative visit estimator and is not connected to a backend or a payment flow.

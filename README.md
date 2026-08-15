# ovation-website

The public pages for the Ovation app: privacy policy, terms of use, and the two
`.well-known` files that let invitation links open in the app instead of the browser.

Served by GitHub Pages at **ovationapp.ch**.

## Why it is a separate repository

The app's own repository is private. These pages have to be public — Apple and Google
both require reachable privacy and terms URLs, and the `.well-known` files are fetched
by the operating system over plain HTTPS. Keeping them apart means the app's source
stays private while its public surface is versioned like everything else.

## The `.well-known` files

`apple-app-site-association` and `assetlinks.json` tie the domain to the two apps, so a
tap on `ovationapp.ch/e/<slug>` opens the invitation in Ovation. They must be served:

- over HTTPS, from the exact paths `/.well-known/…`
- with no redirect (a 301 to `www.` breaks both)
- `apple-app-site-association` with **no** file extension

`assetlinks.json` currently carries the release signing certificate. Enabling Play App
Signing means Google re-signs the app with its own key — the fingerprint it gives you in
Play Console then has to be added to the list as well, or Android links stop opening.

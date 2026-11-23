# RingSeoul

Landing page for RingSeoul — Korean phone booking, done for you.

A 24/7 AI booking agent that phones local Korean shops in natural Korean and books in the customer's name. $6 per confirmed booking; pay nothing if it doesn't happen.

Live site: https://hg000316.github.io/ringseoul/

## Publishing

The site is a single static file, `index.html`, at the repository root.

GitHub Pages serves the **`gh-pages`** branch (root folder). To update the live site, commit the change on `gh-pages` (or update `main` and push it to `gh-pages` as well); a push to `gh-pages` rebuilds the site within a minute or two.

## Where booking requests go

`index.html` is fully static, so the request form posts itself to
[FormSubmit](https://formsubmit.co) — no server, no account.

- Endpoint: `https://formsubmit.co/ajax/hy00031618@gmail.com` (constant `SUBMIT_ENDPOINT`
in the page script). The address after `/ajax/` is the recipient; change it there and
in `CONTACT_EMAIL` (the footer/inquiry address) together.
- The first submission from the live site makes FormSubmit send an **Activate Form** email
to that address. Until the link in it is clicked, submissions are refused — the page shows
the "could not send, email us" message instead of the success screen.
- Each request carries its `RS-…` request number, the shop, both time choices, party size,
name, email and notes in a table-layout email; `_replyto` is the customer's address, so
replying in Gmail goes straight to them.
- The page keeps a copy of every attempt in `localStorage` (`ringseoul.requests.v1`) before
sending, and offers a retry plus a `mailto:` fallback if delivery fails.

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

- Endpoint: `https://formsubmit.co/ajax/1852e961b1c84e4387176552bbb8e5b3` (constant
`SUBMIT_ENDPOINT` in the page script). That string is the **FormSubmit alias** for the
owners inbox: FormSubmit forwards to the real address, so the page never publishes an
email address. To send requests somewhere else, swap the alias for the new address (or
new alias) in that one constant — there is no second place in the page to change.
- The first submission ever to a *new* address makes FormSubmit send an **Activate Form**
email to it. Until the link in it is clicked, submissions are refused — the page shows
the "could not send" message instead of the success screen. The alias above is already
activated.
- Each request carries its `RS-…` request number, the shop, both time choices, party size,
name, email, notes, the `pay6` answer to "would you pay $6 for a confirmed booking?"
(`Yes` / `Maybe` / `No (free beta only)` / `Not answered`), an optional Instagram or
WhatsApp handle, and `source_utm` — the `utm_source`/`utm_medium`/`utm_campaign` tags of
the link the visitor arrived on, or `direct`. `_replyto` is the customer's address, so
replying in Gmail goes straight to them.
- The page keeps a copy of every attempt in `localStorage` (`ringseoul.requests.v1`) before
sending, and on failure shows the request ID so a visitor can quote it when they write
back through the form.

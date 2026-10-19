## What you get

Send a candidate name. You get one report covering:

- **Domains** — each requested extension, checked twice: authoritative registry data (RDAP) and live DNS. `available` means every source that answered agreed the name is unregistered.
- **Handles** — each requested platform, checked against the platform's own endpoint (GitHub API, Reddit JSON, plain HTTP probes elsewhere).
- **App stores** — optional exact-name matches in iTunes and Google Play.
- **Trademarks** — optional lookup attempt by jurisdiction.

## Why you can trust the answers

Every verdict is `available`, `taken` or **`unknown`** — and `unknown` is used whenever the source could not actually be read (login wall, rate limit, bot check, paid API). Each row carries the source name and the HTTP status, so you audit the report instead of trusting it.

The handle checks are **self-calibrating**: before believing a platform, the checker probes it with a random control handle that cannot exist. If the platform answers the same way for the control as for your name, the platform is serving a login shell and the result is reported `unknown` rather than a false `taken`. Instagram and TikTok fail this test today — their rows say so.

## Good for

Naming a product, company, token, channel or domain before you commit: one pass tells you which domains are worth registering and which handles are genuinely free, and names the ones that could not be read instead of guessing at them.

## Limits, stated up front

- Availability of a domain is not a trademark clearance; trademark sources that require a paid API are reported as not checked.
- Rate limits are real: a very large platform list may return `unknown` for some rows.
- Report language is English; hand over a candidate name and optional lists, get markdown back.

---
title: "10 Better Auth plugins that every SaaS should use"
video_id: CpBgjjnXuy4
channel: "[[channels/Dreams of Code]]"
uploaded: 2026-01-18
processed: 2026-07-06
duration: "15:17"
url: https://www.youtube.com/watch?v=CpBgjjnXuy4
playlist: "[[Agents skills n8n]]"
type: review
difficulty: intermediate
use_case: [saas-authentication-setup]
tools: [Better Auth, Neon, Stripe, Polar, Cloudflare Turnstile]
llms: []
protocols: [OAuth, JWT, WebAuthn]
transcript: true
tags: [youtube, ai-automation]
---

# 10 Better Auth plugins that every SaaS should use

![thumbnail](https://i.ytimg.com/vi/CpBgjjnXuy4/maxresdefault.jpg)
▶️ [Watch](https://www.youtube.com/watch?v=CpBgjjnXuy4) | 📅 Uploaded [[uploaded/2026-01-18]] | 🗓️ Processed [[created/2026-07-06]]

## TL;DR
> Dreams of Code runs through 10 Better Auth plugins he considers essential for shipping a SaaS product in 2026 — Stripe billing, last-login-method tracking, captcha, JWT/JWKS, admin/user-management, API keys, CLI device authorization, organizations (B2B), passkeys, and two-factor auth — explaining what each saves you from building by hand. A sponsored segment covers Neon Auth V2, a hosted Better Auth server wired directly into a Neon Postgres database.

**Watch this if:** you're building a SaaS on Better Auth and want to know which of its plugins are worth adding, and why, before implementing any of these features yourself.

## Key Takeaways
- The Stripe plugin handles customer creation on signup, checkout via a single function call, webhook verification/handling, and subscription plan management (monthly/annual price IDs, usage limits, trials) — though the host personally uses Polar.sh instead, which has a less full-featured Better Auth plugin.
- The "Last Login Method" plugin stores which sign-in method a user used last, exposing `getLastUsedLoginMethod`/`isLastUsedLoginMethod` client functions to show a helpful indicator on the login page.
- The Captcha plugin protects sign-up, sign-in, and forgot-password endpoints (plus any custom ones) by requiring a captcha token, supporting Google reCAPTCHA, Cloudflare Turnstile (the host's preference), hCaptcha, and Captcha Fox.
- The JWT plugin issues JSON Web Tokens for authenticated users and publishes a JWKS endpoint, so non-JS/non-TypeScript backend services can independently verify tokens signed by your Better Auth server — useful for zero-trust auth across polyglot services (e.g. a Go or Rust API behind a dedicated TypeScript auth server).
- Neon Auth V2 is a hosted Better Auth implementation wired directly into your Neon Postgres database (enable it from the Neon dashboard, then point your client's base URL at it) — no vendor lock-in since data lives in your own Postgres, and it's free up to 60,000 monthly active users.
- The Admin plugin adds user CRUD, ban/unban, session management, role-based access control, and — the host's favorite — user impersonation for debugging and support.
- The API Key plugin is comprehensive: custom permissions, expirations, deletion, per-key and global rate limiting, and custom key prefixes.
- The Device Authorization plugin implements RFC 8628 (OAuth 2.0 Device Authorization Grant) for CLI/limited-input-device login flows (the same pattern used by the GitHub CLI); the Better Auth CLI ships a working `login` subcommand example.
- The Organizations plugin adds teams, roles, access control, and invites for B2B customers, and combines with the Stripe plugin to attach subscriptions to an organization instead of an individual user.
- The Passkeys plugin (built on WebAuthn) needs only two function calls (register, sign in) to support Face ID/Touch ID/hardware-key passwordless login.
- The Two-Factor plugin supports OTP (email/SMS code), TOTP (Google Authenticator/hardware keys), and backup codes — the host notes equivalent 2FA features can cost $100+/month on other auth providers.

## 🛠 Tools & Software
- [[topics/Better Auth]] — the open-source, self-hostable auth framework whose plugin ecosystem is the entire subject of the video.
- [[topics/Neon]] — sponsor; its Neon Auth V2 feature hosts a Better Auth server directly integrated with a Neon Postgres database, avoiding a separate TypeScript auth service.
- [[topics/Stripe]] — discussed via Better Auth's Stripe plugin (customers, checkout, webhooks, subscription plans) and again combined with the Organizations plugin for B2B billing.
- [[topics/Polar]] — mentioned as the payment provider the host actually uses instead of Stripe, via a less full-featured Better Auth plugin.
- [[topics/Cloudflare Turnstile]] — the host's preferred captcha provider, used with Better Auth's Captcha plugin.

## 🤖 LLMs Mentioned
None identified.

## 📡 Protocols & Standards
- [[topics/OAuth]] — the Device Authorization plugin implements RFC 8628, the OAuth 2.0 Device Authorization Grant, for CLI login flows.
- [[topics/JWT]] — Better Auth's JWT plugin issues JSON Web Tokens and a JWKS endpoint so downstream services can verify them independently of the auth server's language.
- [[topics/WebAuthn]] — the underlying standard for the Passkeys plugin's passwordless, device-based authentication.

## ✅ Action Items
- If billing is on Stripe, add Better Auth's Stripe plugin instead of hand-building customer/checkout/webhook/subscription logic.
- Add the Captcha plugin (Cloudflare Turnstile recommended) to protect signup, sign-in, and forgot-password endpoints from bots.
- Use the JWT plugin if any backend service outside your Better Auth server (a different language/runtime) needs to verify authenticated requests.
- If you don't want to run a separate auth server and already use Neon Postgres, evaluate Neon Auth V2 to get Better Auth hosted and wired to your database directly.
- Add the Organizations plugin (plus Stripe) as soon as you need B2B customers with teams, roles, and per-organization billing.
- Add the Two-Factor and Passkeys plugins for modern, low-effort MFA/passwordless support instead of paying for it via a hosted auth provider.

## 🔗 Related Videos
- None yet.

## Timeline
- `0:00` — Intro: why Better Auth's plugin system is the biggest reason to use it.
- `1:07` — #1 Stripe plugin: customer creation, checkout, webhooks, subscription plan management.
- `2:58` — #2 Last Login Method plugin: remembering and surfacing a user's last sign-in method.
- `4:30` — #3 Captcha plugin: bot protection on signup/sign-in/forgot-password via Turnstile, reCAPTCHA, hCaptcha, Captcha Fox.
- `6:23` — #4 JWT plugin: issuing JWTs and a JWKS endpoint for cross-language/service verification.
- `7:33` — Sponsor: Neon Auth V2, a hosted Better Auth server wired into Neon Postgres.
- `8:43` — #5 Admin plugin: user management, RBAC, and user impersonation.
- `9:44` — #6 API Key plugin: permissions, expirations, rate limiting, custom prefixes.
- `10:34` — #7 Device Authorization plugin: RFC 8628 device flow for CLI apps.
- `11:38` — #8 Organizations plugin: teams, roles, invites, and B2B billing via Stripe.
- `12:31` — #9 Passkeys plugin: WebAuthn-based passwordless login in two function calls.
- `13:31` — #10 Two-Factor plugin: OTP, TOTP, and backup codes.

## Transcript
<details>
<summary>Full transcript</summary>

When it comes to building software, my go-to provider for authentication is Better Auth, and I'm certainly not alone. Some of the popular reasons people love using Better Auth include the fact that it's open-source, highly configurable, has a great developer experience, and lets you keep full control of your own application data. Whilst I appreciate each of these points, perhaps the biggest reason I use Better Auth is because it not only saves me time setting up authentication, it speeds up the entire process of building a SaaS application — thanks to its fantastic plugin system, which makes it incredibly simple to add auth-based features like API keys, magic links, or checking whether a password has been pwned, but also to add other core features like payments, bot protection, zero-trust security, or an improved user experience. In this video, I'm going through 10 of my favorite Better Auth plugins — ones that have saved me weeks of work and make it incredibly easy to ship better products.

The first plugin isn't one I'd actually consider "auth" related, but it's such a huge time-saver it deserves a spot: the Stripe plugin, which I think is the best plugin out there for Better Auth — ironically, one I don't even use myself. If you've ever integrated Stripe before, you know that while it starts simple, it quickly becomes a chore: customer creation, checkout management, subscription handling, and my least favorite, webhooks. This is where the Better Auth Stripe plugin comes in, doing pretty much all the heavy lifting — automatically creating a customer on signup, opening a checkout page for a product with a single function, automatically handling webhooks (including verification and updating user records on purchase), and, my favorite, easily managing subscription plans by defining them in the plugin's subscription config: Stripe price ID for monthly tiers, an optional annual price ID, usage limits, and free trials. With plans defined, you manage them via the Better Auth client — creating a subscription, switching a user's plan, listing active subscriptions, or cancelling outright. It's a huge time-saver, so much so it's a shame I don't use it — I use Polar.sh instead for payments, which does have a Better Auth plugin, just not as full-featured.

One thing I do use is multiple authentication methods, which Better Auth makes easy out of the box — email/password, magic link, and various OAuth providers like Google, GitHub, and (everyone's favorite) Roblox. That versatility is good but can hurt UX once there are two-plus options, which is where plugin #2, Last Login Method, comes in. It isn't the biggest time-saver, but it's one every user appreciates: it stores which login method a user last used, letting you show a helpful indicator on the login page. All it takes is adding the server-side and client-side plugin to your Better Auth config, giving you two new client functions — `getLastUsedLoginMethod` (returns a string) and `isLastUsedLoginMethod` (accepts a string, returns a boolean) — to display an indicator next to the associated login method for a couple of lines of code.

Personally, for auth methods, I'm still a fan of simple email/password, and while Better Auth makes that easy to set up, you still have to be considerate about bot security — two main approaches: rate limiting (which Better Auth provides out of the box, though it's still worth configuring in your infrastructure) and issuing a challenge, which is plugin #3, Captcha. It makes it easy to add a captcha challenge to your auth flow, supporting Google reCAPTCHA, Cloudflare Turnstile, hCaptcha, and Captcha Fox. My preference is Cloudflare Turnstile, which I think gives the best balance of UX and bot protection. Setup is as simple as setting the provider and its secret key; once added, it automatically protects three key endpoints — signup/email, sign-in/email, and forgot-password — all especially bot-susceptible, and you can configure it to protect other endpoints too. Each protected endpoint then requires a captcha token in the request header, obtainable via the relevant captcha service's front-end package (documented with examples). Of all the plugins here, this one requires the most work, but Better Auth still reduces it enough that I don't skip adding captcha to projects like I used to.

Plugin #4 lets me use Better Auth across multiple services, including languages that don't natively support it: the JWT plugin, which adds JSON Web Token generation for authenticated users and publishes a JWKS (JW key store) endpoint exposing the public key used to sign your JWTs, so downstream services can verify tokens are signed by your auth service. This lets you add authentication and zero-trust security to other services just by implementing JWT support, which most languages have a package for — I like using this to run a dedicated TypeScript server just for Better Auth while using a more agreeable language like Go or, more recently, Rust for everything else. Lately, though, I don't even need a TypeScript server, thanks to a brand-new feature from my Postgres provider and today's sponsor, Neon: Neon Auth V2, a hosted implementation of the Better Auth server directly integrated with your Neon Postgres database. Enabling it is as simple as going to the Auth section of the Neon dashboard and clicking Enable, which sets up the auth server and adds the necessary tables to your schema; the Configuration tab gives you the auth URL to paste into your Better Auth client's base URL. Because Neon Auth uses Better Auth under the hood, there's no vendor lock-in — all data is written to your own Neon Postgres database, so you still get Neon's instant branching, data anonymization, and point-in-time recovery, free for up to 60,000 monthly active users (1 million on a paid plan). To get your own database for Neon Auth V2 powered by Better Auth, visit neon.com/dreamsofcode.

Plugin #5 is one I've always implemented by hand but now rely on entirely: the Admin plugin, which lets you define users with the admin role. That sounds simple, but it unlocks a huge number of user-management features — creating, listing, and updating users; banning/unbanning; and managing sessions (listing/revoking). Most of these are reasonably simple to implement by hand, which is why I used to — but this plugin really shines in two more advanced features: role-based access control (managing roles and permissions) and, my favorite, user impersonation, which is great both for debugging in production and for user support.

Plugin #6 is great for any product with a public API: the API Key plugin, which lets a user generate an API key. It sounds simple but is actually comprehensive — custom API key permissions, expirations, deletion, rate limiting for both individual keys and all keys globally, and my favorite, custom key prefixes (a nice developer-experience touch). It's extremely comprehensive, so check the docs (linked in the description) for the full feature list.

Plugin #7 is close to my heart as someone who likes building CLI applications: the Device Authorization plugin, used to enable authentication for devices with limited input, like CLIs. It works via an implementation of RFC 8628, the OAuth 2.0 Device Authorization Grant — basically the login flow you get when authorizing a CLI (if you've used the GitHub CLI, you know the pattern). The Better Auth CLI itself provides a working example via its `login` subcommand, performing the relevant device flow on screen. Under the hood this flow involves several important steps, as with any RFC implementation — you could implement it all by hand, but Better Auth gives you back a huge amount of time to spend on more interesting things.

Plugin #8 is useful if you want your application to support B2B customers (which every app should aim for, since that's where the money is): the Organizations plugin, which lets you easily enable organization support in your authentication. Organizations can feel simple to implement yourself until you get into requirements like teams, roles, access controls, and invites — at which point the scope explodes. Better Auth's plugin provides all of this out of the box. Combined with the Stripe plugin, it lets you associate a subscription with an organization instead of an individual user, making B2B use cases incredibly simple.

Plugin #9 is one I'd never implement by hand, but as a user I've come to appreciate a lot recently: Passkeys, a passwordless authentication method built on top of WebAuthn — instead of typing a password, you authenticate with your device (Face ID, Touch ID, or a hardware key like a YubiKey). Normally passkeys require a lot of work around key generation and cryptography, but Better Auth's Passkey plugin needs just two function calls: one to register a key, one to log in — plus a number of methods for users to manage their own passkeys. Especially in 2026, this provides a modern authentication experience that's arguably the way forward.

The last plugin is probably the least flashy, but for the host it encapsulates a lot of what Better Auth provides: the Two-Factor plugin, which supports setting up and managing two-factor/multi-factor authentication via three approaches — OTP (a code sent to email or phone), TOTP (used with apps like Google Authenticator or hardware keys), and backup codes. Setup is the same pattern as the other plugins: add it to your server and client plugin lists, then migrate your database, after which you get a bunch of client methods for managing MFA. What makes this one stand out is what it represents — the equivalent feature on other auth providers can cost at least $100/month, which is outrageous, and really shows how much value Better Auth provides through these plugins: saving time building software, saving money, and letting you keep ownership of your own application data.

Thanks again to today's sponsor, Neon — check out their new Auth V2 feature at neon.com/dreamsofcode if you want Better Auth wired directly into your Neon Postgres database without deploying a separate TypeScript server. Otherwise, that's all from me — thanks for watching, and I'll see you on the next one.

</details>

# Everyarc — ADR 001: Web first
*Decided by Hew, 2026-10-09. Supersedes the native-specific lines in `everyarc-stack.md`, `everyarc-build-spec.md`, `everyarc-bridge-contract.md` (§4 attestation, push), `everyarc-prd.md`, `everyarc-design-brief.md` and `everyarc-kid-design-brief.md` (platform, haptics). Everything else in those docs stands.*
*v0.1 · 2026-10-09 · Shared. Change it through this doc's changelog.*

---

## Decision
Both apps ship first as **installable web apps from one TypeScript repo**: **Everyarc** (parents; phone first, works in any browser) and **Everyarc Kids** (iPad Safari, added to the home screen, landscape first). The Supabase backend, the three zones, the contract and the engine don't change. Native comes later, by wrapping the web apps or rebuilding the screens, once the engine and content are proven; the contract and the engine carry over either way.

## Why
1. **The hard, new parts don't depend on the platform:** the competency graph, the engine (fluency gate, growth, redirects), the content pipeline with code-checked answers, the phrase bank, the schema, its grants and the bridge filter. Web proves them fastest; screens are the cheaper layer to redo.
2. **One engine, one language.** The moment and session clocks run on the device, offline; the arc runs on the server in Deno Edge Functions. In TypeScript, both are the same `packages/engine` code.
3. **The build loop.** Claude Code can build, run and test a web app end to end (Playwright on WebKit at iPad and iPhone sizes); Claude Design exports HTML, so design to code is close to direct.
4. **Research with children is a link,** not TestFlight and App Review; content and phrase-bank fixes ship the same day (still through review).
5. **Margin.** Web checkout runs about 3% against 15% through in-app purchase (`everyarc-monetization.md`).

## What changes (native → web)

| Concern | Native plan | Web first |
|---|---|---|
| App targets | Two App Store listings; the kid app in the Kids Category | Two installable web apps at **separate origins** (for example `app.` and `kids.`), so a child's iPad never holds a parent's session, cookies or storage |
| UI | SwiftUI | React + TypeScript (Next.js App Router). The kid app is a static export, fully client-side, offline-first |
| Local data and outbox | SwiftData | IndexedDB (an outbox with idempotent IDs, as bridge §6.2 requires) + Cache Storage through a service worker (Serwist) |
| Parent sign-in | Sign in with Apple, passkeys | Supabase Auth on the web: Sign in with Apple and email magic links; passkeys where Supabase supports them (check its docs) |
| Parent app lock | Face ID | A WebAuthn platform-authenticator check (Face ID or Touch ID through the browser) on open after idle |
| Kid device identity | Anonymous sign-in + App Attest | Anonymous sign-in + the single-use pairing code (hashed, five attempts, rate limits) + a **non-extractable WebCrypto P-256 device key** registered at pairing; parent approval unchanged. Lost local storage means pairing again, with approval. Weaker than App Attest: fine for beta, revisit with a native wrapper |
| Parent alerts | APNs | **Web Push** (VAPID) to home-screen-installed parent apps (iOS 16.4+), plus **email for every safety and security alert** and for any adult without push. `home.member_device.apns_token` becomes `push_subscription jsonb` |
| Kid app refresh | Background app refresh | None: fetch on open, Realtime while open, service-worker cache. Still no push, no notification permission |
| Payments | StoreKit 2 + a US web checkout link | Stripe Checkout + webhooks → an Edge Function, behind a flag (still not in production for v1) |
| Capture (M5) | Share extension, document scanner, on-device OCR | File input with camera capture, multi-file upload and the mail drop; images downscaled in the browser; OCR in the reading pipeline. iOS doesn't let web apps be share targets |
| Haptics | Parent app haptics | None on iOS web (Safari has no vibration API). The kid app loses nothing: iPads have no haptic engine |
| Pencil | PencilKit | Pointer Events (`pen`, pressure) on canvas; expect more latency than native in the scratch layer |
| Grain and texture | SwiftUI shaders | SVG filters, CSS and canvas |
| Kids Category rules | Enforced by App Review | **Self-enforced:** a strict CSP with no third-party origins in the kid app, no outbound links (lint + CSP), the grown-up gate for anything parental, no analytics |
| Keeping a child in the app | The app itself | The home-screen app has no address bar; parent onboarding suggests Guided Access |
| Audio playback | AVAudio | Web Audio, unlocked by the first tap; only the child's chosen reading voice is cached (about 316 files) |
| Tests | Swift Testing | Vitest + fast-check, pgTAP, Playwright on WebKit at 1180 × 820 (iPad landscape) and iPhone sizes |
| Hosting | App Store | Vercel; Supabase as before |
| Android | Out of v1 | Works in the browser at no extra cost; not a target |

## What doesn't change
The three zones; `compile_brief()`, the truth line and their proof; roles, grants and RLS; the device RPCs; every contract shape except pairing attestation and the push channel; the engine rules, fluency and growth; the phrase bank and audio rules; the Anthropic and ElevenLabs rules; fictional data only; every hard rule in `CLAUDE.md`.

## Revisit when
The scratch layer's Pencil latency gets in a child's way; parents miss alerts because few install the app; storage eviction loses offline work in practice; or App Store presence starts to matter for growth.

## Changelog
- **v0.1 · 2026-10-09 · kid side (Hew's decision):** web first for both apps.

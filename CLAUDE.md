# CLAUDE.md — «منهج عساف» / rabih-sales

> This file is auto-loaded by Claude Code at the start of every session.
> Read it fully before making any changes to the repo.

## What this project is

A single-page landing site (`index.html`, static HTML) that sells three tiers of
Rabih Assaf's Arabic sales training course. Deployed to Vercel via GitHub
auto-deploy: **push to `main` → live in seconds** at `rabih-sales.vercel.app`.

## The person you're working with

**Yaniv** is running the digital-launch project for the client, Rabih Assaf.
He is technical enough to run commands and read code but does not want to become
the primary developer. Talk to him in Hebrew when the conversation is meta
(planning, decisions, status). Comment code in English. Content copy on the page
itself is Arabic — see the language section below.

## Strategic decisions (change only with Yaniv, then update this file)

These were argued through carefully with Yaniv over many sessions. They are not
frozen — but any change is a conversation with Yaniv first, and this file is
updated in the same commit. Don't drift silently.

- **Language of the page copy**: **Levantine spoken Arabic (لهجة عامية)**, not
  MSA (Modern Standard Arabic). Rabih's Palestinian dialect is the brand.
  Examples of the register: «مش موهبة» not «ليست موهبة», «شو بتشتغل؟» not
  «ماذا تعمل؟», «هلأ» not «الآن». If you're not fluent, ASK before rewriting —
  don't guess.
- **No Israel signaling**: the client's family name Assaf is positioned as a
  brand for the Arab market. The page never mentions Israel, Hebrew, Celcom,
  Pelephone, or Jerusalem-as-Israel. Rabih's real story includes a Jerusalem
  customer and Israeli telecom companies — this has been anonymized to «شركة
  اتصالات كبيرة» and «القدس» stays because Arabic-speakers understand it as
  the Palestinian frame. Don't add nationality markers.
- **Sales model is 100% phone-based**: no direct checkout anywhere on the page.
  All CTAs go to `#lead` (the two-step lead form). Rabih insisted on
  personally speaking with every buyer across all three tiers. Do NOT add
  Hotmart, Stripe, PayPal buttons "for convenience".
  **Review trigger (agreed 2026-09-03):** after ~30 leads, check call-to-close
  for the $500 digital tier. If Rabih is burning hours on $500 calls that don't
  close, add self-checkout for that tier only.
- **The page sells one thing — a qualified call — not a tier** (decided
  2026-09-03). The hero and every primary CTA go straight to `#lead`; "see the
  tracks" (`#pricing`) is the secondary action. Tier choice happens on the call.
  The pricing section stays for anchoring and transparency, below the fold.
- **No navigation menu.** Logo + one CTA in the header, legal links in the
  footer only. Every nav link is an exit from the funnel (decided 2026-09-03).
- **No unverified scarcity.** No "launch price won't last", no "limited seats"
  unless the number is real and stated (the group cap of 10 is real and shown).
- **Positioning is "warm campus", not "luxury boutique"**: inspired by
  stoxacademy.com (studied together). Dark background + amber gold accent +
  green check marks. Bold, energetic, Arabic-first. NOT quiet-luxury coffee
  tones — we tried that direction and rejected it.
- **The three tiers and their prices**:
  - Digital course (recorded) — **$500** (one payment or 3 installments)
  - Group course — **$1,500** (6 live sessions with Rabih, max 10 people)
  - 1:1 mentorship — **$3,500** (3 months, active business owners only)
  Prices are shown in USD. Rabih quoted the group and 1:1 in ILS originally
  (4,500₪ and 8,000₪) and asked us to convert. The 1:1 was bumped from ~$2,700
  to $3,500 deliberately to create a healthier value ladder.
- **No fabricated testimonials**: the testimonials section is commented out in
  the HTML. Do NOT uncomment or add invented ones. When two real ones arrive
  with explicit permission (verbatim quote + first name + role), enable it.
- **Refund promise wording**: «كسب أو نرجّعلك مصاريك» (win, or we return your
  money). This is Rabih's own phrasing. Do NOT add a specific day count (7-day
  guarantee etc.) unless Rabih confirms — the old 7-day text was Hotmart's
  requirement and no longer applies.

## Copy added by Claude on 2026-09-03 — Rabih to confirm the wording

Short strings only; everything else was reused verbatim from existing copy.
- Phone helper: «مع رمز الدولة» + placeholder `+962…`
- Privacy line: «ما منشارك تفاصيلك مع أي طرف ثالث»
- Submit button while sending: «لحظة…»
- Syllabus aside title: «كل المسارات مبنية على هالمنهج»; facts «درس فيديو» / «أقسام»
- Module lesson counts: «٥ دروس» «٥ دروس» «٤ دروس»

## Copy claims that need Rabih's verbatim approval before launch

Search the file for these — they're in the credentials strip and story cards.
Rabih must sign off that each is factually true as written:

- «كسر رقم قياسي عمره 10 سنين بشركة اتصالات كبيرة»
- The first-close story: one customer with 25 telecom lines → left with 50 packages
- «من الاتصالات لعالم العقارات والمقاولات»
- «آلاف مكالمات البيع الحقيقية»
- The land story: six months of "no" then a deal with a developer

## Live TODOs in the code

Search for `TODO` in `index.html`. As of last session:

1. **`LEAD_ENDPOINT`** (JS, near the bottom) — where the two-step form POSTs.
   Currently empty; the payload is `console.log`'d only. Wire to Zapier/Make/
   Google Sheets or a CRM. Payload shape: `{name, phone, email, tier_interest,
   country, job, status, ref_tag, ts}` (`tier_interest` may be `"undecided"`).
2. **`VSL_EMBED`** — the hero video placeholder (16:9 frame under the hero copy).
   Replace the `.vsl` div with the Vimeo/YouTube embed once the VSL is recorded.
   Vertical cuts are for the ads, not the page.
2b. **`EMAIL_CONFIRM`** — two sentences promising a confirmation email were
   removed until auto-email exists; the original text is kept in HTML comments
   next to each spot. Restore them when the automation is live.
2c. **`PHOTO`** — `.bio-photo` in the story section holds a placeholder glyph.
   Replace with `<img src="/photos/portrait.webp">` when Yaniv uploads photos.
3. **`WHATSAPP_NUMBER`** — inside the success screen, there's an `.js-whats`
   link with `href="#"`. Wire it to `https://wa.me/{number}?text=...` once
   Rabih's business WhatsApp number is chosen.
4. **GA4 / Meta Pixel / TikTok Pixel / Snap Pixel** — the tracking blocks at
   the top of `<head>` are commented out. The code already fires GA4 events
   (`cta_click`, `lead_step_1_complete`, `generate_lead`) via `gtag()` — just
   uncomment and add the IDs.
5. **Photos** — currently the page has no images embedded. In a prior session
   we processed real photos of Rabih and a still-life shot; they are NOT in
   the repo yet. If Yaniv wants them added, he'll upload; do not generate
   images with AI to fill in — the "no invented visuals of Rabih" rule is
   strict.

## The two-step lead form — behavior contract

Not obvious from reading the code, so worth calling out:

- Step 1 asks for name, phone, email only (lowest possible friction).
- Step 2 asks for tier interest (radio, 3 options, **optional** — empty is sent
  as `"undecided"`), country, job (freeform), employment status (radio, 3).
  The age field was removed 2026-09-03 (no use on the call, real friction).
- Clicking any tier's CTA on the pricing cards pre-selects that tier's radio
  in step 2 (via `data-tier` on the button). This is intentional — do not
  remove.
- The submit button locks while sending; the success screen shows even if the
  request fails or hangs (4s fallback). Never lose a lead to a network error.
- Analytics fires `lead_step_1_complete` between steps and `generate_lead`
  after step 2 finishes. Yaniv uses the delta to see if step 2 is burning
  qualified leads. Keep both events.
- The success screen tells the user Rabih will call within 24h. This is a
  promise the ops side must actually keep. Not a design detail.

## Layout & visual system

- CSS variables in `:root` control the entire palette. **All color changes go
  through variables**, don't hardcode hex except in the few places that already
  do (checked in code review).
- Palette: `--bg: #0A0908` (near-black), `--amber: #F5A845` (the accent CTA),
  `--green: #6CE08A` (check marks only).
- Fonts: Noto Kufi Arabic for headings, IBM Plex Sans Arabic for body (both
  Google Fonts, `display=swap`). Do not swap these without discussion.
- Section headings use a two-tone pattern: white line, then `<em>` in amber.
  `h2 br` is hidden under 600px, so keep a space before the `<br>`.
- The featured (group) tier is a cream card on the dark page — the one
  intentional light surface. Its text colors are overridden via CSS variables
  scoped to `.tier.featured`.
- RTL: page is `dir="rtl"`. All spacing uses logical properties
  (`inset-inline-start` etc.) so it stays correct. Keep it that way.
- Mobile-first. The sticky bottom CTA appears only under 900px. Body has
  bottom padding so the sticky doesn't cover content.
- Motion respects `prefers-reduced-motion`.

## Deployment

- Repo: `https://github.com/Yanro2403/rabih-sales` (public)
- Live: `https://rabih-sales.vercel.app`
- Push to `main` → auto-deploy to production
- Feature branches → auto-deploy to preview URLs (share these with Yaniv/Rabih
  for review before merging)

## How to work in this repo

- **Small, reviewable commits**. Yaniv reads every diff before he pushes.
- **Never commit an unfinished redesign to `main`**. Use a branch and share
  the preview URL.
- **Test in a mobile viewport** before every commit. This page will convert
  or die on mobile — most traffic will come from Meta/TikTok/Snap ads.
- Before any structural rewrite (pricing structure, tier count, funnel model),
  **STOP and ask Yaniv**. Those decisions took many rounds to settle.

## What's coming next (rough backlog, priority order)

1. **Wire the lead form to a real endpoint** — without this, every real lead is
   lost. Zapier → Google Sheets is fine for MVP.
2. **VSL script + recording** — the hero video is the single biggest conversion
   lever on the page.
3. **Real photos of Rabih embedded** — the page currently has zero visuals.
4. **Tracking pixels** live before any paid traffic.
5. **First soft launch** — small ad budget, watch conversion data.
6. Real testimonials → enable the section (only after step 5 produces students).

## Handoff context

The design and copy went through many rounds with Yaniv in a Claude web
conversation before this repo existed. The current state reflects those
decisions, not a first draft. If something in the code feels arbitrary, it
probably isn't — ask before "improving" it.

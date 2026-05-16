# DESIGN-home.md - VunaPay

**Status:** v0.1
**Screen:** Home / dashboard
**Surface:** Consumer mobile
**Primary users:** A returning user opening the app, usually with intent: send to someone, check whether a payment landed, or peek at the balance before a purchase.
**Form factor:** Mobile, 390px design width.

## 1. Purpose

The home screen is a launch pad, not a destination. It must answer three questions in the first second of looking: how much money do I have, did the last thing I expected happen, and what do I want to do now. Everything else is secondary. The screen reinforces the brand promise on every visit by exposing live network speed metrics - a small but persistent reminder that VunaPay is fast and that fast is normal.

## 2. Information architecture

Top to bottom: time-aware greeting and notification bell; primary balance card showing the linked bank, masked account, and available balance; a four-tile quick-actions row (Enviar, Receber, Histórico, Definições); a recent transactions list of the last five items; a live network banner showing today's count, average settlement speed, and instantaneous-rate; and finally a four-item bottom navigation. The recent transactions list is the largest scrollable region because it is the most-touched after the quick-action tiles.

## 3. Critical flows

**F1 - Send.** User taps Enviar tile (or the bottom-nav Send icon) → routes to send.html step 1.

**F2 - Inspect last transfer.** User taps the topmost recent row → routes to transaction.html with that transfer's ID. Hovered/pressed state precedes navigation.

**F3 - Refresh balance.** Pull-to-refresh on the scroll region triggers a balance fetch and refreshes the recent-transactions list. Network failure surfaces an inline toast and keeps the previous data.

**F4 - Read notification.** Bell badge dot indicates unread items; tap opens a slide-up panel listing recent push events (received transfers, requests, security notices).

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Greeting | Time-aware string | "Bom dia / Boa tarde / Boa noite" + first name. Date below in the user's locale. |
| Balance card | Brand-gradient card with chip detail | Mono balance in 30px. Bank logo and short code at top-left, account masked at bottom. The watermark "SP" is decorative only. |
| Quick tile | Square card with icon + label | Icon in `--brand-subtle` background, brand-green stroke. Hover lightens border. |
| Recent row | Avatar + name + bank + speed + amount + relative time | Sent values are red-toned, received values are green-toned, never colour-only - the leading sign also distinguishes. |
| Network banner | Small live card with three stats | Pulsing dot indicates the rate is live. Updates every 5 seconds. |
| Bottom nav | 4-tab pill | Active tab fills with brand-subtle. The Send tab can be promoted to a centre-floating CTA in a future iteration. |

## 5. States &amp; edge cases

The balance card renders a neutral grey skeleton while loading; if the bank API is unreachable, it shows the last known balance with a small "última actualização há 4 min" annotation. If the user has zero recent transactions, the list region is replaced with the standard empty state ("Ainda não há transferências") and the primary CTA inside the empty state routes to send. If a recent transaction is still processing, its row shows the processing badge inline instead of the speed indicator.

## 6. Copy &amp; content rules

Greetings always use the polite singular form ("Bom dia, Ana"). Currency renders as `MZN 24.350,00`. Amounts in the list show a leading `−` for sent or `+` for received. Relative time follows: "há X min" up to 60 minutes, "há X h" up to 24 hours, then "ontem" with a 24-hour timestamp, then date as `DD/MM`. Bank short codes are always upper-case in the small chip.

## 7. Responsive behaviour

The home screen is mobile-only. Below 360px the quick tiles drop their labels' letter-spacing slightly. The home screen does not have a tablet or desktop variant; users on those form factors are directed to the bank portal.

## 8. Accessibility notes

The balance card's gradient maintains a contrast ratio of at least 7:1 between white text and the gradient mid-point. The pulsing dot in the network banner respects `prefers-reduced-motion` and fades to a static dot. Each recent row is a single tap target with `role="link"` and a label that combines name, direction, amount and time - e.g. "Enviado a Carlos Machava, MZN 1.500,00, há 2 minutos."

## 9. Open questions

Whether the network banner should show the user's own week-over-week speed instead of the network-wide stat is open; current direction is the network number - it sells the promise to every user, every visit. Whether the Send tile should be replaced with a centre-floating CTA is open; current direction is the four-tile grid for v0.1.

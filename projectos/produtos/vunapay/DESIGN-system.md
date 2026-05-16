# DESIGN-system.md - VunaPay

**Status:** v0.1
**Screen:** Living design system reference
**Surface:** All (consumer mobile, bank admin web, infrastructure simulation)
**Primary users:** Designers, engineers, and PMs building any VunaPay surface
**Form factor:** Web reference, fluid (1280px optimal)

## 1. Purpose

The design system is the single source of truth for every VunaPay surface. It exists so a designer landing on a new screen never invents a colour, never picks a new font weight, and never has to ask whether a button corner is 4 or 8 pixels. The system is opinionated: it has one primary green, one accent gold, one typeface for prose and one for figures, and a small number of components that solve the recurring problems in a payment product. Anything outside this set is a mistake or a deliberate, documented escalation.

The system also encodes the brand promise visually. Speed is communicated through spring-easing on success states, instant micro-confirmations on input, and the persistent presence of a sub-second timer on every transaction artefact. Trust is communicated through generous whitespace, hairline borders rather than shadows, and a deliberate restraint with colour: green and gold do most of the work; red is reserved exclusively for errors.

## 2. Information architecture

The reference page is organised top-to-bottom in the order a designer needs the tokens: brand, then colour (light + dark side by side), then typography (with currency and phone-number examples called out as first-class), then layout primitives (radius, spacing, elevation), then components grouped by use - buttons, inputs, the dedicated amount and PIN inputs, bank selector, status badges, transfer card, success screen, transaction row, avatar, empty states, toasts, and modal. The theme toggle lives in the top-right of every screen and is demonstrated on this page in a fixed position so the entire palette flips live.

## 3. Critical flows

**F1 - Theme switch.** User clicks the sun/moon icon. `data-theme` attribute on `<html>` toggles between `light` and `dark`. All custom properties cascade. Choice persists to `localStorage` under the key `vunapaymz-theme` and is read on page load before first paint to avoid a flash.

**F2 - Token lookup.** A designer or engineer opens this page, scrolls or jumps via an in-page nav, and copies the CSS variable name (e.g. `--brand`) directly from the swatch card. Hex is shown as fallback.

**F3 - Component preview.** Every component is shown in its primary state and its key alternate states (hover, focused, disabled, error) on the same row, so the full surface area is visible without interaction.

## 4. Components & patterns

| Token group | Items | Notes |
|---|---|---|
| Colour - surface | `--bg`, `--bg-2`, `--bg-3`, `--surface` | Four-step neutral ramp. `--bg` is page; `--surface` is cards and inputs. |
| Colour - brand | `--brand`, `--brand-2`, `--brand-subtle` | Green is reserved for primary affordances and positive outcomes. |
| Colour - accent | `--accent`, `--accent-subtle` | Gold for the central clearing node and selected delight moments. Never on text. |
| Colour - ink | `--ink`, `--ink-2`, `--ink-3`, `--ink-4` | Four-step text ramp. `--ink-4` is placeholder only. |
| Colour - semantic | `--good`, `--warn`, `--critical`, `--processing` (+ `*-subtle`) | Status pairs always shipped together: solid + tint. |
| Typography | Inter 400/500/600 for prose, JetBrains Mono for figures | Mono is required for currency, phone, IDs and timestamps. |
| Radius | 4 (chip), 8 (card, input, button), 12 (modal) | No 16+. Friendly, not bubbly. |
| Spacing | 4, 8, 12, 16, 20, 24, 32, 40, 48, 64 | 4-pt base. Vertical rhythm uses 8 and 16. |
| Elevation | 1px borders only; modal shadow `0 2px 8px rgba(0,0,0,0.08)` | No drop shadows on cards. Hairlines only. |

### Components

| Component | Purpose | Key states |
|---|---|---|
| Button | All actions | primary, secondary, ghost, danger, disabled, loading |
| Input | Text, number, search | default, focus, filled, error, disabled |
| Amount input | Currency entry | with `MZN` prefix, mono numerals, balance hint below |
| Phone input | Recipient identifier | fixed `+258` prefix, flag, mono |
| PIN input | 6-digit secret | empty, partial, full, error shake |
| Bank selector | Choose participating bank | list with colour bar + short code |
| Status badge | Transaction state | Instantânea, Processando, Falhada, Pendente |
| Transfer card | Compact transaction row | sender → receiver, amount, speed |
| Success screen | Post-transfer celebration | check, amount, speed, IDs |
| Speed indicator | Sub-second timer | mono, in `--good` |
| Avatar | Person identity | initials, hashed colour |
| Empty state | No data | icon, headline, hint, primary action |
| Toast | Transient feedback | info, success, error - top-centre, 3s |
| Modal | Confirmation | 12px radius, 8% shadow, focus trap |

## 5. States & edge cases

Every interactive element has a visible focus state using a 2px outline in `--brand` (light) or `--brand` brightened (dark). Disabled states drop opacity to roughly 40% and prohibit pointer events. Error states pair `--critical` with an icon and a sentence - colour alone never carries meaning.

When the theme switches, the entire page must repaint without layout shift. All component sizes are theme-independent. Custom properties only change colour values, never dimensions or font sizes.

## 6. Copy & content rules

The reference page is bilingual where it has to be - token names and CSS are English, illustrative copy in component previews is Portuguese (Mozambican). Currency examples always use `MZN 1.500,00`. Phone examples always use `+258 84 234 5678`. Transaction IDs always follow `SWP-YYYYMMDD-XXXXXXXX`.

## 7. Responsive behaviour

The reference is laid out on a 12-column grid at 1280px, collapsing to a single-column stack below 720px. Component cards never exceed 480px wide so they read at a glance.

## 8. Accessibility notes

Contrast ratios for ink-on-surface meet WCAG AA in both themes (`--ink` on `--surface` ≥ 13:1, `--ink-2` ≥ 7:1, `--ink-3` ≥ 4.5:1). Status colours are always paired with an icon and a word. Focus rings are visible on every interactive element. PIN entry uses `aria-label` per dot and `aria-live` for the error announcement.

## 9. Open questions

Whether the QR illustration on the receive screen should be a real QR (encoding the user's `+258...` identifier) is open - for v0.1 we use a stylised placeholder. Whether the gold accent extends to onboarding success is also open; current direction is no - green carries the success moment, gold is reserved for the central clearing node.

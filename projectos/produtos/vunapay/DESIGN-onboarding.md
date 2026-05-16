# DESIGN-onboarding.md - VunaPay

**Status:** v0.1
**Screen:** Onboarding (registration + bank link + PIN)
**Surface:** Consumer mobile
**Primary users:** First-time users opening the VunaPay app on a smartphone, having heard of it from a friend, an SMS, an in-branch flyer, or a radio campaign. Many will be opening any banking app for the first time. Most will be on Android, on intermittent 3G/4G, holding the phone in one hand.
**Form factor:** Mobile, 390px wide canvas. Each step is a full screen.

## 1. Purpose

The onboarding flow takes a person from "I have a phone number and a bank account at a participating bank" to "I can send money to anyone in Mozambique in under three seconds." It must feel short, light and survivable on a slow connection. Every step is a discrete screen so the user can answer one question at a time, and the flow tolerates dropping out at any point - a returning user resumes from the last completed step. The flow is gated on three real-world facts: the user owns the phone (SMS code), the user is who they say they are (BI verification against bank records), and the user controls the PIN.

## 2. Information architecture

Six steps shown linearly: Welcome → Phone &amp; OTP → Personal details → Bank link → PIN → Ready. A six-segment progress indicator sits below the back button on every screen except the welcome and the final confirmation, so the user always knows how much remains. The back button never destroys data; values persist in memory across step transitions and are saved server-side at the end of step 4. Step 4 is the only step that talks to the participating bank's API; if it fails, the user can retry the bank lookup without restarting the flow.

## 3. Critical flows

**F1 - Happy path.** User taps "Começar", enters phone, receives SMS, enters OTP, fills name + BI + DOB, picks bank, enters account number, sees verification spinner resolve to a confirmation card, sets a PIN, confirms PIN, lands on the ready screen. Total median time target: 90 seconds.

**F2 - OTP retry.** If the SMS does not arrive, the resend countdown starts at 60 seconds, decrements visibly in a mono timer, and exposes a "Reenviar" link when it hits zero. After two failed resends, the screen offers a "Receber por chamada de voz" option which calls the user and reads the digits.

**F3 - Bank verification failure.** If the bank does not recognise the account number paired with the BI, the field surfaces an inline error and a hint: "O número de conta não corresponde ao BI registado neste banco. Verifique no seu cartão." The user can retry up to five times before the flow offers to contact the bank's support line.

**F4 - PIN mismatch.** Confirm-PIN screen shakes the dot row and resets to empty with the message "Os dois PINs não coincidem. Tente de novo."

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Step indicator | 6 thin segments, 3px tall | Filled-green for done, brand-green for active, neutral for pending. |
| Phone field | `phone-input` with fixed `+258` prefix and Mozambican flag | Mono digits, 44px tall. |
| OTP cells | 6 individual cells | Each cell autoadvances; backspace moves to the previous. |
| Identity fields | Standard `input`, mono for BI and DOB | BI mask `XXXXXXXXXXXXXX` enforced. |
| Bank list | `bank-row` with colour bar + short code + name | One selected at a time; selected state uses brand-subtle background. |
| Verification card | Inline card with spinner + bank name | On success, swaps to a check icon and the masked account tail. |
| PIN dots + keypad | 6 dots + custom 3×4 keypad | Custom keypad is used (not OS keyboard) to prevent screenshots and learn the user's tap pattern. |
| Welcome illustration | Stylised Mozambique outline + animated route lines | Uses brand-subtle background, brand-green nodes; gold pulse on Maputo. |
| Summary card | Brand-gradient card with phone + bank + masked account | Confirms identity at the end of the flow. |

## 5. States &amp; edge cases

If the user enters a phone that is already registered, step 2 redirects to the login flow, preserving the entered phone. If the BI is malformed (wrong length or check character), the field shows an inline error and the Continue button stays disabled. If the user backgrounds the app during the bank verification spinner, the verification continues server-side; on resume, the screen jumps to the verified state. If the user has no SIM in the device or no signal, the OTP screen surfaces a "sem ligação" banner and disables the resend timer.

The PIN screen explicitly forbids three weak patterns: six identical digits, three or more sequential digits (`123456`), and the user's date of birth in `DDMMYY`. Each rejection shows a one-line explanation and re-enables the keypad.

## 6. Copy &amp; content rules

Mozambican Portuguese throughout. Sentences are short and direct: "O seu número", not "Por favor introduza o seu número de telefone". The brand never apologises in failure copy - it states the fact, then states the next action. BI is always written "Bilhete de Identidade" in field labels, "BI" in body copy. The currency, phone format, BI format and date format follow the project rules without exception.

## 7. Responsive behaviour

The flow is mobile-only. Below 320px wide (a vanishingly small population), font sizes drop one step. Above 480px (tablet portrait), the phone canvas centres and the background fades to `--bg-2` to focus the user. There is no desktop variant - onboarding cannot be completed on web.

## 8. Accessibility notes

The OTP cells expose `aria-label="dígito 1"` through 6 and form a single roving tabindex group. The PIN dots announce "PIN entry, 4 of 6 digits entered" via `aria-live="polite"`. The keypad keys have `aria-label` on the backspace button. Colour is never the sole indicator of progress: the active step segment is also marked with a thicker stroke for screen-magnifier users.

## 9. Open questions

Whether the bank link step should support multiple linked accounts in v0.1 is open - current direction is single-account at signup, with multi-account added under "Definições → Contas ligadas" in a later release. Whether biometric unlock (fingerprint / face) should appear before or after the PIN screen is open; current direction is after, on the home screen, so the PIN is always set first.

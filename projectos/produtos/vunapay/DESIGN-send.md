# DESIGN-send.md - VunaPay

**Status:** v0.1
**Screen:** Send money flow
**Surface:** Consumer mobile
**Primary users:** Anyone with the app open who wants to push money to a phone number - the most common, most demanding, most-watched flow.
**Form factor:** Mobile, 390px design width. Five sequential screens.

## 1. Purpose

Sending money is the product. The flow exists to make a transfer feel like a four-tap action: pick the person, type the amount, confirm with PIN, see the success. Every screen should remove anxiety, not add it. Speed is the unspoken hero - the processing screen is brief on purpose, the success screen surfaces the actual settlement time as a moment of delight.

## 2. Information architecture

Five linear screens, each owning one decision: recipient, amount, confirmation, processing, success. The user can step back from any screen except processing without losing data. Recipient is searchable by phone or name; amount is bounded by available balance and per-transfer limits; confirmation surfaces every fact about the transfer including the zero fee; processing animates the interbank route while the central clearing settles; success states the amount, person, time and ID.

## 3. Critical flows

**F1 - Happy path.** Tap recipient → enter amount → enter PIN → wait ≤3 seconds → see success. Median target: 14 seconds end-to-end on a known recipient.

**F2 - New recipient.** User types a phone number not in their contacts → live lookup against the VunaPay registry → contact card appears in step 1 → user proceeds. If the phone is not registered, an inline message offers to send an SMS invitation.

**F3 - Insufficient balance.** When the entered amount exceeds available balance, the Continue button stays disabled and the balance hint turns red with text "Excede o saldo disponível por MZN X.XX".

**F4 - Wrong PIN.** Three wrong attempts triggers a 60-second cool-off; the PIN row shakes on each attempt and the message names the count: "PIN incorrecto. 1 de 3 tentativas."

**F5 - Settlement failure.** If the central clearing rejects, the processing screen routes to a failure variant (not shown in the canvas) with the reason ("conta destinatária temporariamente bloqueada"), the original amount returned, and a single retry CTA.

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Recipient search | Search input + live contact card | Phone match shows the avatar, name, bank and "Registado no VunaPay ✓". |
| Recents grid | 4-cell grid of small avatars | One-tap reuse of frequent recipients. |
| Recipient mini | Compact card on the amount step | Shows avatar, name, bank and phone in mono. |
| Amount input | The hero | 32px mono with `MZN` prefix; tap-to-edit numeric pad on real device. |
| Quick amounts | Pill buttons at 500, 1.000, 2.000, 5.000 | Tappable presets. Custom values still supported. |
| Note field | Optional, 50-char limit | Counter visible. |
| Confirm card | Six-row data card | Most-prominent row is the amount; fee row uses the green "free" pill. |
| PIN entry | 6 dots + native PIN keypad on real device | The `confirm` screen shows dots; on the device the keypad slides up. |
| Process route | Two bank nodes connected by an animated dashed line with a gold particle | Particle travels left→right; both nodes pulse. The visual makes the interbank nature legible even mid-flight. |
| Success | Animated check + amount + speed pill + transaction ID | The speed pill is the brand promise made tangible. |

## 5. States &amp; edge cases

If the recipient has multiple bank accounts at different participating banks, the contact card surfaces a small bank picker beneath the name; default is the most recently used. If the user enters an amount with too many decimals or in a non-Mozambican format, the field rejects on blur and reformats to `MZN 1.500,00`. If the user backgrounds the app during processing, the success screen takes over the next time the app comes to the foreground (using a push notification as fallback). If the network drops mid-confirmation, the screen surfaces "Reconexão automática - não recomeçar" and waits up to 8 seconds before showing a manual retry.

## 6. Copy &amp; content rules

Mozambican Portuguese throughout. Section titles are imperative and short: "Quanto?", "Confirmar", "Concluído". The fee is named "Taxa" and always shown - never elided when zero, because the zero is the differentiator. The settlement-time line in success uses seconds with one decimal: "Concluída em 2.3 segundos". The transaction ID is always rendered in the mono SWP format.

## 7. Responsive behaviour

Mobile-only. The page in this canvas places all five screens side by side at desktop widths for review; in the real app each screen is a full route. Below 360px the amount input drops one font size step and the confirm card uses tighter row padding.

## 8. Accessibility notes

The amount input announces its value on change via `aria-live="polite"`. The confirm card uses a definition list semantically (`<dl>`) so screen readers read "Para: Carlos Machava, Valor: MZN 1.500,00…" The PIN dots use `aria-label` per dot and the keypad has labelled keys. The processing screen exposes its state as "Transferindo MZN 1.500,00 do Banco de Maputo para Banco de Beira" via `aria-live="assertive"`.

## 9. Open questions

Whether to add a biometric shortcut on the confirm screen (so a fingerprint counts for the PIN) is open; current direction is yes, in v0.2, after the PIN is the proven path. Whether to allow scheduled or recurring transfers is out of scope for the consumer app v0.1 - the core promise is "now", and adding "later" dilutes that promise.

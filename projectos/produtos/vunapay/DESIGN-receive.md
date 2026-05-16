# DESIGN-receive.md - VunaPay

**Status:** v0.1
**Screen:** Receive money (Receber + Pedir tabs)
**Surface:** Consumer mobile
**Primary users:** A user who wants to be paid - sharing their phone number, showing a QR, or pinging someone with an explicit request.
**Form factor:** Mobile, 390px design width.

## 1. Purpose

Receiving on VunaPay is identity, not destination. The user's phone number is the receiver address and never changes. The screen exists for two adjacent tasks: handing identity to someone in person (face-to-face - show QR, share number) and asking someone remote to send (push request with a reason and amount). Both tasks live on the same screen because users mentally group them as "I want money to come to me."

## 2. Information architecture

A two-tab toggle at the top: Receber (default) and Pedir. The Receber tab leads with a large QR code rendered around the user's `+258` identifier, the human-readable phone in mono, and a confirmation card showing the user's name, bank and short code. The Pedir tab leads with a recipient picker, an amount input, an optional reason, a primary "Enviar pedido" CTA and a list of recently sent requests with their statuses (Pendente, Pago, Recusado).

## 3. Critical flows

**F1 - In-person receive.** User opens Receber, hands the phone or shows the QR, the payer scans, transfer arrives. The QR encodes a `vunapay://+25884234567` URI in production so any VunaPay app can resolve it directly into step 2 of send.

**F2 - Share number.** Tapping "Partilhar" opens the OS share sheet with the user's phone and a short message: "O meu VunaPay: +258 84 234 5678 - Ana Cossa, Banco de Maputo."

**F3 - Send request.** Pedir tab → pick contact → amount → optional reason → tap CTA. The recipient gets a push notification: "Ana Cossa pede MZN 2.000,00 - Almoço de sexta. [Pagar] [Recusar]". Tap Pagar opens send.html step 3 (confirmation) prefilled.

**F4 - Cancel a pending request.** Long-press a row in "Pedidos enviados" surfaces a "Cancelar" action. Cancelled requests disappear from the list and the recipient's notification is dismissed.

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Tab pill | Two-segment pill | Active uses `--surface` background with subtle shadow inside the `--bg-2` track. |
| QR card | White-background card with QR + brand-mark centre | The brand-mark is rendered with a 3px white halo so the QR remains valid when overlaid. |
| Phone pill | Mono phone number with copy button | Tap copies; toast confirms. |
| Identity card | `--brand-subtle` row with avatar + name + bank | Reassures the user this is what others will see. |
| Recipient picker | Reused from send step 1 | Pulls from contacts and VunaPay registry. |
| Request row | Avatar + name + reason + amount + status | Status is one of three semantic badges. |

## 5. States &amp; edge cases

If the user has no pending requests, the "Pedidos enviados" list is replaced with the empty state ("Ainda não pediu dinheiro a ninguém"). If a payer pays only part of the requested amount (a future feature), the row shows "Pago parcialmente" and the remaining amount in mono. If the QR fails to render (shouldn't happen but the device may be offline), a static fallback shows a hand-typeable URL and the phone number.

## 6. Copy &amp; content rules

Tab labels are imperative one-word: "Receber", "Pedir". The reason field is phrased as a question - "Para que é?" - to elicit a short answer. Status badges are `Pendente`, `Pago`, `Recusado`. Push notification copy follows the pattern: "{Nome} pede MZN {Valor}{ - Reason}". Cancel and decline copy are explicit and friendly.

## 7. Responsive behaviour

Mobile-only. The page in this canvas places both tabs side by side for review. Below 360px the QR shrinks to 180px square and the identity card stacks the bank chip below the name.

## 8. Accessibility notes

The QR includes a visually-hidden text fallback with the encoded URI so screen readers and screen recorders can read it. The tabs use `role="tablist"` with managed `aria-selected`. Status badges always pair a colour with a word, never colour alone. The copy button announces "Número copiado" via `aria-live="polite"` after a successful copy.

## 9. Open questions

Whether to support fixed-amount QR codes (a merchant-style QR that pre-fills both phone and amount on scan) is open; current direction is yes for v0.2, gated behind a "Pedir presencial" mode in the Pedir tab. Whether to allow a request to expire automatically after 7 days is open; current direction is yes, with a clear visible countdown on the row.

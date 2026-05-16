# DESIGN-transaction.md - VunaPay

**Status:** v0.1
**Screen:** Transaction detail
**Surface:** Consumer mobile
**Primary users:** A user inspecting a single transfer - usually to confirm it landed, to share a receipt, or to flag a problem.
**Form factor:** Mobile, 390px design width, full screen.

## 1. Purpose

This screen is proof. It exists to convince the user - quickly and totally - that the transfer happened, where it happened, when it happened, and that the money is now in a real bank account. The settlement banner is the most important element on the page; everything else is supporting evidence.

## 2. Information architecture

Top to bottom: back button + theme toggle; status badge ("Instantânea"); direction label ("Enviado" / "Recebido"); the amount as the visual hero; the route card showing sender → receiver with both banks and a 2.3s speed label between them; a green settlement banner asserting the money is in the bank account; a details card listing date, ID, sender, origin bank, recipient, destination bank, value, fee, note and the destination account tail; and finally a two-button action row for share and report.

## 3. Critical flows

**F1 - Share receipt.** Tap "Partilhar" → OS share sheet with a generated PDF receipt (or text fallback) including all visible fields plus the VunaPay Central settlement signature.

**F2 - Copy ID.** Tap the copy icon next to the SWP id → copies to clipboard, toast confirms.

**F3 - Report.** Tap "Reportar problema" → opens a one-step form pre-filled with the transaction ID and a category picker (não recebido, valor errado, destinatário errado, suspeita de fraude). Submit routes to the bank's dispute queue.

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Status badge | Large good-tinted badge with check icon | Reads "Instantânea" for settled transfers; alternates exist for processing, pending, failed. |
| Amount hero | 44px mono | Direction word above; no currency colouring (the badge carries the meaning). |
| Route card | Two avatars + animated dashed arrow + speed label | The interbank nature is visible - sender bank short-code on the left, receiver on the right. |
| Settlement banner | Green-tinted card with check + 2-line copy | The plain-language reassurance that the money is "not in a wallet". |
| Details list | Definition-list of label/value rows | Mono for IDs and dates; bank rows include the colour chip. |
| Free pill | Small green-tinted pill | Repeats the zero-fee fact to reinforce the differentiator. |
| Action row | Share + Report | Report is ghost in the destructive ink colour. |

## 5. States &amp; edge cases

For a received transfer the direction label is "Recebido", the route is reversed, and the settlement banner reads "Valor recebido na sua conta em 2.3 segundos." For a failed transfer, the badge is critical, the amount is dimmed, the settlement banner is replaced with a critical-tinted explanation card naming the failure reason and the refund timeline, and the primary action becomes "Tentar novamente". For a still-processing transfer the badge animates and the speed label is replaced with a live elapsed counter; auto-refresh polls until it settles.

## 6. Copy &amp; content rules

Mozambican Portuguese throughout. Every label is upper-case mono micro for scan-ability. The settlement banner is the only place the screen makes a comparative claim ("não numa carteira intermediária") - and it makes it plainly and without naming competitors.

## 7. Responsive behaviour

Mobile-only. Below 360px the route card stacks (sender above, receiver below) and the speed label moves to a full-width centred row.

## 8. Accessibility notes

The route card uses `role="group"` with an `aria-label` that summarises the transfer in one sentence. Copy and share buttons have explicit `aria-label`s. The animated arrow respects `prefers-reduced-motion` and falls back to a static dashed line.

## 9. Open questions

Whether the report flow should support attachments (photo of receipt, screenshot) is open; current direction is yes, in v0.2. Whether to expose the central clearing signature (a hash of the settlement) is open; current direction is no for end-users - too noisy - but yes for the bank portal's transaction detail.

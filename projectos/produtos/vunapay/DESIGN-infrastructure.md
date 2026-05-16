# DESIGN-infrastructure.md - VunaPay

**Status:** v0.1
**Screen:** Infrastructure simulation
**Surface:** Presentation / pitch screen
**Primary users:** Central bank officials, commercial-bank executives, regulators, journalists, partner-bank engineers, internal staff demoing the product. Anyone who needs to understand how money moves on VunaPay in the next sixty seconds.
**Form factor:** Full-screen, dark theme always (1440×900 design canvas; scales fluidly to projector / 4K). Locked in dark mode - this is the only screen in the system that doesn't honour the theme toggle.

## 1. Purpose

This screen exists to make a single architectural fact visible and undeniable: **money moves from one real bank account to another real bank account in under three seconds, through a single clearing hub, on Mozambican infrastructure.** Every visual decision serves that thesis. The map shows it's local. The hub-and-spoke topology shows the system is centralised and auditable, not peer-to-peer guesswork. The particles in flight show how fast it is. The bottom three-step explainer translates the visual into prose for an executive who wants the words to repeat in their next meeting.

## 2. Information architecture

A 64px header strip carries the VunaPay Central wordmark, the live timestamp, and the operational status pill. Below it the screen splits into three columns: a 280px left-hand telemetry pane (live counters of transfers simulated, total volume, average speed, success rate, banks active, plus the gold "Settlement Guarantee &lt; 3.0s" callout); a fluid centre map showing the Mozambique outline with eight bank nodes positioned at their cities and a pulsing gold "CENTRAL" hub at geographic centre; and a 320px right-hand controls pane with a from/to/amount form for triggering manual simulations and a live feed of the last eight transfers. A 220px bottom strip spans full width with the three-step Iniciação / Compensação / Liquidação explainer in bilingual Portuguese-English.

## 3. Critical flows

**F1 - Idle demo.** With nothing happening, the screen runs an auto-loop that fires a random simulated transfer between two random banks every 0.8–2.4 seconds. The presenter says nothing; the screen shows everything.

**F2 - Manual demo.** The presenter picks a from-bank, a to-bank, and an amount, clicks "Enviar transferência". A particle in the originating bank's accent colour travels from the bank node to the central hub, pauses 80ms while the hub's gold rings pulse, then a second particle in the destination's accent colour travels out to the receiver and the receiver node flashes green. Total duration roughly 1.3s - visibly the same magnitude as the real-world settlement time.

**F3 - Talking through the explainer.** The presenter walks the audience through the three steps at the bottom. Each step has an MM:SS budget label in mono ("0,3s", "0,8s", "&lt; 2,0s") that adds up to the &lt; 3 second guarantee.

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Header | Full-width dark bar with brand mark, title, timestamp, live pill | Same brand mark used everywhere. |
| Telemetry panel | Stacked label + mono value blocks | Counters update on every simulated transfer. |
| Settlement guarantee card | Gold-tinted, gradient border | Anchors the brand promise in the bottom-left of the column. |
| Map | Inline SVG with simplified Mozambique outline + eight bank nodes + central node + dashed spokes | All data-driven from a single NODES table. |
| Bank node | Circle with bank short-code, accent colour matched to the participants page | Flash animation on receive. |
| Central hub | Gold core + two animated outward-rings | Rings keep pulsing at idle to communicate liveness. |
| Particle | 4px filled circle with a glow filter | Inherits the colour of its origin/destination bank so the flow is colour-readable from the back of the room. |
| Sim form | from / to selects + amount input + send button | Defaults are BDB → BDM, MZN 1.500,00 - a believable plausible transfer. |
| Live feed | Vertically stacked rows with route, amount, speed | Newest at top; capped at 8 rows; entries fade in from the right. |
| Explainer step | Numbered circle + mono time budget + bilingual title + bilingual description | Three-up grid; each step's time adds up to the guarantee. |

## 5. States &amp; edge cases

If the user picks the same bank for from and to, the send button still fires but the simulator silently no-ops (a self-transfer is meaningless on the network). When the live feed is full the oldest entry is removed silently. When particles overlap they composite additively because of the glow filter - this is intentional and desirable on a projector.

## 6. Copy &amp; content rules

This is the only bilingual screen in the system: Portuguese is the primary voice, English is the secondary technical voice for the regulator/international audience. Numerics use Mozambican format throughout. Time budgets in the explainer are written in Portuguese style with a comma decimal ("0,3s") to match the rest of the product, even when an English audience would read "0.3s" - it's a small but consistent local detail.

## 7. Responsive behaviour

The layout is built for a projector or large-screen demo. Below 1200px the right column collapses below the map and the explainer wraps to a single column. Below 800px the screen falls back to a static thesis page (logo, guarantee number, three steps stacked) since simulation at small size loses its impact.

## 8. Accessibility notes

The map's particle animation respects `prefers-reduced-motion`: when set, the auto-loop pauses and manual simulations show a snap-cut (origin → central → destination) instead of moving particles. Every bank node has an `aria-label` with its full name. The live feed is wrapped in an `aria-live="polite"` region. The colour-coded particles are supplemented by the route text in the feed; nothing on screen depends on colour alone.

## 9. Open questions

Whether to allow the audience to scan a QR to fire a transfer themselves (turning a passive demo into a participatory one) is open and intriguing - adds risk of abuse but doubles as a marketing surface. Whether the explainer should expand inline (click step → show technical sub-flow) is open; current direction is to keep it terse for the live demo and put the deep dive in a separate developer-facing page. Whether the central hub should be relabelled "BCM Central" (Banco Central de Moçambique, if the central bank operates the clearing) vs "VunaPay Central" (independent operator) is a product question, not a design one - both labels fit.

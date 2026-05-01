# DESIGN-cidadao.md — Surface 2 · App do Cidadão

**Status:** v0.3 · Abril 2026
**Form factor:** Android PWA (primary), iOS PWA (secondary), USSD short codes for the rest.
**Primary users:** Cidadãos moçambicanos com smartphone (≈45% da população adulta em 2026).
**Setting:** Telefone na mão do cidadão, em qualquer lado. Latência alta, dados intermitentes, baterias baixas.

---

## 1. Product purpose

A pocket-sized presence of the State for the citizen. Three things, in order of priority:

1. **Carry your civic identity.** A digital wallet of your BI, NUIT, and any certidões you've requested or received — verifiable by anyone with a phone camera.
2. **Make requerimentos sem balcão.** Submit certidões, antecedentes, NUIT requests, mudança de morada, and other low-touch civic requests entirely from the phone. Pay by M-Pesa or eMola. Receive the signed document as a PDF + QR.
3. **See who has touched your data.** A first-person view of every read of your civic record, by which operator, in which posto, when, and why. The same data that conservadores see in the eBI surface — surfaced here too.

It deliberately does *not* try to be a banking app, an identity provider for private services, or a notification hub for ministerial PR.

---

## 2. Information architecture

```
Onboarding (one-time)
  └─ Boas-vindas → Verificar BI (NUIT + telefone + OTP) → Aceitar termos → Casa
Casa (Início)
  ├─ Carteira (BI, NUIT, certidões emitidas)
  ├─ Requerimentos (em curso, recentes)
  ├─ Acessos (12 últimos)
  └─ Avisos do Estado
Carteira
  ├─ BI digital → Mostrar QR → Verificável
  ├─ NUIT digital
  └─ Certidões → Detalhe → Partilhar / Imprimir
Requerimentos
  ├─ Lista (estado · data · processo)
  ├─ Detalhe (timeline · anexos · pagamento · documento final)
  └─ Novo requerimento → Wizard (5 passos)
Acessos
  ├─ Lista cronológica
  └─ Item · Quem · Quando · Posto · Acção · Razão · Reportar
Definições
  ├─ Telefone alternativo · 2FA · Idioma · Notificações
  └─ Sair · Dispositivos com sessão
```

A bottom nav with four tabs: **Início · Carteira · Requerimentos · Acessos**. Definições live behind the avatar in the header.

---

## 3. Critical flows

### F1 — Onboarding
One-time. Citizen enters BI + telefone associado. App calls eBI; if the phone matches the registered número, an OTP is sent. After OTP, the app fetches the citizen's identity, NUIT, and last 12 months of civic events. If the phone *doesn't* match, the app refuses and points the citizen to the nearest Balcão for a re-association (this is a security ceiling — the App cannot bypass posto-presence for first-time identity binding).

### F2 — Show BI digital (verification)
Citizen taps the BI card → full-screen view with name, photo, BI number, and a large dynamic QR. The QR rotates every 60 seconds (prevents screenshot replay) and resolves to a `ugd.gov.mz/v/...` URL with the current verification record. Anyone scanning sees: name, BI, photo, validity, **and a green "verified by State" tick** — but no other data.

### F3 — Submit certidão (sem balcão)
5-step wizard mirroring the conservador's wizard but reframed for the citizen:
1. **Tipo** — what do you need? (controlled list)
2. **Confirmar identificação** — show the data the State already has, ask the citizen to confirm or correct
3. **Anexos** — most certidões need none; mudança de morada needs proof of address
4. **Pagamento** — M-Pesa push, eMola, or "vou pagar no balcão"
5. **Submeter** — receive process number; SMS sent

The wizard tells the citizen, on every step, the **expected outcome** ("This will be ready in ~3 working days") and the **fallback** ("If the system is offline, the request stays in your phone and submits automatically").

### F4 — See acessos
List of every read of the citizen's record across all surfaces (eBI, Saúde, Balcão, Auditoria automática). Each item has: who (operator name + role), when, posto, action, reason where given. Tap → detail page. **Reportar** button on each item — surfaces the access to UGD audit team if the citizen suspects misuse. The App never explains away an access ("must have been routine") — it presents the facts and lets the citizen judge.

### F5 — Receive a signed document
After a conservador signs (in the eBI surface), the citizen gets:
- An SMS with the process number and a deep-link
- A push notification (if app open or background-allowed)
- A new card in the Carteira tab
- A new entry in the Requerimentos tab marked "Assinado"

The document opens with a header strip: green tick + *"Assinado pelo Estado · 04 Abr 2026 · 14:42 CAT · Conservador Tomás A. Macuácua"*. Tap → full QR for verification.

### F6 — Offline composing
The citizen can compose a requerimento offline. It saves to local storage. When the phone reconnects, the app submits, fetches confirmation, and shows a banner *"Submetido com 4 h de atraso por falta de rede. Processo P-2026-0091-INH."*

### F7 — USSD fallback (referenced, not built in protótipo)
Citizens without smartphones use `*144#`. They get: BI status, requerimento status, balance of NUIT, and a list of postos near them. Submitting a requerimento via USSD is **not** supported — that requires posto presence.

---

## 4. Components & patterns

| Component | Citizen-app-specific notes |
|---|---|
| Phone frame (in mocks) | 360×760, 24-px screen radius |
| Top bar (in-app) | 56 px, brand left, avatar right; never carries primary nav |
| Bottom nav | 4 tabs: Início · Carteira · Requerimentos · Acessos. Active = navy-700 icon + label |
| Card stack | Carteira shows cards as a vertical stack (not a swiper — accessibility) |
| Status banner | Persistent if there's an open requerimento or pending payment |
| Wizard | Same 5-step skeleton as eBI; copy adapted for citizen voice |
| QR sheet | Full-screen, rotates every 60s, large enough for a partner to scan in poor lighting |
| Acesso item | Always shows "who" + "when" + "where"; tap reveals "reason" |
| Empty states | Plain language, no illustrations, never humorous |

---

## 5. Citizen voice (PT-MZ)

- "O seu BI é digital." not "Tem o seu BI sempre consigo!"
- "Submeta o requerimento." not "Comece a sua jornada digital!"
- "Este pedido demora 3 dias úteis." (always specific)
- "Pode pagar agora ou no balcão." (always offer the offline path)
- "Eulália do BAÚ Inhambane consultou o seu registo às 14:32 — para emitir a sua renovação de BI." (specific, reason where known)
- Never: "Olá, [Nome]! Como podemos ajudar hoje?" — that voice belongs to commercial apps, not the State.

---

## 6. Critical UI states

### 6.1 First-time open, no BI bound
Single-screen onboarding. No carousel of features. No login-with-Google. Only: BI + telephone + OTP.

### 6.2 BI expirado
Carteira shows the BI card with a yellow strip *"BI expirado a 14 Fev 2026 — renove no posto ou submeta um pedido."* Tapping the strip drops into the renewal wizard.

### 6.3 Requerimento rejeitado
Card in Requerimentos with red badge *"Rejeitado"*; tap reveals the conservador's reason verbatim and offers *"Resubmeter com correcções"* or *"Anular pedido"*.

### 6.4 Acesso suspeito (citizen reported)
Once reported, the item gains a tag *"Reportado · em revisão por UGD"*. The citizen sees state changes (UGD ack, investigation, outcome).

### 6.5 Sem rede, com rascunho
Banner top *"Sem rede — pedido guardado, será submetido quando a rede regressar."*

### 6.6 Sessão expirada
After 30 days inactive, app re-asks for OTP on next open. Cards in Carteira remain visible (read-only) but new requerimentos require re-auth.

---

## 7. Privacy & security

- The phone is the credential. If the phone changes, re-binding requires posto presence.
- BI photo is *displayed* on-device but never cached as an image accessible to other apps (rendered into the WebView).
- The QR rotation prevents replay; the resolver page shows the current verification timestamp.
- The citizen can revoke a paired device at any time via Definições → Dispositivos.
- The app shows a footer note on every Acessos page: *"Esta lista é a mesma que o conservador vê na sua ficha. Se vir um acesso que não esperava, pode reportar à UGD."*
- The app never exports identity outside Mozambican government surfaces. Third-party apps cannot request "Login with eBI" — that is by design.

---

## 8. Offline & low-bandwidth

- App targets `< 3 MB` initial install (PWA)
- Cards in Carteira render from local cache; the QR for verification requires network (the QR rotates on a server-issued nonce — no offline verification, deliberately, to prevent forgery)
- Requerimento drafts persist locally
- The app degrades to a minimum mode on 2G: text-only, no images beyond the BI photo, no animations
- Citizens on USSD get a parallel, simpler fallback (referenced above)

---

## 9. Accessibility

- Body floor 16 px, headings ≥ 18 px
- Touch targets 44 px
- High-contrast mode toggle in Definições (separate from system dark mode — which we do *not* support)
- Screen reader labels on every status badge
- "Read aloud" toggle for the document detail page (deferred to v0.4)

---

## 10. Open questions for v0.4

- Bantu language toggle (Macua, Changana, Sena) — pending UX research
- Voice composing for requerimentos — needs accuracy testing with low-literacy users
- Photo upload from camera vs gallery — currently only camera (anti-spoof); revisit
- Accessibility: large-text mode interaction with QR sheet (QR may overflow at +200%)
- Notifications: opt-in vs default-on for "documento assinado" — leaning opt-in, but legal requires more thought

---

*This document is authoritative for the App do Cidadão surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins.*

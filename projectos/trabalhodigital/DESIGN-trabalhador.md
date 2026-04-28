# DESIGN-trabalhador.md — Surface 1 · Trabalhador (PWA mobile)

**Status:** v0.3 · Abril 2026
**Form factor:** Mobile-first PWA (360 × 760 floor). Installs as app icon on Android. Web fallback on desktop.
**Primary users:** Workers in Mozambique with NUSS or BI. Formal sector contracted workers (84% target), informal sector self-registrants (16% growing), domestic workers, agricultural seasonal workers.
**Setting:** Pessoal smartphone. Often outside business hours. Frequently shared device family-wide. Low data budgets.

---

## 1. Product purpose

The first surface where a worker sees their full employment life: contract, salary, deductions, formation, IGT complaint channel, INSS benefits, INEFP courses. Before this surface, workers in Moçambique often didn't see their contract after signing it, didn't know if INSS had been paid, didn't know what subsídios they qualified for, and couldn't easily denounce informally.

Three priority use-cases, in order:

1. **Verificar o meu contracto, salário, descontos.** "O patrão pagou INSS este mês? Quanto desconta? Tenho recibo?"
2. **Acessar direitos.** Subsídio de doença, maternidade, formação profissional, certidões, pensão.
3. **Denunciar irregularidade à IGT.** Anonimamente. Com ou sem testemunhas. Geo-localização opcional.

Deliberately *not*: not a job board (that's INEFP cidadão view), not a salary negotiation tool, not a workplace social network, not a payroll calculator for employers.

---

## 2. Information architecture

```
Onboarding
├─ Tenho NUSS / Não tenho NUSS
├─ BI ou NUIT (cross-eBI / cross-Finanças)
├─ OTP por SMS
├─ 4 perguntas (idioma, sector, situação, alertas)
└─ Carteira INSS digital atribuída
└─ Hoje (default home)
   ├─ Worker card (nome · NUSS · estado actual)
   ├─ Próximo pagamento (data · valor estimado)
   ├─ INSS deste mês (pago · pendente · em mora)
   └─ Avisos (recibo novo · curso recomendado · subsídio aprovado)
└─ Contracto
   ├─ Contracto vigente (timeline · termos · cópia PDF)
   ├─ Contractos passados
   └─ Modelo de contracto se trabalho informal (auto-registar)
└─ Salário
   ├─ Recibos (com payslip detalhado)
   ├─ Histórico salarial (gráfico)
   └─ Calculadora líquido / bruto
└─ INSS
   ├─ Pagos (mensal · cumulativo)
   ├─ Em mora (com botão denunciar à IGT)
   ├─ Subsídios (doença · maternidade · funeral · velhice)
   └─ Pensão estimada
└─ Direitos
   ├─ Os meus direitos (resumo Lei 23/2007)
   ├─ Férias devidas
   ├─ 13.º mês
   ├─ Horas extra (limite legal)
   └─ Despedimento (regras · indemnizações)
└─ Formação
   ├─ Cursos abertos (cross-INEFP)
   ├─ Cursos concluídos
   └─ Certificações
└─ IGT · Denunciar
   ├─ Tenho problema → denúncia (3 passos)
   ├─ Anónima ou identificada
   └─ Estado da minha denúncia
└─ Eu
   ├─ Identidade (BI · NUIT · NUSS · biometria)
   ├─ Contactos
   ├─ Idioma
   └─ Privacidade
```

Bottom nav 4 tabs: Hoje · Salário · INSS · Eu. Direitos & Formação acessíveis a partir de Hoje. IGT acessível como acção rápida.

---

## 3. Critical flows

### F1 — Onboarding com NUSS · trabalhador formal
- BI ou NUIT → cross-eBI verifica identidade
- "Tenho NUSS" → input do número → cross-INSS verifica
- OTP por SMS → entra
- 4 perguntas (idioma, sector actual, alertas)

### F2 — Onboarding sem NUSS · trabalhador informal
- BI → cross-eBI
- Sistema detecta sem NUSS → propõe inscrição imediata
- 3 perguntas (sector, salário aproximado, situação)
- NUSS atribuído em 24h
- Pode começar a contribuir voluntariamente

### F3 — Hoje
- Worker card hero
- Próximo pagamento estimado (do empregador formal · do INSS se pensionista · não aplicável se informal)
- INSS deste mês: pago/pendente/mora
- 4 atalhos (Salário · INSS · Direitos · IGT)
- Notificações recentes

### F4 — Verificar contracto e salário
- Contracto serifado a abrir em viewer
- Termos destacados (salário base, horário, férias, sector, prazo)
- Recibos mensais em lista
- Tap em recibo abre payslip detalhado

### F5 — Denunciar irregularidade
- 3 passos: o problema · provas (opcional) · identificação ou anonimato
- Categorias: salário não pago · não inscrito INSS · descontos retidos · horas extra não pagas · despedimento ilegal · falta segurança · assédio
- Geo-localização opcional (geo do *local de trabalho*, não do trabalhador)
- Submeter → entra na fila IGT
- Acompanhamento por número de denúncia (ANN-2026-MAP-04218)

### F6 — Pedir subsídio (doença/maternidade)
- Pedido com referência médica (cross-Saúde NUS)
- Cálculo automático (base salarial · dias)
- Submeter ao INSS
- Acompanhar estado (em análise · aprovado · pago)

### F7 — Inscrever-me em curso INEFP
- Pesquisar (área, distância, online/presencial)
- Pré-requisitos verificados automaticamente
- Inscrição → cross-INEFP
- Notificação quando aceite
- Certificado adicionado à Carteira após conclusão

### F8 — Carteira INSS digital + cartão de trabalho
- Carteira com NUSS, foto, sector actual
- Equivalente a apresentar carteira física
- QR scanavel por IGT em campo

---

## 4. Components & patterns

| Component | Trabalhador |
|---|---|
| Phone frame | 360 × 760 |
| Bottom nav 4 tabs | Hoje · Salário · INSS · Eu |
| Top header | Branded · estado de conexão |
| Worker card hero | Orange gradient · QR pequeno |
| Payslip inline | Mono-fonte · linhas adições/deduções |
| Auto inline | Para autos da IGT vistos pelo trabalhador |
| Bottom-sheet modals | Para acções (denunciar, pedir subsídio) |
| Touch ≥ 44 px | Body 16 px floor |

---

## 5. Critical UI states

### 5.1 INSS em mora
*"O teu patrão não pagou o teu INSS de Março. Vê os teus direitos · denuncia à IGT (anónimo)."*

### 5.2 Recibo de salário recebido
*"Manuel, o teu recibo de Abril está disponível. Salário líquido: 18 942 MZN. Vê o detalhe →"*

### 5.3 Subsídio aprovado
*"O teu subsídio de doença foi aprovado: 14 dias · 14 280 MZN. Pago via M-Pesa em 48h."*

### 5.4 Curso INEFP correspondente
*"Há um curso de Soldadura Industrial · INEFP Beira · 6 semanas · grátis. Match com o teu sector."*

### 5.5 Denúncia em fila
*"A tua denúncia (ANN-2026-MAP-04218) foi recebida. Inspector atribuído em 5 dias úteis. Acompanha aqui."*

---

## 6. Estado processual · vocabulário cidadão (simplificado)

| Estado oficial | Mostrado ao trabalhador |
|---|---|
| Contracto vigente | "A trabalhar" |
| Contracto suspenso | "Em pausa (doença/maternidade/etc.)" |
| INSS pago | "Em dia" |
| INSS em mora | "Patrão em atraso · ⚠" |
| INSS regularizado | "Em dia · regularizado" |
| Subsídio em análise | "INSS está a verificar" |
| Subsídio aprovado | "Aprovado · pagamento previsto" |
| Denúncia recebida | "Recebida pela IGT" |
| Denúncia em campo | "Inspector em campo" |
| Denúncia resolvida | "Resolvida" |

---

## 7. Cross-system

Trabalhador lê de:
- **Empregador** — recibos de salário, declaração INSS mensal
- **INSS** — descontos pagos, subsídios aprovados, pensão
- **IGT** — estado de denúncias, autos lavrados sobre o meu empregador
- **INEFP** — cursos disponíveis, certificações concluídas

Trabalhador escreve a:
- **IGT** — denúncias
- **INEFP** — inscrições em cursos
- **INSS** — pedidos de subsídio
- **Empregador** — confirmação de recepção de recibos

---

## 8. Privacidade & segurança

- **Localização do trabalhador NUNCA partilhada com empregador.** Dados geo só no contexto de denúncia (do local de trabalho).
- **Denúncia anónima é realmente anónima.** Sistema gera token, IGT recebe sem BI/NUSS do denunciante.
- **2FA por SMS** obrigatório para pedir subsídio, denunciar identificadamente.
- **Logout automático** após 15 min em ecrã sensível (recibo).
- **Sigilo do salário.** Empregador não vê o que outras empresas pagaram ao trabalhador.

---

## 9. Acessibilidade

- Body 16 px floor (não 14)
- Touch targets ≥ 44 px
- Contraste AA+
- Suporte VoiceOver / TalkBack
- Texto alternativo para cada documento
- Modo "fácil de ler" — frases mais curtas, jargão substituído por exemplos

---

## 10. Multilíngue

PT-MZ + Macua + Changana + Sena + Nyungwe (5 línguas). Default PT-MZ. Switch persistente. Documentos legais (contractos, autos) em PT-MZ por consistência institucional, com glossário inline em língua local.

---

## 11. Open questions for v0.4

- **Trabalhadores rurais sem smartphone** — USSD `*146#` cobre o essencial
- **Pagamento offline de subsídio** — quando M-Pesa não chega ou não tem conta bancária
- **Voz (TTS)** para baixa literacia em PT-MZ + locais
- **Voto de greve** consultativo dentro da app · com sindicato OTM

---

*Authoritative for Trabalhador. DESIGN-system.md wins on conflict.*

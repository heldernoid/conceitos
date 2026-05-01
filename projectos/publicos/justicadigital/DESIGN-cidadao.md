# DESIGN-cidadao.md — Surface 3 · Cidadão / Justiça (PWA mobile)

**Status:** v0.3 · Abril 2026
**Form factor:** Mobile-first PWA (360 × 760 floor). Installs as app icon on Android. Web fallback on desktop.
**Primary users:** Cidadãos moçambicanos com NUIT ou BI. Litigantes (autores, réus, testemunhas), pedintes de certidão, denunciantes de crime. Não advogados — para isso o Portal MJCR.
**Setting:** Telemóvel pessoal, qualquer momento. Frequentemente fora de horário comercial. Conectividade variável.

---

## 1. Product purpose

A justiça acessível ao cidadão sem ir ao tribunal. Antes desta superfície, saber o estado de um processo exigia ir ao tribunal e pedir ao escrivão. Pedir uma certidão exigia fila e dia útil. Apresentar queixa-crime exigia ir à esquadra. Esta superfície reduz tudo isso a um telefone.

Three priority use-cases:

1. **Acompanhar processo onde sou parte.** "O meu divórcio foi sentenciado?" "Quando é a próxima audiência?"
2. **Pedir certidão online.** Pago via SISTAFE (cross-system Finanças). Recebo PDF com selo brass + QR.
3. **Apresentar queixa ou solicitar mediação.** Queixa-crime → Portal MJCR / PGR. Mediação → Tribunal Comunitário do meu bairro.

Deliberadamente *não*: não é fórum jurídico, não é affiliate de advogados (apenas directório OAM), não dá conselho legal, não prediz resultado.

---

## 2. Information architecture

```
Onboarding
└─ Hoje (default home)
   ├─ Próxima diligência (se houver)
   ├─ Processos em curso
   └─ Avisos
└─ Processos
   ├─ Lista (autor, réu, testemunha)
   ├─ Detalhe (timeline · peças · próximos passos)
   ├─ Acompanhar processo de outrem (se público)
   └─ Histórico
└─ Pedir
   ├─ Certidão (Civil · Comercial · Predial · processo)
   ├─ Queixa-crime → PGR
   ├─ Mediação comunitária → bairro
   └─ Petição cível → tribunal judicial
└─ Carteira
   ├─ Certidões válidas
   ├─ Notificações oficiais
   └─ Recibos SISTAFE
└─ Eu
   ├─ Identidade (BI · NUIT · biometria)
   ├─ Bairro/morada
   ├─ Idioma
   └─ Privacidade
```

Bottom nav 4 tabs: Hoje · Processos · Pedir · Eu. **Carteira está em "Eu"** para reduzir congestão.

---

## 3. Critical flows

### F1 — Onboarding
- BI ou NUIT
- OTP por SMS
- Cross-check com **eBI** (Governo Digital) — foto, morada
- Biometria opcional (impressão digital · face)
- 4 perguntas: bairro, idioma, contacto preferido, alertas push

### F2 — Hoje
- Processo activo se for parte: "Próxima audiência: 22 Mai · 09:30 · TJ Maputo"
- Acordos pendentes assinatura
- Notificações oficiais não lidas
- Atalho rápido para 4 acções

### F3 — Detalhe do processo
- **Process card** hero (slate gradient · número · partes · estado)
- Timeline imutável
- Peças (PDF download)
- Próximos passos esperados
- "Como apelar" se aplicável (texto educativo)

### F4 — Pedir certidão
- Tipo (Civil · Comercial · Predial · Processo) → pré-preenchimento
- NUIT/BI ja preenchido
- Custo calculado (varia por tipo)
- **Pago via SISTAFE** (cross-system Finanças Digitais)
- PDF com selo brass enviado em 2-5 minutos
- Disponível em **Carteira** (válido 6-12 meses)

### F5 — Apresentar queixa-crime
- Categoria (Violência doméstica · Furto · Burla · Outro)
- Localização (auto via GPS · ou manual)
- Texto livre + fotos opcionais
- Submeter → entra no MP do tribunal (PGR)
- Cidadão recebe número de processo + assistente social se aplicável

### F6 — Solicitar mediação comunitária
- Bairro detectado por morada
- Tribunal Comunitário automaticamente identificado
- Outra parte (nome + bairro)
- Disputa em texto livre (na língua do cidadão)
- Convocatória disparada para juiz comunitário

### F7 — Timeline pessoal
- Todos os meus processos (autor, réu, testemunha) em ordem cronológica
- Filtros (espécie, estado, ano)
- Eventos com badge de espécie

### F8 — Directório OAM
- Pesquisa por bairro, especialidade, língua
- Dados públicos do advogado (cédula OAM, escritório, especialidade)
- **Sem rating, sem chat, sem affiliate.** Apenas referência.

---

## 4. Components & patterns

| Component | Cidadão |
|---|---|
| Phone frame | 360 × 760 |
| Bottom nav 4 tabs | Hoje · Processos · Pedir · Eu |
| Top header | Branded · estado de conexão |
| Process card hero | Slate gradient · QR pequeno |
| Acta inline | Para certidões com selo brass |
| Bottom-sheet modals | Para acções |
| Touch ≥ 44 px | Body 16 px floor |

---

## 5. Critical UI states

### 5.1 Próxima audiência amanhã
*"Tens audiência amanhã às 09:30 no Tribunal Judicial da Cidade de Maputo, sala 3. Apresenta-te 30 min antes."*

### 5.2 Sentença proferida
*"Foi proferida sentença no teu processo. Procedência total. Tens 15 dias para interpor recurso. Saiba mais →"*

### 5.3 Certidão expirada
*"A tua certidão de nascimento (emitida 14 Mai 2025) expirou. Pede uma nova por 200 MZN."*

### 5.4 Citação por edital
*"Foste citado por edital pelo TJ Maputo no processo P-2026-CIV-MAP-00622 (BCI vs Macia). Tens 30 dias para contestar. Procura advogado urgentemente."*

### 5.5 Queixa-crime aceite
*"A tua queixa foi recebida pelo MP. Número: PGR-2026-MAP-12842. Será contactado em 5 dias úteis. Em caso de violência iminente, ligue 119."*

---

## 6. Estado processual · vocabulário cidadão (simplificado)

| Estado oficial | Mostrado ao cidadão |
|---|---|
| Distribuído | "Em fila para o juiz" |
| Em instrução | "Preparando audiência" |
| Em audiência | "Em julgamento" |
| Sentenciado | "Decidido" |
| Transitado em julgado | "Decidido · final" |
| Suspenso | "Em pausa" |
| Em recurso | "Em apelo no Tribunal Supremo" |

> **Não esconder a complexidade**, mas evitar jargão jurídico onde puder. Termos legais sempre acessíveis com tap "o que é isto?"

---

## 7. Cross-system

Cidadão lê de:
- **Portal MJCR** — actualizações de processos (despachos, audiências, sentenças)
- **Tribunal Comunitário** — actualizações de mediação
- **Cadastro Predial** — DUATs registados no meu nome
- **Registos Públicos** — certidões já emitidas (Carteira)

Cidadão escreve a:
- **Portal MJCR** — petições, queixas-crime, pedidos de certidão
- **Tribunal Comunitário** — pedido de mediação
- **Finanças Digitais** — pagamento via SISTAFE para certidões

---

## 8. Privacidade & segurança

- **Sigilo de processo respeitado.** Cidadão só vê processos onde é parte ou que sejam públicos.
- **Sigiloso por defeito.** Família, menores, criminal sensível: identidades protegidas.
- **Não partilhar localização** sem autorização explícita (excepto queixa-crime se assim escolher).
- **Logout automático** após 15 min em ecrã sigiloso.
- **2FA por SMS** obrigatório para pagar certidão, apresentar queixa, ou agir em processo sigiloso.

---

## 9. Acessibilidade

- Body 16 px floor (não 14)
- Touch targets ≥ 44 px
- Contraste AA+
- Suporte VoiceOver / TalkBack
- Texto alternativo para cada documento
- Modo "fácil de ler" (toggle) — frases mais curtas, jargão substituído

---

## 10. Cross-language

Cidadão suporta as mesmas 4 línguas do Tribunal Comunitário (PT-MZ, Macua, Changana, Sena). Default PT-MZ. Switch persistente.

---

## 11. Open questions for v0.4

- **Pagamento offline** — quem não tem M-Pesa nem cartão como paga certidão? Voucher em quiosque?
- **Push para zonas sem internet** — SMS automático para mesmos eventos críticos
- **Modo "fácil de ler"** — implementação em todas as 4 línguas
- **Audio para baixa literacia** — TTS em PT-MZ + locais

---

*Authoritative for Cidadão. DESIGN-system.md wins on conflict.*

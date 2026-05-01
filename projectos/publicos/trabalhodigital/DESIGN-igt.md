# DESIGN-igt.md — Surface 4 · IGT / Inspecção do Trabalho

**Status:** v0.3 · Abril 2026
**Form factor:** Tablet (10–11", 980×680) for field inspectors; Web desktop (1440+) for admin.
**Primary users:** 416 inspectores da IGT em 11 províncias. Director provincial. Director nacional. Gabinete de coordenação com PGR para casos criminais (ex.: trabalho infantil, escravatura moderna).
**Setting:** Field tablets used in obras de construção, fábricas, plantações, mercados — frequently with intermittent connectivity. Office for case management, response review, statistics.

---

## 1. Product purpose

The arm of the State that walks onto the obra and verifies — directly — what the empresa declared. IGT brings law to the floor of the workplace. Before this surface, inspections were paper forms (modelo 6, modelo 7), declarations were checked against memory, and follow-up was ad-hoc. This surface integrates: planeamento dirigido (cross-INSS, cross-Trabalhador), execução em campo (offline tablet, foto-evidência), audiência conciliatória, coima ou regularização, e escalada para tribunal laboral (cross-Justiça).

Three priority use-cases:

1. **Planeamento dirigido.** Lista de empresas a inspeccionar gerada por cross-INSS (mora, discrepâncias) + cross-Trabalhador (denúncias) + sector risk profile.
2. **Inspecção em campo · tablet offline.** Inspector chega à obra. Identifica trabalhadores. Verifica EPI. Foto-evidência geo-referenciada. Lavra auto se aplicável.
3. **Audiência conciliatória.** Em vez de coima imediata, mediação. Empresa pode regularizar em 14 dias e evitar coima. Se mediação falha, escala.

Deliberately *not*: not a denunciation portal (that's Trabalhador app), not a worker registry (that's INSS), not a judicial proceeding (escala para Tribunal Laboral via Justiça Digital).

---

## 2. Information architecture

```
Inspector mobile/tablet
└─ Hoje (default home)
   ├─ Inspecções marcadas (geo-localização)
   ├─ Inspecções iniciadas (em curso, pendente fechar)
   └─ Atribuídas a mim
└─ Inspeccionar (em campo)
   ├─ Empresa (cross-NUEL · ficha)
   ├─ Identificar trabalhadores presentes
   ├─ Verificar EPI / segurança
   ├─ Foto-evidência geo-referenciada
   ├─ Lavrar auto (modelo PT-MZ)
   └─ Notificar empresa
└─ Audiência conciliatória
   ├─ Convocar partes (empresa + delegado sindical)
   ├─ Acordo / regularização / coima
   └─ Acta
└─ Casos
   ├─ Em campo
   ├─ Resposta da empresa pendente (14 dias)
   ├─ Audiência marcada
   ├─ Regularizadas
   ├─ Coimas pagas / pendentes
   └─ Escaladas (cross-Justiça Tribunal Laboral)

Admin web
└─ Painel nacional
   ├─ Mapa de risco por província
   ├─ KPIs (inspecções · autos · coimas · regularizações)
   └─ Sectores de foco
└─ Planeamento
   ├─ Lista cross-INSS (priorizada)
   ├─ Lista cross-Trabalhador (denúncias)
   ├─ Atribuir aos inspectores
   └─ Calendário trimestral
└─ Relatórios
   ├─ Mensal · ao MTSS
   ├─ Anual · OIT
   └─ Public dashboard (dados.trabalho.gov.mz)
```

---

## 3. Critical flows

### F1 — Inspector recebe inspecções do dia
- Tablet mostra 3 inspecções marcadas (geo-pinned)
- Cada uma com contexto: porque está marcada (mora INSS, denúncia, rotina), histórico, alertas
- Carregamento total para offline antes de sair do escritório

### F2 — Chegada à obra · identificar empresa
- Cross-NUEL valida empresa
- Ficha aparece: declarados, sector, histórico de inspecções, mora INSS
- Foto da entrada da obra (geo-referenciada) inicia inspecção

### F3 — Identificar trabalhadores presentes
- Cada trabalhador apresenta BI ou QR da Carteira INSS digital
- Inspector scaneia QR ou pesquisa por BI
- Sistema cruza: este trabalhador está na folha desta empresa?
- Lista visual: declarado · não declarado · sem identificação

### F4 — Verificar EPI · segurança
- Checklist por sector (Construção: capacete, arnês, calçado · Mineração: máscara, lanterna · etc.)
- Por trabalhador, marca conformidade
- Foto-evidência se necessário (com timestamp + GPS)

### F5 — Lavrar auto de notícia (em campo)
- Sistema pré-preenche com base em discrepâncias detectadas
- Inspector revê e edita
- Empresa-side observador pode contrassinar (ou recusar)
- Auto serifado · selo brass · QR · sincronizado quando há sinal

### F6 — Audiência conciliatória
- 14 dias após auto, audiência marcada
- Partes: empresa (RH ou gerente), trabalhador(es) afectado(s), delegado sindical (opcional), inspector
- Acordo: empresa regulariza (paga INSS em mora, compra EPI, etc.) · coima evitada/reduzida
- Sem acordo: coima formal · escalada possível

### F7 — Aplicar coima · pagamento via SISTAFE
- Coima dimensionada por: tipo infracção (Lei 23/2007 art. 215-220), magnitude, reincidência
- Salário Mínimo Nacional 2026: 5 130 MZN. Coimas de 5-200 SMN.
- Pagamento via SISTAFE em 30 dias
- Se não paga: cross-Justiça (execução fiscal)

### F8 — Escalar para Tribunal Laboral (cross-Justiça)
- Casos graves: trabalho infantil, escravatura moderna, despedimento de denunciante, recusa coima
- Cross-Justiça Digital → processo na 1.ª Sec. Laboral

---

## 4. Components & patterns

| Component | IGT |
|---|---|
| Tablet frame | 980×680, 14 px padding, 8 px radius |
| Touch targets | ≥ 48 px |
| Big buttons | 64×96 px com ícone + texto |
| Inspecção card | Geo-pinned, sector chip, risk meter |
| Auto serifado | Plex Serif body, hi-vis stripe header, brass seal |
| QR scanner | Para Carteira INSS digital |
| Risk meter | Para empresas |
| Map admin | mz-provinces.svg + density |
| Two-step modal | Coima ≥ 100 SMN, escalada Tribunal |

---

## 5. Critical UI states

### 5.1 Inspecção marcada hoje
*"3 inspecções hoje. Próxima: Construtora ALPHA · obra Costa do Sol · 09:30. Mora INSS 8 meses. Risco crítico."*

### 5.2 Trabalhador não declarado detectado
*"Manuel Sitole presente em obra. Não está na folha de Abril da Construtora ALPHA. 4.º não declarado encontrado hoje."*

### 5.3 EPI em falta
*"8 dos 14 trabalhadores em altura sem arnês. Infracção muito grave · art. 219. Coima 50-100 SMN."*

### 5.4 Empresa propõe regularização
*"Construtora ALPHA propõe: comprar EPI em 7 dias + plano regularização INSS em 12 meses. Aceitar?"*

### 5.5 Recusa de assinatura
*"Gerente recusou contrassinar o auto. Auto válido na mesma · Lei 23/2007 art. 226. Anexar foto da recusa."*

---

## 6. Cross-system

IGT lê de:
- **INSS** — discrepâncias, mora, lista de empresas a inspeccionar
- **Empregador** — folhas declaradas, contractos
- **Trabalhador app** — denúncias (anónimas + identificadas)
- **eBI · Governo** — identificar trabalhadores
- **Cadastro Predial · Justiça** — identificar obras

IGT escreve a:
- **Empregador** — autos, prazos de resposta
- **INSS** — cruzamento de descobertas em campo
- **Trabalhador** — confirmação de denúncia investigada
- **Justiça Digital · Tribunal Laboral** — escaladas
- **Finanças Digitais · SISTAFE** — coimas pagas
- **dados.trabalho.gov.mz** — agregados

---

## 7. Open questions for v0.4

- TTS para inspectores que precisam de ler partes do auto em voz alta na obra
- Drone foto-evidência para obras de difícil acesso
- Reconhecimento facial para confirmar identidade trabalhadores (privacy concern · não recomendado)
- Acordos colectivos sectoriais — IGT verifica também?

---

*Authoritative for IGT. DESIGN-system.md wins on conflict.*

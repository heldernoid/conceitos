# DESIGN-comunitario.md — Surface 2 · Tribunal Comunitário · Mediação

**Status:** v0.3 · Abril 2026
**Form factor:** Tablet (10–11", 980×680 working area) — chosen for shared use in rural courts, not pocket devices. Desktop fallback for urban tribunais comunitários.
**Primary users:** Juízes comunitários (eleitos pela comunidade, frequentemente não-letrados ou com escolaridade básica), assistentes/secretários comunitários, partes em conflito.
**Setting:** ~1 645 tribunais comunitários espalhados por bairros e localidades, frequentemente em zonas rurais com conectividade intermitente. Audiências realizadas ao ar livre, em escolas, sedes de bairro, ou pequenos pavilhões comunitários.

---

## 1. Product purpose

Tribunais comunitários são uma instituição **única e constitucional** do sistema moçambicano (art. 4 da Constituição, regulada pela Lei 4/92). Resolvem >60% da litigância em zonas rurais — disputas de terra, conflitos familiares, pequenos furtos, dívidas, vizinhança. Os juízes são eleitos pela comunidade, não-togados, frequentemente não-letrados, e o procedimento é **oral, público, e em língua local**.

Esta superfície existe para:

1. **Dignificar e equipar** o juiz comunitário sem o transformar em juiz togado.
2. **Registar acordos de mediação** com a mesma força institucional que actas judiciais (selo brass, hash, validação pública).
3. **Multilíngue por defeito.** Português (PT-MZ) + Macua + Changana + Sena. Switch persistente.
4. **Funcionar offline.** Conectividade rural é intermitente. Tudo funciona offline e sincroniza quando há sinal.
5. **Escalar para tribunal judicial** quando mediação falha — sem fricção, com cross-link directo ao Portal MJCR.

Deliberadamente *não*: não é um tribunal judicial mais simples; não impõe formato escrito como obrigatório; não substitui o juiz por IA; não traduz automaticamente o que o juiz diz (TTS está em open questions para v0.4).

---

## 2. Information architecture

```
Bind ao tribunal comunitário (passo único na primeira utilização) → Início
└─ Início (4 grandes botões touch · ícones)
   ├─ Receber nova queixa
   ├─ Audiências de hoje
   ├─ Acordos por homologar
   └─ Arquivo (consulta)
└─ Queixa
   ├─ Receber (com gravação de voz opcional)
   ├─ Convocar partes (SMS · ou em pessoa)
   └─ Marcar audiência
└─ Audiência
   ├─ Em curso (timer · partes presentes · notas)
   ├─ Acordo (modelo simples)
   └─ Sem acordo (escalar)
└─ Acordo
   ├─ Redigir (modelo de 4 secções · 4 línguas)
   ├─ Partes assinam (digital · pegada digital se não souber escrever)
   ├─ Homologar (selo brass)
   └─ Notificar (SMS · cidadão app)
└─ Definições
   ├─ Língua activa
   ├─ Modo offline
   └─ Sincronizar (manual)
```

Top bar tablet: brand pequeno, identidade do juiz comunitário, **toggle de língua proeminente**, ícone offline/online.

---

## 3. Critical flows

### F1 — Onboarding do juiz comunitário (primeira sessão)
- Tribunal já provisionado pela DJD com tablet pré-configurado (SIM card + dados de identificação do tribunal)
- Juiz introduz nome, BI, fotografia, idiomas que fala
- Tutorial em vídeo curto na língua escolhida
- **Sem password.** Acesso por PIN de 4 dígitos + impressão digital quando disponível.

### F2 — Início · 4 grandes botões
- **Receber queixa** (verde MISAU)
- **Audiências hoje** (slate · com badge se há marcadas)
- **Acordos por homologar** (brass · se há)
- **Arquivo** (cinza)
Plus: ícones de língua e estado offline na topbar. Navegação reduzida ao mínimo.

### F3 — Receber queixa
- Identidade do queixoso (BI ou impressão digital se BI não disponível, com nota)
- Identidade da outra parte (nome + bairro suficiente)
- Natureza do conflito (chips: Terra · Família · Vizinhança · Dívida · Furto pequeno · Outro)
- **Texto livre na língua escolhida** OU **gravação de voz** (mais comum)
- Sistema cria processo número `C-2026-MAP-PCN-00128` (ano, província, bairro/localidade, sequencial)

### F4 — Convocar partes
- SMS automático para a outra parte se há contacto
- Modelo de convocatória **impresso** que o assistente entrega à mão se não há contacto
- Data sugerida 7-14 dias depois (tempo razoável)

### F5 — Audiência de mediação
- Lista de presentes (foto + nome)
- Notas livres durante a sessão
- Timer
- Audio opcional (mais raro porque consome bateria)
- Decisão final: **acordo · sem acordo · adiada**

### F6 — Redigir acordo
- Modelo simples de 4 secções na **língua escolhida**:
  1. Partes
  2. Disputa (1 frase)
  3. Acordo (texto livre, exemplos pré-preenchidos)
  4. Compromissos (datas, montantes, acções)
- Tradução paralela disponível em PT-MZ se acordo é em língua local
- **Modelo PDF impresso** sempre gerado para arquivo físico

### F7 — Assinatura das partes
- Touch-screen para assinar
- Se parte não sabe escrever: **impressão digital** (touch + pressão)
- Foto facultativa do momento da assinatura
- Sistema gera PDF + hash

### F8 — Homologação · selo brass
- Juiz comunitário valida com PIN
- Sistema sela o acordo com brass "Homologado · Tribunal Comunitário · Lei 4/92"
- QR code para validação pública
- Hash registado, sincroniza com DJD quando online
- Notificações SMS para ambas as partes

### F9 — Sem acordo · escalar para tribunal judicial
- Se mediação falha, juiz comunitário marca "sem acordo"
- Botão **Escalar para tribunal judicial** abre cross-link ao Portal MJCR
- Acta de mediação falhada anexada como peça
- Cidadão recebe notificação no Cidadão/Justiça app a explicar próximo passo
- Cumpre o art. 8.º da Lei 4/92

### F10 — Modo offline + sincronizar
- Todas as operações (criar processo, marcar audiência, redigir acordo) funcionam offline
- Fila de sincronização visível na topbar com contagem
- Sincronização manual + automática quando recupera sinal
- Conflitos de sincronização (improváveis dado o âmbito local) resolvidos por timestamp

---

## 4. Components & patterns

| Component | Tribunal Comunitário |
|---|---|
| Tablet frame | 980×680, 14 px padding, 8 px radius |
| Touch targets | ≥ 48 px (mínimo) |
| Font sizes | Body 16 px (não 14 como desktop), headers 22+ |
| Big buttons | 64×96 px com ícone + texto |
| Language switch | Topbar persistente · 4 línguas · estado salvo |
| Acordo serif | IBM Plex Serif para o documento |
| QR | Para validação pública pós-homologação |
| Selo brass | "Homologado · Tribunal Comunitário · Lei 4/92" |
| Offline pill | Visível sempre · contagem de sync queue |

---

## 5. Línguas e localização

### 5.1 Línguas suportadas
- **Português de Moçambique (PT-MZ)** — base, sempre disponível
- **Macua (Emakhuwa)** — falada principalmente em Nampula, Cabo Delgado, Niassa
- **Changana (Xichangana)** — falada principalmente em Maputo, Gaza, Inhambane
- **Sena (Cisena)** — falada principalmente em Sofala, Manica, Tete, Zambézia

### 5.2 Padrões
- Toggle persistente — uma vez escolhida, mantém-se entre sessões neste tribunal
- Acordos podem ser **bilíngues** (língua local + PT-MZ)
- Termos legais (ex.: "homologação", "Lei 4/92") mantêm forma portuguesa nos textos em línguas locais por consistência institucional
- Sistema **não traduz automaticamente** entre línguas — risco de erro semântico em termos legais. Tradução é responsabilidade do juiz/assistente.

### 5.3 Escolha de língua na queixa
- A queixa é redigida na língua que o queixoso falar
- Se a outra parte não fala essa língua, a convocatória é gerada em ambas

---

## 6. Critical UI states

### 6.1 Sem sinal
*"Sem sinal. As tuas alterações estão guardadas. Vão sincronizar quando voltar a haver sinal."*

### 6.2 Convocatória sem contacto
*"A outra parte não tem número. Imprime a convocatória e entrega em mão na morada."* + botão "⤓ Imprimir"

### 6.3 Parte não sabe escrever
*"Se a parte não sabe escrever, pode usar a impressão digital. Coloca o polegar no ecrã."*

### 6.4 Acordo bilíngue
*"Queres redigir o acordo em duas línguas? Útil se as partes preferem línguas diferentes."*

### 6.5 Mediação falhou (3.ª tentativa)
*"3 audiências sem acordo. Tens duas opções: marcar 4.ª tentativa ou enviar para tribunal judicial."*

---

## 7. Estado processual · tribunal comunitário

| State | Tone | Verb |
|---|---|---|
| Recebida | grey | Marcar audiência |
| Convocada | slate | (aguarda audiência) |
| Em mediação | amber | Audiência em curso |
| Acordo | brass | Homologar |
| Homologado | green | (arquivado) |
| Sem acordo | red | Escalar para tribunal judicial |
| Arquivado | grey | (consulta) |
| Escalado | red | (cross-link Portal MJCR) |

---

## 8. Cross-system

Tribunal Comunitário lê de:
- **eBI · Governo Digital** — identidade da parte com BI
- **Cidadão / Justiça** — pedidos de mediação iniciados pelo cidadão

Tribunal Comunitário escreve a:
- **Cidadão / Justiça** — actualizações de mediação (audiência marcada, acordo, escalada)
- **Portal MJCR** — escaladas (mediação falhada → tribunal judicial)
- **dados.justica.gov.mz** — taxa de mediação, tempo médio, agregados anonimizados

---

## 9. Do not

- **Não traduzir automaticamente** entre línguas (risco semântico em termos legais)
- **Não impor formato escrito como obrigatório** — oralidade é princípio do tribunal comunitário
- **Não fazer videoconferência** — tribunais são presenciais por desígnio cultural e legal
- **Não pedir password complexa ao juiz** — PIN 4 dígitos + biometria suficiente
- **Não exibir publicidade.** Sem afiliação OAM, sem advogados sponsored
- **Não auto-resolver disputas** com IA. Mediação é entre humanos, com presença física

---

## 10. Open questions for v0.4

- **TTS em línguas locais** — para juízes com baixa literacia, ouvir convocatórias e acordos
- **Biometria** — impressão digital fiável em tablet de baixo custo
- **Modelos de acordo por tipo de disputa** (terra, família, dívida, vizinhança)
- **Calendário comunitário** — feriados locais, mercado, época de chuvas que afectam audiências
- **Backup físico** — papel ainda matters; print stylesheet para acta + acordo

---

*Authoritative for Tribunal Comunitário. DESIGN-system.md wins on conflict.*

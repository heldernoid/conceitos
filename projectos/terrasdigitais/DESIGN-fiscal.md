# DESIGN-fiscal.md — Fiscal · Tablet rugged campo

**Status:** v0.3 · Abril 2026
**Surface:** 4 de 5
**Persona principal:** Júlia Sumane Tembe · cédula 2418 · SPGC Sofala

---

## 1. Propósito

Tablet rugged operada pelo fiscal de campo. É a interface entre o terreno físico (com todas as suas complicações: terreno acidentado, cobertura 4G fraca, conflitos sociais, autoridades tradicionais) e o cadastro digital nacional.

Tudo o que o fiscal faz aqui é prova legal: GPS RTK ±2 cm, fotos com EXIF imutável, autos serifados assinados in-situ por 3 partes, hash criptográfico em cada artefacto.

Cobre:

- Tarefas do dia atribuídas pelo SPGC
- Demarcação GPS vértice a vértice
- Detecção de sobreposição em tempo real
- Captura de fotos com EXIF + hash
- Geração e assinatura de auto serifado in-situ
- Verificação de denúncias de cidadãos
- Sincronização robusta offline-first

---

## 2. Princípios

### 2.1 Offline-first
Tambara, Mussassa, Macossa não têm 4G fiável. Tablet tem que operar 100% offline. Sync só quando há rede. Cache local para 30 dias de trabalho.

### 2.2 Hash criptográfico em tudo
Cada foto, cada vértice, cada auto tem hash SHA256. Imutabilidade garantida. Tribunal pode confiar.

### 2.3 Régulo é parte do processo
Em zonas rurais, sem assinatura do régulo o auto não é válido. App tem fluxo dedicado para régulo (com ou sem cédula CFJP digital).

### 2.4 Anonimato em denúncias é sagrado
Fiscal nunca menciona nome do denunciante no terreno. Resposta padrão: "verificação cadastral de rotina".

### 2.5 Detecção em tempo real
App alerta antes de gravar vértice se intersecta DUAT existente. Não permite gravar sobreposição silenciosa.

### 2.6 Tablet rugged · não consumer
IP67, 8h autonomia, GPS RTK integrado, anti-roubo, anti-queda. Bezel terra-900 mais grosso é convencional para sinalizar isto na UI.

---

## 3. Cenas (7)

| # | Cena                              | Componentes principais                              |
| - | --------------------------------- | --------------------------------------------------- |
| 1 | Tarefas do dia                    | tablet rugged · roteiro auto-optimizado · 3 KPIs    |
| 2 | Demarcação GPS in-situ            | poly-frame com 4 vértices capturados + estimados · KV detail |
| 3 | Detecção sobreposição             | header vermelho · 3 polígonos · acções in-situ      |
| 4 | Fotos georref. EXIF               | 6 thumbnails com EXIF visível · banner imutabilidade |
| 5 | Auto serifado · assinatura        | auto component completo · 3 espaços assinatura · cadastro-stripe |
| 6 | Verificar denúncia                | header vermelho · comparação fotos antes/agora · 3 next-steps |
| 7 | Sincronização offline → online    | banner reconexão · queue 14 itens · validação SPGC  |

---

## 4. Componentes signature usados

- **Tablet rugged** com bezel terra-900 reforçado e ondulação lateral
- **Field header** terra-900 com GPS chip e meta in-line
- **Poly-frame em campo** com vértices capturados/estimados visualmente distintos
- **Auto serifado** com 3 espaços de assinatura visualmente distintos (presencial/digital/aguarda)
- **EXIF banner** sobre fotos
- **Sync queue** com estados (enviado/a-enviar/queue)

---

## 5. Cross-system

| Cena | Cross                            |
| ---- | -------------------------------- |
| 1    | `cross-SPGC` · atribuição tarefas |
| 2-3  | `cross-cadastro` (interno)       |
| 5    | `cross-empresa` `cross-CFJP`     |
| 6    | `cross-cidadão` `cross-CFJP` `cross-TJ` |
| 7    | `cross-SPGC` · `cross-empresa` `cross-cidadão` (notificações) |

---

## 6. Personas

| Pessoa                | Papel nesta surface                | Continuidade           |
| --------------------- | ---------------------------------- | ---------------------- |
| Júlia Sumane Tembe    | Fiscal protagonista                | aparece também em SPGC e Cidadão (herdeira) |
| Régulo Mahique        | Autoridade tradicional             | reaparece de Empresa e SPGC |
| Eng. António Greenfield | Representante empresa            | continuação Empresa    |
| Felisberto Manjate    | Cidadão denunciante (Cena 6)       | protagonista do Cidadão |
| Reg. Manjate Cossa    | Titular DUAT-1992 (Cena 3)         | continuação Empresa/SPGC |
| António Tembe         | Ocupante ilegal (Cena 6)           | nova                   |

---

## 7. Edge cases

- **Régulo sem cédula CFJP digital** → assina em papel · fiscal fotografa com EXIF
- **Sem rede durante todo o dia** → sync ao regressar à base · 30 dias autonomia local
- **Tablet roubado** → remote wipe via SPGC · GPS tracking activo
- **Bateria criítica** → modo low-power · só GPS + foto, sem mapa offline
- **Fiscal acidente** → botão SOS chama equipa SPGC + ambulância (cross-Saúde)
- **Conflito violento no terreno** → fiscal abandona local · escala para PRM e SPGC

---

## 8. KPIs operacionais

- **5 tarefas/dia** é o standard (1-2 demarcações grandes ou 4-5 pequenas + 1 verificação)
- **Erro RTK médio &lt; 4 cm** é aceitável; &gt; 8 cm dispara re-formação
- **Sync &lt; 5 min** ao regressar à base é o target
- **Bateria 42% ao fim do dia** é o ponto de carregar (não mais baixo)

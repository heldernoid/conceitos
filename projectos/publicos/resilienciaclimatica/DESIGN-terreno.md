# DESIGN-terreno.md — Surface 3 · Coordenador no terreno

**Status:** v0.3 · Surface 3 de 7
**Persona protagonista:** Aníbal Cossa · coordenador INGD distrital · Mecúfi, Cabo Delgado
**Forma:** tablet rugged · 12" · IP67 · GPS + GSM + offline-first

---

## 1. Propósito

Onde a tecnologia toca a lama. Coordenador INGD com tablet rugged · 4h após landfall do Chido em Mecúfi · começa avaliação no terreno. Censo de afectados, triagem médica, distribuição de bens, registo em abrigos, comunicação de óbitos com dignidade, relatório fim do dia.

Esta surface valida que o sistema funciona **no pior cenário** · GSM intermitente · chuva · pessoas em pânico · informação contraditória.

---

## 2. Princípios

1. **Tablet rugged · não phone** · 12" para tabelas grandes · IP67 contra chuva
2. **Offline-first** · trabalha sem GSM · sincroniza quando há rede
3. **Cross-eBI primeiro** · BI scaneado em 2 segundos · não escrever nomes manualmente
4. **Triagem médica padrão START** · 4 cores · vermelho/amarelo/verde/preto
5. **QR em tudo** · cada saco arroz · cada chapa zinco · auditável depois
6. **Óbitos comunicados pessoalmente** · nunca por SMS · sempre Padre + voluntário CV

---

## 3. Cenas (7)

| # | Título | Componente |
|---|---|---|
| 01 | Chegada · Mecúfi 4h após landfall | Tablet rugged · plano do dia · 8 paragens |
| 02 | Censo · Família Sitole 7 pessoas | cross-eBI valida · zona crítica · sobrinho desaparecido |
| 03 | Triagem médica · Anastácia 71a | START · prioridade vermelha · evacuação aérea Pemba |
| 04 | Distribuição · 28 famílias · QR | Lista cross-eBI · arroz/água/medicação/cobertores · scaneado |
| 05 | Registo em abrigos · Centro Comunitário | 218/240 · 91% · alerta para próximo abrigo |
| 06 | Comunicar óbitos · 4 confirmados | Sóbrio · Padre + voluntário Cruz Vermelha · presencialmente |
| 07 | Relatório fim do dia · 18:42 | 14h trabalho · cross-system actualizado · próximo dia: Pemba |

---

## 4. Componentes signature usados

- `.alerta-pulsante` (Cena 1) · L3 ainda activo
- `.abrigo-card` (Cena 5) · cheio (91%)

---

## 5. Cross-system

- `cross-eBI` · censo em segundos
- `cross-Vida Civil` · óbitos para registo digno
- `cross-Saúde` · feridos · cartão SIS-MA · evacuação para hospital
- `cross-CFJP` · régulo Mahique de Cheringoma confirma identidades em comunidades
- `cross-Terras` · DUATs destruídos sinalizados
- `cross-INGD` · sync com Esperança em Pemba

---

## 6. Edge cases

- **Bruno Sitole · 22a · desaparecido** · não confirmado morto · 30 dias antes de presunção legal
- **Anastácia · prioridade vermelha** · helicóptero · cooperação com Hospital Provincial Pemba (38 km)
- **Adulto não identificado falecido** · cross-eBI por digital ou tatuagens · só depois cross-Vida Civil
- **Menor de 8 anos falecido** · família a localizar · cuidados especiais para irmãos · cross-Justiça tutela
- **GSM falha · 4 distritos** · tablet sincroniza ao regressar a Mecúfi-Sede onde há sinal
- **2 abrigos cheios em simultâneo** · sistema redirecciona automaticamente

---

## 7. Personas referenciadas

- **Aníbal Cossa** · protagonista · coordenador INGD distrital
- **Família Sitole · José + 6** · censada na Cena 2 · regressa em Surface 6 (reconstrução)
- **Anastácia Sitole · 71a · sogra do José** · evacuação aérea
- **Bruno Sitole · 22a · sobrinho** · desaparecido · regressa 4 dias depois
- **Rosalina Macuácua, Domingos Cossa** · 2 dos 4 óbitos registados
- **Padre Manuel Cossa** · acompanha notificação às famílias
- **Maria Tembe** · coordenadora abrigo Centro Comunitário Mecúfi

---

## 8. Open questions

- **Conectividade satélite** (Starlink/Inmarsat) em zonas onde GSM falha completamente · custo?
- **Identificação de cadáveres irreconhecíveis** · base de dados de digitais cross-eBI funciona post-mortem?
- **Estrangeiros afectados** · turistas em Mecúfi · cooperação consular cross-Migrações
- **Cumprir prazos de notificação familiar** vs **dignidade de processo presencial**

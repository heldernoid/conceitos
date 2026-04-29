# DESIGN-sucessao.md — Surface Sucessão · processo guiado

**Status:** v0.3 · Abril 2026
**Surface:** 5 de 6
**Persona-alvo:** sucessão de João Mahique Tembe (falec. 14.02.2026) · 3 herdeiros: Filomena (viúva) + Felisberto e Júlia (filhos)

---

## 1. Propósito

Quando alguém falece (cross-Hospital), o processo de sucessão abre-se automaticamente. Esta surface guia os herdeiros pelos 6 passos:

1. **Sucessão aberta** · automaticamente em 0,8s após registo do óbito
2. **Inventário de bens** · cross-Terras + cross-Bo Moçambique + cross-NUEL listam tudo
3. **Cálculo de quotas** · Lei 22/2009 supletiva ou testamento (1/3 livre disposição)
4. **Acordo dos herdeiros** · partilha amigável (gratuita) ou litigiosa (Tribunal)
5. **Repartição executada** · transferências automáticas cross-system
6. **Imposto sucessório** · 10% para descendentes · cônjuge isento

Objectivo · reduzir prazo médio de sucessão de **18 meses para 6 meses**, custo de 12% do valor herdado para 4%, conflitos familiares de 24% para 8%.

---

## 2. Princípios

### 2.1 Inventário automático
Sem este pacote, herdeiros tinham que ir a cada conservatória, banco, BAU, separadamente. Aqui · `cross-Terras` lista todos os DUATs, `cross-Bo Moçambique` lista contas, `cross-NUEL` lista participações em empresas. Em segundos.

### 2.2 Cálculo transparente
Lei 22/2009 é matemática. Cônjuge sobrevivo · meação 50% (regime comunhão geral) + quota concorrente com filhos. Cena 3 mostra cálculo passo-a-passo · sem mistério.

### 2.3 Partilha amigável incentivada
Acordo entre herdeiros é gratuito e rápido · evita Tribunal de Família. Lei 22/2009 art. 162. Cena 4 mostra como os 3 herdeiros propõem e aceitam pacotes.

### 2.4 Usufruto vitalício para viúva
Cláusula típica em famílias moçambicanas · viúva idosa mantém habitação. Quando ela falecer, casa transmite-se aos descendentes. Respeito pela cultura.

### 2.5 Imposto sucessório · sem surpresas
Filomena (cônjuge sobrevivo) · isenta. Filhos · 10% sobre quota recebida. Pago via M-Pesa ou transferência. Cross-AT regista.

### 2.6 Cross-system massivo
14 entidades notificadas · NUIT cessado, pensão sobrevivência aberta para Filomena, DUATs averbados, conta bancária distribuída, eleitor riscado, NUEL transmitido em Assembleia.

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Sucessão aberta · 3 herdeiros | KPIs · linha do tempo do processo |
| 2 | Inventário · 6 bens automaticamente | Tabela completa cross-system |
| 3 | Cálculo de quotas · Lei 22/2009 | Cálculo passo-a-passo + pie chart SVG |
| 4 | Acordo dos herdeiros · partilha amigável | Tabela de partilha + 3 cards de concordância |
| 5 | Repartição executada · transferências | Lista de cross-system com timestamps |
| 6 | Imposto sucessório · 10% | Cálculo por herdeiro + M-Pesa |
| 7 | Cross-system · 14 entidades | 2 cards · cadeia inicial + execução |

---

## 4. Componentes signature

- `.timeline-vida` (Cena 1)
- `.av.falec` para João + `.av.bebe` para herdeiros vivos
- Pie chart SVG (Cena 3) — único do pacote
- `.assento.obito` referenciado de Cidadão Cena 6

---

## 5. Cross-system (14 entidades)

`cross-DNRN`, `cross-AT`, `cross-INSS`, `cross-Terras`, `cross-NUEL`, `cross-Eleições`, `cross-Bo Moçambique`, `cross-Família`, `cross-Sucessão`, `cross-Sociedade Aberta`, `cross-Saúde`, `cross-Transportes`, `cross-CFJP`, `cross-Justiça`.

---

## 6. Edge cases

- **Sucessão litigiosa** (herdeiros não concordam) → Tribunal de Família · cross-Justiça · prazo longo
- **Herdeiro desconhecido** (filho não reconhecido em vida) → DNA + tribunal · pode reclamar quota
- **Falecido sem herdeiros legitimários** → bens vão para o Estado (Lei 22/2009 art. 158)
- **Falecido com testamento** → 1/3 livre disposição respeitado, 2/3 para herdeiros legitimários
- **Bens fora de Moçambique** → cross-Migrações + cooperação bilateral · processo paralelo no país onde estão os bens
- **Herdeiro estrangeiro** (filho que vive na África do Sul) → identidade verificada via consulado · cross-MNEC
- **Dívidas do falecido** → herdeiros podem aceitar ou repudiar a herança · 60 dias para decidir
- **Bens em casamento polygamico costumeiro** → cada esposa tem direitos específicos · prioridade cultural reconhecida pela Lei 22/2009 com adaptações

---

## 7. Personas

| Persona | Papel |
|---|---|
| João Mahique Tembe (falecido) | 1957-2026 · pai de Felisberto e Júlia · marido de Filomena |
| Filomena Cossa Tembe | Viúva · 64a · meação 50% |
| Felisberto Manjate | Filho · quota 25% · DUAT Vilankulo + carro |
| Júlia Sumane Tembe | Filha · quota 25% · DUAT Cheringoma · fiscal SPGC Sofala |
| Sr.ª Cremilda Tembe | Conservadora supervisiona acordo (Surface 3) |

# DESIGN-ajuda.md — Surface 5 · Transparência da ajuda

**Status:** v0.3 · Surface 5 de 7
**Persona protagonista:** Joana Mahique Cossa · jornalista Savana · investiga gestão de fundos pós-Chido
**Forma:** desktop frame · ferramenta de investigação jornalística pública · acessível a qualquer cidadão

---

## 1. Propósito

Cada metical · cada dólar · auditável por qualquer cidadão sem pedido formal. 30,3 M USD recebidos pós-Chido (Banco Mundial 12,4M · UN OCHA 8,2M · UE/ECHO 6,8M · diáspora · cidadãos M-Pesa). Esta surface mostra fluxo completo · 5 camadas (doadores → INGD → província → distrito → família) · cada nó com timestamp e hash imutável.

Validação directa de cross-Sociedade Aberta (pacote 9). Sem este pacote · auditoria CIP demorava 18 meses como aconteceu pós-Idai. Aqui · paralela.

---

## 2. Princípios

1. **Transparência sem expor cidadão** · família "110100382418" · não nome · não BI
2. **Cada metical rastreável** · família Sitole · 1 120 USD · origem identificável
3. **Auditoria CIP em paralelo** · não 18 meses depois
4. **Cidadão pode contestar** · 84 contestações · 74% a favor do cidadão
5. **Histórico Idai como contraponto** · mostrar evolução · 2019 → 2024
6. **M-Pesa fecha o ciclo** · cidadão também pode doar · isento IRPS automático

---

## 3. Cenas (7)

| # | Título | Conteúdo |
|---|---|---|
| 01 | Doadores · top 10 | 214 doadores · tabela auditável · cross-MEF/MNE/MTel |
| 02 | Fluxo expandido · 5 camadas | Sankey doadores → INGD → província → distrito → famílias |
| 03 | Cada metical · família Sitole | 1 120 USD discriminados · origem por bem · cross-eBI |
| 04 | CIP audita · CIP-2026-0142 | 1,8M USD esclarecidos · 0 desvio · ajustes contabilísticos |
| 05 | Cidadão contesta · Sr. Carlos | CONT-2026-0418 · INGD investiga em 14 dias |
| 06 | Histórico Idai · 7 anos depois | Casos relevantes Idai · evolução até Chido |
| 07 | Cidadão MZ pode doar · M-Pesa | 820k USD de 14 218 contribuições · isento IRPS |

---

## 4. Componentes signature usados

- `.fluxo-ajuda` (Cena 2) · sankey 5 camadas · transparência absoluta
- KPIs grandes (Cena 1, 7) · 30,3M / 25,4M / 4,9M

---

## 5. Cross-system

- `cross-Sociedade Aberta` · principal · transparência institucionalizada
- `cross-CIP` · auditoria pública · processo CIP-2026-0142
- `cross-AT` · isenção IRPS · doações dedutíveis até 5%
- `cross-Bo Moçambique` · transferências interbancárias rastreáveis
- `cross-CNPDP` · anonimização cidadão (família = ID, não nome)
- `cross-eBI` · validação identidade família
- `cross-MEF` (Min. Economia e Finanças) · doadores institucionais
- `cross-MNE` (Min. Negócios Estrangeiros) · cooperação bilateral
- `cross-MTel` (M-Pesa, e-Mola) · doações cidadã

---

## 6. Edge cases

- **Anonimização**: público vê família por ID · só CIP/AT/INGD/própria família vê nomes
- **Discrepância sistema vs cidadão** (Sr. Carlos) · investigação 14 dias · GPS entregador, régulo, recibo
- **Doadores menores** · 204 doadores < 1% · todos visíveis em lista completa · não ocultos
- **Diáspora MZ Portugal** · IBAN europeu · processo cross-Bo Moçambique
- **Criptomoeda internacional** · ainda não regulamentado em MZ · open question
- **Doação anónima** · permite mas regista NUIT internamente para AT

---

## 7. Personas referenciadas

- **Joana Mahique Cossa** · protagonista · jornalista Savana (continuidade Sociedade Aberta)
- **Família Sitole** (Surfaces 3, 6) · caso de rastreabilidade
- **Sr. Carlos Macuácua** · 68a · viúvo · Quissanga · contestação 0418
- **Régulo Mahique de Cheringoma** · valida queixa do Sr. Carlos
- **Banco Mundial / UN OCHA / UE-ECHO / USAID-BHA** · doadores institucionais reais
- **Conselho Cristão de Moçambique · CTA** · doadores nacionais reais
- **Diáspora MZ África do Sul · Portugal** · doadores comunitários

---

## 8. Open questions

- **Anonimização vs auditabilidade externa** · cidadão sem cargo público vê só IDs · jornalista pode pedir mais?
- **Doadores anónimos** · permitir? Compromisso entre privacidade e transparência?
- **Casos antigos** (Idai 2019) · reconstruir transparência retroactivamente · viável?
- **ONGs intermediárias** · cross-MISAU regula registo · controlo de ONGs sem registo?
- **Dedução IRPS automática** · risco de doações falsas para evasão · cross-AT auditoria

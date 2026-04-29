# DESIGN-empresa.md — Surface Empresa · cadeia de propriedade

**Status:** v0.3 · Abril 2026
**Surface:** 3 de 5
**Persona-alvo:** Costa Norte Logística SA (fictícia) · NUEL E-2017-NPL-008412

---

## 1. Propósito

Ficha de pessoa colectiva com toda a cadeia de propriedade visível. Implementa operacionalmente a Lei 14/2018 anti-branqueamento (art. 14, identificação de beneficiário efectivo) e a Lei 10/2017 direito à informação.

A persona Costa Norte é alvo de investigação pelo conflito de interesses do beneficiário efectivo (Eng. Nhantumbo, DG da empresa pública adjudicante PCFM Norte SA).

---

## 2. Princípios

### 2.1 Beneficiário efectivo é central
Não basta saber quem aparece nas escrituras. A cadeia accionista é desagregada até à pessoa singular última, com cálculo automático da percentagem efectiva (directa + indirecta).

### 2.2 Cadeia visual é canónica
A `.net-card` SVG é o componente identificador desta surface. Pessoa singular = vermelho, empresa = cobalto, contrato público = brass. Pessoa pública na cadeia = stroke vermelho mais grosso.

### 2.3 Cruzamento automático com pessoas públicas
Sempre que um beneficiário efectivo é também pessoa pública, banner red aparece. Isto é o que torna o sistema operacionalmente útil para detectar conflitos de interesses.

### 2.4 Audit trail imutável
Lei 14/2018 obriga registo histórico de alterações accionistas, capital, sede, objecto. Cada alteração é datada, hash criptográfico, irreversível. Reverter exige despacho judicial.

### 2.5 Demonstrações financeiras públicas
Receita anual cruzada com cross-AT IRPC. Empresas com &gt; 50 funcionários ou capital &gt; 10 M MT são automaticamente públicas (limiares ilustrativos).

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Cabeçalho empresa | Hero cobalto + 4 KPIs · banner com pessoa pública na cadeia |
| 2 | Cadeia accionista visual | `.net-card` grande · 3 níveis · MTS Investments mostrada como nó intermédio |
| 3 | Beneficiário efectivo · cálculo | `.ficha public` ampliada · `.ledger-row` 3-coluna mostrando 62%+22% |
| 4 | Demonstrações 5 anos | Bar chart SVG inline · linha vertical 2021 (DG nomeação) · breakdown receita |
| 5 | Contratos públicos | Tabela 2 contratos · banner red conflito · ambos do mesmo adjudicante |
| 6 | Pessoas ligadas | Conselho de Administração + auditora + conselho fiscal |
| 7 | Histórico imutável | Audit trail 9 eventos · evento crítico (nomeação 2021) destacado em red |

---

## 4. Componentes signature

- `.net-card` em Cena 2 ampliada (1100×360 viewBox) — peça mais elaborada do pacote
- `.ficha empresa` (cobalto) em cabeçalho
- `.ledger-row` adaptada para histórico de alterações
- Bar chart SVG inline em Cena 4 (não componente, ad-hoc por ser específica)

---

## 5. Cálculo do beneficiário efectivo

```
Detenção_efectiva(P, E) = Detenção_directa(P, E) +
                          Σ Detenção_directa(P, Ei) × Detenção_directa(Ei, E)
                          para todas Ei intermediárias
```

Exemplo Nhantumbo → Costa Norte:
- Directa: 62%
- Indirecta via MTS Investments: 22% × 100% (detém MTS integralmente) = 22%
- **Total efectivo: 84%**

Limiar de divulgação obrigatória Lei 14/2018: 25%. Nhantumbo ultrapassa largamente.

---

## 6. Cross-system

`cross-NUEL` (BAU) · `cross-NUIT` (AT) · `cross-Bo Moçambique` (regulação cambial) · `cross-Contratação Pública UFSA` · `cross-CIP` · `cross-NUSS` (218 inscritos) · `cross-INSS`

---

## 7. Edge cases

- **Holding em jurisdição offshore** → identificação obrigatória do beneficiário efectivo último, mesmo via Maurícias, Dubai, Lisboa
- **Trust ou fundação como sócio** → trustee ou conselho de fundação revelados
- **Sócios menores de idade** → identificação reduzida (apenas iniciais + parentesco), nunca nome completo
- **Empresa em insolvência** → ficha mantida com tag "insolvente" · administrador judicial substitui CA
- **Empresa com declaração falsa de beneficiário efectivo** → cross-PGR · enriquecimento ilícito + branqueamento

---

## 8. Limiares de inclusão automática

| Limiar | Inclusão |
|---|---|
| Capital social &gt; 10 M MT | Sim, pública |
| Funcionários &gt; 50 | Sim, pública |
| Contrato público adjudicado | Sim, qualquer valor |
| Beneficiário efectivo é pessoa pública | Sim, mesmo abaixo de outros limiares |
| Capital &lt; 1 M MT + sem contratos públicos + sem pessoa pública | Não, fica em registo BAU privado |

---

## 9. Personas/empresas fictícias

| Entidade | Papel |
|---|---|
| Costa Norte Logística SA | Alvo |
| MTS Investments Lda | Holding intermediária |
| Portos & Caminhos de Ferro Norte SA | Empresa pública adjudicante |
| Auditores Associados Lda | Auditora externa |
| Mussassa Agro Lda | Empresa periférica do grupo |
| Eng. Augusto Nhantumbo | Beneficiário efectivo 84% (pessoa pública) |
| Maria Sumane | Cônjuge · 10% directo |
| Pedro Sitole, João Macuácua, Cristina Tembe Cossa | Vogais CA |
| Helena Cossa | Sócia rotativa Auditores Associados |
| Joaquina Mucavele | Presidente Conselho Fiscal |

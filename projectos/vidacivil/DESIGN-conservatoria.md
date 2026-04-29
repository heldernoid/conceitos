# DESIGN-conservatoria.md — Surface Conservatória · funcionária

**Status:** v0.3 · Abril 2026
**Surface:** 3 de 6
**Persona:** Sr.ª Cremilda Tembe · Conservadora do Registo Civil de Maxixe

---

## 1. Propósito · "ponto-de-completamento"

A conservatória deixa de ser ponto-de-partida (onde tudo começava) · passa a ser **ponto-de-completamento** (onde se finaliza o que outros já registaram).

Dos 14 actos do dia da Sr.ª Cremilda:
- 5 vêm do hospital (provisórios a completar com nome)
- 2 vêm de parto domiciliar (parteira credenciada)
- 1 vem de casamento religioso (averbamento)
- O resto são casamentos civis, divórcios, óbitos sem hospital, mudança de nome.

Esta inversão de papel libera a conservatória do gargalo que era: o cidadão tinha que se deslocar para um único ponto. Agora · o registo viaja até onde está a vida.

---

## 2. Princípios

### 2.1 Reaproveitamento total
Quando pais comparecem para escolher nome · a app não pede informação que o hospital já registou. Sexo, hora, peso, mãe · tudo herdado do `.assento-prov`. Sr.ª Cremilda só finaliza nome + paternidade.

### 2.2 Solenidade nos casamentos
Casamento civil é momento solene. Plex Serif majestoso, fórmula legal, assinaturas de testemunhas. Cerimónia tem peso institucional.

### 2.3 Sobriedade nos divórcios
Divórcio consensual sem filhos menores tratado eficientemente · 30 minutos. Sem julgamento, sem drama. Acordo de partilha pré-validado.

### 2.4 Estatística diária para INE
Cada acto alimenta indicadores nacionais em tempo real. Antes recolhidos manualmente em formulários P3 com 60 dias de atraso, agora cross-INE em 0,8 segundos.

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Painel · 14 actos hoje | Sidebar conservatória + tabela de agendamentos |
| 2 | Pais escolhem nome · Lara | Form com `.assento-prov` herdado + sidebar de pais presentes |
| 3 | Confirmar paternidade · Felisberto | Termos solenes + biometria + assinatura digital |
| 4 | Assento finalizado · Lara Manjate Sumane | `.assento.nascimento` completo + `.cedula` infantil |
| 5 | Casamento civil · António + Marta | 8 testemunhas + 3 regimes de bens visualizados |
| 6 | Divórcio consensual · Pedro + Cristina | `.assento.divorcio` + tabela de partilha 50/50 |
| 7 | Estatística diária · cross-INE | 4 KPIs + bar chart + decomposição |

---

## 4. Componentes signature

- Sidebar `.sidebar` com nav-side e contadores
- `.assento-prov` reaproveitado (Cena 2)
- `.assento.nascimento` finalizado (Cena 4)
- `.cedula` (Cena 4)
- `.regime-card` em 3 variantes (Cena 5)
- `.assento.divorcio` (Cena 6)

---

## 5. Cross-system

`cross-eBI`, `cross-DNRN`, `cross-DIC` (cédula em emissão), `cross-Hospital` (provisórios herdados), `cross-CFJP` (parteira tradicional), `cross-Justiça` (divórcio litigioso), `cross-INE` (estatística vital).

---

## 6. Edge cases

- **Pais não comparecem em 30 dias** → bebé fica "Manjate Sumane (sem primeiro nome)" durante 12 meses · após esse prazo, conservadora atribui nome genérico ("Maria" para feminino, "João" para masculino) e família pode contestar
- **Casamento poligâmico costumeiro** → reconhecido culturalmente, registado como uniões separadas
- **Casamento por procuração** → admitido pela Lei 10/2004 art. 14 com cuidados especiais
- **Divórcio com filhos menores** → encaminhado obrigatoriamente para Tribunal de Família (cross-Justiça)
- **Óbito sem hospital, sem médico legista próximo** → autoridade local declara, médico legista valida posteriormente
- **Pessoas indígenas com nome tradicional + civil** → admitidos ambos · "nome civil" para registo, "nome tradicional" como nome alternativo

---

## 7. Personas

| Persona | Papel |
|---|---|
| Sr.ª Cremilda Tembe | Conservadora · Maxixe · supervisiona equipa de 5 |
| António Sitole + Marta Cossa | Casamento civil 10:00 · 8 testemunhas |
| Pedro Cossa + Cristina Mahique | Divórcio consensual sem filhos menores |
| Padre António Sitole | Oficiante religioso · averbamento |
| Felisberto + Joana + Lara | Cena 2-4 · completar nome do bebé |

# DESIGN-cidadao.md — Surface 2 · Cidadão · "estou recenseado?"

**Status:** v0.4 · Surface 2 de 7
**Persona protagonista:** Felisberto Manjate · 38a · Maxixe (continuidade família 11 pacotes)
**Forma:** phone mockup · 360px · 4G

---

## 1. Propósito

Como o cidadão comum acede ao seu registo eleitoral · 30 segundos · sem fila. Felisberto Manjate · cidadão central da série Conceitos · 5.ª eleição · sempre Mesa 0142. Esta superfície valida que toda a infra-estrutura técnica das outras superfícies se traduz em vivência cidadã digna · sem fricção.

---

## 2. Princípios

1. **Phone simples sempre** · 360px
2. **"Perguntar é grátis · sempre"** · acesso ao próprio registo é direito
3. **3 acções principais** · ver registo · auditar · contestar
4. **Histórico sem comprometer anonimato** · sistema sabe que votou · não sabe em quem
5. **Edge cases reais** · transferência · contestação · comprovativo
6. **Linguagem clara · sem jargão** · NUEL explicado quando aparece

---

## 3. Cenas (7)

| # | Título | Cenário |
|---|---|---|
| 01 | Estou recenseado? · 30 seg | Phone · estado activo · NUEL · mesa atribuída |
| 02 | Mesa atribuída · 0142 · 600m | Mesa-card + mapa simbólico + equipa da mesa |
| 03 | Histórico de votos · 4 eleições | Lista cronológica · 2014→2024 · próxima 2029 |
| 04 | Verificação cruzada · 4 fontes | `.verificacao-cruzada` · 4 hashes públicos |
| 05 | Pedido de transferência · trabalho | Edge cases · 7 cenários (diáspora, hospital, etc) |
| 06 | Contestar erro · presunção a favor | Tipos · 14 dias · escala TES |
| 07 | Comprovativo · QR + assinatura | Certidão · 6 usos comuns |

---

## 4. Componentes signature usados

- `.caderno-publico` (Cena 1) · estado activo
- `.mesa-card` (Cena 2) · normal
- `.verificacao-cruzada` (Cena 4) · 4 fontes ✓

---

## 5. Cross-system

- `cross-Vida Civil` · idade · vivacidade
- `cross-eBI` · biometria
- `cross-Terras` · endereço · mesa próxima
- `cross-AT` · NUIT distinto NUEL
- `cross-Migrações` · diáspora
- `cross-TES` · contestações escaláveis
- `cross-Sociedade Aberta` · transparência

---

## 6. Edge cases

- **Trabalha noutra zona** · pedido de transferência 5 meses antes
- **Mudou de morada** · cross-Terras propaga · mesa nova
- **Diáspora** · cross-Migrações · embaixadas · 12 países
- **Detido preventivo** · mesa móvel
- **Refugiado interno** · mesa do abrigo · cross-Resiliência
- **Sem-abrigo** · último endereço ou pedido manual
- **Hospital de longa permanência** · mesa móvel
- **Voto facultativo** · não votar não tem penalização

---

## 7. Personas referenciadas

- **Felisberto Manjate** · protagonista (continuidade 11 pacotes)
- **Joana Sumane Manjate** · esposa
- **Pedro Manjate Sumane** · filho · cross-referência Surface 3
- **Aurélio Tembe** · presidente Mesa 0142 · cross-Surface 4
- **Sr. Domingos Cossa** · caso de contestação · cross-Surface 1

---

## 8. Open questions

- App em **modo offline** para zonas sem GSM · sincroniza depois?
- **Idosos sem smartphone** · ainda 28% rurais · alternativa via régulo?
- **Anonimato perfeito** vs **histórico pessoal útil** · onde está a linha?
- **Notificações push** · só quando há acção do cidadão · ou também passivas?

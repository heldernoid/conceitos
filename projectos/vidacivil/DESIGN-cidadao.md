# DESIGN-cidadao.md — Surface Cidadão · vida documentada

**Status:** v0.3 · Abril 2026
**Surface:** 1 de 6 · destacada
**Persona:** Felisberto Manjate · 38 anos · Inhambane · BI 110100442918 (continuidade Terras + Sociedade Aberta)

---

## 1. Propósito

Linha do tempo pessoal da vida documentada de qualquer cidadão · 5 actos vitais visualizados num só lugar com `.timeline-vida`. Todos os assentos online, descarregáveis, com QR validável e hash imutável.

A surface é o "rosto cidadão" do pacote · onde Felisberto vê a sua própria vida arquivada e pode partilhar documentos com terceiros (banco, hospital, escola).

---

## 2. Princípios

### 2.1 Tempo é a estrutura central
Não é tabela, não é mapa · é cronologia vertical. Cada evento da vida é um nó com cor própria (nascimento verde, casamento brass, óbito cinza, presente vermelho-livro pulsante). Componente signature: `.timeline-vida`.

### 2.2 Documentos como artefactos
Cena 2, 4, 6 mostram documentos serifados completos (assento de nascimento, certidão de casamento, certidão de óbito do pai). Plex Serif domina · papel cartolina · selo brass · QR validável.

### 2.3 Reuso máximo
A linha do tempo carrega-se inteiramente cross-DNRN. Nenhum dado manualmente inserido. Os 5 actos representados estão todos baseados em assentos legais reais de Felisberto.

### 2.4 Partilha controlada
Cena 7 mostra mecanismo de partilha de certidão · link único, expiração configurável, hash imutável, revogável. Nada sai do controlo do titular.

---

## 3. Cenas (7)

| # | Cena | Componente principal |
|---|---|---|
| 1 | Linha do tempo · 5 actos | `.timeline-vida` + sidebar de acções |
| 2 | Assento de nascimento · 1988 | `.assento.nascimento` + ações |
| 3 | BI online · 2002-2032 | Card BI custom + cross-system |
| 4 | Certidão casamento · 2018 | `.assento.casamento` + `.regime-card` |
| 5 | Bebé Lara nasceu · provisório | `.assento-prov` + `.cedula` + SMS |
| 6 | Falecimento do pai · 2026 | `.assento.obito` + cross-system propaga |
| 7 | Pedir certidão · partilhar | Form + histórico de partilhas |

---

## 4. Componentes signature usados

- `.timeline-vida` (Cenas 1)
- `.assento` em 4 variantes (Cenas 2, 4, 5, 6)
- `.assento-prov` (Cena 5)
- `.cedula` (Cena 5)
- `.regime-card` (Cena 4)

---

## 5. Cross-system

`cross-eBI` (sessão), `cross-DIC` (BI), `cross-DNRN` (todos os assentos), `cross-AT` (NUIT), `cross-INSS` (pensão), `cross-Terras` (DUATs), `cross-Saúde` (cartão SIS-MA), `cross-Eleições` (eleitor), `cross-Bo Moçambique` (contas bancárias herança).

---

## 6. Edge cases

- **Cidadão sem assento de nascimento** → fluxo "registo tardio" via Surface 3 (Conservatória)
- **Cidadão com nome alterado** → linha do tempo mostra apenas nome actual · cross-Surface 6 redacted
- **Cidadão falecido** (Cidadão de outro perfil consulta a sua linha) → linha pára em data de óbito · banner livro
- **Estrangeiro residente** → linha começa em "naturalização" · sem assento de nascimento MZ
- **Refugiado registado MZ** → linha começa em "registo de refugiado" · cross-Migrações

---

## 7. Persona

Felisberto Manjate é a continuidade de Terras Digitais (8.º pacote) e Sociedade Aberta (9.º). Aqui ganha família alargada · esposa Joana, filha recém-nascida Lara, pai falecido João, mãe Filomena, irmã Júlia. Toda a sua vida documentada num só ecrã.

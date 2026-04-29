# DESIGN-jornalista.md — Surface Jornalista · investigação credenciada

**Status:** v0.3 · Abril 2026
**Surface:** 4 de 5
**Persona-alvo:** Joana Mahique Cossa (fictícia) · Savana · credencial INC-2024-0418

---

## 1. Propósito

Workspace dedicado ao jornalismo de investigação. Funcionalidades além do cidadão comum:

- Investigações organizadas (4 activas + arquivo)
- Notas privadas cifradas no servidor
- Cronologia de cada investigação (auditável internamente)
- Cruzamento de NUITs · poderosa ferramenta investigativa
- Watchlist com alertas em tempo real
- Exportação CSV/JSON/datasette para jornalismo de dados
- Pegada visível · simetria também aplicável ao jornalista
- Publicação com hash imutável

A persona Joana é a investigadora da reportagem "Rácio 14× de uma vida pública" sobre Eng. Nhantumbo · publicada em Savana 18.04.2026.

---

## 2. Princípios

### 2.1 Credenciação INC obrigatória
Acesso de jornalista exige credencial activa do Instituto Nacional de Comunicação Social. Sem credencial, jornalista usa surface de cidadão comum (sem ferramentas avançadas).

### 2.2 Notas privadas cifradas
Cada investigação tem espaço de notas. Cifradas com chave pessoal · nem o operador do sistema lê. Único caso de informação que NÃO é pública neste pacote — a privacidade do trabalho jornalístico em curso é protegida.

### 2.3 Pegada visível para o titular
Cada consulta da Joana fica visível para o titular consultado (Surface 5). A simetria é absoluta: o jornalista é tão investigado pelo titular quanto o titular é investigado pelo jornalista.

### 2.4 Cruzamento limitado
50 cruzamentos/mês por jornalista. Padrões anómalos (100+ pessoas em 1h) disparam revisão CNPDP da credencial. Evita uso da ferramenta para perseguição ou listas de inimigos.

### 2.5 Hash imutável de publicação
Cada artigo publicado gera hash SHA256. Edições futuras ficam registadas como tal · não é possível "apagar" reportagens silenciosamente. Direito a réplica do visado anexa-se ao hash original.

### 2.6 Anti-perseguição · proteção do investigado
Pedidos de explicação não respondidos, padrões anómalos de consulta, investigações sem publicação dentro de 12 meses · todos disparam revisão CNPDP. Profissão jornalística é protegida; abuso da credencial é punido.

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Workspace · 4 investigações + alertas | KPIs · 2 listas (investigações + alertas watchlist) |
| 2 | Investigação activa · INV-2026-014 | Pull-quote hipótese · cronologia interna · notas privadas serif |
| 3 | Cruzamento de NUITs | Tabela 14 pessoas · ligações por tipo · banner cuidado |
| 4 | Watchlist · 42 entidades | 7 alertas + configuração de tipos de alerta |
| 5 | Exportar dataset | Pré-visualização CSV · histórico de exportações com hash |
| 6 | Pegada visível | Lado-a-lado: que vejo / que vê de mim · pedidos de explicação recebidos |
| 7 | Publicar investigação | Artigo serif "Rácio 14× de uma vida pública" · com link permanente e hash |

---

## 4. Componentes signature

- `.av` com `background: var(--red-700)` para o jornalista (pessoa pública também)
- `.pull-quote` recorrente (Cena 2 hipótese, Cena 6 reportagem do Savana)
- Notas privadas em block serif italic com fundo `paper-2` e barra esquerda preta
- Cena 7 quasi-newspaper-layout: serif XL, deck italic, inline `.redacted` no nome

---

## 5. Categorias de alertas watchlist

| Tipo | Quando | Cor |
|---|---|---|
| Novo NUEL associado | Pessoa cria empresa | red `⚠` |
| Contrato público adjudicado | Empresa &gt; 1 M MT | amber `⚡` |
| Novo DUAT registado | Pessoa torna-se titular | amber `⚡` |
| Declaração de bens · entrega/alteração | Lei 16/2012 | ink `i` |
| Mudança patrimonial &gt; 10% | Variação significativa | amber `⚡` |
| Processo CIP/PGR aberto | Investigação iniciada | red `⚠` |
| Conduta limpa anual | Sem flags · 12 meses | green `✓` |

---

## 6. Cross-system

`cross-INC` (credencial) · `cross-NUEL` · `cross-NUIT` · `cross-AT` · `cross-CIP` · `cross-PGR` · `cross-CNPDP` (auditoria de credencial) · `cross-Terras` · `cross-Contratação Pública`

---

## 7. Edge cases

- **Jornalista freelancer sem empregador** → credencial INC pessoal · NUIT próprio · acesso idêntico a empregado
- **Jornalista estrangeiro de órgão internacional** → acordo bilateral SADC · credencial via embaixada
- **Investigação com fonte protegida** → NUITs de fontes não entram no sistema · jornalista declara separadamente · CNPDP não tem acesso
- **Reportagem retirada por pressão judicial** → fica registado como "retirada por sentença" · hash original mantém-se · réplica do visado anexa-se mas não substitui
- **Publicação fora de Moçambique** → link permanente apontará para URL externa · hash mantém-se · CNPDP regista mas não regula

---

## 8. Personas/empresas fictícias

| Persona | Papel |
|---|---|
| Joana Mahique Cossa | Jornalista protagonista · 8 anos Savana |
| Savana | Jornal real-fictício (nome real, peças fictícias) |
| MediaCoop | Editora ficcional do Savana |
| Dr. Mucavele | Director Savana · revisão jurídica |
| Eng. A. Nhantumbo | Alvo da investigação principal |
| Dra. Cremilda Sitole | Alvo investigação secundária (magistrada) |
| Manuel Tembe Sumane | Alvo investigação terciária (antigo governador) |

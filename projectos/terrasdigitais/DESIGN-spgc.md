# DESIGN-spgc.md — SPGC · Admin provincial

**Status:** v0.3 · Abril 2026
**Surface:** 3 de 5
**Persona principal:** Eng. F. Macuácua · Chefe SPGC Manica · 28 funcionários

---

## 1. Propósito

Web admin desktop para os 11 SPGC provinciais (Serviços Provinciais de Geografia e Cadastro) — a camada operacional que faz o cadastro funcionar de facto. Cada SPGC gere milhares de DUATs, recebe centenas de pedidos por trimestre, supervisiona dezenas de fiscais de campo, e arbitra conflitos.

Cobre:

- Dashboard com KPIs provinciais
- Fila de pedidos pendentes (ordenada por prazo)
- Conflitos e sobreposições · resolução por cessão
- Auditoria de qualidade de fiscais
- Mapa cadastral provincial choropleth
- Tribunal Comunitário · processos em mediação
- Caducidade · DUATs com taxa em atraso

---

## 2. Princípios

### 2.1 Pareceres em paralelo
SPGC orquestra pareceres concorrentes (ANAC, CPI, CFJP, fiscal de campo) sem os bloquear em série. Reduz prazos.

### 2.2 Cessão é o caminho preferido para conflitos
62% dos conflitos resolvem-se por cessão negociada (compensação ou troca de terra). SPGC supervisiona para garantir não-coercitividade. Tribunal Administrativo é último recurso.

### 2.3 Caducidade como mecanismo activo
Terra acumulada por especuladores absentees é o calcanhar de Aquiles do sistema. SPGC tem dever activo de extinguir DUATs com 365+ dias de taxa em atraso. Terra extinta volta ao banco do Estado.

### 2.4 Auditoria é constante
8% de amostragem aleatória das demarcações é re-medida. Fiscais com erro &gt; 8 cm sistemático são re-formados ou suspensos.

### 2.5 Cross-province quando útil
Fiscal de uma província pode trabalhar pontualmente noutra (ex: J. Sumane Tembe é Sofala mas opera em Manica). Sistema permite e regista.

---

## 3. Cenas (7)

| # | Cena                          | Componentes                                          |
| - | ----------------------------- | ---------------------------------------------------- |
| 1 | Dashboard SPGC                | sidebar com counters · 4 KPIs · prioridades + stock  |
| 2 | Fila de pedidos pendentes     | filtros badge · tabela 8 colunas com cross-tags      |
| 3 | Conflito · resolução por cessão | 2 polígonos sobrepostos · 3 caminhos · CFJP card    |
| 4 | Auditoria fiscais             | KPIs · tabela qualidade · case detail flagged        |
| 5 | Mapa cadastral provincial     | choropleth 12 distritos Manica · stats por distrito  |
| 6 | Tribunal comunitário          | 14 processos · estados resolução · limites           |
| 7 | Caducidade · 8 DUATs          | tabela atrasos · stepper 7 passos · redistribuição   |

---

## 4. Componentes signature usados

- **Sidebar com counters** (Cena 1) — única do pacote · padrão admin
- **Tabela com filtro-badges** (Cena 2) — pattern reuse-friendly
- **Conflito com 2 polígonos + sobreposição** (Cena 3) — versão grande do componente da empresa
- **Choropleth provincial** (Cena 5) — Manica esquemático, 12 distritos
- **Stepper 7 passos vertical** (Cena 7) — caducidade

---

## 5. Cross-system

| Cena | Cross                            |
| ---- | -------------------------------- |
| 1    | múltiplos · resumo dashboard     |
| 2    | `cross-CPI` `cross-ANAC` `cross-CFJP` `cross-NUSS` |
| 3    | `cross-TJ` `cross-CFJP`          |
| 4    | interno · auditoria              |
| 5    | `cross-ANAC` (zonas conservação) |
| 6    | `cross-CFJP` `cross-TJ Adm`      |
| 7    | `cross-AT` (taxas) · `cross-eBI` (sucessão) |

---

## 6. Personas

| Pessoa                 | Papel                                |
| ---------------------- | ------------------------------------ |
| Eng. F. Macuácua       | Chefe SPGC Manica                    |
| Eng. P. Cossa          | Director Geral DINAGECA (referência) |
| J. Sumane Tembe        | Fiscal estrela · Sofala (cross-prov) |
| J. Macuácua            | Fiscal flagged · Tambara             |
| Juiz J. Cossa          | Tribunal Comunitário Báruè           |
| Régulo Mahique         | Autoridade tradicional (reaparece)   |

---

## 7. Edge cases

- **DUAT herdado mas titular falecido sem herdeiros** → caducidade após 24 meses, terra ao Estado
- **Empresa em insolvência** → administrador judicial assume gestão temporária
- **Conflito tripartido** (3+ partes) → tribunal comunitário aglomera, não trata em série
- **Fiscal flagged 3 vezes** → suspensão automática · investigação interna SPGC
- **Sobreposição entre províncias** → SPGC origem coordena com SPGC vizinho

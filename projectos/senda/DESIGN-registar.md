# DESIGN-registar.md — Surface 5 · Registar institucional

**Persona principal:** Maria Cumbe · Registar UEM · 18 anos na instituição
**Persona secundária:** Ana Cristina Tembe · diplomada Eng. Informática 2025
**Forma:** Desktop frame (todas as cenas) — vista institucional
**Foco temporal:** ciclo completo Ana Cristina · 2021 (matrícula) → 2025 (diploma)
**Total cenas:** 7

---

## 1. Propósito

Mostrar o **operador institucional** · não o cidadão. SENDA não é só para o aluno · é também para a Registar. Maria gere 18 412 alunos · 28 cursos · 14 diplomas para emitir hoje. A interface dela é diferente da interface de Pedro · mas ambas correm no mesmo SENDA.

Esta surface segue **um caso de ciclo completo** · 4 anos comprimidos:
- 2021 · Maria matricula Ana
- 2022-2024 · 3 anos de cadeiras · Maria audita
- 2025 · Maria audita 240 ECTS · pede emissão de diploma · diploma sai

---

## 2. 7 cenas

| # | Título | Momento institucional |
|---|---|---|
| 1 | Painel da Registar · 30.04.2026 | Vista diária · 14 diplomas hoje · Ana destacada |
| 2 | Matrícula 1.º ano · Setembro 2021 | Ana entra · 4 segundos · pré-preenchido |
| 3 | Lançamento de notas · semestre 2025 | Folha de notas · prof. Pedro Cossa · Compiladores |
| 4 | Auditoria de grau · 4.º ano | 240 ECTS · todas verificadas · pré-requisitos OK |
| 5 | Diploma · workflow 5 passos · 22h | Standard nacional · pedido → publicação |
| 6 | Diploma emitido · 15.06.2025 | Componente signature 6 em peso · fac-símile |
| 7 | Maria fala · 18 anos · pull quote | Vivência institucional · antes vs depois |

---

## 3. Componente signature 6 · `.diploma-fac-simile`

A peça mais elaborada visualmente do SENDA. Réplica fiel de um diploma físico:
- Fundo papel-marfim · `linear-gradient(135deg, #fdfcf7 0%, #f9f6ef 100%)`
- Borda azul-deep 2px
- Watermark "SENDA" diagonal (rotate -12deg) · letterspacing 0.4em · opacity 0.05
- Header institucional · logo UEM · "Universidade Eduardo Mondlane · Fundada 1962"
- Título bilingue PT/EN · "Diploma de Licenciatura · Undergraduate Degree Diploma"
- Bloco legal do Reitor · bilingue
- Nome do estudante em Lora 28pt
- Curso em Lora 20pt · bilingue
- 2 assinaturas (Reitor + Registadora)
- Footer com data, label SENDA, QR placeholder, DOC ID

**Princípio:** o diploma digital deve parecer **ao mesmo tempo solene como o físico E moderno como o digital**. Lora dá a solenidade · QR + DOC ID dão a modernidade.

---

## 4. Workflow de emissão · 5 passos · 22 horas (Cena 5)

| Passo | Tempo médio | Quem | O que |
|---|---|---|---|
| 1 | 1 min | Maria | Pede emissão · auditoria positiva |
| 2 | 2 seg | Sistema | Gera DOC ID · cross-AT NUIT |
| 3 | 18 h | Reitor + Registadora | Assinaturas digitais eGov-MZ |
| 4 | 4 seg | Sistema | PDF bilingue · QR · watermark |
| 5 | imediato | Sistema | Publica · email · cross-Trabalho notificado |

Antes do SENDA · 30-90 dias · 800 MT custo. Hoje · 22 horas · 0 MT.

---

## 5. Auditoria de grau (Cena 4)

Maria pode ver de uma vez:
- 1.º ano · 60 ECTS · 11 cadeiras · todas ✓
- 2.º ano · 60 ECTS · 10 cadeiras · todas ✓
- 3.º ano · 60 ECTS · 10 cadeiras + estágio cross-Trabalho ✓
- 4.º ano · 60 ECTS · 9 cadeiras + tese 18,5 ✓
- **Total · 240/240 · média 16,8**

7 pré-requisitos validados automaticamente: 240 ECTS · obrigatórias · estágio · tese · mensalidades · sem disputas · sem plágio.

Antes · 14 dias · auditoria manual · risco de erro.

---

## 6. Cross-systems

cross-Vida Civil · cross-eBI · cross-AT · cross-INSS · cross-Trabalho · cross-Justiça · cross-Sociedade Aberta · cross-Educação Digital (notas anteriores).

---

## 7. Pull quote · Maria · 18 anos institucional

Cena 7 termina com Maria. Conta:
- Comecei em 2007 · 14 anos com papel
- Inundação 2009 destruiu arquivo · 4 218 processos perdidos
- Levou 2 anos a reconstituir
- "Eu olho para esta jovem que vai apanhar o diploma · e sei que ela nunca vai precisar de me ligar daqui a 10 anos a pedir uma cópia"
- "Acompanhar pessoas · não administrar papel"

Estatística complementar: 28 412 diplomas emitidos por Maria em 18 anos · 4 218 perdidos por inundação 2009 · 0 perdidos pós-SENDA.

---

## 8. Edge cases mencionados

- Falsificação histórica · funcionário público com diploma falso (caso 2025)
- Diploma fac-símile mantém-se mesmo para cerimónia presencial · papel + digital coexistem
- Cerimónia presencial 21.06.2025 · momento ritual preservado · só infra-estrutura mudou

---

## 9. Personas

- **Maria Cumbe** · Registar UEM · 44 anos · 18 anos na instituição · narradora
- **Ana Cristina Tembe** · diplomada · Eng. Informática · 2025 · 240 ECTS · média 16,8
- **Domingos António Chissano** · mencionado · Eng. Civil aguarda tese
- **João Manjate** · mencionado · Direito · próximo da fila
- **Prof. Pedro Cossa** · docente · Compiladores · lança notas
- **Prof. Dr. António José Cumbe** · Reitor · assina diplomas
- **Dra. Maria da Graça Mondlane** · Registadora geral · co-assina

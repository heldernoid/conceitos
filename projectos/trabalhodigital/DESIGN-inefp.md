# DESIGN-inefp.md — Surface 5 · INEFP / Emprego e Formação Profissional

**Status:** v0.3 · Abril 2026
**Form factor:** Web (cidadão + admin · responsive). Cidadão view designed mobile-first; admin desktop.
**Primary users:** Cidadãos procurando vaga ou curso (lado público); funcionários do INEFP gerindo cursos, certificações, programas (lado admin); empregadores que oferecem vagas ou aceitam estagiários.
**Setting:** Sede do INEFP em Maputo, delegações provinciais, centros de formação. Plataforma pública 24/7.

---

## 1. Product purpose

INEFP existe para emparelhar oferta e procura no mercado laboral moçambicano e qualificar a força de trabalho. Antes desta superfície, vagas eram afixadas em paredes, cursos eram conhecidos por boca-a-boca, e certificações eram em papel. Esta superfície expõe vagas, cursos, programas, e certificações em plataforma única — gratuita, não-comissionada, integrada com Trabalhador e Empregador.

Three priority use-cases:

1. **Cidadão procura emprego ou curso.** Pesquisar por sector, distrito, qualificação, prazo. Inscrever-se em vaga (cross-Empregador) ou curso. Sem comissão, sem affiliate.
2. **INEFP gere cursos e certificações.** Abrir turma, gerir candidatos, conceder certificações OIT/SADC, registar conclusão.
3. **Empregador anuncia vaga ou aceita estagiário.** Programa Jovem-Trabalhador (subsídio 30%), Estágio Profissional, Reabilitação Profissional.

Deliberately *not*: not a CV builder with templates, not a "rate this employer" tool, not a paid premium tier, not algorithmic matching that hides candidates with low scores.

---

## 2. Information architecture

```
Cidadão (público · sem login para pesquisar)
└─ Vagas
   ├─ Pesquisar (sector · distrito · qualificação)
   ├─ Vagas em destaque
   ├─ Vagas no meu sector (se logado)
   └─ Detalhe vaga (descrição · candidatar)
└─ Cursos
   ├─ Catálogo (12 áreas · 184 cursos)
   ├─ Próximas turmas
   ├─ Inscrever-se (cross-Trabalhador)
   └─ Os meus cursos (se logado)
└─ Certificações
   ├─ As minhas certificações
   └─ Validar certificação (público · QR)
└─ Programas
   ├─ Jovem-Trabalhador (18-35)
   ├─ Estágio Profissional (recém-formados)
   ├─ Reabilitação Profissional (deficiência)
   └─ Auto-emprego e micro-crédito formação

INEFP admin
└─ Painel
   ├─ Vagas activas · candidatos · ocupações
   ├─ Cursos abertos · turmas · conclusão
   └─ KPIs nacionais
└─ Gerir cursos
   ├─ Catálogo
   ├─ Abrir turma
   └─ Atribuir formadores
└─ Certificar
   ├─ Aprovar conclusão (cross-formador)
   ├─ Lavrar certificado · selo brass
   └─ Notificar Trabalhador app
└─ Programas
   ├─ Aprovar candidaturas (Jovem-Trabalhador, etc.)
   ├─ Subsídios (cross-INSS · cross-SISTAFE)
   └─ Monitoria
└─ Estatísticas públicas
   └─ dados.trabalho.gov.mz
```

---

## 3. Critical flows

### F1 — Cidadão home · pesquisar vaga
- Sem login obrigatório
- Filtros: sector, distrito, qualificação mínima, prazo
- Resultado: lista de vagas activas
- Vaga em destaque (cross-Empregador): publicada por Construtora MZ Lda, Padaria Cuamba, etc.

### F2 — Cidadão pesquisar curso
- Catálogo por área (12 áreas: construção, mineração, agricultura, pescas, comércio, serviços, indústria, doméstico, sector público, informal, tecnologias, gestão)
- Próximas turmas com vagas restantes
- Inscrever-se requer login (cross-Trabalhador via NUSS/BI)

### F3 — Inscrever-se em curso · cross-Trabalhador
- Pré-requisitos verificados automaticamente
- Match com perfil (sector actual, formação prévia)
- Confirmação · entra na turma
- Notificação na Trabalhador app

### F4 — Empregador publicar vaga
- Cross-Empregador app
- Salário, sector, qualificação, tipo de contracto
- Validar antes de publicar (sem promessas vagas, sem discriminação)
- Vaga visível em 24h

### F5 — INEFP aprovar conclusão de curso · lavrar certificado
- Formador submete avaliação
- Sistema gera certificado serifado (Plex Serif · selo brass)
- Notifica trabalhador via app
- Adiciona à carteira do trabalhador

### F6 — Programa Jovem-Trabalhador · subsídio
- Empregador contrata jovem 18-35 anos
- Recebe subsídio de 30% do salário durante 6 meses (cross-INSS · cross-SISTAFE)
- Compromisso: manter vínculo por 18 meses pós-subsídio

### F7 — Estatísticas públicas
- dados.trabalho.gov.mz: salário médio por sector, taxa de empregabilidade pós-curso, vagas em aberto
- Anonimizado, agregado, sem identificações pessoais

---

## 4. Components & patterns

| Component | INEFP |
|---|---|
| Public hero | Para cidadão · pesquisa proeminente |
| Vaga card | Empregador · sector · salário · prazo |
| Curso card | Área · formador · vagas restantes |
| Programa banner | Jovem-Trabalhador · destaque |
| Auto / certificado serifado | Selo brass · QR validação |
| Admin painel | Side rail orange-900 |

---

## 5. Critical UI states

### 5.1 Vaga em destaque
*"Construtora MZ Lda procura: 4 pedreiros 1.ª classe · 22 000 MZN/mês · sem termo. Apresentar até 14 Mai."*

### 5.2 Curso com poucas vagas
*"Soldadura industrial · 6 semanas · INEFP Maputo · grátis. Restam 8 / 24 vagas. Inscrever-me →"*

### 5.3 Certificado emitido
*"Manuel Sitole concluiu Cofragens Industriais. Certificado CERT-2024-INEFP-148218 · selado · QR validação · adicionado à Carteira."*

### 5.4 Programa Jovem-Trabalhador
*"Tens 28 anos · primeiro emprego formal há < 2 anos. Empresa que te contrata recebe subsídio 30% por 6 meses. Vê vagas Jovem-Trabalhador →"*

### 5.5 Validar certificado público
*"Certificado válido · CERT-2024-INEFP-148218 · Manuel Sitole · Cofragens Industriais · 3 semanas · 4 Nov 2024."*

---

## 6. Cross-system

INEFP lê de:
- **eBI · Governo** — identidade
- **Trabalhador app** — perfil, sector, formação prévia
- **Empregador app** — vagas publicadas, programa Jovem-Trabalhador
- **INSS** — para verificar elegibilidade (programa requer NUSS)

INEFP escreve a:
- **Trabalhador app** — inscrições, certificados, vagas correspondentes
- **Empregador app** — candidatos, conclusões de formação
- **INSS** — confirmação de cursos (relevante para subsídio doença pós-formação)
- **SISTAFE** — pagamento de subsídios programa
- **dados.trabalho.gov.mz** — agregados públicos

---

## 7. Open questions for v0.4

- Reconhecimento de qualificações estrangeiras (SADC reciprocity)
- Trabalhadores migrantes intra-SADC (acordo de mobilidade laboral)
- Cursos online · validação de presença remota
- Microformação modular · stackable credentials
- Acessibilidade física dos centros de formação para pessoas com deficiência

---

*Authoritative for INEFP. DESIGN-system.md wins on conflict.*

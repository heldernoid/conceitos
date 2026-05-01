# DESIGN-candidatura.md — Surface 3 · Candidatura nacional

**Persona:** Pedro Manjate Sumane · 18 anos · candidato 2027/2028
**Forma:** Desktop frame (wizard) + browser de cursos
**Modelo conceptual:** antagning.se / CNAES / Studielink
**Total cenas:** 7

---

## 1. Propósito

Demonstrar a **eliminação radical de fricção** no acesso ao ensino superior. Antes de SENDA · candidato pagava 4 emolumentos a 4 universidades · fazia 4 exames diferentes · podia ser admitido em todas e ter que escolher · pagava propinas em duplicado · processo caótico.

Em SENDA · **uma candidatura · 8 preferências · 1 exame nacional · 1 colocação automática · 0 MT**.

Esta surface é a maior do SENDA (712 linhas) porque tem:
- 4 passos do wizard
- Browser de cursos com filtros
- Score calculator
- Probabilidades de colocação
- Calendário do processo
- Paralelo nacional

---

## 2. 7 cenas

| # | Título | Etapa do wizard |
|---|---|---|
| 1 | Início · perfil · 12.ª concluída | Pré-wizard · perfil já verificado |
| 2 | Browser de cursos · 218 cursos | Pré-wizard · pesquisa e descoberta |
| 3 | Passo 1 · Verificação | Identidade + académico + 3 declarações |
| 4 | Passo 2 · Preferências (8 stack) | Drag-and-drop · cores por elegibilidade |
| 5 | Passo 3 · Exame nacional | Convocatória · 4 provas · local atribuído |
| 6 | Passo 4 · Revisão final | Resumo · botão definitivo |
| 7 | Submissão · 218 412 candidatos | Algoritmo público · paralelo nacional |

---

## 3. Componentes signature usados

- `.programa-card` · cards de cursos com 3 elegibilidades (qualificado verde · condicional amarelo · não vermelho)
- `.preferencias-stack` · 8 cards com num-pref colorido por estado
- `.score-calculator` (cena de probabilidades)
- Wizard bar custom (4 passos · active/done/upcoming)

---

## 4. Modelo de elegibilidade

| Estado | Cor | Significado |
|---|---|---|
| Qualificado | Verde | Score acima do corte 2026 · alta probabilidade |
| Condicional | Amarelo | Score próximo do corte · pode entrar se outros desistirem |
| Não-qualificado | Vermelho | Score abaixo do corte · improvável · safety net necessária |

Sistema **não impede** candidatura condicional ou não-qualificada · mostra com transparência. Cidadão decide.

---

## 5. Cross-systems

cross-Educação Digital (notas 12.ª pré-preenchidas) · cross-Vida Civil · cross-Terras (mesa de exame próxima) · cross-Justiça (disputas) · cross-Sociedade Aberta (algoritmo público).

---

## 6. Algoritmo de matching · público

Determinístico · publicado em `github.com/senda-mz/match-algorithm`:

```
for cada candidato in ordem(score_DESC):
  for pref in candidato.preferencias:
    if curso.vagas > 0 and candidato.score >= curso.cutoff:
      colocar(candidato, curso)
      curso.vagas -= 1
      break
  else:
    candidato.estado = "sem colocação"
```

Pesquisador pode replicar · jornalista pode validar · cidadão pode auditar. **Nenhum algoritmo de Estado deveria ser caixa preta.**

---

## 7. Edge cases mencionados

- Não-colocados (desenvolvido em Surface 4 · Cena 5)
- Disputas de score (cross-Justiça · 14 dias)
- Algoritmo redo se erro detectado
- 2.ª chance Janeiro 2028 · vagas remanescentes

---

## 8. Personas

- **Pedro Manjate Sumane** · candidato · 18 anos · 1.ª preferência Eng. Inf. UEM
- **Felisberto Manjate** · pai · pull quote final · "candidatei-me em 2007 · pagou emolumentos"

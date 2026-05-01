# DESIGN-registos.md — Surface 5 · Registos Públicos · DNRN

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1280+ floor) for conservadores e notários. Mobile responsive subset for cidadão consult.
**Primary users:** Conservadores do Registo Civil, Comercial, Predial. Notários. OAM. Funcionários do DNRN. Cidadãos consultando situação de empresa, imóvel ou pessoa.
**Setting:** 128 conservatórias e cartórios notariais espalhados pelo país. Trabalho diário de emissão, escrituração e autenticação.

---

## 1. Product purpose

Direcção Nacional dos Registos e Notariado (DNRN) administra os três grandes registos públicos moçambicanos:

- **Registo Civil** — nascimento, casamento, óbito (~5,8 M registos vivos)
- **Registo Comercial** — empresas, alterações estatutárias (~218 k empresas)
- **Registo Predial** — imóveis, escrituras, hipotecas (~684 k inscrições)

Esta superfície unifica os três fluxos sob uma identidade visual única e cruza com os outros sistemas. Antes desta superfície, cada registo tinha sistema separado, formulários distintos, prazos opacos.

Three priority use-cases:

1. **Emitir certidão** — pedida via Cidadão app, processada e selada aqui.
2. **Lavrar escritura pública** — notário no cartório, com partes presentes, com selo brass + QR.
3. **Registar empresa nova** — cross-system com Finanças (NUIT) e DUAT (Predial se há sede).

Deliberadamente *não*: não é cartório online (escrituras requerem presença física por lei), não é fórum, não é affiliate de notários.

---

## 2. Information architecture

```
Painel Conservador (interno)
├─ Pedidos de certidão (fila)
├─ Escrituras agendadas
├─ Registos pendentes (empresa, casamento, óbito)
└─ Estatísticas

Acto · escolher tipo
├─ Certidão (Civil · Comercial · Predial · Negativa)
├─ Escritura pública (notário)
├─ Registo novo (nascimento · casamento · óbito · empresa · imóvel)
├─ Anular acto registado
└─ Autenticação de documento

Detalhe · acto
├─ Pré-visualização serif
├─ Partes (ou requerente)
├─ Documentos anexos
├─ Selo brass + QR de validação
└─ Cross-system com Cidadão / Finanças / Cadastro
```

---

## 3. Critical flows

### F1 — Painel conservador
Lista pedidos de certidão · escrituras agendadas · alertas. Drª. Rosa Sumbane (conservadora) abre a sua fila do dia.

### F2 — Emitir certidão
- Cidadão pediu certidão de nascimento via Cidadão app (cena 4 do cidadao.html)
- Conservadora valida assento, assina digitalmente, sela com brass
- PDF entregue na Carteira do cidadão em < 5 minutos

### F3 — Escritura pública (notário)
- Partes presentes no cartório (compra-e-venda de imóvel)
- Notário verifica BIs, NUITs, certidões prediais (cross-Cadastro), pagamento SISA (cross-Finanças)
- Lavra escritura serifada
- Partes assinam (digital · pegada digital se não souber escrever)
- Notário lavra o selo brass

### F4 — Registar empresa nova
- Cross-Finanças: NUIT pré-atribuído
- Cross-Cadastro: DUAT da sede (se há imóvel)
- Estatutos anexados
- Sócios identificados (cross-eBI)
- Registo Comercial concluído em 24h se documentação completa

### F5 — Anular escritura registada
- Apenas com sentença transitada em julgado
- Two-step + OTP + número de processo + justificação

### F6 — Autenticar documento
- Cidadão / advogado / empresa traz documento para autenticação
- Notário valida autoria, sela com brass + QR
- Documento autenticado é equivalente a documento público

### F7 — Directório de notários OAM
Pesquisa por bairro, especialidade, língua. Sem rating, sem comissão.

---

## 4. Components & patterns

| Component | Registos |
|---|---|
| Conservatória panel | Slate · com filtros por tipo de acto |
| Acta serifada | Para certidões e escrituras |
| Selo brass "Carimbada DNRN" | Em todo acto registado |
| QR validação | Em todo PDF emitido |
| Cross-system badges | "Cross-Finanças · NUIT", "Cross-Cadastro · DUAT" |
| Two-step modal | Anulação, rectificação |

---

## 5. Critical UI states

### 5.1 Certidão pedida via app
*"3 pedidos de certidão na sua fila. Próximo: certidão de nascimento de M. Cuamba (BI 110100442918), pago via SISTAFE há 4 minutos."*

### 5.2 Escritura · partes incompletas
*"Falta presença de uma das partes (vendedor T. Massingue) para lavrar escritura. Reagendar?"*

### 5.3 Empresa · NUIT pendente
*"NUIT solicitado a Finanças Digitais há 8 minutos. Aguarda emissão (≤ 1h) antes de concluir registo comercial."*

### 5.4 SISA por pagar
*"Compra-e-venda suspende-se: SISA de 248 000 MZN não paga. SISTAFE notificado. Pague antes de lavrar escritura."*

### 5.5 Anulação por sentença
*"Sentença transitada em julgado · P-2024-COM-MAP-00284 · ordena rectificação. Requer two-step + OTP."*

---

## 6. Cross-system

Registos lê de:
- **eBI · Governo Digital** — identidade das partes
- **Finanças Digitais** — NUIT, SISA, certidão fiscal
- **Cadastro Predial** — DUAT, planta, conflitos
- **Portal MJCR** — sentenças que ordenam rectificação ou anulação
- **Cidadão / Justiça** — pedidos de certidão

Registos escreve a:
- **Cidadão / Justiça** — certidões na Carteira
- **Cadastro Predial** — escrituras associadas a DUATs
- **Finanças Digitais** — eventos tributáveis (compra-e-venda gera SISA)
- **dados.justica.gov.mz** — agregados (tempo médio, certidões emitidas)

---

## 7. Open questions for v0.4

- Apostille Haia · escrituras para uso no estrangeiro
- Reconhecimento de assinatura digital qualificada (conformidade UE/SADC)
- Print stylesheet · cartórios continuam a imprimir originais
- Auditoria automática · cruzar Predial e Cadastro mensalmente

---

*Authoritative for Registos Públicos. DESIGN-system.md wins on conflict.*

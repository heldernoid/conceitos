# DESIGN-cidadao.md — Cidadão · App móvel

**Status:** v0.3 · Abril 2026
**Surface:** 1 de 5
**Persona principal:** Felisberto Manjate · 38 anos · Maxixe · 2 DUATs (residencial + machamba)

---

## 1. Propósito

A app móvel do titular cidadão. Cobre tudo o que um proprietário de DUAT precisa de fazer sem ir a um SPGC físico:

- Ver os seus DUATs e respectivos polígonos
- Pagar a taxa anual via M-Pesa
- Iniciar transmissão por sucessão
- Denunciar ocupação ilegal do seu terreno
- Reclamar boa fé histórica (Lei 19/97 art. 12)
- Validar autenticidade do título por QR

Não cobre (deliberadamente):

- Pedido novo de DUAT (vai para Surface Empresa, mesmo para empresário individual)
- Subdivisão para venda (não existe — DUAT não se vende)
- Negociação cara-a-cara — qualquer disputa escala para Cena 6

---

## 2. Princípios

### 2.1 Linguagem
- **Nunca** "vender", "comprar", "minha propriedade".
- **Sempre** "DUAT", "transmitir por sucessão", "ceder direitos de uso".
- A constitucionalidade (terra é do Estado) não é negociável e a UI reflecte isto.

### 2.2 Anonimato em denúncias
Ocupações ilegais em MZ envolvem frequentemente actores com poder local. Sem garantia de anonimato, a maioria dos cidadãos não denunciaria. A app garante-o por design.

### 2.3 Boa fé histórica é central
O artigo 12 da Lei 19/97 reconhece direito a quem ocupa terra há &gt; 10 anos. Milhões de famílias rurais beneficiam disto. A Cena 7 trata o tema com a centralidade que merece — **não é uma feature secundária**.

### 2.4 5 línguas + USSD
PT-MZ é o default mas Macua, Changana, Sena e Nyungwe têm paridade total. USSD `*146*1#` para feature phones onde não há dados móveis.

### 2.5 eBI sempre
Sem identidade digital, sem app. Não há cadastro paralelo de utilizadores. `cross-eBI` aparece visível em cada operação sensível.

---

## 3. Cenas (7)

| # | Cena                          | Componentes-chave                                   |
| - | ----------------------------- | --------------------------------------------------- |
| 1 | Login eBI · 5 línguas + USSD  | langtoggle · OTP SMS · USSD fallback                |
| 2 | O meu DUAT · home             | duat-card hero · banner amber taxa · row-cards      |
| 3 | Detalhe + polígono            | poly-frame · vertex-tbl · duat-doc serifado · timeline |
| 4 | Pagar taxa M-Pesa             | composição taxa · 3 métodos · cross-AT              |
| 5 | Transmissão por sucessão      | stepper 5 passos · acta notarial · cross-eBI por herdeiro |
| 6 | Denúncia ocupação             | poly-frame com sobreposição · foto+EXIF · anonimato |
| 7 | Boa fé histórica · Lei 19/97  | critérios auto-validados · 2 testemunhos · régulo · ha-meter |

---

## 4. Componentes signature usados

- **DUAT-card hero** (Cenas 2, 3) — gradient ocre→savana, mini-mapa inset, selo brass
- **Polígono GPS frame** (Cenas 3, 6) — vertex-tbl, sobreposição vermelha em conflito
- **DUAT serifado mini** (Cena 3) — versão compacta para mobile
- **Hectare meter** (Cena 7) — visual de área proposta
- **Stepper 5 passos** (Cena 5) — fluxo de sucessão
- **Cross-tags visíveis** — `cross-eBI`, `cross-AT`, `cross-fiscal`, `cross-TJ`, `cross-CFJP`

---

## 5. Cross-system interop

| Cena | Cross dispara                       | Pacote irmão           |
| ---- | ----------------------------------- | ---------------------- |
| 1    | `cross-eBI` · validação BI + OTP    | Governo Digital        |
| 2    | `cross-AT` · verificar taxa paga    | Finanças Digitais      |
| 4    | `cross-AT` · pagamento confirmação  | Finanças Digitais      |
| 5    | `cross-eBI` · biometria por herdeiro| Governo Digital        |
| 5    | `cross-fiscal` · se subdivisão      | Surface Fiscal (interno) |
| 6    | `cross-fiscal` · 14 dias verificação| Surface Fiscal         |
| 6    | `cross-TJ` · escalada se conflito   | Justiça Digital        |
| 7    | `cross-CFJP` · validação régulo SMS | Justiça Digital        |
| 7    | `cross-fiscal` · visita 30 dias     | Surface Fiscal         |

---

## 6. Estados de cada DUAT (recap)

- `vigente` (verde) — taxa em dia, sem disputa
- `pedido` (amber) — em processo de emissão (boa fé, sucessão, novo)
- `conflito` (vermelho) — sobreposição ou denúncia activa
- `caducado` (cinza) — &gt; 365 dias de taxa em atraso ou explicitamente extinto

A app mostra cada DUAT com a sua pílula correspondente.

---

## 7. Edge cases tratados

- **DUAT herdado mas não registado** → Cena 5 + Cena 7 combinadas (sucessão sob boa fé)
- **Ocupação por familiar** → Cena 6 com flag de "conflito familiar" → tribunal comunitário primeiro
- **Taxa atrasada &gt; 90 dias** → app entra em modo banner vermelho, oferece plano de pagamento
- **BI caducado** → bloqueia tudo, deep-link para Governo Digital
- **Sem rede** → cache local de polígono e título serifado · queue de pagamentos pendentes
- **Régulo sem telefone** → Cena 7 fallback: assinatura física em formulário PDF, fiscal recolhe in-situ

---

## 8. Personas convencionadas (cross-package consistency)

| Pessoa                   | Papel nesta surface          | Cross-refs            |
| ------------------------ | ---------------------------- | --------------------- |
| Felisberto Manjate       | titular principal · BI 110100442918 | aparece também em SPGC e Fiscal |
| João Mahique Tembe       | de cuius (Cena 5)            | titular falecido      |
| Júlia Sumane Tembe       | herdeira + fiscal Sofala (cross-pacote) | reaparece em Fiscal como funcionária |

---

## 9. Open questions

- USSD: profundidade real do menu (3 níveis? 5?) precisa validação com utilizadores rurais.
- Boa fé: 2 testemunhos é o mínimo legal, mas em zonas de migração massiva pode não bastar — possível requerer 3 ou parecer comunitário formal.
- Subdivisão por sucessão: fiscal cobra deslocação? actualmente o protótipo assume gratuita por lei.

# DESIGN-system.md — Transportes Digitais

**Status:** v0.3 · Abril 2026
**Ownership:** DTrD · Direcção de Transportes Digitais (sob MTC)
**Stakeholders:** MTC, INATTER, ANE, CFM, Portos de Moçambique, PRM-Trânsito, Aduanas (ATM)

---

## 1. Sector & purpose

Transportes Digitais cobre o ciclo completo de pessoas, viaturas e cargas a moverem-se em Moçambique:

- **Rodoviário** — emissão de cartas, registo de viaturas, IPO, IUC, multas, fiscalização
- **Transporte público** — chapas, machibombos, táxis · alvarás, rotas, tarifas
- **Multimodal** — Porto Maputo / Beira / Nacala · CFM (Caminhos de Ferro de Moçambique) · 6 fronteiras-chave

O sistema substitui:
- Cartões de carta plastificados perdidos a cada 2-3 anos
- Filas no INATTER (3-5 dias para registo de viatura)
- Multas em livro carbonado, frequentemente perdidas
- Manifestos de carga em papel nas fronteiras
- Falta de visibilidade entre PRM-Trânsito e INATTER

E inaugura:
- Carta de condução digital (cross-eBI) com QR validável
- Registo automóvel com cross-NUIT do proprietário
- Multas com pagamento M-Pesa em 30 dias · contestação em 60 dias
- Manifestos digitais cross-Aduanas em fronteira
- Fiscalização integrada com câmaras de velocidade e álcool em tempo real

---

## 2. Brand foundations

### 2.1 Cobalt road-sign blue
Cor de autoridade rodoviária. A mesma família do azul das placas de auto-estrada. Comunica oficialidade, segurança, profissionalismo. Diferencia-se intencionalmente do navy do Governo Digital — é mais saturado, mais "estrada" do que "ministério".

```
--cobalt-900: #0F2A52   (govstrip · driver-card hero)
--cobalt-800: #163A6E
--cobalt-700: #1E4A8C   (PRIMARY · botões · selo)
--cobalt-600: #2A5DA8
--cobalt-500: #4577C2
--cobalt-300: #93B2DA
--cobalt-200: #B9CDE5
--cobalt-100: #DCE7F3   (badges · backgrounds claros)
--cobalt-50:  #EEF3FA   (canvas elevations)
```

### 2.2 Asphalt charcoal (co-anchor 1)
Para PRM-Trânsito · estrada · matrículas · sinaléctica. Asfalto.

```
--asphalt-900: #0E1116   (matrícula border · texto enfático)
--asphalt-700: #2A2E33
--asphalt-500: #4A4F57
--asphalt-300: #8B8F96
--asphalt-100: #DCDEE2
```

### 2.3 Amber sign yellow (co-anchor 2)
Para avisos · cuidado · IPO a vencer · multa pendente · cunho da matrícula MZ. **Não para PRM-Trânsito hi-vis.**

```
--amber-500: #D69E1A   (avisos · star da matrícula)
--amber-700: #8C5F00
--amber-100: #F8EBC3
```

### 2.4 Hi-vis (PRM-Trânsito accessório)
Reservado para o uniforme da PRM em campo · auto de notícia banner · selo da PRM. **NÃO entra no sistema regular.** Aparece só nas superfícies da Polícia.

```
--hivis-yellow: #FFEC1F
--hivis-black: #0E1116
```

### 2.5 Cool road-grey canvas
`#F4F6F9` — fundo neutro frio, ligeiramente azulado para harmonia com cobalt. Diferencia-se do creme do Trabalho (que era warm) e do off-white de Saúde.

---

## 3. Modos de transporte (8 chips fechados)

Sistema de chips para identificar tipo de viatura em qualquer superfície. Cores escolhidas para serem distintas em mapas e tabelas.

| Modo | Cor | Uso |
|---|---|---|
| `.mode.ligeiro` | Cobalt #2A5DA8 | Automóvel particular (até 9 lugares) |
| `.mode.pesado` | Brown #5C3A24 | Camião · pesado de mercadorias |
| `.mode.passageiro` | Green #0E7A4D | Machibombo · pesado de passageiros |
| `.mode.chapa` | Red #C73E2E | Chapa-100 · semicolectivo (15-25 lugares) |
| `.mode.taxi` | Amber #D69E1A | Táxi · ligeiro de aluguer |
| `.mode.moto` | Purple #7A4A8C | Motociclo · ciclomotor |
| `.mode.ferrov` | Steel #62697A | Ferroviário (CFM) |
| `.mode.marit` | Teal #0E5C6B | Marítimo / fluvial (Porto · ferry) |

Os chips são fechados — qualquer nova categoria precisa entrar nesta lista, não inventar inline.

---

## 4. Type system

**Plex Sans** — UI normal (mesma do Trabalho/Saúde para consistência da família Conceitos)
**Plex Mono** — matrículas, números de carta, NUIT, identificadores, valores monetários, GPS
**Plex Serif** — Carta de condução, livrete, autos da PRM, certificados oficiais. Comunica autoridade documental.

Hierarquia:
- `t-h1` 28 px — page hero
- `t-h2` 22 px — section heading
- `t-h3` 18 px — subsection
- `t-body` 14 px — paragraphs
- `t-meta` 12 px — captions, timestamps

---

## 5. Identifiers (formats)

Cada superfície usa estes formatos consistentemente:

- **Carta de condução**: `CD-2026-MAP-018421` (cross-eBI BI source)
- **Matrícula MZ**: `AAA 123 MP` (3 letras + 3 dígitos + 2 letras província)
  - MP = Maputo Cidade · MZ = Maputo Província · BR = Beira · NP = Nampula · TT = Tete · etc.
- **Livrete (registo)**: `LV-2026-MP-148218`
- **NUIT do proprietário**: `400 184 218` (cross-Finanças)
- **Auto PRM**: `AT-2026-MAP-04218` (auto de trânsito)
- **Multa**: `M-2026-04218 / NIM-2026-MAP-08412`
- **IPO** (Inspecção Periódica Obrigatória): `IPO-2026-MP-018421`
- **Alvará TP** (transporte público): `AT-2026-CHAPA-04218`
- **Carga / manifesto**: `MF-2026-PMA-014218` (PMA = Porto Maputo)

---

## 6. Components catalogue

### 6.1 Plate (matrícula MZ)
Componente icónico. Bordo preto, fundo branco gradiente, número monoespaçado. Tira azul-cobalt à esquerda com estrela amber + sigla "MZ".

```html
<span class="plate">
  <span class="country">MZ</span>
  <span class="num">AAA 482 MP</span>
</span>
```

Tamanhos: `.sm` (badge inline), default (cards), `.lg` (hero).

### 6.2 Driver card
Carta de condução em forma de hero card. Gradiente cobalt-900 → cobalt-700, número CD em mono, foto stub à direita. QR para validação pública.

### 6.3 Licence (carta de condução serifada)
Documento serifado completo. Header gradiente cobalt, body em Plex Serif, footer com selo "DTrD-MTC" rotacionado -4°. Mostrado quando o cidadão expande a carta ou quando a PRM scaneia.

### 6.4 Auto de Notícia (PRM-Trânsito)
Auto serifado clássico. Header opcional com hi-vis stripe (8px amarelo-preto). Selo brass cobalt OU hi-vis (amarelo + preto). Sempre Plex Serif no body.

### 6.5 Mode chips
Os 8 chips de modo de transporte. Sem combinações — cada viatura é exactamente UM modo.

### 6.6 Speedometer
Para PRM-Trânsito · radar de velocidade. Arco semi-circular com gradiente verde→amber→vermelho. Valor central em mono 28 px.

### 6.7 Risk meter
Para condutores e empresas (frota): low / med / high / critical. Reutiliza o componente do Trabalho.

### 6.8 Phone frame & Tablet frame
Phone 360×720 (Condutor) · Tablet 980×680 (PRM-Trânsito). Iguais aos do Trabalho.

---

## 7. Cross-system contracts

| Sistema | Lê de | Escreve para |
|---|---|---|
| **Governo Digital · eBI** | Identidade do condutor | — |
| **Saúde Digital · NUS** | Tipo sanguíneo (carta) · cross-feridos sinistro | — |
| **Finanças · NUIT/SISTAFE** | NUIT proprietário · IUC · pagamentos multa | IPO/IUC/multas a cobrar |
| **Trabalho · NUSS** | Motoristas profissionais (cross-alvará) · INSS chapas | — |
| **Justiça · TJ Administrativo** | — | Multas não pagas → execução fiscal |
| **Aduanas · ATM** | Importação de viaturas (livrete novo) · manifesto carga | Validação na fronteira |

Cada cross-action tem um badge cobalt visível na UI: `Cross-eBI · ✓`, `Cross-Finanças · IUC`, etc.

---

## 8. Languages (5 langs · Condutor app)

Mesma família do Trabalho:
- **Português MZ** (default)
- **Macua** (norte · Nampula, Cabo Delgado, parte de Niassa)
- **Changana** (sul · Maputo, Gaza, Inhambane)
- **Sena** (centro · Sofala, Manica, Tete)
- **Nyungwe** (Tete fluvial · Cahora Bassa)

Toggle no topo do app. Strings críticas (auto de notícia, valores, prazos) sempre também em PT-MZ ao lado do localizado.

USSD `*146#` low-tech fallback para consultas básicas (carta vigente · multa pendente · IPO).

---

## 9. Hi-vis usage rules (strict)

Hi-vis amarelo-preto é signature da PRM-Trânsito.

- ✅ Auto de notícia · header opcional
- ✅ Selo de auto da PRM (alternativa ao selo cobalt)
- ✅ Banner de inspecção em campo (PRM-Trânsito tablet)
- ✅ Marker do inspector no mapa
- ❌ Driver card · livrete · matrícula
- ❌ Botões CTA
- ❌ Backgrounds genéricos
- ❌ INATTER admin (que usa cobalt institucional)

Se a hi-vis aparece, é porque há fiscalização activa.

---

## 10. Open questions for v0.4

- Carta SADC reciprocity (BLNS — Botswana, Lesotho, Namíbia, Swazi)
- Importação paralela de viaturas (Japão · cross-Aduanas)
- Veículos eléctricos (categoria nova de IPO/IUC)
- Drone cargo (futuro · ainda sem regulamentação)
- ANE manutenção rodoviária (interface com utentes)
- Acessibilidade (cartas para condutores surdos · semáforos sonoros)

---

*Authoritative for Transportes Digitais. Wins on conflict with surface-specific docs.*

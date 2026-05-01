# DESIGN-cidadao.md — Surface 2 · Cidadão em risco

**Status:** v0.3 · Surface 2 de 7
**Persona protagonista:** Felisberto Manjate · cidadão · Maxixe, Inhambane (continuidade família 10 pacotes)
**Forma:** phone mockup · 360px · GSM intermitente · 3G/4G

---

## 1. Propósito

Como o cidadão comum recebe alertas, prepara família, evacua e regressa. Não é o operador profissional · é a pessoa de quem o sistema cuida. Esta surface valida que toda a infra-estrutura técnica das outras superfícies se traduz em vivência cidadã digna · sem fricção.

Família Manjate Sumane · 4 pessoas · 1 bebé (Lara) · 1 idosa (Filomena, 64a, sogra). Composição diversa · cada caso especial.

---

## 2. Princípios

1. **Phone simples sempre** · 360px · não tablet · cidadão usa o que tem
2. **Linguagem directa** · imperativos curtos · "Vá para o abrigo X agora"
3. **Linguagem inclusiva** · 4 línguas · PT · Macua · Sena · Changana
4. **3 níveis de antecipação** · L1 informativo · L2 prepare · L3 evacue
5. **Família dimensiona tudo** · Lara dimensiona kit · Filomena dimensiona medicação
6. **Sem pânico** · cores quentes mas controladas · frases declarativas

---

## 3. Cenas (7)

| # | Título | Cenário |
|---|---|---|
| 01 | SMS de alerta · 04:42 | L2 chega · família ainda em casa · 36h até landfall |
| 02 | Plano familiar | App mostra 4 pessoas · pontos de encontro · contacto Júlia em Beira |
| 03 | Kit de emergência | Checklist personalizado · Lara leite · Filomena medicação · animais |
| 04 | Alerta sobe para L3 · evacuar | 14h depois · evacuar para Escola 25 de Junho · 600m |
| 05 | Em abrigo · 19:08 | Registado em 4 minutos · cross-eBI · sala 04 · medicação distribuída |
| 06 | Contactar família | GSM intermitente · mensagem prioritária via INGD para Júlia |
| 07 | Pedido de socorro · vizinho | Sr. Macuácua, 78a, idoso isolado · não atende · SAR mobiliza |

---

## 4. Componentes signature usados

- `.alerta-pulsante` (Cenas 1, 4) · L2 e L3 · pulsação visual aumenta com gravidade
- `.kit-emergencia` (Cena 3) · 9 itens dimensionados pela família
- `.abrigo-card` (Cena 5) · estado do abrigo onde Felisberto está

---

## 5. Cross-system

- `cross-Vida Civil` · família 4 pessoas conhecida · plano dimensionado
- `cross-Saúde` · medicação Filomena pré-aprovada · cartão SIS-MA
- `cross-INGD` · canal prioritário GSM em catástrofe
- `cross-Trabalho` · ausência justificada · empregador notificado
- `cross-CFJP` · régulo confirma vizinhança Sr. Macuácua
- `cross-eBI` · registo no abrigo em 4 minutos
- `cross-MTN/Vodacom/Tmcel` · alertas SMS multi-rede

---

## 6. Edge cases

- **Lara · 5 meses** · necessidades especiais · leite em pó · prioridade absoluta no abrigo
- **Filomena · 64a** · medicação diária crónica · stock 7 dias garantido
- **Animais · 2 cabras + 14 galinhas** · vizinho Domingos cuida (acordo prévio)
- **Sr. Macuácua · 78a · isolado** · prioridade SAR · não tem app, não atende telemóvel
- **GSM intermitente pós-landfall** · canal prioritário INGD para 3 mensagens/pessoa/dia
- **Linguagem** · alertas em PT mas crítico em Macua/Sena/Changana se zona requer

---

## 7. Personas referenciadas

- **Felisberto Manjate** · protagonista (continuidade 10 pacotes)
- **Joana Sumane** · esposa · enfermeira (sabe 1.º socorros)
- **Lara Manjate Sumane** · 5 meses · cross-Vida Civil
- **Filomena Cossa Tembe** · 64a · sogra · cross-Saúde
- **Júlia Sumane Tembe** · irmã da Joana · Beira (contacto fora da zona) · Vida Civil + Terras
- **Padre Manuel Cossa** · coordenador abrigo Escola 25 de Junho
- **Sr. Macuácua** · vizinho idoso isolado · 78a · cross-CFJP confirma
- **Domingos** · vizinho · cuida dos animais
- **Dr. Pedro Cossa** · médico · referenciado em farmácia móvel

---

## 8. Open questions

- App em **modo offline completo** · em 2024 ainda muitas zonas sem cobertura · sincroniza quando há rede?
- **Aviso por sirene** em zonas críticas costeiras · paralelo ao SMS · responsabilidade de quem?
- **Pessoas sem telemóvel** · ainda 22% rurais · alerta via régulo + rádio
- **Família dispersa** · pais em Maxixe + filhos em Maputo a estudar · 2 alertas distintos?
- **Animais grandes** (gado bovino) · não cabe em abrigos · perde-se sempre?

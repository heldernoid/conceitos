# DESIGN-mesa.md — Surface 4 · Mesa de voto · Aurélio

**Status:** v0.4 · Surface 4 de 7
**Persona protagonista:** Aurélio Tembe · 67a · prof. reformado · presidente Mesa 0142 Maxixe · 5.ª eleição
**Forma:** tablet rugged STED · 12" · IP67 · 18h bateria · GSM + WiFi

---

## 1. Propósito

Onde a tecnologia toca o cidadão. Dia eleitoral · 14.10.2029 · Mesa 0142 · Aurélio preside · 13 horas em pé · 418 cidadãos · 14 casos especiais · 0 incidências graves · acta 100% match com OCI. **O sistema é tecnológico · mas a confiança é humana.**

Esta surface valida que toda a infra-estrutura funciona no momento decisivo · com pessoas reais · em pé · com pressa · com humanidade.

---

## 2. Princípios

1. **Tablet rugged · não phone** · 12" para tabelas grandes · IP67 contra chuva
2. **cross-eBI primeiro** · BI scaneado em 2 segundos
3. **Boletim físico em papel** · pilar · auditável sem electricidade
4. **4 camadas anti-fraude** · biometria · NUEL único · lock nacional · tinta indelével
5. **Casos especiais com humanidade** · cego · cadeira de rodas · sem documento · 1.ª vez
6. **Acta com 7 assinaturas** · presidente + escrutinadores + secretário + MININT + 2 OCI
7. **Cofre lacrado · 5 anos** · boletins físicos para auditoria futura

---

## 3. Cenas (7)

| # | Título | Cenário |
|---|---|---|
| 01 | Abertura · 06:00 · 4 selos | Aurélio · checklist abertura · equipa presente |
| 02 | Eleitor chega · família Manjate · 09:14 | 4 passos · BI → biometria → boletim → urna |
| 03 | BI scaneado · cross-eBI · 1,8s | Verificação 4 pontos · biometria + lock nacional |
| 04 | Vota em papel · cabine · urna · tinta | 2 minutos · boletim fac-símile · marcação UC |
| 05 | Casos especiais · 14 ao longo do dia | Cega braille · cadeira rodas · BI roubado · 1.º voto Pedro |
| 06 | Acta de contagem · 19:42 · 412 votos | Resultado mesa · 7 assinaturas · hash |
| 07 | Encerramento · 19:00 · 100% participação | Pull quote Aurélio · 67a · 5.ª eleição |

---

## 4. Componentes signature usados

- `.caderno-publico` (Cena 3) · estado activo
- `.boletim-fac-simile` (Cena 4) · marcado em UC
- `.contagem-publica` (Cena 6) · resultado mesa
- `.verificacao-cruzada` (Cena 3) · 4 pontos

---

## 5. Cross-system

- `cross-eBI` · validação 2 segundos
- `cross-Vida Civil` · vivacidade última verificação
- `cross-Saúde` · acessibilidade · braille · cadeira rodas
- `cross-MININT` · ordem · não interfere · neutralidade
- `cross-OCI` · 2 observadores presentes · contagem paralela
- `cross-CNPDP` · privacidade na validação · logs auditáveis
- `cross-TES` · contestações escaláveis (BI roubado · voto excepcional)

---

## 6. Edge cases · 14 casos reais

- **Cega · braille** · 16 boletins braille pré-impressos · acompanhante respeita privacidade
- **Cadeira de rodas** · rampa obrigatória desde 2014 · cabine adaptada
- **BI roubado ontem** · escala cross-eBI · biometria + foto · voto excepcional
- **D. Hortência · 1.ª vez resolvida** · estava no caderno após contestação
- **Pedro · 1.º voto · trémulo** · Aurélio dá calma · momento simbólico
- **Eleitor de outra mesa por engano** · redirecionado · mesa correcta a 2 km
- **Gestante a parir hoje** · mesa móvel hospitalar
- **2 estrangeiros que pensaram poder votar** · não podem · explicado cordialmente
- **Menor que tentou votar** · 17a · cordial recusa
- **Idosa que não sabe ler** · acompanhante fiscal MININT · imparcialidade
- **Tinta indelével falhou em 1 lote** · substituído em 30 min · sem voto duplo
- **+3 outros casos simples**

Total · 14 casos · 0 cidadãos saíram sem votar (excepto não-elegíveis).

---

## 7. Personas referenciadas

- **Aurélio Tembe** · protagonista · presidente Mesa 0142 · 67a · 5.ª eleição
- **Felisberto Manjate** + Joana + Pedro · família votando junta · momento simbólico
- **Joaquim Cossa** · 1.º escrutinador · cred. 2024
- **Mariana Macuácua** · 2.ª escrutinadora
- **Lucinda Mussa** · secretária · regista actas
- **Cabo Sumane** · MININT · ordem
- **Joana Mahique Cossa** + Anastácio Mussa · 2 observadores OCI
- **D. Margarida Tembe** · 78a · cega · braille
- **Sr. Macuácua** · 84a · cadeira de rodas
- **Sr. Cossa** · BI roubado ontem
- **D. Hortência Macuácua** · caso resolvido · 1.ª vez

---

## 8. Open questions

- **Mesa móvel hospitalar** · viável em hospitais grandes? Quem credencia?
- **Tinta indelével · alternativas tecnológicas** (digital ink) · ainda não fiável?
- **Voto presidencial separado de legislativo** · 2 boletins · 2 cabines · 2 actas?
- **Subsídio mesa 4200 MT** · suficiente para 13 horas? Aurélio é prof. reformado · outros?
- **Recrutamento equipa de mesa** · voluntário · sorteio · profissional?

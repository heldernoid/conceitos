# DESIGN-multimodal.md — Surface 5 · Multimodal · Portos · CFM · Fronteiras

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1440+ floor) · cross-stakeholder
**Primary users:** Operadores de Porto (Maputo · Beira · Nacala) · CFM (Caminhos de Ferro de Moçambique) · Aduanas (ATM) · INATTER · transitários · agentes de fronteira (PRM Imigração + Migração + ATM) · staff de logística

---

## 1. Product purpose

A superfície que cose o transporte multimodal moçambicano: marítimo + ferroviário + rodoviário + aéreo. Antes desta camada, mover um contentor do Porto de Maputo até Tete via Beira era uma cadeia de papéis fragmentada: BL marítimo, manifesto rodoviário, carta de porte CFM, declaração aduaneira em cada modo. Esta superfície substitui:

- Manifestos de carga em papel multiplicados por modo
- Sem cross-Aduanas até à fronteira final
- CFM sem visibilidade do porto
- 6 fronteiras críticas operando em silos
- Atrasos de 2-5 dias em transbordo Porto→Comboio

E inaugura:
- Manifesto digital único · cobre toda a viagem multimodal
- Cross-Aduanas em tempo real em cada ponto
- Visibilidade fim-a-fim para o transitário e cliente final
- Dashboard nacional · 3 portos + CFM + 6 fronteiras
- Pré-clearance fronteira via app antes da chegada

---

## 2. Stakeholders & responsibilities

| Entidade | Responsabilidade | Acesso |
|---|---|---|
| **Portos de Moçambique · CFM-Sul** | Operação Porto Maputo | Manifestos · contentores · navios |
| **Cornelder Moçambique** | Operação Porto Beira (concessão) | Manifestos · contentores · navios |
| **Northern Development Corridor** | Operação Porto Nacala (concessão) | Manifestos · contentores · navios |
| **CFM** | Ferrovia Linha Norte · Centro · Sul · Linha Sena · Linha Machipanda | Composições · cargas · horários |
| **ATM · Aduanas** | Desalfandegamento em todos os pontos | Read/write em todas as superfícies |
| **PRM Imigração + Migração** | Pessoas em fronteira | 6 fronteiras-chave |
| **INATTER** | Viaturas que importem ou exportem | Read |
| **MTC** | Tutela política | Read · relatórios mensais |

---

## 3. Information architecture

```
Sign in (functional + 2FA, RBAC por entidade)
└─ Dashboard nacional
   ├─ Mapa operacional (3 portos + CFM linhas + 6 fronteiras)
   ├─ KPIs (TEUs · toneladas · viaturas · pessoas)
   ├─ Backlog atual (esperas em cada ponto)
   └─ Alertas (atrasos · inspeções pendentes · greve · maré)
└─ Portos
   ├─ Maputo (TEUs · navios atracados · backlog)
   ├─ Beira (TEUs · navios · linhas Sena)
   ├─ Nacala (TEUs · navios · linha Norte)
   └─ Operação · pátio · gruas
└─ CFM
   ├─ Linha Sul (Maputo - Ressano Garcia · Komatipoort)
   ├─ Linha Centro (Beira - Machipanda - Harare)
   ├─ Linha Sena (Beira - Tete · carvão)
   ├─ Linha Norte (Nacala - Cuamba - Lichinga · Malawi)
   ├─ Composições activas
   └─ Calendarização
└─ Fronteiras (6 chave)
   ├─ Ressano Garcia (RSA · M4) — 38% volume rodoviário
   ├─ Lebombo (RSA · turística)
   ├─ Machipanda (Zimbabué · Manica)
   ├─ Mussina (não operacional)
   ├─ Mandimba (Malawi · Niassa)
   ├─ Negomano (Tanzânia · Cabo Delgado)
   ├─ Pessoas + cargas
   └─ Pré-clearance app
└─ Manifestos
   ├─ Em curso (todos os modos)
   ├─ Pendentes inspecção Aduanas
   ├─ Encerrados
   └─ Histórico
└─ Transitários
   ├─ Lista (482 transitários activos)
   ├─ Avaliação
   └─ Auditoria
```

---

## 4. Critical flows

### F1 — Dashboard nacional
Mapa operacional. Porto Maputo: 14 navios · 8 412 TEUs · backlog 2 dias. Beira 6 navios · 4 218 TEUs. Nacala 4 navios · 2 184 TEUs. CFM com 18 composições activas. 6 fronteiras com tempos médios de espera.

### F2 — Manifesto multimodal · Maputo → Tete via Beira
- Contentor MZ-2026-PMA-018421 chegou em navio
- Operador transitário cria manifesto: Porto Maputo → camião → Beira → CFM Sena → Moatize/Tete
- Cross-Aduanas pré-aprova · trânsito interno aduaneiro
- Cada ponto sela e passa
- Cliente final em Tete vê tracking em tempo real

### F3 — Pré-clearance fronteira Ressano Garcia
- Camião com produtos manufacturados sai de Joanesburgo
- Transitário declara via app antes da chegada
- Aduanas pré-aprova · paga IVA + direitos via SISTAFE
- Camião chega · QR scan na portaria · libertação em 8 minutos (vs 2-4 horas)

### F4 — CFM Linha Sena · carvão Moatize → Beira
- Composição CFM-2026-SEN-04218 · 84 vagões · 6 720 toneladas carvão
- Vale Moçambique (mineradora · concessionária) submete carga
- Cross-Aduanas (operação interna · sem desalfandegamento)
- CFM aceita · programa horário (3 dias Moatize→Beira)
- Em Beira · transbordo para navio bulk carrier

### F5 — Fronteira pessoas · Negomano (Cabo Delgado · Tanzânia)
- Bus de passageiros chega à fronteira
- App PRM Migração faz scan de BIs
- Cross-eBI · cross-saúde · cross-Justiça (mandados)
- Triagem em 2-4 minutos por pessoa · vs 15-20 antes

### F6 — Backlog em Porto Beira · escalada
- Sistema detecta backlog de 5 dias
- Causas: pico sazonal · grua avariada · falta de motoristas
- Director Beira escala ao MTC
- Cross-CFM · pode ferry-boat para Maputo? Cross-Maputo Porto · capacidade?

### F7 — Inspecção Aduanas · suspeita
- Contentor sinalizado por raio-X · suspeita de armas
- ATM e PRM coordenam abertura física
- Cross-Justiça se confirma · processo penal
- Multimodal trava · contentor não passa

---

## 5. Components

| Component | Multimodal |
|---|---|
| Top bar | Multi-stakeholder badge (entidade) |
| Dashboard map | MZ + 3 portos + CFM linhas + 6 fronteiras |
| KPI cards | Por modo · TEUs · toneladas · viaturas |
| Manifesto componente | Auto serifado + selo cobalt |
| TEU/contentor pill | `MZ-2026-PMA-018421` |
| Mode chips | Marit · Ferrov · Pesado |
| Border crossing card | Tempo médio · backlog · pré-clearance |
| Composição CFM | Lista de vagões · operador |
| Cross-Aduanas badge | Em todos os pontos |

---

## 6. Critical UI states

### 6.1 Manifesto em curso
*"Manifesto MF-2026-PMA-014218 · Porto Maputo → Tete via Beira · 3 modos · etapa 2/3 (em comboio Sena)."*

### 6.2 Backlog crítico em porto
*"Beira · backlog 5 dias · 1 grua avariada · pico sazonal carvão. Cross-CFM tem capacidade Linha Sena? Escalar MTC?"*

### 6.3 Pré-clearance pronto
*"Camião KZN-9482 · pré-clearance Aduanas ✓ · pode passar fronteira sem fila."*

### 6.4 Suspeita raio-X
*"Contentor MZ-2026-BRA-018412 · raio-X sinalizou armas. Suspender. ATM + PRM abrir fisicamente."*

### 6.5 CFM atraso
*"CFM-2026-SEN-04218 · 14h atraso · chuva forte Sofala. ETA Beira 3 Mai 11:00 (era 2 Mai 21:00)."*

---

## 7. Cross-system

Multimodal lê de:
- **eBI · Governo** — passageiros em fronteira
- **INATTER** — viaturas a entrar/sair
- **Justiça** — mandados (cross-fronteira)
- **PRM-Trânsito** — autos sobre camiões
- **Saúde** — quarentenas (cross-fronteira)

Multimodal escreve a:
- **Aduanas · ATM** — declarações multi-modais
- **Operador** — atrasos sobre carga
- **Condutor app** — alertas para motoristas em fronteira
- **PRM Imigração** — bulk imports / exports
- **Finanças · SISTAFE** — taxas portuárias · ferroviárias · fronteiriças
- **dados.transportes.gov.mz** — agregados · TEUs · toneladas · cross-fronteira

---

## 8. Border specifics

| Fronteira | País vizinho | Volume típico | Pré-clearance |
|---|---|---|---|
| **Ressano Garcia** | África do Sul (M4 · N4 RSA) | 38% rodoviário · 1 200 cam/dia | ✓ obrigatório camiões |
| **Lebombo** | RSA (turística) | 14% · 80% pessoas | Opcional |
| **Machipanda** | Zimbabué (corredor Beira) | 18% · carga + pessoas | ✓ recomendado |
| **Mandimba** | Malawi (Niassa) | 8% · pessoas + chapa fronteiriça | Em piloto |
| **Negomano** | Tanzânia (Cabo Delgado) | 6% · pessoas + alguma carga | Em piloto |
| **Lichinga (Malawi)** | Malawi (Lago Niassa) | 4% · pessoas · ferry | Manual |

---

*Authoritative for Multimodal. DESIGN-system.md wins on conflict.*

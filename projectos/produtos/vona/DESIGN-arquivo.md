# DESIGN · Surface 5 · Arquivo · privacidade

**Persona** · Manuel Tembe · 52 anos · jornalista de investigação · 18 meses CJC-MZ.
**Hora** · contexto · pesquisa em curso · 14 semanas de investigação.
**Princípios servidos** · 4 (arquivo é território editorial) · 7 (anti-linchamento extendido).

## Por que arquivo precisa de surface dedicada

Material arquivado é o tesouro e o risco de Vona. **Tesouro** · 1 247 testemunhos de violência doméstica permitem ver padrões que publicação individual ocultaria. **Risco** · arquivo grande é alvo · vigilância · pressão. Esta surface mostra como o sistema equilibra acesso editorial responsável com proteção de fontes.

## 7 cenas · estrutura

**Cena 1 · Manuel Tembe · perfil + investigação actual.** "Violência doméstica em Maputo · padrões silenciosos" · 14 semanas · 1 247 testemunhos · 0 vítimas identificadas. O que o arquivo serve.

**Cena 2 · 5 categorias do arquivo.** Privacidade vítima (2 anos) · investigação em curso (project-lifetime) · identificação de menor (5 anos) · conteúdo gráfico extremo (3 anos) · pedido da fonte (à vontade da fonte). Cada uma com regras próprias.

**Cena 3 · pesquisa do Manuel · 240 itens · "violência doméstica · Maputo · 2024-2026".** Interface de pesquisa do arquivo. Thumbnails borradas · metadata genérica. Manuel decide quais abrir · cada abertura registada. Análise agregada · 87 testemunhos em 3 bairros · janela 19h-23h.

**Cena 4 · política de retenção · 2 anos · purga automática.** Cronologia de um item · submissão · indexação · uso · purga prevista. 3 razões para purgar · risco de fuga · direito a esquecer · anti-vigilância. Hash mantido · conteúdo apagado.

**Cena 5 · sigilo de fonte · camadas de identidade.** Tabela quem-vê-o-quê · público vê "fonte cidadã" · sysadmin vê só metadata cifrada · polícia direta nunca · só com mandado caso-a-caso. Cifragem técnica AES-256 + HSM físico.

**Cena 6 · output · Manuel publica peça · 0 vítimas identificadas.** Como se transforma material protegido em jornalismo público. Re-anonimização cruzada · aviso prévio a associações de protecção · aprovação editora-chefe.

**Cena 7 · purga Janeiro 2026 · 412 itens apagados.** Verificação independente · advogada CJC + auditor académico · cidadãos-fontes notificados em massa. Apagar é prática editorial · acto político.

## Decisão crítica · 5 categorias · não 1

Diferentes razões precisam diferentes regras. Whistleblower (categoria 5) tem proteção absoluta. Identificação de menor precisa retenção mais longa para evidência futura. Investigação em curso precisa flexibilidade. Uniformidade seria injusta · ou demasiado restritiva ou demasiado permissiva.

## Decisão crítica · purga obrigatória · não opcional

Sem prazo · arquivo cresce indefinidamente · vira tesouro de Estado quando governo mudar. Prazo curto (2 anos) · forçar disciplina editorial. Prolongamentos possíveis mas com revisão · max 3 vezes.

## Decisão crítica · acesso interno restrito por nível

Manuel tem nível 3 · permite categoria privacidade-vítima e investigação em curso. Não permite categoria 5 (pedido-fonte) ou conteúdo gráfico extremo (precisa nível 4). Cada acesso é registado · cada login é auditável · auditor revê mensalmente padrões anormais.

## Tabela · quem vê identidade da fonte

| Quem | Cândida (publicado) | Categoria 5 (whistleblower) |
|---|---|---|
| Público | "fonte cidadã ★ 4,8" | "fonte protegida" |
| Editores adjuntos | "Cândida S." | nada |
| Beatriz · editora-chefe | nome completo | nada · nem ela |
| Manuel · jornalista | "Cândida S." | nada |
| Advogada CJC · Filomena | nome completo · só legal | nome completo · só legal |
| Sysadmin | metadata cifrada · sem nome | metadata cifrada · sem nome |
| Polícia directa | NUNCA | NUNCA |
| Polícia · com mandado | caso a caso | NUNCA · sigilo absoluto |

## O que NÃO está nesta surface (deliberado)

- Sem "browse archive" público (arquivo não é jornalismo · é matéria-prima)
- Sem download em massa interno (cada item · acesso registado)
- Sem reconhecimento facial mesmo para arquivo (vigilância)
- Sem retenção indefinida (excepto categoria 5 · só fonte decide)
- Sem export para 3rd parties · nem ONGs · nem investigação académica sem auditor

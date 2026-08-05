# Somos Atitude — Estado do Projeto (consolidado)
**Última consolidação: 31/07/2026 (v3 — enriquecimento v2 + msg1 com gancho)**

> Sempre que possível, cheque `FONTES.md` para a versão viva do schema, workflows e site (atualizados automaticamente via GitHub). Este arquivo é o histórico narrativo de decisões e a referência de regras de negócio — o `FONTES.md` é a referência técnica de dados.

---

# PARTE 1 — RESUMO DO ESTADO ATUAL

## 1.1 O que está em produção

| Componente | Status | Observação |
|---|---|---|
| A0 — Busca CNPJá v2 | ✅ Operacional | Sourcing de leads via CNPJá API |
| A1 p1 — Higienização | ✅ Operacional | Validação WhatsApp, matching Google Places |
| A1 p2 — Enriquecimento | ✅ Operacional | Diagnóstico de site/GBP + score determinístico (fn_calcular_score) |
| A2 Disparo v3.2 | ✅ Operacional, 100% automatizado | Disparos manuais descontinuados |
| A2 Resposta (W1+W2) | ✅ Operacional, modo autônomo, **permanece em n8n** | Guardrails + agente de conversa; migração para Zaia SUSPENSA (ver §1.3) |
| W3-A — Motor de Follow-up | ✅ Operacional, validado com envios reais | f1_email, f2_breakup, conversa_parada_auto |
| W3-B — Leitor de Caixa | ❌ Não construído | Respostas por e-mail ao F1 não são capturadas automaticamente ainda |
| Raio-X — Avaliação de Presença | ✅ Skill + anúncio CTWA em produção | Fluxo de avaliação gratuita via anúncio |
| Site somosatitude.com.br | ✅ Publicado, SEO 100/100 | GA4 instalado, portfólio de 6 demos fictícias; preços atualizados em 30/07 |
| Repositório GitHub (atitude-docs) | ✅ Ativo | Schema + 8 workflows-chave sincronizados automaticamente (ver FONTES.md) |

## 1.2 Regras de negócio vigentes (nunca contradizer)

**Catálogo e preços (site = agente, sempre) — vigentes, conferidos contra a tabela `servicos` em 30/07/2026:**

| Produto | Slug | Preço | Prazo | Checkout |
|---|---|---|---|---|
| Criação de Site | `criacao_site` | R$ 599,00 (R$ 419,30 com PRIME30) | até 10 dias úteis após onboarding | `iomwbqf_981774` |
| Redesign de Site | `redesign_site` | idêntico a criacao_site (mesmo produto, mesmo link) | idêntico | idêntico |
| Config. GBP | `config_gbp` | R$ 237,00 | upsell pós-venda do site, não vender antes | `3drni7u_981788` |
| E-book "Nunca Mais Sem Clientes — O Método do Serviço Lucrativo" | `ebook_gestao` | R$ 57,00 | order bump apenas | `4x6a6s9_1008091` |
| E-book GBP na Prática | `ebook_gbp` | R$ 37,00 | order bump apenas | `sfehmrx_981791` |
| Hospedagem | `hospedagem` | R$ 79,00/mês (R$ 55,30/mês com PRIME30, desconto recorrente enquanto o cupom estiver válido para o lead) | recorrente, mencionar só após aceite do site | `bdmw48k_981794` |

- **PRIME30** (30% off): só para leads de prospecção outbound; prazo de 7 dias contado do momento em que o agente apresenta a oferta (nunca do disparo); nunca calculado pelo agente — sempre injetado pronto via `empresas.cupom_expira_em`; mencionado no máximo 1x proativamente; **nunca aparece no site**. Aplica-se a criacao_site/redesign_site E à hospedagem (desconto recorrente).
- Para leads de **origem site**: nenhum cupom é oferecido proativamente; PRIME30 só pode aparecer como facilitador em objeção de preço explícita (intenção objecao_preco), nunca antes, nunca como boas-vindas, nunca se o lead já aceitou o preço cheio.
- **SITE30** (30% off): exclusivo da campanha paga CTWA de criação de site; nunca aplicado a leads de origem site. Cupom de campanha não tem contagem por lead — nunca inventar data de validade.
- Config. GBP nunca é oferecido no primeiro contato — é upsell pós-venda do site. Exceção: lead de anúncio CTWA cujo produto-alvo é config_gbp compra GBP direto, sem recondução para site.
- E-books nunca são oferecidos ativamente pelo agente — só order bump no Cakto. Exceções: lead de anúncio CTWA do próprio e-book (venda direta); e, no ramo MODO AVALIAÇÃO, o ebook_gbp pode ser oferecido como complemento quando o achado do raio-x mencionou Google/GBP.
- Garantia: 7 dias pela Cakto.
- Pedido de desconto além do PRIME30 → sempre escalar para humano.

**Comportamento do agente (princípios inegociáveis):**
1. Soar humano — mensagens curtas, 1 pergunta por vez, espelhar o registro do cliente
2. Nunca inventar preço, prazo ou recurso fora da base
3. Vender ajudando — o diagnóstico é o argumento, não pressão
4. Proteger o chip — delay humano antes de responder, janela de horário, opt-out irrevogável
5. Em dúvida, não responder e escalar para humano

**Domínios do site:** `somosatitude.com.br` (canonical) e `somosatitude.online` recebem cópia idêntica; redirecionamento 301 definitivo está **deliberadamente adiado** até o fim da campanha atual (links já distribuídos com os dois domínios).

### 1.2.1 Histórico de alterações de preço/catálogo

| Data | Alteração | Motivo |
|---|---|---|
| 17/07/2026 (F0) | Catálogo original: site R$ 897 (PRIME30 R$ 627,90), hospedagem R$ 99/mês, e-book "Gestão Financeira para Autônomos" (checkout `rbqeqnj_981805`) | Definição inicial validada na F0 |
| 30/07/2026 | Site R$ 897 → **R$ 599** (PRIME30 R$ 419,30) · Hospedagem R$ 99 → **R$ 79/mês** + PRIME30 recorrente (R$ 55,30) | Ajuste de mercado |
| 30/07/2026 | `ebook_gestao` substituído: "Gestão Financeira para Autônomos" → **"Nunca Mais Sem Clientes — O Método do Serviço Lucrativo"** (checkout `4x6a6s9_1008091`, área de membros com e-book + checklist + planilha; produto antigo desativado no Cakto; tabela `anuncios` conferida — nenhuma referência ao antigo) | Reposicionamento para prestadores de serviço em geral |

**Regra de manutenção:** toda alteração de preço/prazo/garantia/produto exige, no mesmo dia: (1) tabela `servicos` no Supabase, (2) `index.html` nos 2 domínios (texto + JSON-LD FAQPage), (3) cópia do `index.html` no repositório `atitude-docs/site/`, (4) nova linha nesta tabela de histórico com data e motivo.

## 1.3 Migração n8n W2 → Zaia — SUSPENSA (30/07/2026)

A migração das respostas inbound do WhatsApp para a plataforma Zaia foi testada em pilot e **suspensa em 30/07/2026: a plataforma não atendeu às necessidades da operação**. A arquitetura vigente permanece 100% em n8n:

- **`a2-resposta-v3` continua ativo** — todo o inbound (W1 guardrails + W2 agente) segue rodando em n8n/Evolution, em modo autônomo
- W3 Follow-up Engine permanece como está (f1_email, f2_breakup, conversa_parada_auto — nada foi desativado)
- As 3 tarefas n8n pós-migração foram **canceladas** (desativar follow-ups na view do W3, polling da Ticket API, sync de opt-out)
- **Zaia Partners white-label (Path B, R$ 990/mês) suspenso junto** com a migração

**Registro do que foi construído no pilot** (caso a decisão seja revisitada com outra plataforma): BYOK Anthropic, 6 tools consultando o Supabase dinamicamente (catálogo, objeções, dossiê via RPC `buscar_dossie`, tickets, bloqueio, follow-up), Conditional Prompt "Modo Anúncio", classificador v2. Motivos da suspensão incluem instabilidade observada já no setup: configurações de Provider/Model/Temperature resetando entre sessões e erros intermitentes de geração de resposta.

**Aproveitamento fora do Zaia (independente de plataforma):**
- **Classificador v2** — campos `pede_desconto_extra`, `intencoes_secundarias`, `produto_mencionado`, `mensagem_automatica`, `ja_objetou_antes`. Verificado no workflow vivo em 30/07: **nunca foi aplicado ao W2 do n8n** (produção roda a v1). Vira pendência: portar para o W2 (ver §1.4). Valor: move decisões críticas do julgamento do gerador para flags determinísticos — escalonamento de desconto extra e regra "nunca insistir 2x na mesma objeção" deixam de depender da interpretação do Sonnet.
- **Segurança no banco** — chaves `sb_publishable_` e GRANT SELECT de `empresas` restrito a 12 colunas não-PII foram aplicados direto no Supabase e **permanecem como melhoria definitiva**, independente do Zaia.

## 1.4 Pendências ativas (todas as frentes)

| # | Item | Depende de / Prioridade |
|---|---|---|
| 1 | Portar classificador v2 (spec do pilot Zaia) para o W2 do n8n | Prioridade média — melhoria de qualidade, não bloqueante |
| 2 | Subir `index.html` atualizado (preços 30/07) no repositório `atitude-docs/site/` | Rápido — arquivo no repo está com placeholder |
| 3 | Rodar T-RX1 (raio-x) com lead real ponta-a-ponta | Só simulado até agora |
| 4 | Redirecionamento 301 `.online → .com.br` | Fim da campanha atual |
| 5 | Prova social real no site (depoimentos/mockups) | Primeiros clientes pagos |
| 6 | Gravar links de demos em `servicos.link_material` | Decisão pendente |
| 7 | Meta Conversions API | Infra pronta (ctwa_clid + domain verification já no ar) |
| 8 | Micro-SaaS MVP (scheduling + WhatsApp para MEIs de beleza) | Fase de validação com 15-20 clientes existentes |
| 9 | W3-B Leitor de Caixa (Gmail OAuth) | Não construído — respostas por e-mail não são capturadas |
| 10 | Alias `contato@somosatitude.com.br` verificado no Gmail + SPF/DKIM | Retomar se taxa de resposta do F1 vier baixa |
| 11 | Whisper vs Groq (transcrição de áudio) | Decisão adiada, não bloqueia nada |
| 12 | Gap frente a concorrentes no score (8 pts hoje zerados) | Melhoria futura do A1 p2 |
| 13 | Repontuar base após qualquer mudança de peso no score | `select * from fn_recalcular_scores();` |
| 14 | Conferência visual no Gerenciador Meta: nenhum criativo ativo do e-book antigo | Residual da troca do e-book (tabela `anuncios` já conferida — limpa) |

---

# PARTE 2 — HISTÓRICO DETALHADO POR FRENTE

## 2.1 A2 Resposta v3 — Especificação original (16/07/2026)

**Arquitetura em 6 camadas:**
```
Evolution API (webhook messages.upsert)
  → CAMADA 1: Recepção e guardrails (determinístico, código)
  → CAMADA 2: Compreensão (mídia, debounce de rajada)
  → CAMADA 3: Contexto (dossiê do lead)
  → CAMADA 4: Agente (classificador Haiku + gerador Sonnet)
  → CAMADA 5: Ações (responder, atualizar CRM, escalar)
  → CAMADA 6: Motores paralelos (follow-up, alertas, métricas)
```

**Camada 1 — Guardrails (ordem dos filtros):**
1. Grupo (`@g.us`, `@broadcast`) → descarta
2. Mensagem própria (`fromMe`) → descarta
3. Remetente desconhecido → registra em `mensagens_desconhecidas`, alerta humano
4. Opt-out (SAIR/PARE/PARAR/REMOVER/NÃO QUERO) → `opt_out=true`, confirmação única, nunca mais contatado
5. Detector de robô/autoresposta (`bot_suspeito`): 1 sinal forte ou 2 fracos marca; 2ª ocorrência → para de responder, escala humano
6. Rate limit por lead: 6/hora, 15/dia
7. Rate limit global do chip
8. Deduplicação por `evolution_id`
9. Janela de resposta: 07h–21h, todos os dias (decidido na F0: seg-sáb)

**Camada 2 — Mídia:**
- Áudio: transcrição via Whisper ou Groq (decisão adiada, nó plugável); falha → resposta padrão + alerta
- Imagem: Claude com visão; comprovante de pagamento nunca dá baixa automática, sempre escala humano
- Rajada (debounce): buffer de 45s reiniciável, processa como entrada única
- Delay humano: 20-90s antes de enviar + "digitando" via Evolution

**Camada 3 — Dossiê (montado a cada mensagem):**
- Bloco A (quem é): nome, segmento, score, gbp_rating, site_diagnostico, instagram, idade do negócio
- Bloco B (histórico): últimas 20 interações, canal, etapa, roteiro usado
- Bloco C (estado comercial): estagio_conversa, interesse_servicos, negócio aberto, flags de atenção
- Bloco D (agora): mensagem(ns) recebida(s) + hora local

**Camada 4 — Agente:**
- Classificador (Haiku, JSON estrito): interesse_claro, pergunta_produto, pergunta_preco, objecao (6 subtipos), aceite, recusa_educada, opt_out_implicito, pedido_humano, reclamacao, fora_de_contexto, mensagem_automatica, confirmacao_pagamento, duvida_pos_venda
- Gerador (Sonnet): retorna `{resposta, acoes[], confianca}`; confiança <70 → escala para revisão humana
- Regras rígidas: 1-4 linhas, máx 1 pergunta, nunca inventa preço/prazo/link, nunca insiste após recusa, espelha registro do cliente, proibidas palavras-gatilho (grátis, promoção, urgente)

**Bases de conhecimento:**
- Base do cliente = o dossiê
- Base de produtos = tabela `servicos` expandida (descricao_curta, beneficios, preco, faq, link_checkout, quando_ofertar etc.)
- Base de vendas = tabela `objecoes` (subtipo, contexto, abordagem como instrução, exemplo few-shot)

**Metodologia de conversa:** Conexão → Diagnóstico → Valor antes de preço → Prova → Fechamento suave → Pós-aceite

**Follow-up engine (visão original, depois evoluída no W3):**
- F1 D+3 (novo ângulo) → F2 D+7 (break-up) → `perdido_silencio`
- Conversa parada: D+2 retoma do ponto exato
- Pós-checkout: D+1 lembrete, D+3 escala humano

**Estados da conversa (`estagio_conversa`):**
`aguardando_resposta → em_conversa → qualificando → oferta_apresentada → negociando → checkout_enviado → cliente_pago → onboarding` | terminais: `recusado`, `perdido_silencio`, `opt_out`, `atendimento_humano`

**Formulário de onboarding (pós-aceite):** página HTML própria com pré-preenchimento via slug, 5 seções (confirmação de dados, sobre o negócio, identidade visual, GBP específicos, autorização) — grava na tabela `onboarding`.

**Testes de aceite definidos:** T-R1 a T-R12, cobrindo grupo, eco, opt-out, bot, rajada, áudio, desconhecido, aceite, preço sem base, follow-up, rate limit.

**Fases de implantação:** F0 (decisões + patch-07) → F1 (W1+W2 copiloto) → F2 (W3 + autonomia parcial) → F3 (onboarding + checkout real) → F4 (webhook pagamento + alertas) → F5 (desligar piloto antigo).

---

## 2.2 A2 Resposta v3 — Validação F0 (fechada em 17/07/2026)

**As 10 perguntas em aberto foram respondidas:**
1. Checkout: **Cakto**
2. Preços: definidos na F0 e revisados em 30/07/2026 (ver catálogo vigente em §1.2 e histórico em §1.2.1)
3. Como falar preço: valor fechado, nunca faixa
4. Transcrição de áudio: em aberto (não bloqueia)
5. Modo copiloto semana 1: sim, toda resposta aprovada
6. Janela: 07h–21h, segunda a sábado
7. Cadência follow-up: D+3 e D+7
8. Escalonamento: WhatsApp pessoal
9. Formulário: página HTML própria
10. Voz do agente: "Assistente da Atitude", terceira pessoa institucional

Combo "Kit Presença Digital" **não existe** como produto — os e-books entram como order bump nativo do Cakto.

**Regra do cupom PRIME30 (crítica, controle de estado por lead):**
- `empresas.cupom_oferecido_em` gravado no momento exato da 1ª menção
- `empresas.cupom_expira_em` = `cupom_oferecido_em + 7 dias`, calculado em código (n8n), nunca pelo agente
- Mencionado no máximo 1x proativamente; se expirado e o lead volta perguntando, agente não prorroga sozinho — escala (`escalar_humano:oferta_expirada`)

**Regras de oferta por produto:** ver tabela consolidada em §1.2 — a lógica de "quando_ofertar" de cada serviço vem deste documento original.

**Patch-07 (5 partes), todas validadas em produção:**
- 07a: tabela `objecoes` + 6 subtipos
- 07b: tabela `servicos` expandida, 6 produtos completos
- 07c: campos novos em `empresas`/`interacoes` + 4 tabelas novas + `config`
- 07d: views `vw_followups_devidos` e `vw_atencao_humana`
- 07e: prazo de entrega padronizado

**Convenções fixadas:** `interacoes.direcao` = 'entrada'|'saida'; `interacoes.etapa` para entrada = 'resposta_cliente'; `empresas.status='respondeu'` na 1ª entrada, sempre via código, nunca pelo agente.

---

## 2.3 A2 Resposta v3 — Base de objeções (patch-07a, 17/07/2026)

6 subtipos ativos na tabela `objecoes`, todos seguindo o formato `{subtipo, contexto, abordagem (instrução), exemplo (few-shot), ativo}`:

**Regras que valem para todas as objeções:**
- Sempre validar o que o cliente disse antes de contra-argumentar
- 1-4 linhas, máximo 1 pergunta
- Nunca insistir 2x na mesma objeção — na 2ª vez, aceitar com elegância e agendar follow-up ou encerrar
- Facilitadores de preço disponíveis: PRIME30 (se válido), parcelamento Cakto, hospedagem só após entrega

| Subtipo | Gatilho | Abordagem resumida |
|---|---|---|
| `preco` | "Tá caro" | Validar → reancorar na dor_resumida → facilitadores (PRIME30, parcelamento, hospedagem depois). Desconto extra = escalar |
| `tempo` | "Sem tempo agora" | Validar → tirar peso ("trabalho é quase todo nosso") → se persistir, agendar follow-up na data indicada |
| `ja_tenho` | "Já tenho site/Instagram" | Nunca desqualificar → usar site_diagnostico real como espelho → oferecer raio-x |
| `vou_pensar` | "Vou pensar" | Validar sem grude → 1 pergunta aberta pra revelar dúvida real → se mantiver, follow-up D+2 |
| `desconfianca` | "É golpe?" | Validar com sinceridade → provas verificáveis (site oficial, CNPJ, dado real do dossiê, garantia 7d) → se persistir, escalar |
| `nao_decide` | "Preciso falar com sócio" | Respeitar → oferecer resumo encaminhável → perguntar quando decidem → follow-up pós-data |

**Observações de implementação:**
- Exemplos são few-shot (estilo), não templates literais — nunca enviar o texto exato
- Pedido de desconto além do PRIME30 sempre escala — agente não tem alçada de negociação
- Garantia de 7 dias é a configurada no Cakto; se algum produto tiver garantia diferente, ajustar em `servicos.faq`
- Nota (30/07): os valores citados nos exemplos few-shot da tabela `objecoes` podem referenciar o preço antigo (R$ 627,90); os exemplos são de estilo, não de conteúdo literal — mas na próxima revisão da base de objeções, atualizar os números para os vigentes

---

## 2.4 Sistema de Pontuação de Leads — Score Determinístico (patch-08, 21/07/2026)

**Por que mudou:** o score antes era "estimado" pelo Claude Haiku de forma subjetiva, não auditável, não reproduzível. Substituído por função SQL `fn_calcular_score(empresa_id)`, determinística, com detalhamento gravado em `empresas.score_detalhe` (jsonb). Claude segue responsável só pela `dor_resumida` (texto).

**Rubrica — 100 pontos:**
```
FIT DO NEGÓCIO ................. 40 pts
SINAL DE OPORTUNIDADE .......... 40 pts
VIABILIDADE DE CONTATO ......... 20 pts
PENALIDADES .................... negativas
```

- **Fit (40):** nicho (0-15, via `score_nichos`) + ticket potencial (4-15, porte/MEI/rede) + recorrência fixa (10)
- **Oportunidade (40):** site_status (4-20) + prova social/avaliações (0-12) + gap concorrentes (0/8, não coletado ainda)
- **Viabilidade (20):** WhatsApp validado (1-10) + decisor identificável (0-5) + cidade prioritária (0-5, via `score_cidades`)
- **Penalidades:** site ok + nota ≥4.5 (-20) · nota <3.5 com 10+ avaliações (-15) · já recusou (-30) · telefone repetido/contador (-10)

**Faixas de ação (`vw_fila_priorizada`):** 85-100 ataque_imediato · 65-84 alta · 40-64 média · 0-39 baixa.

**Integração:** nó "Calcular Score" no A1 p2, entre "Gravar Enriquecimento" e "Resumo" — todo lead novo sai pontuado automaticamente. Claude não opina mais em score.

**Ciclo de calibragem:** revisar pesos a cada ~20 fechamentos reais; documentar cada ajuste com razão antes de mudar.

**Pendências:** gap frente a concorrentes ainda vale 0 (não implementado); peso do nicho "estética" (8 pts) é chute inicial sem histórico; repontuar toda a base com `fn_recalcular_scores()` sempre que pesos mudarem.

---

## 2.5 Avaliação de Presença Digital — Skill + anúncio CTWA (22/07/2026)

**Skill `avaliacao-presenca` instalada**, fluxo:
- Entrada: nome do negócio + cidade (lead escalado via `escalar_humano:avaliacao_site`)
- Etapa 0: resolve CNPJ nos bastidores (nunca pede ao lead)
- Etapa 1: checklist com evidência (busca local, GBP, site, Instagram, NAP)
- **Etapa 1.5 (obrigatória, bloqueia envio):** conferência manual do Google Maps — busca web não enxerga o Maps
- Etapa 2: síntese 2 pontos fortes + 3 "custando cliente"
- Etapa 3: PDF raio-x 1 página, identidade Atitude, sem preço/oferta
- Etapa 4: mensagem de devolução + ponte suave (pergunta orientada a "não", sem produto)
- Etapa 5: registra interação, `atualizar_estagio:qualificando`, follow-up D+2, SLA 1 dia útil

**Teste real validado:** Concept Clinic (Catalão-GO) — CNPJ resolvido, Maps conferido (5,0★, 173 avaliações), lead ideal para `criacao_site`.

**Anúncio CTWA no ar:** ad_source_id `120256543797570339`, servico_alvo `avaliacao_presenca`, criativo sem CTA de rodapé (botão nativo do anúncio já cobre), descrição "Raio-X gratuito da sua presença digital: veja o que está fazendo você perder clientes."

**Fluxo operacional resumido:** clique no anúncio → agente coleta nome+cidade → escala → alerta 🎯 no WhatsApp pessoal → roda skill → confere Maps → PDF + devolução prontos → envia pelo chip → registra + follow-up D+2.

**Pendências (algumas já resolvidas em sessões posteriores):**
- Teste de aceite do 1º clique real do anúncio
- SLA virou promessa pública — automatizar se o volume crescer
- Regra da ponte suave migra da skill para o prompt quando `escalar_humano` virar ação executável

---

## 2.6 Site somosatitude.com.br — Estado, regras e portfólio (22/07/2026, preços atualizados em 30/07/2026)

**Estrutura publicada:**
```
index.html + og-cover.png + portfolio/ (6 demos fictícias)
```
Publicação sempre nos dois domínios, cópia idêntica, canonical sempre `.com.br`.

**Regras de consistência site ↔ agente (invioláveis):** ver tabela unificada em §1.2. Qualquer mudança de preço/prazo/garantia precisa ser feita em `servicos` (Supabase) E `index.html` no mesmo dia (regra de manutenção completa em §1.2.1). Em 30/07/2026 o `index.html` foi atualizado com os preços vigentes (site R$ 599, hospedagem R$ 79/mês, e-book "Nunca Mais Sem Clientes") no mesmo dia da alteração no banco — regra cumprida.

**PRIME30 nunca aparece no site** — é condicionado por lead, quebraria o controle de estado se publicado.

**Portfólio (6 demos fictícias):** Vitalle Odontologia, Espaço Aura (estética), Almeida & Rocha (advocacia), Movimente (fisioterapia), Ana Beatriz (psicologia), Patas & Cia (veterinária). Todas com: barra "site de demonstração", rodapé "(fictícia)", `noindex`, CTA rastreável para o WhatsApp da empresa. Mapeamento sugerido segmento→demo pendente de gravação no banco (`servicos.link_material`).

**Padrões técnicos mantidos:** title ≤60 chars, meta description 150-160, JSON-LD LocalBusiness + FAQPage, CSS com `prefers-reduced-motion`, `:focus-visible`, `text-wrap: balance`.

**Checklist de publicação:** editar → validar → subir nos 2 domínios → conferir og-cover e portfolio → testar âncora do menu → testar preview WhatsApp → se mudou preço/prazo, atualizar Supabase no mesmo dia → subir cópia do `index.html` no `atitude-docs/site/`.

### 2.6.1 Complemento — GA4 instalado (22/07/2026)

- Propriedade **G-7S2RWDMWM1** no head
- Evento `whatsapp_click` cobrindo os 6 links `wa.me`, com parâmetros `cta` (cta_principal/cta_avaliacao/cta_modelo/outro) e `secao`
- Valores de `cta` espelham as origens do A2 (permite cruzar cliques × leads que chegaram no WhatsApp)
- Demos do portfólio **não têm** a tag GA4 (rastreadas via frase "Vi o modelo de..." no A2)

---

## 2.7 W3 — Follow-up Engine — Design original (24/07/2026)

**Cadência final decidida:** `msg1 WhatsApp (D0) → F1 e-mail (D+3) → F2 break-up WhatsApp (D+7) → perdido_silencio`. Reduzida de 3 toques WhatsApp (F0 original) para 2 WhatsApp + 1 e-mail, para proteger o chip.

**Decisões-chave do brainstorming:**
- Infra de e-mail: Gmail gratuito com "enviar como" `contato@somosatitude.com.br` via SMTP
- Volume: teto de 20 e-mails/dia
- Autonomia: total (diferente do W2, que nasceu copiloto)
- Escopo v1: só disparo frio (conversa parada e pós-checkout ficaram pra v2 — depois antecipado, ver §2.8)
- CTA do e-mail em texto puro, sem hyperlink
- Janela: motor 09h30 seg-sáb, leitor de caixa 17h30 diário

**Componentes desenhados:**
- **W3-A Motor de Follow-up**: lê `vw_followups_devidos` → prioriza e corta pelo teto → monta contexto → gera (Sonnet) → valida → envia → registra → agenda encerramento
- **W3-B Leitor de Caixa**: lê Gmail diariamente, cruza remetente, registra entrada, cancela follow-ups, alerta humano

**Banco (patch-10):** `interacoes.canal`, `empresas.email_followup`/`email_status`, view `vw_followups_devidos` reescrita, `config.followup`, function `fn_encerrar_silencio`.

**Conteúdo das mensagens:** F1 e-mail com assunto curto sem spam-words, abertura referenciando o WhatsApp, corpo consultivo, CTA texto puro, assinatura pessoal "Thyago — Somos Atitude". F2 curto e elegante, nunca repete argumento anterior.

**Pré-requisitos:** SPF/DKIM do domínio, credencial Gmail no n8n, patch-10 aplicado, cota de chip combinada confirmada.

**Testes de aceite definidos:** T-W3-1 a T-W3-8.

---

## 2.8 W3 — Follow-up Engine — Encerramento de implementação (27/07/2026)

Este documento é a **fonte de verdade real** sobre o W3 — várias decisões evoluíram durante a construção em relação ao spec original (§2.7).

**Em produção:** workflow `W3-A — Motor de Follow-up`, 09h30 seg-sáb, processando 3 tipos em ordem de prioridade: `conversa_parada_auto` → `f2_breakup` → `f1_email`. Validado com 15+ e-mails F1, break-ups F2, 4 retomadas de anúncio reais.

**Mudanças em relação ao spec original:**

1. **Cadência F1/F2 mais conservadora**: F2 só é devido quando o lead não tem e-mail utilizável OU quando F1 já foi enviado há ≥2 dias (`f2_apos_f1_dias`). Elimina break-up chegar antes do lead ter chance de responder o e-mail.

2. **Novo tipo `conversa_parada_auto`** (não estava no spec original, implementado a pedido explícito): retomada D+1 para leads de anúncio/site cujo último turno foi `resposta_agente` sem retorno. Prioridade máxima na fila. Gerador simples (não reusa o motor completo do W2) — lê a última mensagem do agente e gera lembrete de 1-3 frases reabrindo exatamente o que ficou pendente.

3. **Idempotência via constraint de banco (crítico)** — motivada por 2 incidentes reais em produção:
   - Envio duplicado (mesmo lead recebeu 2 break-ups no mesmo dia)
   - Registro fantasma (marcado executado sem o envio ter acontecido, porque a ordem antiga era enviar → registrar)
   - Correção: constraints `uq_followup_tipo_unico` e `uq_followup_conversa_parada_auto`; ordem invertida para `Registrar Followup → Enviar → Registrar Interação`

4. **SMTP em vez de Gmail API** para envio (App Password, sem OAuth) — funcionou sem necessidade de OAuth. O Leitor de Caixa (não construído) ainda vai precisar de OAuth para leitura.

5. **Resumo do alerta pessoal** corrigido para contemplar os 3 tipos (antes só somava F1/F2).

**Banco atual (patch-10+10b+10c+11):** backfill de e-mail aplicado a 104/112 leads. `config.followup` com `f2_apos_f1_dias: 2` e `conversa_parada_dias: 1` adicionados. View `vw_followups_devidos` reescrita com 6 ramos: f1_email, f2_breakup, conversa_parada_auto, encerrar_silencio, conversa_parada (manual), pos_checkout.

**Pendência conhecida aceita como backlog:** alias `contato@somosatitude.com.br` ainda não verificado no Gmail — e-mails saem "via gmail.com" tecnicamente, sem SPF do domínio autorizando. Sem risco à entrega até agora; retomar se taxa de resposta do F1 vier baixa.

**Testes de aceite — status real:** T-W3-1 e T-W3-2 validados em produção com casos reais. T-W3-3, T-W3-5, T-W3-6, T-W3-8 ainda não testados com caso real (implementados, aguardando volume/oportunidade). T-W3-4 depende do W3-B (não construído). `conversa_parada_auto` e idempotência: ambos validados com casos reais.

---

## 2.9 Repositório GitHub e automação de documentação (30/07/2026)

Ver `FONTES.md` para os links vivos. Resumo da sessão de criação:

- Repositório `atitude-docs` criado (público, sem segredos)
- Workflow n8n `schema-para-github`: exporta schema do Supabase via função `fn_exportar_schema()`, commita diariamente às 6h
- Workflow n8n `workflows-para-github`: exporta 8 workflows-chave via API do n8n, com mascaramento automático de segredos (chaves Supabase `sb_secret_`/JWT, Evolution API, Anthropic `sk-ant-`, tokens Bearer genéricos), usando arquitetura de **Loop Over Items sequencial** (batchSize=1) para evitar race condition no SHA do GitHub — commita diariamente às 6h15
- Debugging notável: a primeira versão em cadeia HTTP simples sofria de race condition entre items concorrentes disputando o SHA do mesmo arquivo no GitHub; resolvido reestruturando para loop sequencial fechado (Commit GitHub → volta para Loop Over Items)
- `FONTES.md` no Project Knowledge aponta para os 8 workflows individuais + schema + site + status, todos com atualização automática
- O `site/index.html` do repositório é de **atualização manual** — subir a cópia a cada publicação do site (pendência #2 do §1.4 após a alteração de 30/07)

---

## 2.10 Revisão de catálogo, troca do e-book e suspensão do Zaia (30/07/2026)

Sessão de conferência de valores durante a unificação dos documentos do projeto. Três frentes resolvidas:

**a) Divergência de preços detectada e sanada na documentação.** O consolidado anterior ainda registrava os valores da F0 (R$ 897 / R$ 627,90 / hospedagem R$ 99), enquanto banco, workflow em produção e site já praticavam os valores novos (R$ 599 / R$ 419,30 / hospedagem R$ 79 com PRIME30 recorrente R$ 55,30 — ajuste de mercado aplicado em 30/07, com `index.html` atualizado no mesmo dia). Documentação alinhada; histórico formalizado em §1.2.1. Decisão de processo: preços continuam registrados neste arquivo único (sem arquivo separado), com a obrigação de manter o histórico de alterações a cada mudança.

**b) Troca do e-book `ebook_gestao`.** O produto antigo ("Gestão Financeira para Autônomos", checkout `rbqeqnj_981805`) foi substituído pelo novo **"Nunca Mais Sem Clientes — O Método do Serviço Lucrativo"** (checkout `4x6a6s9_1008091`), reposicionado para prestadores de serviço em geral (clínicas, dentistas, psicólogos, salões, oficinas, autônomos). Migração executada e verificada em todas as camadas:
- Cakto: produto novo com área de membros completa (e-book + checklist + planilha, 3 conteúdos publicados); order bump do checkout do site já apontando pro novo; produto antigo desativado
- Banco: `servicos` atualizado (nome, descricao_curta, descricao_completa, beneficios, link_checkout)
- Workflow: nenhuma ação necessária — o A2 monta o catálogo dinamicamente da tabela `servicos`
- Site: card do e-book atualizado no `index.html`, publicado
- Tabela `anuncios`: conferida por query — nenhuma referência ao produto antigo (0 rows)
- Existe um segundo e-book produzido (\"Método Agenda Lucrativa\", segmentado para saúde) que foi descartado por ora — sem pendência associada

**c) Suspensão da migração para o Zaia** — detalhes completos em §1.3. `a2-resposta-v3` permanece como o motor de inbound. Verificação feita no workflow vivo: o classificador v2 desenhado no pilot nunca chegou ao n8n (produção roda v1) — portá-lo virou a pendência #1 do §1.4.

---
# Sessão 31/07/2026 — Enriquecimento v2 + msg1 com gancho (A1 p2 + A2 Disparo)

## Objetivo
Deixar a msg1 mais específica e assertiva: enriquecer o lead com dados que já pagamos
(Places tier Enterprise) ou que custam zero (regex no HTML), e dar ao gerador dois
ângulos de abordagem — gancho positivo verificável + dor — em vez de só a dor.

## O que foi entregue

### Banco (patch-10-enriquecimento-extra.sql)
- Colunas novas em `empresas`: `gancho_abordagem` (text) e `enriquecimento_extra` (jsonb:
  instagram_handle, site_titulo, site_meta_description, site_tem_whatsapp, site_https,
  gbp_fotos_qtd, gbp_tem_horario, gbp_tipo_google, gbp_editorial,
  review_mais_recente_dias, review_destaque {texto, nota, autor})
- `vw_fila_disparo` recriada com as 2 colunas apendadas no fim (vw_fila_priorizada intacta)
- Reset da fila: 73 leads de `fila` → `novo` para re-enriquecimento no modelo novo
  (protegido por NOT EXISTS em interacoes msg1/msg2; disparador estava pausado)

### A1 p2 — Enriquecimento v2 (6 nós alterados)
1. **Places Text Search**: FieldMask + photos, regularOpeningHours, editorialSummary,
   primaryTypeDisplayName (mesmo tier de custo do reviews); maxResultCount 5 → 10
   (custo por request, não por resultado)
2. **Match GBP v5**: reviews 3 → 5 com publishTime; cálculo de review_mais_recente_dias;
   extração de gbp_extra (fotos, horário, tipo, editorial). Fallback nome+cidade
   reescrito: varre TODOS os candidatos (não só places[0]), normaliza acentos,
   exige 2+ palavras significativas OU 1 palavra + bairro conferindo (stopwords
   filtradas), e desempata pelo candidato mais completo em dados (telefone > rating
   > fotos > horário)
3. **Preparar Análise**: extração determinística via regex do HTML bruto —
   instagram_handle (com exclusão de paths de post), title, meta description,
   presença de wa.me, https
4. **Claude Classificar (prompt v3)**: campos novos gancho_abordagem e review_destaque;
   regra 6 com allowlist fechada de fontes (rating>=4.5 + avaliações | review real |
   editorial) e denylist explícita (idade, horário, tipo); max_tokens 700 → 900
5. **Aplicar Classificação**: monta enriquecimento_extra (parte determinística grava
   mesmo se o Claude falhar); **TRAVA DETERMINÍSTICA DO GANCHO** — gancho só é aceito
   se houver fonte real nos dados (rating>=4.5 c/ avaliações, review_destaque válido,
   ou editorial); senão null independente do LLM. Princípio: LLM sugere, código decide.
6. **Resolver Conflito de Place**: limpa também gbp_extra/review_destaque/gancho do
   enriquecimento_extra ao desvincular um place conflitante
## 2.11 Painel de prospecção — correções e blindagem do funil (05/08/2026)

Sessão longa de manutenção disparada por um pedido simples ("o painel
quebrou") que acabou revelando uma cadeia de bugs relacionados —
todos com a mesma raiz: campos/colunas que existiam mas não eram lidos
corretamente, ou regras de negócio que existiam em um lugar (banco) mas
não eram aplicadas em outro (painel, motor de follow-up). Registrado
aqui porque o padrão de causa-raiz se repetiu 6 vezes na mesma sessão
e vale a lição para o futuro: **sempre que um número parecer errado,
suspeitar primeiro de origem/agregação/coluna morta antes de suspeitar
de lógica**.

### a) Painel HTML quebrado (GRANT por coluna)

O fix de segurança de 30/07 (GRANT SELECT restrito a 12 colunas
não-PII em `empresas`) quebrou o `painel-prospeccao.html`, que fazia
`empresas?select=*` — PostgREST exige grant em TODAS as colunas para
`select=*`. Corrigido com `vw_painel_empresas`, view dedicada com
grant total para `anon`, sem PII. Painel também ganhou fallback
adaptativo (tenta a view → tenta select=* → cai numa lista explícita
de colunas, removendo qualquer coluna sem grant automaticamente) para
não quebrar de novo se o schema mudar sem avisar.

### b) Métricas com taxa de resposta acima de 100% (causa tripla)

`vw_metricas_diarias` mostrava taxas de resposta de até 429%. Três
causas empilhadas, todas corrigidas:
1. **Misturava origem** — "respostas" somava conversas de anúncio/site
   junto com prospecção fria, mas "disparos" só existe no funil frio.
   Corrigido: `vw_metricas_diarias` agora filtra `origem='cnpja'` nos
   dois lados; nova view `vw_metricas_anuncio_diaria` cobre o inbound
   separadamente (sem "taxa de resposta" — não faz sentido nesse funil).
2. **Contava mensagem, não lead** — um lead que manda 3 mensagens no
   mesmo dia contava como 3 respostas. Corrigido com
   `count(DISTINCT empresa_id)`.
3. **Coluna morta** — `interacoes.classificacao` está NULL em 100%
   das 442 interações históricas (nenhum pipeline atual a preenche;
   provável resquício de versão anterior do schema). `interesses` e
   `opt_outs` sempre mostravam zero por causa disso. Corrigido lendo
   `empresas.interesse_servicos` (jsonb) e `empresas.opt_out`, que são
   as fontes reais e já vêm sendo gravadas corretamente pelos
   workflows — nenhuma mudança necessária em n8n/Zaia/MODO ANÚNCIO.
   **Pendência de limpeza de schema:** `interacoes.classificacao`
   candidata a `DROP COLUMN` numa faxina futura (confirmado sem
   nenhuma view/função dependente via varredura em
   `information_schema` + `pg_proc`).

### c) Blindagem de follow-up — `fn_contato_permitido()`

Vazamento identificado: leads já descartados (`descartado_x`,
`perdido_silencio`) continuavam aparecendo na fila de retomada D+1
porque esse ramo da view só olhava a última interação, nunca o
`status`. Corrigido centralizando a decisão de contato em UM lugar:

```sql
fn_contato_permitido(empresas) → boolean
```

bloqueia: opt_out, atendimento_humano, bot_suspeito, status
descartado%/perdido_silencio/perdido/sem_celular/sem_whatsapp/
opt_out/invalido/cliente/pos_venda.

Todos os ramos da agenda de follow-up (`vw_followups_agenda`, ver
item d) passam por essa função. Um **trigger** em `empresas`
(`trg_cancelar_followups_bloqueio`) cancela automaticamente
followups pendentes assim que um lead vira bloqueado — mata órfãos
na origem, não só retroativamente.

Validado em produção: 4 leads reais (G.R.P, Mendes, Antônio, Joyce)
removidos da fila antes de qualquer envio indevido — zero mensagem
enviada por engano.

### d) Refatoração da fonte de follow-up: `vw_followups_agenda`

`vw_followups_devidos` (consumida pelo n8n W3-A) tinha toda a lógica
de elegibilidade embutida com filtro `<= now()`, o que a impedia de
mostrar "amanhã"/"futuro" — necessário para o painel. Refatorado para
hierarquia de fonte única:

- **`vw_followups_agenda`** — TODA a lógica, datas projetadas, sem
  corte temporal. Base única; nova regra entra só aqui.
- **`vw_followups_devidos`** — casca: `WHERE devido_em <= now()`.
  Mesmas 7 colunas, mesma ordem — o node "Buscar Fila" do W3-A não
  mudou uma linha.
- **`vw_painel_followups`** — casca sem PII, grant anon, consumida
  pelo painel (tela Follow-ups com blocos Atrasados/Hoje/Amanhã/
  Futuros).

Nota de leitura importante para não reabrir a mesma dúvida: o painel
bucketiza por **dia**, o motor filtra por **timestamp exato** — um
item "Hoje" no painel pode não estar devido ainda no momento em que
o motor roda. Isso é esperado, não é bug.

### e) Funil de acompanhamento — leads presos indefinidamente

Identificado (a partir do caso real "LKMI Clínica de Estética" /
Luciano, que já tinha recebido o F2 de despedida em 31/07 mas
continuava aparecendo em `abordado` como se a conversa seguisse
ativa) que **nada movia o status da empresa quando o ciclo de
follow-up terminava**. A peça para isso — `fn_encerrar_silencio()` —
já existia pronta no banco, e o node "Encerrar Silêncio" já existia
corretamente conectado no W3-A (`Encerramento? → True → Encerrar
Silêncio → Loop`, chamando a função via RPC). **Não havia lacuna no
workflow** — o tipo `encerrar_silencio` simplesmente nunca tinha tido
um caso real vencido até 05/08 (prazo configurado:
`encerramento_pos_f2_dias = 7`).

20 leads do funil frio presos em `abordado`/`respondeu` (com F2
executado, silêncio total desde então) foram movidos manualmente
para `perdido_silencio` — decisão de negócio correta, mas
tecnicamente adiantada em 1-6 dias em relação ao prazo oficial (o
mais antigo, Lidiane Araújo, só venceria em 06/08).

**Extensão do mesmo padrão para o funil de anúncio/site** (não
coberto antes — esse funil não tinha NENHUM mecanismo de
encerramento, nem manual nem automático): três novos ramos
adicionados a `vw_followups_agenda`, todos reaproveitando o mesmo
tipo `encerrar_silencio` (zero alteração necessária no workflow n8n,
já que o Code node "Priorizar e Cortar" e o node "Encerramento?" já
reconhecem essa string):

1. **Frio** (já existia): F2 executado + 7 dias sem resposta.
2. **Anúncio, nunca respondeu à retomada D+1**: retomada executada +
   7 dias sem resposta desde então.
3. **Anúncio, esfriou sem retomada** (novo padrão, confirmado com
   dado: 14 de 30 leads ativos em `qualificando`/`oferta_apresentada`
   parados, 10 já com 7+ dias): cobre leads cuja última mensagem foi
   deles — `conversa_parada_auto` só dispara quando a última mensagem
   é nossa `resposta_agente`, então esses nunca chegavam a receber
   retomada nenhuma. Prazo: 7 dias sem NENHUMA interação (qualquer
   direção). Destino: igual aos demais, `perdido_silencio`.

Aplicado em produção; 9 dos 18 leads represados do ramo 2 já
venceram o prazo no dia da aplicação e devem sumir do funil no
próximo run do W3-A sem intervenção manual.

**Pendência identificada, não resolvida nesta sessão:** 2 leads em
`estagio_conversa='checkout_enviado'` (Luciana Cunha, e um lead sem
nome preenchido) não têm NENHUM registro correspondente em
`negocios` — o ramo `pos_checkout` da agenda depende dessa tabela e
por isso nunca os processa. Causa não identificada (falha de
instrumentação no MODO ANÚNCIO ao gerar o link de checkout? webhook
do Cakto que não disparou?). Não criar um mecanismo de prazo em cima
do sintoma sem antes entender a causa — investigar em sessão futura.

**Lição de processo registrada:** nesta sessão o Claude propôs por
duas vezes uma correção em cima de suposição não verificada (workflow
w3-a de memória, sem checar o JSON real; hipótese de node faltando
que na verdade já existia). Corrigido ao longo da sessão. Reforça a
prática já documentada em `FONTES.md`: **sempre buscar a versão viva
do workflow/schema antes de propor mudança**, nunca assumir a partir
de memória de sessões anteriores.

### Bug crítico corrigido — colapso de itens em lote (A1 p2)
Os nós "Checar Place Duplicado" / "Resolver Conflito de Place" (adicionados em
28/07 10:18, APÓS o último lote de 25 — nunca haviam rodado com lote real) perdiam
itens: leads sem gbp_place_id não emitiam output no Checar, e o Resolver rodava em
modo run-once retornando 1 item. Num lote de 10, só 1 lead era gravado.
Correção (determinística, arquitetura batelada):
- Checar Place Duplicado: **Execute Once** + consulta única `gbp_place_id=in.(...)`
  com todos os places do lote (fallback "__nenhum__" para lote sem places)
- Resolver Conflito: reconstrói o lote inteiro de `$('Aplicar Classificação').all()`
  e retorna N itens — N entram, N saem, por construção
- Gravar Enriquecimento: `Prefer: return=representation` (era minimal — output vazio
  colapsava o pareamento downstream)
- Calcular Score: usa `$json.id` da linha retornada pelo Gravar

### A2 Disparo v3.2 (2 nós alterados)
- **Buscar 1 Lead da Fila**: select + gancho_abordagem, enriquecimento_extra
- **Claude Gerar Mensagem (prompt v2)**: regra 10 nova — abre pelo GANCHO quando
  existir, dor como transição; review_destaque com nome de pessoa/serviço pode ser
  citado entre aspas simples; máximo 2 dados por mensagem; proibido inventar números.
  Payload troca gbp_reviews[0] cru pelo review_destaque curado + gancho + instagram.
  Validador e fallback inalterados.

## Testes executados
| Teste | Resultado |
|---|---|
| T-E1 (lead sem GBP/site) | ✅ enriquecimento_extra grava parte determinística; gancho null |
| T-E1b (lead com GBP via fallback) | ✅ Autêntica Brand: place correto escolhido por completude |
| Trava do gancho | ✅ Haiku violou a regra 6 v3 (lead 84) → trava em código bloqueou; query de auditoria = 0 ganchos sem fonte |
| Lote de 10 | ✅ 10 entram → 10 gravados após fix do colapso |
| Fila completa | ✅ 71 na fila, 19 com GBP (26,8% vs 17,6% do modelo antigo), 13 com gancho |
| T-D2 (msg1 real) | ✅ Lead 239 (Revitalize/Leticia): mensagem abre pelo gancho, ignora review vazio, 2 dados, termina em pergunta — enviada como 1º disparo real do modelo novo |

## Decisões
- Disparos de hoje (31/07): execução MANUAL, uma a uma, para conferência das mensagens
  antes do envio. Schedule do A2 Disparo permanece desligado até validação do dia.
- limite_diario no config está em 7 (conferir se intencional antes de religar o cron)
- Leads franquia (Espaçolaser) sem match: comportamento aceito — telefone corporativo
  difere do PDV; melhor tem_gbp=false honesto que citar unidade errada

## Backlog (registrado, fora desta entrega)
1. **A0 + geocoding**: adicionar `geocoding=true` na consulta CNPJá e mapear
   latitude/longitude no nó "Mapear Registros1" (campos lat/lng existem na tabela e
   estão 100% vazios — confirmado que o CNPJá fornece, nunca foi pedido). Depois,
   plugar `locationBias` no Places Text Search do A1 p2 para leads futuros.
   Verificar custo de crédito do geocoding antes.
2. **Qualidade do review_destaque**: exigir texto real com mínimo ~30 caracteres no
   classificador (caso observado: "Avaliação 5 estrelas" de review sem texto —
   inofensivo porque o gerador ignora, mas polui o dado).
3. **Roteiros msg1**: atualizar exemplos na tabela `roteiros` para refletir o padrão
   gancho→dor (hoje o guia/exemplo é anterior ao gancho).
4. **Re-enriquecimento periódico**: leads antigos fora do reset (abordados/respondeu)
   seguem com dados do modelo antigo; avaliar re-enriquecer antes de follow-ups
   relevantes.

# PARTE 3 — GLOSSÁRIO DE REFERÊNCIA RÁPIDA

**Stack:** n8n (self-hosted, `automacao.atitudesolucoes.com.br`) · Supabase (`qqxnnwycebhugikunxne`) · Evolution API (`whatsapp.atitudesolucoes.com.br`, instância `atitude-principal`) · Claude (Haiku classificador, Sonnet gerador) · Cakto (pagamentos)

**WhatsApp:** `5562981950604` = empresa · `5562981394546` = pessoal (alertas)

**Tabelas-chave:** `empresas`, `interacoes`, `anuncios`, `followups_agendados`, `config`, `aprovacoes_pendentes`, `objecoes`, `servicos`, `socios`, `onboarding`, `conversa_buffer`, `mensagens_desconhecidas`

**Views-chave:** `vw_followups_devidos`, `vw_fila_disparo`, `vw_fila_priorizada`, `vw_atencao_humana`

**Princípio database-first:** buscar todo contexto via SQL/HTTP antes de chamadas de LLM; pipelines determinísticos > agentic para classificação e scoring.

---
*Fim do documento consolidado (v2, 30/07/2026). Documentos-fonte originais (a remover do projeto após a próxima revisão): projeto-a2-resposta-v3.md, a2-resposta-v3-validacao-f0.md, a2-resposta-v3-objecoes.md, doc-score-deterministico.md, avaliacao-presenca-encerramento.md, site-somosatitude-estado-v2.md, site-index-ga4.md, w3-followup-engine-design.md, w3-followup-engine-encerramento.md, e a versão anterior deste consolidado.*

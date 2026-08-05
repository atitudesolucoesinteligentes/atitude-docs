## Automação
- schema.md: ✅ automatizado — atualiza diariamente às 6h via workflow n8n `schema-para-github`
- workflows/: ✅ automatizado — atualiza diariamente às 6h15 via workflow n8n `workflows-para-github` (8 workflows-chave, com mascaramento automático de segredos)
- site/index.html: atualização manual a cada alteração no site

## Segurança
- Tokens (GitHub PAT, n8n API key, Supabase service_role) vivem só dentro dos nodes do n8n — nunca em arquivo texto na máquina local
- Renovar GitHub PAT (`n8n-atitude-docs`) até 28/out/2026
- Renovar n8n API key (`export-github`) até 29/ago/2026

## Painel de prospecção
- painel-prospeccao.html: ✅ operacional — views dedicadas
  (vw_painel_empresas, vw_painel_followups) com grant anon completo,
  sem depender de select=* em `empresas`
- Funil separado em duas telas: Prospecção fria (por status) e
  Anúncio/site (por estagio_conversa) — cada uma reflete
  automaticamente ativo_no_funil = fn_contato_permitido(empresas.*)
- Métricas separadas por origem (cnpja vs anuncio/site); taxa de
  resposta contada por lead único, não por mensagem

## Follow-up e blindagem de contato
- fn_contato_permitido(): ✅ fonte única da decisão "pode contatar
  este lead?" — usada por toda a árvore de follow-up e pelo painel
- Trigger trg_cancelar_followups_bloqueio: ✅ cancela followups
  pendentes automaticamente quando um lead vira bloqueado
- vw_followups_agenda: ✅ fonte única de lógica de follow-up (nova
  regra entra só aqui); vw_followups_devidos e vw_painel_followups
  são cascas — motor n8n e painel não precisam de alteração quando
  a agenda muda
- Encerramento automático por silêncio (fn_encerrar_silencio, node
  já existente no W3-A): ✅ agora cobre funil frio (F2 + 7d) E
  funil de anúncio (retomada D+1 + 7d, ou 7d sem interação em
  qualificando/oferta_apresentada)

## Pendências
- checkout_enviado (anúncio) sem registro em `negocios` para
  alguns leads — causa não identificada, investigar instrumentação
  do MODO ANÚNCIO / webhook Cakto
- interacoes.classificacao — coluna morta (NULL em 100% dos
  registros), candidata a DROP COLUMN em faxina futura de schema
- T-W3-11 (pendente de observação, não de ação): confirmar no
  próximo run do W3-A que os leads de anúncio recém-elegíveis para
  encerrar_silencio realmente saem do funil sem intervenção manual

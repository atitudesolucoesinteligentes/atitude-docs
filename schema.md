# Schema — Somos Atitude (gerado em 2026-08-07)

# TABELAS

## Tabela: a2_config
- `chave` text NOT NULL
- `valor` text NOT NULL
- `atualizado_em` timestamp with time zone DEFAULT now()

## Tabela: a2_envios
- `id` bigint NOT NULL
- `lead_id` uuid
- `whatsapp` text NOT NULL
- `mensagem` text NOT NULL
- `enviado_em` timestamp with time zone DEFAULT now()

## Tabela: a2_respostas
- `id` uuid NOT NULL DEFAULT gen_random_uuid()
- `lead_id` uuid
- `telefone` text NOT NULL
- `mensagem` text
- `categoria` text
- `resumo` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: anuncios
- `id` bigint NOT NULL
- `ad_source_id` text
- `nome_interno` text
- `plataforma` text
- `servico_alvo` text
- `promessa_do_criativo` text
- `oferta` text
- `ativo` boolean DEFAULT true
- `criado_em` timestamp with time zone DEFAULT now()
- `frase_gatilho` text

## Tabela: aprovacoes_pendentes
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `numero` text NOT NULL
- `resposta_balões` jsonb NOT NULL
- `acoes_sugeridas` jsonb NOT NULL
- `confianca_geracao` integer NOT NULL
- `intencao` text
- `resumo_classificacao` text
- `status` text NOT NULL DEFAULT 'pendente'::text
- `criado_em` timestamp with time zone DEFAULT now()
- `resolvido_em` timestamp with time zone

## Tabela: assinatura_eventos
- `id` bigint NOT NULL DEFAULT nextval('assinatura_eventos_id_seq'::regclass)
- `cakto_event_id` text
- `assinatura_id` bigint
- `tipo` text NOT NULL
- `payload` jsonb
- `processado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: assinaturas
- `id` bigint NOT NULL DEFAULT nextval('assinaturas_id_seq'::regclass)
- `empresa_id` bigint NOT NULL
- `produto` text NOT NULL
- `plano` text
- `cakto_subscription_id` text
- `cakto_customer_id` text
- `cakto_order_id` text
- `email` text
- `valor` numeric
- `status` text NOT NULL DEFAULT 'ativa'::text
- `valido_ate` date
- `proximo_ciclo` date
- `link_pagamento` text
- `aceite_em` timestamp with time zone
- `aceite_canal` text
- `termos_versao` text
- `origem_atualizacao` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()
- `atualizado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: cnae_ciclo_caixa
- `cnae_prefixo` text NOT NULL
- `descricao` text
- `grupo` text
- `observacao` text

## Tabela: config
- `chave` text NOT NULL
- `valor` jsonb NOT NULL

## Tabela: conversa_buffer
- `id` bigint NOT NULL
- `empresa_id` bigint
- `remote_jid` text NOT NULL
- `mensagem` text
- `midia_tipo` text NOT NULL DEFAULT 'texto'::text
- `midia_base64_ref` text
- `evolution_id` text
- `recebida_em` timestamp with time zone NOT NULL DEFAULT now()
- `processar_apos` timestamp with time zone NOT NULL
- `processado` boolean NOT NULL DEFAULT false
- `processado_em` timestamp with time zone

## Tabela: empresas
- `id` bigint NOT NULL
- `cnpj` text
- `cnpj_raiz` text
- `filial_numero` integer
- `matriz_filial` text
- `razao_social` text
- `nome_fantasia` text
- `nome_exibicao` text
- `situacao` text
- `situacao_motivo` text
- `situacao_data` date
- `data_abertura` date
- `natureza_juridica_codigo` text
- `natureza_juridica` text
- `qualificacao_responsavel` text
- `cnae_principal` text
- `cnae_descricao` text
- `cnaes_secundarios` jsonb
- `segmento` text
- `mei` boolean
- `simples` boolean
- `porte_codigo` text
- `porte_descricao` text
- `capital_social` numeric
- `situacao_especial` text
- `situacao_especial_data` date
- `cep` text
- `tipo_logradouro` text
- `logradouro` text
- `numero` text
- `complemento` text
- `bairro` text
- `municipio` text
- `uf` text
- `codigo_ibge` integer
- `lat` numeric
- `lng` numeric
- `telefone_original` text
- `whatsapp` text
- `whatsapp_valido` boolean
- `whatsapp_verificado_em` timestamp with time zone
- `email` text
- `email_contab` boolean DEFAULT false
- `tem_site` boolean
- `site_url` text
- `site_status` text
- `site_sinais` jsonb
- `site_diagnostico` text
- `tem_gbp` boolean
- `gbp_place_id` text
- `gbp_rating` numeric
- `gbp_avaliacoes` integer
- `gbp_reviews` jsonb
- `gbp_url` text
- `gbp_match_confianca` text
- `tem_instagram` boolean
- `instagram` text
- `instagram_url` text
- `enriquecido_em` timestamp with time zone
- `perfil_oferta` text
- `dor_resumida` text
- `score` numeric
- `status` text NOT NULL DEFAULT 'novo'::text
- `opt_out` boolean NOT NULL DEFAULT false
- `tentativas` integer NOT NULL DEFAULT 0
- `ultimo_contato` timestamp with time zone
- `proximo_followup` date
- `interesse_servicos` jsonb
- `obs` text
- `origem` text NOT NULL DEFAULT 'cnpja'::text
- `importacao_id` bigint
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()
- `atualizado_em` timestamp with time zone NOT NULL DEFAULT now()
- `slug` text
- `producao_status` text NOT NULL DEFAULT 'pendente'::text
- `url_nova` text
- `url_proposta` text
- `contrato_status` text NOT NULL DEFAULT 'pendente'::text
- `contrato_em` date
- `telefones_json` jsonb
- `emails_json` jsonb
- `tem_celular` boolean
- `situacao_codigo` integer
- `motivo_codigo` integer
- `porte_codigo_num` integer
- `natureza_codigo` integer
- `simples_desde` date
- `mei_desde` date
- `fonte_atualizado_em` timestamp with time zone
- `nome_socio` text
- `flag_filial_repetida` boolean NOT NULL DEFAULT false
- `flag_rede` boolean NOT NULL DEFAULT false
- `flag_tel_repetido` boolean NOT NULL DEFAULT false
- `estagio_conversa` text
- `atendimento_humano` boolean NOT NULL DEFAULT false
- `bot_suspeito` boolean NOT NULL DEFAULT false
- `motivo_atencao` text
- `cupom_oferecido_em` timestamp with time zone
- `cupom_expira_em` timestamp with time zone
- `estagio_manual` text
- `mensagem_gerada_em` timestamp with time zone
- `enviado_manual_em` timestamp with time zone
- `score_detalhe` jsonb
- `anuncio_id` bigint
- `ctwa_clid` text
- `gbp_business_status` text
- `motivo_descarte` text
- `email_followup` text
- `email_status` text DEFAULT 'sem_email'::text
- `raiox_achados` jsonb
- `raiox_em` timestamp with time zone
- `gancho_abordagem` text
- `enriquecimento_extra` jsonb
- `esteira` text
- `esteira_definida_em` timestamp with time zone
- `esteira_motivo` text
- `opt_out_em` timestamp with time zone
- `opt_out_motivo` text
- `opt_out_canal` text
- `raiox_fin_nota` numeric
- `raiox_fin_faixa` text
- `raiox_fin_em` timestamp with time zone

## Tabela: followups_agendados
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `tipo` text NOT NULL
- `devido_em` timestamp with time zone NOT NULL
- `contexto` text
- `executado_em` timestamp with time zone
- `cancelado_motivo` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: importacoes
- `id` bigint NOT NULL
- `fonte` text NOT NULL DEFAULT 'cnpja'::text
- `filtros` jsonb
- `total_api` integer
- `total_gravados` integer
- `saldo_consumido` numeric
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()
- `cursor_token` text
- `paginas_lidas` integer
- `creditos_custo` numeric

## Tabela: interacoes
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `canal` text NOT NULL DEFAULT 'whatsapp'::text
- `direcao` text NOT NULL
- `etapa` text
- `roteiro_codigo` text
- `mensagem` text
- `copy_fallback` boolean DEFAULT false
- `classificacao` text
- `evolution_id` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()
- `intencao` text
- `confianca` integer
- `midia_tipo` text
- `transcricao` boolean

## Tabela: leads
- `id` uuid NOT NULL DEFAULT gen_random_uuid()
- `whatsapp` text NOT NULL
- `nome` text
- `empresa` text
- `segmento` text
- `cidade` text
- `site` text
- `google_place_id` text
- `rating` numeric
- `status` text NOT NULL DEFAULT 'prospect'::text
- `origem` text DEFAULT 'prospeccao'::text
- `opt_out` boolean DEFAULT false
- `total` integer
- `scores` jsonb
- `etapa_fraca` text
- `dinheiro_alerta` boolean
- `recomendacao` text
- `tentativas` integer DEFAULT 0
- `ultimo_contato` timestamp with time zone
- `proximo_followup` timestamp with time zone
- `notas` text
- `created_at` timestamp with time zone DEFAULT now()
- `updated_at` timestamp with time zone DEFAULT now()
- `avaliacoes` integer

## Tabela: mensagens_desconhecidas
- `id` bigint NOT NULL
- `remote_jid` text NOT NULL
- `telefone` text
- `mensagem` text
- `midia_tipo` text DEFAULT 'texto'::text
- `evolution_id` text
- `recebida_em` timestamp with time zone NOT NULL DEFAULT now()
- `tratado` boolean NOT NULL DEFAULT false
- `tratado_em` timestamp with time zone
- `obs` text
- `payload_raw` jsonb
- `origem_anuncio` boolean DEFAULT false
- `anuncio` jsonb

## Tabela: negocios
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `servico_codigo` text NOT NULL
- `valor` numeric
- `recorrente_mensal` numeric
- `status` text NOT NULL DEFAULT 'proposta'::text
- `proposta_em` date
- `fechado_em` date
- `pago` numeric DEFAULT 0
- `obs` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: objecoes
- `id` bigint NOT NULL
- `subtipo` text NOT NULL
- `contexto` text
- `abordagem` text NOT NULL
- `exemplo` text
- `ativo` boolean NOT NULL DEFAULT true
- `created_at` timestamp with time zone NOT NULL DEFAULT now()
- `updated_at` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: onboarding
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `dados_confirmados` jsonb
- `descricao_negocio` text
- `servicos_precos` jsonb
- `diferenciais` jsonb
- `publico_alvo` text
- `horario_funcionamento` jsonb
- `formas_pagamento` jsonb
- `redes_sociais` jsonb
- `whatsapp_atendimento` text
- `logo_url` text
- `quer_criacao_logo` boolean
- `cores_preferidas` text
- `fotos_urls` jsonb
- `sites_referencia` jsonb
- `dominio_possui` boolean
- `dominio` text
- `depoimentos` text
- `autoriza_reviews_google` boolean
- `gbp_categoria` text
- `gbp_tipo_atendimento` text
- `gbp_area_atendimento` text
- `gbp_telefone_publico` text
- `gbp_perfil_existente` boolean
- `gbp_tem_acesso_email` boolean
- `gbp_email_google` text
- `gbp_atributos` jsonb
- `gbp_ciente_verificacao` boolean
- `aceite_termos` boolean
- `aceite_termos_em` timestamp with time zone
- `call_alinhamento` text
- `token` text
- `iniciado_em` timestamp with time zone NOT NULL DEFAULT now()
- `concluido` boolean NOT NULL DEFAULT false
- `concluido_em` timestamp with time zone

## Tabela: planilhas_cliente
- `id` bigint NOT NULL DEFAULT nextval('planilhas_cliente_id_seq'::regclass)
- `empresa_id` bigint NOT NULL
- `spreadsheet_id` text NOT NULL
- `versao_template` text NOT NULL DEFAULT 'v1.0'::text
- `email_google` text
- `propriedade_transferida_em` timestamp with time zone
- `ativada_em` timestamp with time zone
- `ultimo_lancamento_em` date
- `ultima_analise_em` timestamp with time zone
- `analise_demo_em` timestamp with time zone
- `status` text NOT NULL DEFAULT 'provisionada'::text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: raiox_financeiro
- `id` bigint NOT NULL DEFAULT nextval('raiox_financeiro_id_seq'::regclass)
- `empresa_id` bigint NOT NULL
- `versao_quiz` text NOT NULL DEFAULT '1.0'::text
- `pontos` integer NOT NULL
- `nota` numeric NOT NULL
- `faixa` text NOT NULL
- `dimensoes` jsonb NOT NULL
- `dimensao_mais_fraca` text
- `respostas` jsonb NOT NULL
- `perfil` jsonb
- `contexto` jsonb
- `consentimento` jsonb
- `idempotency_key` text
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()

## Tabela: roteiros
- `id` bigint NOT NULL
- `codigo` text NOT NULL
- `perfil_oferta` text NOT NULL
- `etapa` text NOT NULL
- `servicos` jsonb
- `ativo` boolean NOT NULL DEFAULT true
- `guia` text
- `exemplo` text

## Tabela: score_cidades
- `municipio` text NOT NULL
- `pontos` integer NOT NULL

## Tabela: score_nichos
- `cnae_prefixo` text NOT NULL
- `descricao` text
- `pontos` integer NOT NULL

## Tabela: servicos
- `codigo` text NOT NULL
- `nome` text NOT NULL
- `tipo` text NOT NULL
- `preco_sugerido` numeric
- `ativo` boolean NOT NULL DEFAULT true
- `descricao_curta` text
- `descricao_completa` text
- `beneficios` jsonb
- `preco` numeric
- `preco_texto` text
- `prazo_entrega` text
- `faq` jsonb
- `link_checkout` text
- `link_material` text
- `quando_ofertar` text
- `preco_promocional` numeric
- `cupom_codigo` text
- `cupom_prazo_dias` integer

## Tabela: socios
- `id` bigint NOT NULL
- `empresa_id` bigint NOT NULL
- `nome` text
- `qualificacao` text
- `qualificacao_codigo` integer
- `identificador` text
- `documento` text
- `data_entrada` date
- `faixa_etaria` text
- `representante_nome` text
- `representante_qualif` text
- `decisor` boolean DEFAULT false
- `criado_em` timestamp with time zone NOT NULL DEFAULT now()
- `person_id` text
- `papel` text

## Tabela: warmup_canal
- `instancia` text NOT NULL DEFAULT 'atitude-principal'::text
- `dia` date NOT NULL DEFAULT CURRENT_DATE
- `mensagens_enviadas` integer NOT NULL DEFAULT 0
- `teto_do_dia` integer NOT NULL

# VIEWS

## View: vw_a2_fila
```sql
 SELECT id,
    nome,
    empresa,
    segmento,
    cidade,
    site,
    rating,
    whatsapp
   FROM leads
  WHERE ((status = 'prospect'::text) AND (COALESCE(opt_out, false) = false) AND (COALESCE(tentativas, 0) = 0) AND (whatsapp IS NOT NULL) AND (whatsapp ~ '^55\d{10,11}$'::text))
  ORDER BY id;
```

## View: vw_atencao_humana
```sql
 SELECT id AS empresa_id,
    nome_exibicao,
    whatsapp,
    status,
    estagio_conversa,
    atendimento_humano,
    bot_suspeito,
    motivo_atencao,
    ultimo_contato,
    ( SELECT i.mensagem
           FROM interacoes i
          WHERE ((i.empresa_id = e.id) AND (i.direcao = 'entrada'::text))
          ORDER BY i.criado_em DESC
         LIMIT 1) AS ultima_mensagem_cliente,
    ( SELECT i.criado_em
           FROM interacoes i
          WHERE ((i.empresa_id = e.id) AND (i.direcao = 'entrada'::text))
          ORDER BY i.criado_em DESC
         LIMIT 1) AS ultima_mensagem_em
   FROM empresas e
  WHERE ((atendimento_humano = true) OR (bot_suspeito = true))
  ORDER BY ultimo_contato DESC NULLS LAST;
```

## View: vw_dashboard_leads
```sql
 SELECT e.slug,
    e.nome_exibicao AS nome,
    e.segmento AS nicho,
    e.municipio AS cidade,
    e.gbp_rating AS nota,
    e.gbp_avaliacoes AS avaliacoes,
    e.email,
    e.telefone_original AS telefone,
    e.whatsapp,
    e.site_url AS "siteAntigo",
    COALESCE(e.site_diagnostico, e.dor_resumida) AS motivo,
        CASE
            WHEN ((e.status = ANY (ARRAY['perdido'::text, 'opt_out'::text, 'invalido'::text, 'descartado'::text])) OR (e.perfil_oferta ~~ 'descartado%'::text)) THEN 'descartado'::text
            WHEN (e.status = ANY (ARRAY['cliente'::text, 'pos_venda'::text])) THEN 'fechado'::text
            WHEN ((e.status = 'respondeu'::text) AND (EXISTS ( SELECT 1
               FROM negocios n
              WHERE (n.empresa_id = e.id)))) THEN 'respondeu'::text
            WHEN (e.status = ANY (ARRAY['proposta'::text, 'negociacao'::text])) THEN 'proposta'::text
            WHEN (e.producao_status = 'publicado'::text) THEN 'publicado'::text
            WHEN (e.producao_status = 'redesenhado'::text) THEN 'redesenhado'::text
            ELSE 'novo'::text
        END AS status,
    e.url_nova AS "urlNova",
    COALESCE(ng.data_proposta, ( SELECT (max(i.criado_em))::date AS max
           FROM interacoes i
          WHERE ((i.empresa_id = e.id) AND (i.direcao = 'saida'::text) AND (i.etapa = ANY (ARRAY['msg1'::text, 'msg2'::text]))))) AS "dataProposta",
    ng.valor_total AS valor,
    ng.mrr AS manutencao,
    ng.pago_total AS pago,
    e.obs,
    e.contrato_status AS "contratoStatus",
    e.contrato_em AS "contratoEm",
    e.cnpj AS "docCliente",
    concat_ws(', '::text, NULLIF(concat_ws(' '::text, e.tipo_logradouro, e.logradouro), ''::text), NULLIF(e.numero, ''::text), NULLIF(e.complemento, ''::text), NULLIF(e.bairro, ''::text), concat(e.municipio, '-', e.uf), NULLIF(('CEP '::text || e.cep), 'CEP '::text)) AS "endCliente"
   FROM (empresas e
     LEFT JOIN LATERAL ( SELECT min(n.proposta_em) AS data_proposta,
            sum(n.valor) FILTER (WHERE (n.status <> 'perdido'::text)) AS valor_total,
            sum(n.recorrente_mensal) FILTER (WHERE (n.status = 'fechado'::text)) AS mrr,
            sum(n.pago) AS pago_total
           FROM negocios n
          WHERE (n.empresa_id = e.id)) ng ON (true));
```

## View: vw_fila_disparo
```sql
 SELECT id,
    cnpj,
    cnpj_raiz,
    filial_numero,
    matriz_filial,
    razao_social,
    nome_fantasia,
    nome_exibicao,
    situacao,
    situacao_motivo,
    situacao_data,
    data_abertura,
    natureza_juridica_codigo,
    natureza_juridica,
    qualificacao_responsavel,
    cnae_principal,
    cnae_descricao,
    cnaes_secundarios,
    segmento,
    mei,
    simples,
    porte_codigo,
    porte_descricao,
    capital_social,
    situacao_especial,
    situacao_especial_data,
    cep,
    tipo_logradouro,
    logradouro,
    numero,
    complemento,
    bairro,
    municipio,
    uf,
    codigo_ibge,
    lat,
    lng,
    telefone_original,
    whatsapp,
    whatsapp_valido,
    whatsapp_verificado_em,
    email,
    email_contab,
    tem_site,
    site_url,
    site_status,
    site_sinais,
    site_diagnostico,
    tem_gbp,
    gbp_place_id,
    gbp_rating,
    gbp_avaliacoes,
    gbp_reviews,
    gbp_url,
    gbp_match_confianca,
    tem_instagram,
    instagram,
    instagram_url,
    enriquecido_em,
    perfil_oferta,
    dor_resumida,
    score,
    status,
    opt_out,
    tentativas,
    ultimo_contato,
    proximo_followup,
    interesse_servicos,
    obs,
    origem,
    importacao_id,
    criado_em,
    atualizado_em,
    slug,
    producao_status,
    url_nova,
    url_proposta,
    contrato_status,
    contrato_em,
    telefones_json,
    emails_json,
    tem_celular,
    situacao_codigo,
    motivo_codigo,
    porte_codigo_num,
    natureza_codigo,
    simples_desde,
    mei_desde,
    fonte_atualizado_em,
    nome_socio,
    flag_filial_repetida,
    flag_rede,
    flag_tel_repetido,
    gancho_abordagem,
    enriquecimento_extra,
    esteira
   FROM empresas e
  WHERE ((status = 'fila'::text) AND (opt_out = false) AND (tem_celular = true) AND (whatsapp_valido = true) AND (flag_filial_repetida = false) AND (flag_tel_repetido = false) AND (COALESCE(perfil_oferta, ''::text) !~~ 'descartado%'::text) AND (tentativas = 0))
  ORDER BY score DESC NULLS LAST, criado_em;
```

## View: vw_fila_disparo_digital
```sql
 SELECT id,
    cnpj,
    cnpj_raiz,
    filial_numero,
    matriz_filial,
    razao_social,
    nome_fantasia,
    nome_exibicao,
    situacao,
    situacao_motivo,
    situacao_data,
    data_abertura,
    natureza_juridica_codigo,
    natureza_juridica,
    qualificacao_responsavel,
    cnae_principal,
    cnae_descricao,
    cnaes_secundarios,
    segmento,
    mei,
    simples,
    porte_codigo,
    porte_descricao,
    capital_social,
    situacao_especial,
    situacao_especial_data,
    cep,
    tipo_logradouro,
    logradouro,
    numero,
    complemento,
    bairro,
    municipio,
    uf,
    codigo_ibge,
    lat,
    lng,
    telefone_original,
    whatsapp,
    whatsapp_valido,
    whatsapp_verificado_em,
    email,
    email_contab,
    tem_site,
    site_url,
    site_status,
    site_sinais,
    site_diagnostico,
    tem_gbp,
    gbp_place_id,
    gbp_rating,
    gbp_avaliacoes,
    gbp_reviews,
    gbp_url,
    gbp_match_confianca,
    tem_instagram,
    instagram,
    instagram_url,
    enriquecido_em,
    perfil_oferta,
    dor_resumida,
    score,
    status,
    opt_out,
    tentativas,
    ultimo_contato,
    proximo_followup,
    interesse_servicos,
    obs,
    origem,
    importacao_id,
    criado_em,
    atualizado_em,
    slug,
    producao_status,
    url_nova,
    url_proposta,
    contrato_status,
    contrato_em,
    telefones_json,
    emails_json,
    tem_celular,
    situacao_codigo,
    motivo_codigo,
    porte_codigo_num,
    natureza_codigo,
    simples_desde,
    mei_desde,
    fonte_atualizado_em,
    nome_socio,
    flag_filial_repetida,
    flag_rede,
    flag_tel_repetido,
    gancho_abordagem,
    enriquecimento_extra,
    esteira
   FROM vw_fila_disparo
  WHERE (COALESCE(esteira, ''::text) = 'presenca_digital'::text);
```

## View: vw_fila_disparo_financeiro
```sql
 SELECT id,
    cnpj,
    cnpj_raiz,
    filial_numero,
    matriz_filial,
    razao_social,
    nome_fantasia,
    nome_exibicao,
    situacao,
    situacao_motivo,
    situacao_data,
    data_abertura,
    natureza_juridica_codigo,
    natureza_juridica,
    qualificacao_responsavel,
    cnae_principal,
    cnae_descricao,
    cnaes_secundarios,
    segmento,
    mei,
    simples,
    porte_codigo,
    porte_descricao,
    capital_social,
    situacao_especial,
    situacao_especial_data,
    cep,
    tipo_logradouro,
    logradouro,
    numero,
    complemento,
    bairro,
    municipio,
    uf,
    codigo_ibge,
    lat,
    lng,
    telefone_original,
    whatsapp,
    whatsapp_valido,
    whatsapp_verificado_em,
    email,
    email_contab,
    tem_site,
    site_url,
    site_status,
    site_sinais,
    site_diagnostico,
    tem_gbp,
    gbp_place_id,
    gbp_rating,
    gbp_avaliacoes,
    gbp_reviews,
    gbp_url,
    gbp_match_confianca,
    tem_instagram,
    instagram,
    instagram_url,
    enriquecido_em,
    perfil_oferta,
    dor_resumida,
    score,
    status,
    opt_out,
    tentativas,
    ultimo_contato,
    proximo_followup,
    interesse_servicos,
    obs,
    origem,
    importacao_id,
    criado_em,
    atualizado_em,
    slug,
    producao_status,
    url_nova,
    url_proposta,
    contrato_status,
    contrato_em,
    telefones_json,
    emails_json,
    tem_celular,
    situacao_codigo,
    motivo_codigo,
    porte_codigo_num,
    natureza_codigo,
    simples_desde,
    mei_desde,
    fonte_atualizado_em,
    nome_socio,
    flag_filial_repetida,
    flag_rede,
    flag_tel_repetido,
    gancho_abordagem,
    enriquecimento_extra,
    esteira
   FROM vw_fila_disparo
  WHERE (COALESCE(esteira, ''::text) = 'financeiro'::text);
```

## View: vw_fila_priorizada
```sql
 SELECT id,
    cnpj,
    cnpj_raiz,
    filial_numero,
    matriz_filial,
    razao_social,
    nome_fantasia,
    nome_exibicao,
    situacao,
    situacao_motivo,
    situacao_data,
    data_abertura,
    natureza_juridica_codigo,
    natureza_juridica,
    qualificacao_responsavel,
    cnae_principal,
    cnae_descricao,
    cnaes_secundarios,
    segmento,
    mei,
    simples,
    porte_codigo,
    porte_descricao,
    capital_social,
    situacao_especial,
    situacao_especial_data,
    cep,
    tipo_logradouro,
    logradouro,
    numero,
    complemento,
    bairro,
    municipio,
    uf,
    codigo_ibge,
    lat,
    lng,
    telefone_original,
    whatsapp,
    whatsapp_valido,
    whatsapp_verificado_em,
    email,
    email_contab,
    tem_site,
    site_url,
    site_status,
    site_sinais,
    site_diagnostico,
    tem_gbp,
    gbp_place_id,
    gbp_rating,
    gbp_avaliacoes,
    gbp_reviews,
    gbp_url,
    gbp_match_confianca,
    tem_instagram,
    instagram,
    instagram_url,
    enriquecido_em,
    perfil_oferta,
    dor_resumida,
    score,
    status,
    opt_out,
    tentativas,
    ultimo_contato,
    proximo_followup,
    interesse_servicos,
    obs,
    origem,
    importacao_id,
    criado_em,
    atualizado_em,
    slug,
    producao_status,
    url_nova,
    url_proposta,
    contrato_status,
    contrato_em,
    telefones_json,
    emails_json,
    tem_celular,
    situacao_codigo,
    motivo_codigo,
    porte_codigo_num,
    natureza_codigo,
    simples_desde,
    mei_desde,
    fonte_atualizado_em,
    nome_socio,
    flag_filial_repetida,
    flag_rede,
    flag_tel_repetido,
        CASE
            WHEN (score >= (85)::numeric) THEN 'ataque_imediato'::text
            WHEN (score >= (65)::numeric) THEN 'alta'::text
            WHEN (score >= (40)::numeric) THEN 'media'::text
            ELSE 'baixa'::text
        END AS prioridade
   FROM vw_fila_disparo;
```

## View: vw_followup_unificado
```sql
 WITH marco AS (
         SELECT e_1.id AS empresa_id,
            GREATEST(COALESCE(( SELECT max(i.criado_em) AS max
                   FROM interacoes i
                  WHERE ((i.empresa_id = e_1.id) AND (i.direcao = 'saida'::text) AND (i.etapa = ANY (ARRAY['msg1'::text, 'msg2'::text])))), '-infinity'::timestamp with time zone), COALESCE(( SELECT (max(n.proposta_em))::timestamp with time zone AS max
                   FROM negocios n
                  WHERE (n.empresa_id = e_1.id)), '-infinity'::timestamp with time zone)) AS ultimo_marco
           FROM empresas e_1
        )
 SELECT e.id,
    e.slug,
    e.nome_exibicao,
    e.segmento,
    e.municipio,
    e.whatsapp,
    e.whatsapp_valido,
    e.email,
    m.ultimo_marco,
    (EXTRACT(day FROM (now() - m.ultimo_marco)))::integer AS dias_sem_resposta,
        CASE
            WHEN e.whatsapp_valido THEN 'whatsapp'::text
            ELSE 'email'::text
        END AS canal_sugerido
   FROM (empresas e
     JOIN marco m ON ((m.empresa_id = e.id)))
  WHERE ((m.ultimo_marco > '-infinity'::timestamp with time zone) AND (m.ultimo_marco < (now() - make_interval(days => COALESCE(( SELECT ((config.valor ->> 'dias_espera'::text))::integer AS int4
           FROM config
          WHERE (config.chave = 'followup'::text)), 3)))) AND (e.opt_out = false) AND (e.status <> ALL (ARRAY['cliente'::text, 'pos_venda'::text, 'perdido'::text, 'descartado'::text, 'invalido'::text, 'opt_out'::text])) AND (NOT (EXISTS ( SELECT 1
           FROM interacoes i
          WHERE ((i.empresa_id = e.id) AND (i.direcao = 'entrada'::text) AND (i.criado_em > m.ultimo_marco))))) AND (NOT (EXISTS ( SELECT 1
           FROM interacoes i
          WHERE ((i.empresa_id = e.id) AND (i.etapa = 'followup'::text))))))
  ORDER BY m.ultimo_marco;
```

## View: vw_followups_agenda
```sql
 WITH cfg AS (
         SELECT config.valor
           FROM config
          WHERE (config.chave = 'followup'::text)
        ), msg1 AS (
         SELECT interacoes.empresa_id,
            min(interacoes.criado_em) AS enviada_em
           FROM interacoes
          WHERE ((interacoes.direcao = 'saida'::text) AND (interacoes.etapa = 'msg1'::text) AND (interacoes.canal = 'whatsapp'::text))
          GROUP BY interacoes.empresa_id
        ), elegiveis AS (
         SELECT e.id,
            e.slug,
            e.email_followup,
            e.email_status,
            e.email_contab,
            m.enviada_em
           FROM (empresas e
             JOIN msg1 m ON ((m.empresa_id = e.id)))
          WHERE ((e.status = 'abordado'::text) AND (COALESCE(e.origem, ''::text) <> ALL (ARRAY['anuncio'::text, 'site'::text])) AND fn_contato_permitido(e.*) AND (NOT (EXISTS ( SELECT 1
                   FROM interacoes i2
                  WHERE ((i2.empresa_id = e.id) AND (i2.direcao = 'entrada'::text))))))
        ), conversa_parada_auto AS (
         SELECT e.id AS empresa_id,
            e.slug,
            (ultima.criado_em + make_interval(days => ((cfg.valor ->> 'conversa_parada_dias'::text))::integer)) AS devido_em
           FROM ((empresas e
             JOIN LATERAL ( SELECT i.criado_em,
                    i.direcao,
                    i.etapa
                   FROM interacoes i
                  WHERE (i.empresa_id = e.id)
                  ORDER BY i.criado_em DESC
                 LIMIT 1) ultima ON (true))
             CROSS JOIN cfg)
          WHERE ((COALESCE(e.origem, ''::text) = ANY (ARRAY['anuncio'::text, 'site'::text])) AND fn_contato_permitido(e.*) AND (ultima.direcao = 'saida'::text) AND (ultima.etapa = 'resposta_agente'::text) AND (NOT (EXISTS ( SELECT 1
                   FROM followups_agendados f
                  WHERE ((f.empresa_id = e.id) AND (f.tipo = 'conversa_parada_auto'::text))))))
        ), silencio_anuncio AS (
         SELECT f.empresa_id,
            e.slug,
            f.executado_em AS retomada_em
           FROM (followups_agendados f
             JOIN empresas e ON ((e.id = f.empresa_id)))
          WHERE ((f.tipo = 'conversa_parada_auto'::text) AND (f.executado_em IS NOT NULL) AND fn_contato_permitido(e.*) AND (NOT (EXISTS ( SELECT 1
                   FROM interacoes i
                  WHERE ((i.empresa_id = f.empresa_id) AND (i.direcao = 'entrada'::text) AND (i.criado_em > f.executado_em))))))
        ), estagio_esfriado AS (
         SELECT e.id AS empresa_id,
            e.slug,
            ult.criado_em AS ultima_interacao_em
           FROM (empresas e
             JOIN LATERAL ( SELECT max(i.criado_em) AS criado_em
                   FROM interacoes i
                  WHERE (i.empresa_id = e.id)) ult ON (true))
          WHERE ((e.origem = ANY (ARRAY['anuncio'::text, 'site'::text])) AND (e.estagio_conversa = ANY (ARRAY['qualificando'::text, 'oferta_apresentada'::text])) AND fn_contato_permitido(e.*) AND (ult.criado_em IS NOT NULL) AND (NOT (EXISTS ( SELECT 1
                   FROM followups_agendados f
                  WHERE ((f.empresa_id = e.id) AND (f.tipo = 'conversa_parada_auto'::text) AND (f.executado_em IS NOT NULL) AND (NOT (EXISTS ( SELECT 1
                           FROM interacoes i2
                          WHERE ((i2.empresa_id = e.id) AND (i2.direcao = 'entrada'::text) AND (i2.criado_em > f.executado_em))))))))))
        )
 SELECT el.id AS empresa_id,
    el.slug,
    'f1_email'::text AS tipo,
    (el.enviada_em + make_interval(days => ((cfg.valor ->> 'f1_email_dias'::text))::integer)) AS devido_em,
    el.email_followup,
    el.email_contab,
    NULL::text AS contexto
   FROM (elegiveis el
     CROSS JOIN cfg)
  WHERE ((el.email_status = 'valido'::text) AND (el.email_followup IS NOT NULL) AND (NOT (EXISTS ( SELECT 1
           FROM followups_agendados f
          WHERE ((f.empresa_id = el.id) AND (f.tipo = 'f1_email'::text))))) AND (NOT (EXISTS ( SELECT 1
           FROM followups_agendados f
          WHERE ((f.empresa_id = el.id) AND (f.tipo = 'f2_breakup'::text) AND (f.executado_em IS NOT NULL))))))
UNION ALL
 SELECT el.id AS empresa_id,
    el.slug,
    'f2_breakup'::text AS tipo,
    GREATEST((el.enviada_em + make_interval(days => ((cfg.valor ->> 'f2_breakup_dias'::text))::integer)), COALESCE((f1.executado_em + make_interval(days => ((cfg.valor ->> 'f2_apos_f1_dias'::text))::integer)), (el.enviada_em + make_interval(days => ((cfg.valor ->> 'f2_breakup_dias'::text))::integer)))) AS devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    NULL::text AS contexto
   FROM ((elegiveis el
     CROSS JOIN cfg)
     LEFT JOIN followups_agendados f1 ON (((f1.empresa_id = el.id) AND (f1.tipo = 'f1_email'::text) AND (f1.executado_em IS NOT NULL))))
  WHERE ((NOT (EXISTS ( SELECT 1
           FROM followups_agendados f
          WHERE ((f.empresa_id = el.id) AND (f.tipo = 'f2_breakup'::text))))) AND ((el.email_status <> 'valido'::text) OR (el.email_followup IS NULL) OR (f1.executado_em IS NOT NULL)))
UNION ALL
 SELECT cp.empresa_id,
    cp.slug,
    'conversa_parada_auto'::text AS tipo,
    cp.devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    NULL::text AS contexto
   FROM conversa_parada_auto cp
UNION ALL
 SELECT el.id AS empresa_id,
    el.slug,
    'encerrar_silencio'::text AS tipo,
    (f2.executado_em + make_interval(days => ((cfg.valor ->> 'encerramento_pos_f2_dias'::text))::integer)) AS devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    NULL::text AS contexto
   FROM ((elegiveis el
     CROSS JOIN cfg)
     JOIN followups_agendados f2 ON (((f2.empresa_id = el.id) AND (f2.tipo = 'f2_breakup'::text) AND (f2.executado_em IS NOT NULL))))
UNION ALL
 SELECT sa.empresa_id,
    sa.slug,
    'encerrar_silencio'::text AS tipo,
    (sa.retomada_em + make_interval(days => ((cfg.valor ->> 'encerramento_pos_f2_dias'::text))::integer)) AS devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    NULL::text AS contexto
   FROM (silencio_anuncio sa
     CROSS JOIN cfg)
UNION ALL
 SELECT ee.empresa_id,
    ee.slug,
    'encerrar_silencio'::text AS tipo,
    (ee.ultima_interacao_em + make_interval(days => ((cfg.valor ->> 'encerramento_pos_f2_dias'::text))::integer)) AS devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    NULL::text AS contexto
   FROM (estagio_esfriado ee
     CROSS JOIN cfg)
UNION ALL
 SELECT fa.empresa_id,
    e.slug,
    'conversa_parada'::text AS tipo,
    fa.devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
    fa.contexto
   FROM (followups_agendados fa
     JOIN empresas e ON ((e.id = fa.empresa_id)))
  WHERE ((fa.tipo = 'conversa_parada'::text) AND (fa.executado_em IS NULL) AND (fa.cancelado_motivo IS NULL) AND fn_contato_permitido(e.*))
UNION ALL
 SELECT n.empresa_id,
    e.slug,
    'pos_checkout'::text AS tipo,
        CASE
            WHEN (NOT (EXISTS ( SELECT 1
               FROM followups_agendados f
              WHERE ((f.empresa_id = n.empresa_id) AND (f.tipo = 'pos_checkout'::text) AND (f.contexto = 'lembrete'::text))))) THEN (n.criado_em + make_interval(days => ((cfg.valor ->> 'pos_checkout_lembrete_dias'::text))::integer))
            ELSE (n.criado_em + make_interval(days => ((cfg.valor ->> 'pos_checkout_escalar_dias'::text))::integer))
        END AS devido_em,
    NULL::text AS email_followup,
    false AS email_contab,
        CASE
            WHEN (NOT (EXISTS ( SELECT 1
               FROM followups_agendados f
              WHERE ((f.empresa_id = n.empresa_id) AND (f.tipo = 'pos_checkout'::text) AND (f.contexto = 'lembrete'::text))))) THEN 'lembrete'::text
            ELSE 'escalar'::text
        END AS contexto
   FROM ((negocios n
     CROSS JOIN cfg)
     JOIN empresas e ON ((e.id = n.empresa_id)))
  WHERE ((n.status = 'checkout_enviado'::text) AND (n.pago IS NULL) AND fn_contato_permitido(e.*));
```

## View: vw_followups_devidos
```sql
 SELECT empresa_id,
    slug,
    tipo,
    devido_em,
    email_followup,
    email_contab,
    contexto
   FROM vw_followups_agenda
  WHERE ((devido_em <= now()) OR (tipo = ANY (ARRAY['conversa_parada'::text, 'pos_checkout'::text])))
  ORDER BY devido_em;
```

## View: vw_metricas_anuncio_diaria
```sql
 SELECT (i.criado_em)::date AS dia,
    count(DISTINCT i.empresa_id) FILTER (WHERE (i.direcao = 'entrada'::text)) AS leads_conversando,
    count(*) FILTER (WHERE (i.direcao = 'entrada'::text)) AS mensagens_recebidas,
    count(*) FILTER (WHERE (i.direcao = 'saida'::text)) AS mensagens_enviadas,
    count(DISTINCT i.empresa_id) FILTER (WHERE ((i.direcao = 'entrada'::text) AND (COALESCE(e.interesse_servicos, '[]'::jsonb) <> '[]'::jsonb))) AS interesses,
    count(DISTINCT i.empresa_id) FILTER (WHERE ((i.direcao = 'entrada'::text) AND e.opt_out)) AS opt_outs
   FROM (interacoes i
     JOIN empresas e ON ((e.id = i.empresa_id)))
  WHERE (e.origem = ANY (ARRAY['anuncio'::text, 'site'::text]))
  GROUP BY ((i.criado_em)::date)
  ORDER BY ((i.criado_em)::date) DESC;
```

## View: vw_metricas_diarias
```sql
 SELECT (i.criado_em)::date AS dia,
    count(*) FILTER (WHERE ((i.direcao = 'saida'::text) AND (i.etapa = 'msg1'::text))) AS disparos,
    count(DISTINCT i.empresa_id) FILTER (WHERE ((i.direcao = 'entrada'::text) AND (e.origem = 'cnpja'::text))) AS respostas,
    count(DISTINCT i.empresa_id) FILTER (WHERE ((i.direcao = 'entrada'::text) AND (e.origem = 'cnpja'::text) AND (COALESCE(e.interesse_servicos, '[]'::jsonb) <> '[]'::jsonb))) AS interesses,
    count(DISTINCT i.empresa_id) FILTER (WHERE ((i.direcao = 'entrada'::text) AND (e.origem = 'cnpja'::text) AND e.opt_out)) AS opt_outs
   FROM (interacoes i
     JOIN empresas e ON ((e.id = i.empresa_id)))
  WHERE (e.origem = 'cnpja'::text)
  GROUP BY ((i.criado_em)::date)
  ORDER BY ((i.criado_em)::date) DESC;
```

## View: vw_painel_empresas
```sql
 SELECT id,
    slug,
    razao_social,
    nome_fantasia,
    nome_exibicao,
    segmento,
    cnae_principal,
    cnae_descricao,
    bairro,
    municipio,
    uf,
    data_abertura,
    status,
    estagio_conversa,
    perfil_oferta,
    dor_resumida,
    score,
    tem_site,
    site_url,
    site_diagnostico,
    tem_gbp,
    gbp_rating,
    gbp_avaliacoes,
    tem_instagram,
    whatsapp_valido,
    opt_out,
    tentativas,
    ultimo_contato,
    motivo_descarte,
    motivo_atencao,
    raiox_em,
    criado_em,
    origem,
    interesse_servicos,
    fn_contato_permitido(empresas.*) AS ativo_no_funil
   FROM empresas;
```

## View: vw_painel_followups
```sql
 SELECT a.empresa_id,
    a.empresa_id AS id,
    a.slug,
    a.tipo,
        CASE
            WHEN (a.tipo = 'f1_email'::text) THEN 'email'::text
            WHEN (a.tipo = 'encerrar_silencio'::text) THEN 'sistema'::text
            ELSE 'whatsapp'::text
        END AS canal,
    a.devido_em,
    ((a.devido_em AT TIME ZONE 'America/Sao_Paulo'::text))::date AS devido_dia,
    e.nome_exibicao,
    e.municipio,
    e.uf,
    e.perfil_oferta,
    e.score,
    e.status,
    e.ultimo_contato,
    ((e.email_status = 'valido'::text) AND (e.email_followup IS NOT NULL)) AS tem_email
   FROM (vw_followups_agenda a
     JOIN empresas e ON ((e.id = a.empresa_id)))
  ORDER BY a.devido_em;
```

## View: vw_planilha_disparo_manual
```sql
 SELECT e.whatsapp AS telefone,
    (e.nome_exibicao ||
        CASE
            WHEN (e.nome_socio IS NOT NULL) THEN ((' ('::text || e.nome_socio) || ')'::text)
            ELSE ''::text
        END) AS nome,
    e.municipio AS cidade,
    e.perfil_oferta AS perfil,
    i.mensagem,
        CASE
            WHEN i.copy_fallback THEN 'NAO (fallback)'::text
            ELSE 'SIM'::text
        END AS gerado_por_ia,
    e.mensagem_gerada_em
   FROM (empresas e
     JOIN interacoes i ON (((i.empresa_id = e.id) AND (i.etapa = 'msg1'::text))))
  WHERE (e.estagio_manual = 'mensagem_gerada'::text)
  ORDER BY e.mensagem_gerada_em DESC;
```

## View: vw_sem_celular
```sql
 SELECT id,
    slug,
    nome_exibicao,
    nome_socio,
    razao_social,
    municipio,
    bairro,
    telefone_original,
    email,
    cnpj,
    (((email IS NOT NULL))::integer + ((nome_socio IS NOT NULL))::integer) AS facilidade
   FROM empresas
  WHERE (status = 'sem_celular'::text)
  ORDER BY (((email IS NOT NULL))::integer + ((nome_socio IS NOT NULL))::integer) DESC, criado_em;
```

# FUNÇÕES

## Função: buscar_dossie
```sql
CREATE OR REPLACE FUNCTION public.buscar_dossie(p_telefone text)
 RETURNS TABLE(nome_exibicao text, dor_resumida text, site_diagnostico text, perfil_oferta text, estagio_conversa text, gbp_rating numeric, gbp_avaliacoes integer, cupom_oferecido_em timestamp with time zone, cupom_expira_em timestamp with time zone, atendimento_humano boolean, bot_suspeito boolean)
 LANGUAGE sql
AS $function$
  select
    nome_exibicao, dor_resumida, site_diagnostico, perfil_oferta,
    estagio_conversa, gbp_rating, gbp_avaliacoes,
    cupom_oferecido_em, cupom_expira_em, atendimento_humano, bot_suspeito
  from empresas
  where whatsapp = p_telefone
     or whatsapp = case
          when length(p_telefone) = 12 then substr(p_telefone,1,4) || '9' || substr(p_telefone,5)
          when length(p_telefone) = 13 then substr(p_telefone,1,4) || substr(p_telefone,6)
        end
  limit 1;
$function$

```

## Função: fn_a2_envios_hoje
```sql
CREATE OR REPLACE FUNCTION public.fn_a2_envios_hoje()
 RETURNS integer
 LANGUAGE sql
 STABLE
AS $function$
  SELECT COUNT(*)::INTEGER
  FROM a2_envios
  WHERE (enviado_em AT TIME ZONE 'America/Sao_Paulo')::date
      = (now() AT TIME ZONE 'America/Sao_Paulo')::date;
$function$

```

## Função: fn_a2_proximo_envio
```sql
CREATE OR REPLACE FUNCTION public.fn_a2_proximo_envio()
 RETURNS TABLE(lead_id uuid, nome text, empresa text, segmento text, cidade text, site text, rating numeric, whatsapp text, enviados_hoje integer, limite_diario integer)
 LANGUAGE plpgsql
 STABLE
AS $function$
DECLARE
  v_limite INTEGER;
  v_hoje INTEGER;
  v_ativo BOOLEAN;
BEGIN
  SELECT valor::BOOLEAN INTO v_ativo FROM a2_config WHERE chave = 'ativo';
  SELECT valor::INTEGER INTO v_limite FROM a2_config WHERE chave = 'limite_diario';
  v_hoje := fn_a2_envios_hoje();

  IF NOT COALESCE(v_ativo, false) OR v_hoje >= v_limite THEN
    RETURN;
  END IF;

  RETURN QUERY
  SELECT f.id, f.nome, f.empresa, f.segmento, f.cidade,
         f.site, f.rating, f.whatsapp, v_hoje, v_limite
  FROM vw_a2_fila f
  LIMIT 1;
END;
$function$

```

## Função: fn_assinatura_ativa
```sql
CREATE OR REPLACE FUNCTION public.fn_assinatura_ativa(p_empresa_id bigint, p_plano text DEFAULT NULL::text)
 RETURNS boolean
 LANGUAGE sql
 STABLE
AS $function$
  select exists (
    select 1 from assinaturas
     where empresa_id = p_empresa_id
       and (p_plano is null or plano = p_plano)
       and status in ('ativa','inadimplente')
       and (valido_ate is null or valido_ate >= current_date)
  );
$function$

```

## Função: fn_calcular_score
```sql
CREATE OR REPLACE FUNCTION public.fn_calcular_score(p_empresa_id bigint)
 RETURNS integer
 LANGUAGE plpgsql
AS $function$
declare
  e record;
  v_nicho int := 4;          -- padrão: nicho novo/não testado
  v_ticket int;
  v_recorrencia int := 10;   -- negócio local = SEO local sempre relevante
  v_site int;
  v_prova int;
  v_whats int;
  v_decisor int;
  v_cidade int := 0;
  v_penal int := 0;
  v_penal_fechada int := 0;  -- patch-09: fechamento temporário no Google
  v_total int;
  det jsonb;
begin
  select * into e from empresas where id = p_empresa_id;
  if not found then return null; end if;

  -- ===== FIT DO NEGÓCIO (40) =====
  select pontos into v_nicho from score_nichos
   where e.cnae_principal like cnae_prefixo || '%' limit 1;
  v_nicho := coalesce(v_nicho, 4);

  -- Ticket potencial: dados reais da Receita (melhor que "cara de faturamento")
  v_ticket := case
    when e.flag_rede or (e.porte_codigo_num is not null and e.porte_codigo_num >= 3) then 15
    when coalesce(e.mei, false) = false and coalesce(e.gbp_avaliacoes, 0) >= 50   then 12
    when coalesce(e.mei, false) = false                                            then 9
    else 4  -- MEI/autônomo
  end;

  -- ===== SINAL DE OPORTUNIDADE (40) — quanto pior, maior =====
  v_site := case e.site_status
    when 'sem_site'   then 20
    when 'fora_do_ar' then 18
    when 'terceiros'  then 16
    when 'fraco'      then 12
    when 'ok'         then 4
    else 10  -- não verificado ainda
  end;

  v_prova := case
    when e.gbp_rating >= 4.5 and e.gbp_avaliacoes >= 50 then 12
    when e.gbp_rating >= 4.0 and e.gbp_avaliacoes >= 15 then 8
    when e.gbp_rating >= 4.0                            then 4
    else 0
  end;
  -- (Gap frente a concorrentes: 8 pts previstos na rubrica; não coletamos
  --  ainda — fica 0 e vira melhoria futura do A1 p2)

  -- ===== VIABILIDADE DE CONTATO (20) =====
  v_whats := case
    when e.whatsapp_valido = true then 10
    when e.tem_celular = true     then 6
    when e.whatsapp is not null   then 4
    else 1
  end;

  v_decisor := case
    when e.flag_rede or e.flag_filial_repetida then 0   -- decisão longe
    when coalesce(e.mei, false) or e.nome_socio is not null then 5
    else 3
  end;

  select pontos into v_cidade from score_cidades where municipio = e.municipio;
  v_cidade := coalesce(v_cidade, 0);

  -- ===== PENALIDADES =====
  if e.site_status = 'ok' and coalesce(e.gbp_rating, 0) >= 4.5 then
    v_penal := v_penal - 20;  -- presença já boa, pouco a vender
  end if;
  if coalesce(e.gbp_rating, 5) < 3.5 and e.gbp_avaliacoes >= 10 then
    v_penal := v_penal - 15;  -- o problema é o serviço, não o site
  end if;
  if e.status in ('descartado', 'opt_out', 'perdido') then
    v_penal := v_penal - 30;  -- já recusou/saiu
  end if;
  if e.flag_tel_repetido then
    v_penal := v_penal - 10;  -- contato ambíguo (provável contador)
  end if;
  -- patch-09: Google marca o negócio como temporariamente fechado
  -- (CLOSED_PERMANENTLY não pontua: vira status='descartado' no A1 e cai na penalidade acima)
  if e.gbp_business_status = 'CLOSED_TEMPORARILY' then
    v_penal_fechada := -30;
    v_penal := v_penal + v_penal_fechada;
  end if;

  v_total := greatest(0, least(100,
    v_nicho + v_ticket + v_recorrencia + v_site + v_prova
    + v_whats + v_decisor + v_cidade + v_penal));

  det := jsonb_build_object(
    'nicho', v_nicho, 'ticket', v_ticket, 'recorrencia', v_recorrencia,
    'site', v_site, 'prova_social', v_prova, 'gap_concorrentes', 0,
    'whatsapp', v_whats, 'decisor', v_decisor, 'cidade', v_cidade,
    'penalidades', v_penal, 'fechada_temporariamente', v_penal_fechada,
    'total', v_total,
    'calculado_em', now());

  update empresas set score = v_total, score_detalhe = det
   where id = p_empresa_id;

  return v_total;
end;
$function$

```

## Função: fn_cancelar_followups
```sql
CREATE OR REPLACE FUNCTION public.fn_cancelar_followups(p_slug text, p_motivo text)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
begin
  update followups_agendados f
  set cancelado_motivo = p_motivo
  from empresas e
  where e.slug = p_slug and f.empresa_id = e.id
    and f.executado_em is null and f.cancelado_motivo is null;
end $function$

```

## Função: fn_classificar_sem_celular
```sql
CREATE OR REPLACE FUNCTION public.fn_classificar_sem_celular()
 RETURNS trigger
 LANGUAGE plpgsql
AS $function$
begin
  if new.tem_celular = false and new.status = 'novo' then
    new.status := 'sem_celular';
  end if;
  return new;
end;
$function$

```

## Função: fn_confirmar_envio_manual
```sql
CREATE OR REPLACE FUNCTION public.fn_confirmar_envio_manual(p_slug text, p_mensagem text, p_roteiro text DEFAULT NULL::text)
 RETURNS text
 LANGUAGE plpgsql
AS $function$
declare
  v_empresa_id bigint;
begin
  select id into v_empresa_id from empresas where slug = p_slug;

  if v_empresa_id is null then
    return 'ERRO: slug não encontrado: ' || p_slug;
  end if;

  update empresas
  set status = 'abordado',
      tentativas = 1,
      ultimo_contato = now(),
      estagio_manual = 'enviado_manual',
      enviado_manual_em = now()
  where id = v_empresa_id;

  -- registra a msg1 apenas se ainda não existir (idempotente)
  if not exists (
    select 1 from interacoes
    where empresa_id = v_empresa_id and direcao = 'saida' and etapa = 'msg1'
  ) then
    insert into interacoes (empresa_id, canal, direcao, etapa, roteiro_codigo, mensagem, criado_em)
    values (v_empresa_id, 'whatsapp', 'saida', 'msg1', p_roteiro, p_mensagem, now());
    return 'OK: envio confirmado + msg1 registrada para ' || p_slug;
  end if;

  return 'OK: envio confirmado (msg1 já existia) para ' || p_slug;
end;
$function$

```

## Função: fn_contato_permitido
```sql
CREATE OR REPLACE FUNCTION public.fn_contato_permitido(e empresas)
 RETURNS boolean
 LANGUAGE sql
 IMMUTABLE
AS $function$
  SELECT NOT e.opt_out
     AND NOT e.atendimento_humano
     AND COALESCE(e.bot_suspeito, false) = false
     AND e.status NOT LIKE 'descartado%'
     AND e.status NOT IN ('perdido_silencio','perdido','sem_celular',
                          'sem_whatsapp','opt_out','invalido',
                          'cliente','pos_venda');
$function$

```

## Função: fn_cota_pro_restante
```sql
CREATE OR REPLACE FUNCTION public.fn_cota_pro_restante(p_empresa_id bigint)
 RETURNS integer
 LANGUAGE sql
 STABLE
AS $function$
  select 20 - (
    select count(*)::int
      from interacoes
     where empresa_id = p_empresa_id
       and etapa = 'pergunta_pro'
       and criado_em >= date_trunc('month', now())
  );
$function$

```

## Função: fn_dashboard_update
```sql
CREATE OR REPLACE FUNCTION public.fn_dashboard_update(p_slug text, p_patch jsonb)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
declare
  v_id bigint;
  v_status text := p_patch->>'status';
begin
  select id into v_id from empresas where slug = p_slug;
  if v_id is null then raise exception 'slug % não encontrado', p_slug; end if;

  -- status do kanban -> campos internos
  if v_status is not null then
    if v_status in ('redesenhado','publicado') then
      update empresas set producao_status = v_status where id = v_id;
    elsif v_status = 'proposta' then
      update empresas set status = 'proposta' where id = v_id;
    elsif v_status = 'respondeu' then
      update empresas set status = 'respondeu' where id = v_id;
    elsif v_status = 'fechado' then
      update empresas set status = 'cliente' where id = v_id;
    elsif v_status = 'descartado' then
      update empresas set status = 'descartado' where id = v_id;
    elsif v_status = 'novo' then
      update empresas set status = 'novo', producao_status = 'pendente' where id = v_id;
    end if;
  end if;

  -- campos diretos
  update empresas set
    nome_exibicao   = coalesce(p_patch->>'nome',            nome_exibicao),
    segmento        = coalesce(p_patch->>'nicho',           segmento),
    municipio       = coalesce(p_patch->>'cidade',          municipio),
    email           = coalesce(p_patch->>'email',           email),
    whatsapp        = coalesce(p_patch->>'whatsapp',        whatsapp),
    url_nova        = coalesce(p_patch->>'urlNova',         url_nova),
    obs             = coalesce(p_patch->>'obs',             obs),
    contrato_status = coalesce(p_patch->>'contratoStatus',  contrato_status),
    contrato_em     = coalesce((p_patch->>'contratoEm')::date, contrato_em)
  where id = v_id;

  -- financeiro: valor/manutenção/pago vão para um negócio "principal"
  if p_patch ? 'valor' or p_patch ? 'manutencao' or p_patch ? 'pago' then
    insert into negocios (empresa_id, servico_codigo, valor, recorrente_mensal, pago,
                          status, proposta_em)
    values (v_id, 'criacao_site',
            (p_patch->>'valor')::numeric,
            (p_patch->>'manutencao')::numeric,
            coalesce((p_patch->>'pago')::numeric, 0),
            case when v_status = 'fechado' then 'fechado' else 'proposta' end,
            coalesce((p_patch->>'dataProposta')::date, current_date))
    on conflict do nothing;

    update negocios set
      valor             = coalesce((p_patch->>'valor')::numeric, valor),
      recorrente_mensal = coalesce((p_patch->>'manutencao')::numeric, recorrente_mensal),
      pago              = coalesce((p_patch->>'pago')::numeric, pago),
      proposta_em       = coalesce((p_patch->>'dataProposta')::date, proposta_em),
      status            = case when v_status = 'fechado' then 'fechado' else status end,
      fechado_em        = case when v_status = 'fechado'
                               then coalesce(fechado_em, current_date) else fechado_em end
    where empresa_id = v_id
      and id = (select max(id) from negocios where empresa_id = v_id);
  end if;
end;
$function$

```

## Função: fn_definir_esteira
```sql
CREATE OR REPLACE FUNCTION public.fn_definir_esteira(p_empresa_id bigint)
 RETURNS text
 LANGUAGE plpgsql
AS $function$
declare
  e             record;
  v_esteira     text;
  v_motivo      text;
  v_idade_anos  numeric;
begin
  select * into e from empresas where id = p_empresa_id;
  if not found then
    return null;
  end if;

  v_idade_anos := extract(epoch from (now() - e.data_abertura::timestamptz)) / 31557600;

  if e.data_abertura is not null and v_idade_anos < 2 then
    v_esteira := 'presenca_digital'; v_motivo := 'idade_menor_2a';

  elsif coalesce(e.mei, false) then
    v_esteira := 'presenca_digital'; v_motivo := 'mei';

  elsif e.perfil_oferta in ('criacao_zero','site_para_gbp','sem_gbp') then
    v_esteira := 'presenca_digital'; v_motivo := 'perfil_digital';

  elsif e.porte_codigo_num in (1,3,5)
        and e.data_abertura is not null and v_idade_anos >= 2
        and exists (select 1 from cnae_ciclo_caixa c
                     where e.cnae_principal like c.cnae_prefixo || '%') then
    v_esteira := 'financeiro'; v_motivo := 'porte_cnae_ciclo';

  elsif e.perfil_oferta = 'descartado_site_bom'
        and e.data_abertura is not null and v_idade_anos >= 2 then
    v_esteira := 'financeiro'; v_motivo := 'resgate_site_bom';

  else
    v_esteira := null; v_motivo := 'sem_regra';
  end if;

  update empresas
     set esteira            = v_esteira,
         esteira_motivo     = v_motivo,
         esteira_definida_em = now()
   where id = p_empresa_id;

  return v_esteira;
end $function$

```

## Função: fn_definir_whatsapp_manual
```sql
CREATE OR REPLACE FUNCTION public.fn_definir_whatsapp_manual(p_slug text, p_whatsapp text)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
begin
  update empresas
  set whatsapp = regexp_replace(p_whatsapp, '\D', '', 'g'),
      tem_celular = true,
      status = 'novo',              -- volta para o funil: A1 p1 valida na Evolution
      whatsapp_valido = null,
      whatsapp_verificado_em = null
  where slug = p_slug;
end;
$function$

```

## Função: fn_encerrar_silencio
```sql
CREATE OR REPLACE FUNCTION public.fn_encerrar_silencio(p_slug text)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
begin
  update empresas
  set status = 'perdido_silencio',
      estagio_conversa = 'perdido_silencio'
  where slug = p_slug;

  perform fn_cancelar_followups(p_slug, 'perdido_silencio');
end $function$

```

## Função: fn_envios_hoje
```sql
CREATE OR REPLACE FUNCTION public.fn_envios_hoje()
 RETURNS integer
 LANGUAGE sql
AS $function$
  select count(*)::int from interacoes
  where direcao = 'saida' and etapa = 'msg1'
    and criado_em::date = current_date;
$function$

```

## Função: fn_exportar_schema
```sql
CREATE OR REPLACE FUNCTION public.fn_exportar_schema()
 RETURNS text
 LANGUAGE plpgsql
 SECURITY DEFINER
 SET search_path TO 'public'
AS $function$
declare
  v_tabelas text;
  v_views   text;
  v_funcoes text;
begin
  -- Tabelas e colunas
  select string_agg(t.def, E'\n\n' order by t.table_name)
  into v_tabelas
  from (
    select c.table_name,
      '## Tabela: ' || c.table_name || E'\n' ||
      string_agg(
        '- `' || c.column_name || '` ' || c.data_type ||
        case when c.is_nullable = 'NO' then ' NOT NULL' else '' end ||
        coalesce(' DEFAULT ' || c.column_default, ''),
        E'\n' order by c.ordinal_position
      ) as def
    from information_schema.columns c
    join information_schema.tables tb
      on tb.table_name = c.table_name
     and tb.table_schema = 'public'
     and tb.table_type = 'BASE TABLE'
    where c.table_schema = 'public'
    group by c.table_name
  ) t;

  -- Views
  select string_agg(
    '## View: ' || table_name || E'\n```sql\n' || view_definition || E'\n```',
    E'\n\n' order by table_name)
  into v_views
  from information_schema.views
  where table_schema = 'public';

  -- Funções
  select string_agg(
    '## Função: ' || p.proname || E'\n```sql\n' || pg_get_functiondef(p.oid) || E'\n```',
    E'\n\n' order by p.proname)
  into v_funcoes
  from pg_proc p
  join pg_namespace n on n.oid = p.pronamespace
  where n.nspname = 'public' and p.prokind = 'f';

  return '# Schema — Somos Atitude (gerado em ' || now()::date || ')'
    || E'\n\n# TABELAS\n\n'  || coalesce(v_tabelas, '(nenhuma)')
    || E'\n\n# VIEWS\n\n'    || coalesce(v_views, '(nenhuma)')
    || E'\n\n# FUNÇÕES\n\n'  || coalesce(v_funcoes, '(nenhuma)');
end;
$function$

```

## Função: fn_higiene_cadastral
```sql
CREATE OR REPLACE FUNCTION public.fn_higiene_cadastral()
 RETURNS jsonb
 LANGUAGE plpgsql
AS $function$
declare v jsonb;
begin
  -- 3.1 Mesma raiz de CNPJ na base: mantém a MATRIZ (ou a de menor id)
  --     como principal; as demais ganham a flag
  update empresas e set flag_filial_repetida = true
  where exists (
    select 1 from empresas x
    where x.cnpj_raiz = e.cnpj_raiz and x.id <> e.id
      and ( (x.matriz_filial = 'MATRIZ' and e.matriz_filial <> 'MATRIZ')
         or (x.matriz_filial = e.matriz_filial and x.id < e.id) ));

  -- 3.2 Rede/franquia: 3+ estabelecimentos da mesma raiz
  update empresas e set flag_rede = true
  where (select count(*) from empresas x where x.cnpj_raiz = e.cnpj_raiz) >= 3;

  -- 3.3 WhatsApp repetido entre raízes diferentes (provável contador)
  update empresas e set flag_tel_repetido = true
  where e.whatsapp is not null
    and exists (select 1 from empresas x
                where x.whatsapp = e.whatsapp
                  and x.cnpj_raiz <> e.cnpj_raiz);

  -- 3.4 Limpeza do nome de exibição vindo de razão social
  update empresas set nome_exibicao = trim(regexp_replace(nome_exibicao,
      '\s+(LTDA|EIRELI|EIRELE|MEI?|EPP|S/?A)\.?\s*$', '', 'i'))
  where nome_exibicao ~* '\s(LTDA|EIRELI|EIRELE|MEI?|EPP|S/?A)\.?\s*$';

  select jsonb_build_object(
    'filiais_repetidas', (select count(*) from empresas where flag_filial_repetida),
    'redes',             (select count(*) from empresas where flag_rede),
    'tel_repetidos',     (select count(*) from empresas where flag_tel_repetido)
  ) into v;
  return v;
end;
$function$

```

## Função: fn_proximo_envio
```sql
CREATE OR REPLACE FUNCTION public.fn_proximo_envio()
 RETURNS SETOF empresas
 LANGUAGE sql
AS $function$
  select * from vw_fila_disparo limit 1;
$function$

```

## Função: fn_recalcular_scores
```sql
CREATE OR REPLACE FUNCTION public.fn_recalcular_scores()
 RETURNS TABLE(empresas_atualizadas integer)
 LANGUAGE plpgsql
AS $function$
begin
  perform fn_calcular_score(id) from empresas where enriquecido_em is not null;
  return query select count(*)::int from empresas
   where score_detalhe is not null;
end;
$function$

```

## Função: fn_registrar_followup
```sql
CREATE OR REPLACE FUNCTION public.fn_registrar_followup(p_slug text, p_canal text, p_texto text DEFAULT NULL::text)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
declare v_id bigint;
begin
  select id into v_id from empresas where slug = p_slug;
  if v_id is null then raise exception 'slug % não encontrado', p_slug; end if;

  if exists (select 1 from interacoes
             where empresa_id = v_id and etapa = 'followup') then
    raise exception 'empresa % já recebeu follow-up (máx. 1)', p_slug;
  end if;

  insert into interacoes (empresa_id, canal, direcao, etapa,
                          roteiro_codigo, mensagem)
  values (v_id, p_canal, 'saida', 'followup', 'generico_followup', p_texto);

  update empresas
     set ultimo_contato = now(),
         proximo_followup = null
   where id = v_id;
end;
$function$

```

## Função: fn_registrar_interesse
```sql
CREATE OR REPLACE FUNCTION public.fn_registrar_interesse(p_empresa_id bigint, p_codigo text)
 RETURNS void
 LANGUAGE sql
AS $function$
  update empresas
  set interesse_servicos = coalesce(interesse_servicos, '[]'::jsonb) || to_jsonb(p_codigo)
  where id = p_empresa_id
    and not coalesce(interesse_servicos, '[]'::jsonb) ? p_codigo;
$function$

```

## Função: fn_registrar_oferta_cupom
```sql
CREATE OR REPLACE FUNCTION public.fn_registrar_oferta_cupom(p_empresa_id bigint)
 RETURNS void
 LANGUAGE plpgsql
AS $function$
declare v_dias int;
begin
  select cupom_prazo_dias into v_dias
  from servicos where cupom_codigo = 'PRIME30' and ativo = true limit 1;
  update empresas
  set cupom_oferecido_em = now(),
      cupom_expira_em = now() + make_interval(days => v_dias)
  where id = p_empresa_id and cupom_oferecido_em is null;
end $function$

```

## Função: fn_registrar_opt_out
```sql
CREATE OR REPLACE FUNCTION public.fn_registrar_opt_out(p_telefone text, p_motivo text DEFAULT 'pediu_saida'::text, p_canal text DEFAULT 'whatsapp'::text)
 RETURNS bigint
 LANGUAGE plpgsql
AS $function$
declare
  v_id   bigint;
  v_slug text;
begin
  select id, slug into v_id, v_slug
    from empresas
   where whatsapp = regexp_replace(p_telefone, '\D', '', 'g')
   limit 1;

  if v_id is null then
    return null;
  end if;

  update empresas
     set opt_out        = true,
         opt_out_em     = now(),
         opt_out_motivo = p_motivo,
         opt_out_canal  = p_canal
   where id = v_id;

  insert into interacoes (empresa_id, canal, direcao, etapa, mensagem)
  values (v_id, p_canal, 'entrada', 'opt_out', p_motivo);

  if v_slug is not null then
    perform fn_cancelar_followups(v_slug, 'opt_out');
  end if;

  return v_id;
end $function$

```

## Função: fn_touch_atualizado_em
```sql
CREATE OR REPLACE FUNCTION public.fn_touch_atualizado_em()
 RETURNS trigger
 LANGUAGE plpgsql
AS $function$
begin new.atualizado_em := now(); return new; end;
$function$

```

## Função: fn_trg_cancelar_followups_bloqueio
```sql
CREATE OR REPLACE FUNCTION public.fn_trg_cancelar_followups_bloqueio()
 RETURNS trigger
 LANGUAGE plpgsql
AS $function$
BEGIN
  IF fn_contato_permitido(OLD) AND NOT fn_contato_permitido(NEW) THEN
    UPDATE followups_agendados
       SET cancelado_motivo = 'bloqueio: ' || NEW.status
             || CASE WHEN NEW.opt_out THEN ' (opt_out)' ELSE '' END
     WHERE empresa_id = NEW.id
       AND executado_em IS NULL
       AND cancelado_motivo IS NULL;
  END IF;
  RETURN NEW;
END $function$

```

## Função: fn_warmup_pode_enviar
```sql
CREATE OR REPLACE FUNCTION public.fn_warmup_pode_enviar(p_instancia text DEFAULT 'atitude-principal'::text)
 RETURNS boolean
 LANGUAGE sql
AS $function$
  select coalesce(
           (select mensagens_enviadas from warmup_canal
             where instancia = p_instancia and dia = current_date), 0)
         < fn_warmup_teto_hoje(p_instancia);
$function$

```

## Função: fn_warmup_registrar_envio
```sql
CREATE OR REPLACE FUNCTION public.fn_warmup_registrar_envio(p_instancia text DEFAULT 'atitude-principal'::text)
 RETURNS integer
 LANGUAGE plpgsql
AS $function$
declare v integer;
begin
  perform fn_warmup_teto_hoje(p_instancia);
  update warmup_canal
     set mensagens_enviadas = mensagens_enviadas + 1
   where instancia = p_instancia and dia = current_date
   returning mensagens_enviadas into v;
  return v;
end $function$

```

## Função: fn_warmup_teto_hoje
```sql
CREATE OR REPLACE FUNCTION public.fn_warmup_teto_hoje(p_instancia text DEFAULT 'atitude-principal'::text)
 RETURNS integer
 LANGUAGE plpgsql
AS $function$
declare
  c              jsonb;
  v_teto         integer;
  v_dias_no_teto integer;
begin
  select valor into c from config where chave = 'warmup';

  if c is null then
    return 10;
  end if;

  select teto_do_dia into v_teto
    from warmup_canal
   where instancia = p_instancia
   order by dia desc
   limit 1;
  v_teto := coalesce(v_teto, (c->>'teto_inicial')::int);

  if (c->>'congelado_ate') is not null
     and (c->>'congelado_ate')::date >= current_date then
    insert into warmup_canal (instancia, dia, teto_do_dia)
    values (p_instancia, current_date, v_teto)
    on conflict (instancia, dia) do nothing;
    return v_teto;
  end if;

  select count(*) into v_dias_no_teto
    from warmup_canal
   where instancia = p_instancia and teto_do_dia = v_teto;

  if v_dias_no_teto >= (c->>'dias_por_degrau')::int then
    v_teto := least(v_teto + (c->>'incremento')::int, (c->>'teto_maximo')::int);
  end if;

  insert into warmup_canal (instancia, dia, teto_do_dia)
  values (p_instancia, current_date, v_teto)
  on conflict (instancia, dia) do nothing;

  return v_teto;
end $function$

```
## Automação
- schema.md: ✅ automatizado — atualiza diariamente às 6h via workflow n8n `schema-para-github`
- workflows/: ✅ automatizado — atualiza diariamente às 6h15 via workflow n8n `workflows-para-github` (8 workflows-chave, com mascaramento automático de segredos)
- site/index.html: atualização manual a cada alteração no site

## Segurança
- Tokens (GitHub PAT, n8n API key, Supabase service_role) vivem só dentro dos nodes do n8n — nunca em arquivo texto na máquina local
- Renovar GitHub PAT (`n8n-atitude-docs`) até 28/out/2026
- Renovar n8n API key (`export-github`) até 29/ago/2026

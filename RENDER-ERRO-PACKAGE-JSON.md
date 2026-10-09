# Corrigir erro ENOENT package.json no Render

Este repositório agora inclui um `package.json` na raiz para que `npm install` funcione mesmo quando o serviço Render está com Root Directory vazio.

## Se você quer publicar o Agent neste serviço
- Root Directory: deixe vazio (raiz do repositório)
- Build Command: `npm install`
- Start Command: `npm start`

O `npm start` da raiz inicia `agent/agent.js`.

## Importante
1. Extraia o ZIP.
2. Envie TODO o conteúdo de dentro da pasta `sl-bot-master-suite` para a raiz do GitHub `gerentesecond01-debug/mastereagente`, incluindo o novo `package.json` da raiz. Não envie apenas a pasta externa como uma subpasta.
3. Faça commit/push para `main`.
4. No Render, confirme que o serviço está ligado ao repositório e ao commit novo. Depois clique em Manual Deploy → Deploy latest commit.

Se preferir manter Root Directory = `agent`, então o serviço deve ter Build `npm install` e Start `npm start`, e precisa apontar para o mesmo commit atualizado.

O arquivo raiz resolve o erro de arquivo ausente, mas não garante sozinho que as variáveis de ambiente, autenticação, conexão com o Master ou integração Second Life estejam configuradas corretamente.

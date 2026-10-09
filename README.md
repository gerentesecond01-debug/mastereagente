# SL Bot Master + Agent — instalação e Render

Este repositório contém o painel Master, o Agent e a configuração de implantação. Os serviços são separados.

## Implantar no Render (recomendado)

1. Envie todos os arquivos desta pasta para a raiz do seu repositório GitHub. O arquivo `render.yaml` precisa ficar na raiz, no mesmo nível das pastas `master/` e `agent/`.
2. No Render, abra **New → Blueprint** e conecte o repositório.
3. O Blueprint cria `sl-bot-master`, `sl-bot-agent` e o banco PostgreSQL. Ele configura automaticamente os diretórios corretos: `master` para o painel e `agent` para o Agent.
4. Espere os dois serviços e o banco terminarem de criar. O Master gera `ADMIN_PASSWORD`, `SESSION_SECRET` e `DATA_ENCRYPTION_KEY` como variáveis secretas.
5. Abra o serviço `sl-bot-master` → **Environment** para consultar/definir `ADMIN_PASSWORD`; use essa senha para entrar no painel. Não publique segredos em logs ou no GitHub.
6. Abra a URL pública do Master e entre. O Agent deve aparecer em **Servidores** para aprovação.

### Se preferir configurar serviços manualmente

**Master (Web Service)**
- Root Directory: `master`
- Build Command: `npm install`
- Start Command: `npm start`
- Health Check Path: `/health`
- Variáveis obrigatórias: `NODE_ENV=production`, `DATABASE_URL` (URL interna de um PostgreSQL), `ADMIN_PASSWORD`, `SESSION_SECRET`, `DATA_ENCRYPTION_KEY`.

**Agent (Web Service)**
- Root Directory: `agent`
- Build Command: `npm install`
- Start Command: `npm start`
- Health Check Path: `/health`
- Variáveis: `MASTER_HOST` = hostname do serviço Master, sem `https://` (ex.: `sl-bot-master.onrender.com`); `AGENT_KEY` = identificador único do Agent. O código também aceita `MASTER_URL` como URL completa.

O erro `ENOENT ... /src/package.json` acontece quando o Root Directory está vazio ou incorreto. Não basta configurar apenas `npm install` e `npm start`: cada serviço deve executar na sua pasta. O Blueprint da raiz resolve isso.

## Executar localmente com Docker

1. Copie `.env.example` para `.env`.
2. Troque `ADMIN_PASSWORD`, `SESSION_SECRET` e `DATA_ENCRYPTION_KEY` por valores fortes e únicos.
3. Execute `docker compose up --build -d`.
4. Abra `http://localhost:10000`.
5. Acompanhe: `docker compose logs -f master agent`. Para desligar: `docker compose down`.

## Importante

- O Agent precisa ser aprovado no painel e atribuído a uma configuração de bot antes de controlar uma sessão.
- Para login no Second Life, use uma conta de bot válida e siga os termos da plataforma. Nunca comite credenciais.
- A busca global de avatares depende dos recursos públicos disponíveis e pode não retornar dados estruturados; o link oficial continua sendo a alternativa.
- O plano gratuito do Render pode suspender serviços por inatividade, ter limites de uso e não ser adequado para um bot que precise ficar conectado continuamente.

## Verificações locais

Na pasta `master`: `npm test`
Na pasta `agent`: `npm test`

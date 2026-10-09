# SL Bot Master + Agent — pacote inicial

Este pacote junta o painel web Master e o serviço Agent num projeto só, mantendo os dois serviços separados por segurança e arquitetura. O Master fornece a interface gráfica; o Agent controla a sessão do bot no Second Life.

## Iniciar com Docker (recomendado)

Requisitos: Docker Desktop com Docker Compose.

1. Copie `.env.example` para `.env`.
2. Edite `.env` e defina valores próprios para `ADMIN_PASSWORD`, `SESSION_SECRET` e `DATA_ENCRYPTION_KEY` (não publique esses valores).
3. Na pasta do projeto, execute `docker compose up --build -d`.
4. Abra `http://localhost:10000` (ou a porta configurada em `MASTER_PORT`).
5. Entre com a senha que colocou em `ADMIN_PASSWORD`.
6. Abra **Servidores** no painel e aprove o Agent quando aparecer. Depois, crie/configure o bot e atribua um servidor disponível.

Para acompanhar a inicialização: `docker compose logs -f master agent`.
Para desligar: `docker compose down`. Para apagar também o banco local, use `docker compose down -v` (isso apaga os dados salvos).

## O que está incluído

- `master/`: painel gráfico, API e armazenamento PostgreSQL.
- `agent/`: serviço que se registra no Master e executa o runtime do bot.
- `docker-compose.yml`: sobe banco, Master e Agent numa rede local compartilhada.
- `.env.example`: modelo de configuração do Master.

## Importante sobre o Second Life

O painel e a comunicação Master/Agent ficam funcionais localmente, mas o bot só poderá entrar no Second Life depois que você cadastrar as credenciais de uma conta de bot válida no painel e configurar os dados necessários. Não coloque senhas reais no código nem compartilhe o arquivo `.env`.

A pesquisa global de avatares não é garantida por este pacote: a interface de controle de bots é diferente da busca global de pessoas do viewer oficial. Acesso a perfis e busca pública depende de APIs/fontes compatíveis e pode mudar.

## Problemas comuns

- Se o Master não iniciar, confira `docker compose logs -f master` e os três segredos do `.env`.
- Se o Agent não aparecer, confira `docker compose logs -f agent` e se `MASTER_URL` está como `http://master:10000`.
- Para reiniciar: `docker compose restart master agent`.

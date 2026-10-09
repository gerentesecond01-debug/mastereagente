# Deploy de painel + agente no mesmo endereço

Esta versão foi preparada para executar o painel Master e um Agent no mesmo serviço Web do Render.

- URL principal `/`: painel visual.
- URL `/agent/health`: health check do Agent através do proxy.
- O Agent roda internamente na porta 10001; o painel usa a porta fornecida pelo Render.
- O banco PostgreSQL continua sendo um recurso separado, criado pelo Blueprint.

## Publicar
1. Extraia este ZIP.
2. Envie o conteúdo da pasta `sl-bot-master-suite` para a raiz do repositório GitHub (não envie a pasta externa como uma camada extra).
3. No Render, use **New + → Blueprint** e selecione o repositório para aplicar o `render.yaml`.
4. Se já houver serviços antigos com esses nomes, revise o Blueprint para evitar duplicatas. Não apague o serviço antigo até confirmar que o novo painel funciona.
5. Após o deploy, abra a URL do serviço Web e confira `/` para o painel.

## Observações
- Defina `ADMIN_PASSWORD` para uma senha forte no Render. O padrão do código (`admin123`) não é recomendado.
- Não publique chaves nem segredos em arquivos do GitHub.
- O agente precisa de configuração válida para conectar ao Second Life; este deploy não garante login automático de uma conta.
- A busca pública do Second Life depende da disponibilidade do site externo.

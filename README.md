# Automation Kit

O Automation Kit é um kit de inicialização open-source para automação com IA, baseado no template oficial do n8n Self-hosted AI Starter Kit. Ele fornece um ambiente Docker Compose robusto para rodar n8n com integrações de IA locais, incluindo Ollama para LLMs, Qdrant para armazenamento de vetores, PostgreSQL para dados, e os serviços personalizados Wuzapi (para administração e APIs) e Waha (para funcionalidades específicas). Além disso, inclui o Cloudflare Tunnel (cloudflared) para expor os serviços de forma segura pela internet.

Curated by n8n-io, ele combina a plataforma low-code n8n com componentes de IA e serviços adicionais para workflows self-hosted e seguros.

## O que está incluído
- ✅ **n8n self-hosted** - Plataforma low-code com mais de 400 integrações e componentes avançados de IA
- ✅ **Ollama** - Plataforma LLM multiplataforma para instalar e rodar LLMs locais
- ✅ **Qdrant** - Armazenamento de vetores open-source de alto desempenho com API completa
- ✅ **PostgreSQL** - Banco de dados robusto para gerenciar grandes volumes de dados de forma segura
- ✅ **Wuzapi** - Serviço personalizado para administração e APIs, integrado ao ambiente
- ✅ **Waha** - Serviço adicional para funcionalidades específicas (ex.: integração com WhatsApp ou outras APIs)
- ✅ **Cloudflare Tunnel (cloudflared)** - Ferramenta para expor os serviços de forma segura via internet

## O que você pode construir
⭐️ Agentes de IA para agendamento de compromissos
⭐️ Resumo de PDFs corporativos de forma segura, sem vazamento de dados
⭐️ Bots Slack mais inteligentes para comunicação e operações de TI
⭐️ Análise privada de documentos financeiros a custo mínimo
⭐️ Gestão de usuários e webhooks via Wuzapi
⭐️ Automação de mensagens via Waha (ex.: WhatsApp)
⭐️ Acesso remoto seguro aos serviços via Cloudflare Tunnel
Instalação
Clonando o Repositório
git clone https://github.com/ulissesms/automation-kit.git
cd automation-kit

Rodando o ambiente com Docker Compose
Para usuários com Nvidia GPU
docker compose --profile gpu-nvidia up

Nota: Se você nunca usou sua GPU Nvidia com Docker antes, siga as instruções do Ollama Docker.
Para usuários Mac / Apple Silicon
Se você usa um Mac com processador M1 ou superior, não é possível expor a GPU para o Docker. Há duas opções:

Rode o kit totalmente em CPU, como na seção "Para todos os outros" abaixo.
Rode o Ollama diretamente no seu Mac para inferência mais rápida e conecte ao n8n.

Para rodar o Ollama no Mac, siga as instruções de instalação do Ollama e rode o kit assim:
docker compose up

Após seguir o quick start abaixo, altere as credenciais do Ollama no n8n usando http://host.docker.internal:11434/ como host.
Para todos os outros
docker compose --profile cpu up

⚡️ Quick Start e Uso
O núcleo do Automation Kit é um arquivo Docker Compose pré-configurado com redes, armazenamento e múltiplos serviços. Após os passos de instalação acima, siga estas etapas:

Abra http://localhost:5678/ no navegador para configurar o n8n. Isso só precisa ser feito uma vez.
Abra o workflow incluído: http://localhost:5678/workflow/srOnR8PAY3u4RSwb
Selecione "Test workflow" para executar o workflow.
Se for a primeira vez, aguarde o Ollama baixar o Llama3.2. Verifique o progresso nos logs do console Docker.

Para abrir o n8n localmente, visite http://localhost:5678/ no navegador. Para acessar remotamente via Cloudflare Tunnel, use o domínio fornecido após a configuração (ex.: https://seu-subdominio.trycloudflare.com).
Com sua instância n8n, você terá acesso a mais de 400 integrações e nós de IA. Para manter tudo local, use o nó Ollama para o modelo de linguagem e Qdrant como armazenamento de vetores. O Wuzapi e Waha podem ser integrados via APIs ou webhooks.
Nota: Este kit é projetado para proof-of-concept. Personalize conforme suas necessidades.
Upgrade

Para setups com Nvidia GPU:
docker compose --profile gpu-nvidia pull
docker compose create && docker compose --profile gpu-nvidia up


Para Mac / Apple Silicon:
docker compose pull
docker compose create && docker compose up


Para setups sem GPU:
docker compose --profile cpu pull
docker compose create && docker compose --profile cpu up



👓 Leitura Recomendada
Consulte o conteúdo do n8n para começar com IA. Para suporte, vá ao Fórum n8n.
🛍️ Mais Templates de IA
Visite a galeria de templates de IA do n8n para mais ideias.
Dicas e Truques
Acessando Arquivos Locais
Uma pasta compartilhada é criada no diretório do projeto, montada em /data/shared no container n8n. Use esse caminho em nós que interagem com o sistema de arquivos.
Configurando o Cloudflare Tunnel

Após iniciar o ambiente, o cloudflared criará um túnel. Veja os logs para o domínio gerado:docker logs cloudflared


Adicione os serviços desejados (ex.: n8n, wuzapi) ao túnel editando o arquivo de configuração ou variáveis de ambiente.

Configuração
Arquivo .env.example
Um exemplo de arquivo .env está fornecido como .env.example. Crie seu próprio .env a partir dele:
DB_HOST=postgres-1
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=sua_senha
DB_NAME=wuzapi
WUZAPI_ADMIN_TOKEN=seu_token_wuzapi
N8N_PROTOCOL=http
N8N_HOST=localhost
N8N_PORT=5678
OLLAMA_HOST=http://host.docker.internal:11434
QDRANT_HOST=qdrant
QDRANT_PORT=6333
WAHA_HOST=http://host.docker.internal:3000
WAHA_TOKEN=seu_token_waha
CLOUDFLARE_TUNNEL_TOKEN=seu_token_cloudflare
CLOUDFLARE_TUNNEL_DOMAIN=seu-subdominio.trycloudflare.com


DB_HOST/DB_PORT/DB_USER/DB_PASSWORD/DB_NAME: Configurações do PostgreSQL para o Wuzapi.
WUZAPI_ADMIN_TOKEN: Token de autenticação para o Wuzapi (porta 8080).
N8N_PROTOCOL/N8N_HOST/N8N_PORT: Configurações do n8n (porta 5678).
OLLAMA_HOST: Host do Ollama (ajuste para Mac ou GPU).
QDRANT_HOST/QDRANT_PORT: Configurações do Qdrant (porta 6333).
WAHA_HOST/WAHA_TOKEN: Configurações do Waha (porta 3000, token específico).
CLOUDFLARE_TUNNEL_TOKEN: Token de autenticação do Cloudflare Tunnel (obtenha em seu painel Cloudflare).
CLOUDFLARE_TUNNEL_DOMAIN: Domínio gerado pelo túnel (ex.: seu-subdominio.trycloudflare.com).


Obtenha o CLOUDFLARE_TUNNEL_TOKEN no painel Cloudflare (seção Zero Trust > Tunnels).

Uso
Acesse a Interface de Administração

n8n: Abra http://localhost:5678/ localmente ou https://seu-subdominio.trycloudflare.com via Cloudflare Tunnel.
Wuzapi: Abra http://localhost:8080/admin localmente ou https://seu-subdominio.trycloudflare.com:8080/admin via túnel, usando o token ${WUZAPI_ADMIN_TOKEN} (ex.: cabeçalho Authorization: Bearer ...).

Endpoints da API
Os endpoints da API podem incluir (confira a documentação ou código para detalhes exatos):

Wuzapi:
GET /api: Informações gerais da API.
GET /api/users: Lista usuários registrados.
POST /api/users: Cria um novo usuário.
GET /admin: Interface de administração.Exemplo:

curl -v -H "Authorization: Bearer ${WUZAPI_ADMIN_TOKEN}" https://seu-subdominio.trycloudflare.com/api


Waha:
GET /status: Verifica o status do serviço.
POST /send: Envia mensagens (requer token e dados no corpo).Exemplo:

curl -v -H "Authorization: Bearer ${WAHA_TOKEN}" -d '{"message": "Teste"}' https://seu-subdominio.trycloudflare.com:3000/send



Integração com n8n

Adicione um nó "HTTP Request" no n8n:
Wuzapi: URL: https://seu-subdominio.trycloudflare.com/api, Headers: Authorization: Bearer ${WUZAPI_ADMIN_TOKEN}
Waha: URL: https://seu-subdominio.trycloudflare.com:3000/send, Headers: Authorization: Bearer ${WAHA_TOKEN}


Execute o fluxo para interagir com os serviços.

Solução de Problemas

Porta não acessível:
Verifique com docker port <serviço>. Ajuste o docker-compose.yml se necessário.


Erro de banco de dados:
Confirme que os bancos n8n e wuzapi existem. Veja os logs com docker logs <serviço>.


Token inválido:
Verifique se os tokens no .env e nas tabelas correspondem.


Cloudflare Tunnel falha:
Confirme o CLOUDFLARE_TUNNEL_TOKEN e veja os logs com docker logs cloudflared.



Contribuindo

Faça um fork deste repositório.
Crie uma branch:git checkout -b feature/nova-funcionalidade


Envie suas alterações:git commit -m "Descrição da alteração"
git push origin feature/nova-funcionalidade


Abra um pull request.

Licença
Este projeto está licenciado sob a Apache License 2.0 - veja o arquivo LICENSE para detalhes.
Suporte
Junte-se ao Fórum n8n para compartilhar seu trabalho, perguntar ou propor ideias.
# Automation Kit

O Automation Kit é um kit de inicialização open-source para automação com IA, baseado no template oficial do n8n Self-hosted AI Starter Kit. Ele fornece um ambiente Docker Compose robusto para rodar n8n com integrações de IA locais, incluindo Ollama para LLMs, Qdrant para armazenamento de vetores, PostgreSQL para dados, e múltiplos serviços de WhatsApp: **Evolution API** (API robusta para WhatsApp Business), **Wuzapi** (administração e APIs) e **Waha** (funcionalidades específicas). Além disso, inclui o Cloudflare Tunnel (cloudflared) para expor os serviços de forma segura pela internet.

Curated by n8n-io, ele combina a plataforma low-code n8n com componentes de IA e serviços adicionais para workflows self-hosted e seguros.

## O que está incluído
- ✅ **n8n self-hosted** - Plataforma low-code com mais de 400 integrações e componentes avançados de IA
- ✅ **Ollama** - Plataforma LLM multiplataforma para instalar e rodar LLMs locais
- ✅ **Qdrant** - Armazenamento de vetores open-source de alto desempenho com API completa
- ✅ **PostgreSQL** - Banco de dados robusto para gerenciar grandes volumes de dados de forma segura
- ✅ **Wuzapi** - Serviço personalizado para administração e APIs, integrado ao ambiente
- ✅ **Waha** - Serviço adicional para funcionalidades específicas (ex.: integração com WhatsApp ou outras APIs)
- ✅ **Evolution API** - API robusta para WhatsApp Business com múltiplas instâncias e webhooks
- ✅ **Cloudflare Tunnel (cloudflared)** - Ferramenta para expor os serviços de forma segura via internet

## O que você pode construir
- ⭐️ **Agentes de IA para agendamento de compromissos**
- ⭐️ **Resumo de PDFs corporativos de forma segura, sem vazamento de dados**
- ⭐️ **Bots Slack mais inteligentes para comunicação e operações de TI**
- ⭐️ **Análise privada de documentos financeiros a custo mínimo**
- ⭐️ **Gestão de usuários e webhooks via Wuzapi**
- ⭐️ **Automação de mensagens via Waha (ex.: WhatsApp)**
- ⭐️ **WhatsApp Business API robusta com Evolution API (múltiplas instâncias)**
- ⭐️ **Chatbots inteligentes integrados com IA via Evolution API**
- ⭐️ **Acesso remoto seguro aos serviços via Cloudflare Tunnel**
## Instalação

### Clonando o Repositório
```bash
git clone https://github.com/ulissesms/automation-kit.git
cd automation-kit
```

### Configuração do Ambiente
Copie o arquivo de exemplo e configure suas variáveis:
```bash
cp .env.example .env
# Edite o arquivo .env com suas configurações
```

### Rodando o ambiente com Docker Compose

#### Para usuários com Nvidia GPU
```bash
docker compose --profile gpu-nvidia up
```

**Nota**: Se você nunca usou sua GPU Nvidia com Docker antes, siga as [instruções do Ollama Docker](https://hub.docker.com/r/ollama/ollama).

#### Para usuários Mac / Apple Silicon
Se você usa um Mac com processador M1 ou superior, não é possível expor a GPU para o Docker. Há duas opções:

1. Rode o kit totalmente em CPU, como na seção "Para todos os outros" abaixo
2. Rode o Ollama diretamente no seu Mac para inferência mais rápida e conecte ao n8n

Para rodar o Ollama no Mac, siga as [instruções de instalação do Ollama](https://ollama.ai/download) e rode o kit assim:
```bash
docker compose up
```

Após seguir o quick start abaixo, altere as credenciais do Ollama no n8n usando `http://host.docker.internal:11434/` como host.

#### Para todos os outros
```bash
docker compose --profile cpu up
```

## ⚡️ Quick Start e Uso

O núcleo do Automation Kit é um arquivo Docker Compose pré-configurado com redes, armazenamento e múltiplos serviços. Após os passos de instalação acima, siga estas etapas:

1. **Configure o n8n**: Abra `http://localhost:5678/` no navegador para configurar o n8n. Isso só precisa ser feito uma vez.

2. **Teste o workflow incluído**: Abra o workflow incluído: `http://localhost:5678/workflow/srOnR8PAY3u4RSwb`

3. **Execute o teste**: Selecione "Test workflow" para executar o workflow.

4. **Aguarde o download**: Se for a primeira vez, aguarde o Ollama baixar o Llama3.2. Verifique o progresso nos logs do console Docker.

### Acessos aos Serviços

- **n8n**: `http://localhost:5678/` (automação e workflows)
- **Evolution API**: `http://localhost:8021/manager` (painel de gerenciamento WhatsApp)
- **Wuzapi**: `http://localhost:8080/admin` (administração WhatsApp alternativa)
- **Waha**: `http://localhost:3000/` (dashboard WhatsApp)
- **Qdrant**: `http://localhost:6333/dashboard` (armazenamento de vetores)
- **PostgreSQL**: `localhost:5432` (banco de dados)
- **Redis**: `localhost:6379` (cache e sessões)

### Integração com n8n

Com sua instância n8n, você terá acesso a mais de 400 integrações e nós de IA. Para manter tudo local:
- Use o nó **Ollama** para modelos de linguagem
- Use **Qdrant** como armazenamento de vetores
- Integre **Evolution API**, **Wuzapi** e **Waha** via APIs ou webhooks

**Nota**: Este kit é projetado para proof-of-concept. Personalize conforme suas necessidades.
## Upgrade

### Para setups com Nvidia GPU:
```bash
docker compose --profile gpu-nvidia pull
docker compose create && docker compose --profile gpu-nvidia up
```

### Para Mac / Apple Silicon:
```bash
docker compose pull
docker compose create && docker compose up
```

### Para setups sem GPU:
```bash
docker compose --profile cpu pull
docker compose create && docker compose --profile cpu up
```



## 👓 Leitura Recomendada
Consulte o [conteúdo do n8n](https://docs.n8n.io/) para começar com IA. Para suporte, vá ao [Fórum n8n](https://community.n8n.io/).

## 🛍️ Mais Templates de IA
Visite a [galeria de templates de IA do n8n](https://n8n.io/workflows/) para mais ideias.
## Dicas e Truques

### Acessando Arquivos Locais
Uma pasta compartilhada é criada no diretório do projeto, montada em `/data/shared` no container n8n. Use esse caminho em nós que interagem com o sistema de arquivos.

### Configurando o Cloudflare Tunnel
Após iniciar o ambiente, o cloudflared criará um túnel. Veja os logs para o domínio gerado:

```bash
docker logs cloudflared
```

Adicione os serviços desejados (ex.: n8n, wuzapi) ao túnel editando o arquivo de configuração ou variáveis de ambiente.

## Configuração

### Arquivo .env.example
Um exemplo de arquivo .env está fornecido como `.env.example`. Crie seu próprio `.env` a partir dele:

```env
# Configurações do PostgreSQL
DB_HOST=postgres-1
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=sua_senha
DB_NAME=wuzapi

# Configurações do Wuzapi
WUZAPI_ADMIN_TOKEN=seu_token_wuzapi

# Configurações do n8n
N8N_PROTOCOL=http
N8N_HOST=localhost
N8N_PORT=5678

# Configurações do Ollama
OLLAMA_HOST=http://host.docker.internal:11434

# Configurações do Qdrant
QDRANT_HOST=qdrant
QDRANT_PORT=6333

# Configurações do Waha
WAHA_HOST=http://host.docker.internal:3000
WAHA_TOKEN=seu_token_waha

# Configurações do Cloudflare Tunnel
CLOUDFLARE_TUNNEL_TOKEN=seu_token_cloudflare
CLOUDFLARE_TUNNEL_DOMAIN=seu-subdominio.trycloudflare.com

# Configurações da Evolution API
EVOLUTION_SERVER_URL=http://localhost:8021
EVOLUTION_API_KEY=B6D711FCDE4D4FD5936544120E713976
EVOLUTION_LOG_LEVEL=ERROR
EVOLUTION_WEBHOOK_URL=http://host.docker.internal:5678/webhook/evolution

# Configurações do Redis
REDIS_PASSWORD=yourredispassword
```

### Descrição das Variáveis

- **DB_HOST/DB_PORT/DB_USER/DB_PASSWORD/DB_NAME**: Configurações do PostgreSQL para o Wuzapi
- **WUZAPI_ADMIN_TOKEN**: Token de autenticação para o Wuzapi (porta 8080)
- **N8N_PROTOCOL/N8N_HOST/N8N_PORT**: Configurações do n8n (porta 5678)
- **OLLAMA_HOST**: Host do Ollama (ajuste para Mac ou GPU)
- **QDRANT_HOST/QDRANT_PORT**: Configurações do Qdrant (porta 6333)
- **WAHA_HOST/WAHA_TOKEN**: Configurações do Waha (porta 3000, token específico)
- **EVOLUTION_SERVER_URL**: URL do servidor Evolution API (porta 8021)
- **EVOLUTION_API_KEY**: Chave de API para autenticação na Evolution API
- **EVOLUTION_LOG_LEVEL**: Nível de log da Evolution API (ERROR, WARN, INFO, DEBUG)
- **EVOLUTION_WEBHOOK_URL**: URL do webhook para receber eventos da Evolution API
- **REDIS_PASSWORD**: Senha do Redis para cache e sessões
- **CLOUDFLARE_TUNNEL_TOKEN**: Token de autenticação do Cloudflare Tunnel (obtenha em seu painel Cloudflare)
- **CLOUDFLARE_TUNNEL_DOMAIN**: Domínio gerado pelo túnel (ex.: seu-subdominio.trycloudflare.com)


**Nota**: Obtenha o `CLOUDFLARE_TUNNEL_TOKEN` no painel Cloudflare (seção Zero Trust > Tunnels).

## Uso

### Acesse a Interface de Administração

- **n8n**: Abra `http://localhost:5678/` localmente ou `https://seu-subdominio.trycloudflare.com` via Cloudflare Tunnel
- **Wuzapi**: Abra `http://localhost:8080/admin` localmente ou `https://seu-subdominio.trycloudflare.com:8080/admin` via túnel, usando o token `${WUZAPI_ADMIN_TOKEN}` (ex.: cabeçalho `Authorization: Bearer ...`)
- **Evolution API**: Acesse `http://localhost:8021/manager` para o painel de gerenciamento ou use a API em `http://localhost:8021`

### Endpoints da API

Os endpoints da API podem incluir (confira a documentação ou código para detalhes exatos):

#### Wuzapi:
- `GET /api`: Informações gerais da API
- `GET /api/users`: Lista usuários registrados
- `POST /api/users`: Cria um novo usuário
- `GET /admin`: Interface de administração

**Exemplo:**
```bash
curl -v -H "Authorization: Bearer ${WUZAPI_ADMIN_TOKEN}" https://seu-subdominio.trycloudflare.com/api
```

#### Evolution API:
- `GET /instance/fetchInstances`: Lista todas as instâncias
- `POST /instance/create`: Cria uma nova instância
- `GET /instance/connect/{instanceName}`: Conecta uma instância
- `GET /instance/qrcode/{instanceName}`: Obtém o QR Code para conexão
- `POST /message/sendText/{instanceName}`: Envia mensagem de texto

**Exemplo:**
```bash
# Criar uma instância
curl -X POST "http://localhost:8021/instance/create" \
  -H "Content-Type: application/json" \
  -H "apikey: ${EVOLUTION_API_KEY}" \
  -d '{
    "instanceName": "minha-instancia",
    "token": "meu-token-personalizado",
    "qrcode": true,
    "webhook": "http://host.docker.internal:5678/webhook/evolution"
  }'

# Obter QR Code
curl -X GET "http://localhost:8021/instance/qrcode/minha-instancia" \
  -H "apikey: ${EVOLUTION_API_KEY}"

# Enviar mensagem
curl -X POST "http://localhost:8021/message/sendText/minha-instancia" \
  -H "Content-Type: application/json" \
  -H "apikey: ${EVOLUTION_API_KEY}" \
  -d '{
    "number": "5511999999999",
    "text": "Olá! Esta é uma mensagem da Evolution API"
  }'
```


#### Waha:
- `GET /status`: Verifica o status do serviço
- `POST /send`: Envia mensagens (requer token e dados no corpo)

**Exemplo:**
```bash
curl -v -H "Authorization: Bearer ${WAHA_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{"message": "Teste"}' \
  https://seu-subdominio.trycloudflare.com:3000/send
```

### Integração com n8n

Adicione um nó "HTTP Request" no n8n:

- **Wuzapi**: 
  - URL: `https://seu-subdominio.trycloudflare.com/api`
  - Headers: `Authorization: Bearer ${WUZAPI_ADMIN_TOKEN}`

- **Waha**: 
  - URL: `https://seu-subdominio.trycloudflare.com:3000/send`
  - Headers: `Authorization: Bearer ${WAHA_TOKEN}`

- **Evolution API**: 
  - URL: `http://localhost:8021/message/sendText/sua-instancia`
  - Headers: `apikey: ${EVOLUTION_API_KEY}`

Execute o fluxo para interagir com os serviços.

## Solução de Problemas

### Porta não acessível:
Verifique com `docker port <serviço>`. Ajuste o `docker-compose.yml` se necessário.

### Erro de banco de dados:
Confirme que os bancos n8n e wuzapi existem. Veja os logs com `docker logs <serviço>`.

### Token inválido:
Verifique se os tokens no `.env` e nas tabelas correspondem.

### Cloudflare Tunnel falha:
Confirme o `CLOUDFLARE_TUNNEL_TOKEN` e veja os logs com `docker logs cloudflared`.

### Evolution API não conecta:
- Verifique se o Redis está funcionando: `docker logs redis`
- Confirme se o PostgreSQL está acessível: `docker logs postgres`
- Verifique os logs da Evolution API: `docker logs evolution-api`

### QR Code não aparece:
- Acesse `http://localhost:8021/instance/qrcode/sua-instancia`
- Verifique se a instância foi criada corretamente
- Confirme se a `EVOLUTION_API_KEY` está correta



## Contribuindo

1. Faça um fork deste repositório
2. Crie uma branch:
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
3. Envie suas alterações:
   ```bash
   git commit -m "Descrição da alteração"
   git push origin feature/nova-funcionalidade
   ```
4. Abra um pull request

## Licença
Este projeto está licenciado sob a Apache License 2.0 - veja o arquivo [LICENSE](LICENSE) para detalhes.

## Suporte
Junte-se ao [Fórum n8n](https://community.n8n.io/) para compartilhar seu trabalho, perguntar ou propor ideias.
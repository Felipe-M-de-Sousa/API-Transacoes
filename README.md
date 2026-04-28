🚀 Projeto API Transações - Checkpoint DevOps
📌 Descrição
Aplicação Java Spring Boot com banco MySQL, containerizada com Docker.

Implementa um CRUD de transações financeiras.

🧱 Arquitetura
🐳 Docker
☕ Java 17 + Spring Boot
🗄️ MySQL 8
☁️ Execução local ou em VM (Azure)
📦 Containers
Serviço	Nome	Porta
MySQL	mysql-dimdim	3306
API	api-dimdim	8080
🖥️ 1. Execução LOCAL
🔧 Pré-requisitos
Docker instalado
🗄️ Build da imagem MySQL
cd mysql-dimdim
docker build -f Dockerfile.mysql -t mysql-dimdim .
🧱 Criar rede e volume
docker volume create mysql-dimdim-data
docker network create dimdim-network
🚀 Executar container MySQL
docker run -d \
  --name mysql-dimdim \
  --network dimdim-network \
  -p 3306:3306 \
  -v mysql-dimdim-data:/var/lib/mysql \
  mysql-dimdim
☕ Build da API
cd ../transacoes-api
docker build -f Dockerfile.api -t api-dimdim .
🚀 Executar container da API
docker run -d \
  --name api-dimdim \
  --network dimdim-network \
  -p 8080:8080 \
  api-dimdim
📊 Verificar containers
docker ps
🧪 Testes da API
🔍 Listar
curl http://localhost:8080/api/transacoes
➕ Criar
curl -X POST http://localhost:8080/api/transacoes \
 -H "Content-Type: application/json" \
 -d '{"descricao":"Teste","valor":100}'
🌐 Acesso
👉 No navegador:

http://localhost:8080/api/transacoes
☁️ 2. Execução na VM (Azure)
🔑 Acessar VM
ssh adminlnx@IP_DA_VM
▶️ Subir containers
docker start mysql-dimdim
docker start api-dimdim
📊 Verificar
docker ps
🧪 Testar na VM
curl http://localhost:8080/api/transacoes

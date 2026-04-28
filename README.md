# 🚀 Projeto DimDim API - Checkpoint DevOps

## 📌 Descrição
Aplicação desenvolvida em **Java com Spring Boot**, integrada a um banco de dados **MySQL**, utilizando **Docker** para containerização.

A API implementa um **CRUD de transações financeiras**.

---

## 🧱 Arquitetura

- 🐳 Docker  
- ☕ Java 17 + Spring Boot  
- 🗄️ MySQL 8  
- ☁️ Execução local ou em VM (Azure)  

---

## 📦 Containers

| Serviço | Nome           | Porta |
|--------|----------------|-------|
| MySQL  | mysql-dimdim   | 3306  |
| API    | api-dimdim     | 8080  |

---

## 🖥️ 1. Execução LOCAL

### 🔧 Pré-requisitos
- Docker instalado

---

### 🗄️ Build da imagem MySQL
```bash
cd mysql-dimdim
docker build -f Dockerfile.mysql -t mysql-dimdim .
```

### 🧱 Criar rede e volume
```bash
docker volume create mysql-dimdim-data
docker network create dimdim-network
```

### 🚀 Executar container MySQL
```bash
docker run -d \
  --name mysql-dimdim \
  --network dimdim-network \
  -p 3306:3306 \
  -v mysql-dimdim-data:/var/lib/mysql \
  mysql-dimdim
```

☕ Build da API
```bash
cd ../transacoes-api
docker build -f Dockerfile.api -t api-dimdim .
```

🚀 Executar container da API
```bash
docker run -d \
  --name api-dimdim \
  --network dimdim-network \
  -p 8080:8080 \
  api-dimdim
```

📊 Verificar containers
```bash
docker ps
```

🧪 Testes da API
🔍 Listar transações
```bash
curl http://localhost:8080/api/transacoes
```

➕ Criar transação
```bash
curl -X POST http://localhost:8080/api/transacoes \
 -H "Content-Type: application/json" \
 -d '{"descricao":"Teste","valor":100}'
```

🌐 Acesso via navegador
```bash
http://localhost:8080/api/transacoes
```

☁️ 2. Execução na VM (Azure)
🔑 Acessar VM
```bash
ssh adminlnx@IP_DA_VM
```

▶️ Subir containers
```bash
docker start mysql-dimdim
docker start api-dimdim
```

📊 Verificar containers
```bash
docker ps
```

🧪 Testar API na VM
```bash
curl http://localhost:8080/api/transacoes
```

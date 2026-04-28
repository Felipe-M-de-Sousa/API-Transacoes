java-api-devops-linuxContainer
🚀 Projeto DimDim API - Checkpoint DevOps
📌 Descrição
Este projeto consiste em uma aplicação Java Spring Boot integrada a um banco de dados MySQL, utilizando Docker para containerização e execução em ambiente cloud (Azure VM).

A aplicação implementa um CRUD de transações financeiras.

🧱 Arquitetura
🐳 Docker
☕ Java 17 + Spring Boot
🗄️ MySQL 8
☁️ Azure Virtual Machine
A comunicação entre os containers ocorre por meio de uma rede Docker interna.

📦 Containers
Serviço	Nome	Porta
MySQL	mysql-dimdim	3306
API	api-dimdim	8080
1. Ligar a VM
Conectar via SSH normalmente:

ssh adminlnx@IP_DA_VM

2. Subir containers (se não estiverem rodando)
docker start mysql-dimdim

docker start api-dimdim

3. (Opcional)
Mostrar que está rodando:

docker ps

4. Testes da API
Listar transações
curl -X GET http://localhost:8080/api/transacoes
Criar transação
curl -X POST http://localhost:8080/api/transacoes \
 -H "Content-Type: application/json" \
 -d '{"descricao":"Compra mercado","valor":100}'
Atualizar transação
curl -X PUT http://localhost:8080/api/transacoes/1 \
 -H "Content-Type: application/json" \
 -d '{"descricao":"Alterado","valor":200,"dataTransacao":"2024-06-18T00:00:00"}'
Remover transação
curl -X DELETE http://localhost:8080/api/transacoes/id
Acesso à aplicação
Local (dentro da VM)
curl http://localhost:8080/api/transacoes
Externo (via navegador)
(http://102.37.154.61:8080/api/transacoes)

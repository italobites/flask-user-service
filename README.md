# Projeto Flask + PostgreSQL com Docker

## Descrição

Esse projeto é uma API simples feita com Flask, usando PostgreSQL como banco de dados.
Tudo roda em containers com Docker e Docker Compose.

A ideia é: criar e listar usuários, com os dados sendo salvos no banco mesmo depois de reiniciar os containers.

---

## Tecnologias utilizadas

-Python (Flask)

-PostgreSQL

-Docker

-Docker Compose

---

## Como executar o projeto

### 1 - Clonar o repositório

```bash
git clone https://github.com/italobites/flask-user-service.git
cd flask-user-service
```

---

### 2 - Criar o arquivo `.env`

Na raiz do projeto, crie um arquivo chamado `.env` com o seguinte conteúdo:

```env
POSTGRES_DB=app_db
POSTGRES_USER=app_user
POSTGRES_PASSWORD=app_password

DB_HOST=db
DB_PORT=5432
DB_NAME=app_db
DB_USER=app_user
DB_PASSWORD=app_password
```

---

### 3 - Subir os containers

```bash
docker compose up --build
```

Na primeira vez pode demorar um pouco por causa do build.

---

## Acessar a aplicação

Depois que subir, é só abrir no navegador:

```
http://localhost:5000
```

---

## Endpoints

### Criar usuário

**POST** `/users`

Exemplo de body:

```json
{
  "name": "Nome"
}
```

---

### Listar usuários

**GET** `/users`

---

## Persistência de dados

Dados ficam salvos em um volume do Docker.
Ou seja, mesmo que você pare ou recrie os containers, os dados continuam lá.

---

## Segurança

As configurações do banco (usuário, senha, etc.) ficam no arquivo `.env`, em vez de ficarem direto no código.

---

## Comunicação entre containers

A API se conecta ao banco usando o nome do serviço (`db`) como host.
Isso funciona porque os containers estão na mesma rede do Docker.

---

## Estrutura do projeto

```
.
├── app.py
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env
└── README.md
```

---

## Testes

Você pode testar usando a extensão REST Client do VS Code ou direto pelo terminal com curl.

Exemplo:

```bash
curl -X POST http://localhost:5000/users \
-H "Content-Type: application/json" \
-d '{"name": "Nome"}'
```

```bash
curl http://localhost:5000/users
```

---

## Últimas Considerações

É um projeto simples, mas já cobre o básico de uma aplicação backend com banco de dados rodando em containers, incluindo persistência e uso de variáveis de ambiente.

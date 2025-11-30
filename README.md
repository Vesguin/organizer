# NF Organizer Full Stack (Etapa N2 – Persistência)

Este projeto é uma aplicação Full Stack conteinerizada para extração, verificação e persistência de dados de Notas Fiscais (PDF → JSON → Banco de Dados).
Inclui extração com o Gemini, checagem de existência no banco via Prisma e persistência completa conforme requisitos da Atividade N2.

---

## Arquitetura

O projeto utiliza Docker Compose para três serviços principais:

**1. Backend – Node.js/Express**
API REST, agentes Gemini, validação e persistência via Prisma ORM.

**2. Database – PostgreSQL 16**
Banco relacional usado para armazenar fornecedores, faturados, despesas e movimentos.

**3. Frontend – React + Vite**
Interface para upload de PDFs, exibição dos dados extraídos e persistência.

---

## Pré-requisitos

* Git
* Docker Desktop
* Chave de API válida do Gemini (Google AI Studio)

---

# 1. Inicialização do Projeto

## Passo 1 — Clonar o repositório (CORRIGIDO)

git clone [https://github.com/Vesguin/organizer](https://github.com/Vesguin/organizer)
cd organizer

---

## Passo 2 — Criar o arquivo `.env`

Crie um arquivo chamado `.env` na raiz do projeto com o conteúdo abaixo:

GEMINI_API_KEY="SUA_CHAVE_AQUI"
PORT=3000
POSTGRES_USER=postgres_nf_user
POSTGRES_PASSWORD=nf_dev_2025
POSTGRES_DB=nf_db

---

## Passo 3 — Subir toda a aplicação (Build + Run + Migrações)

docker compose up -d --build

---

# 2. Acesso aos Serviços

Frontend: [http://localhost:5173](http://localhost:5173)
Backend (API): [http://localhost:3000](http://localhost:3000)

---

# 3. Fluxo de Uso da Etapa N2

1. O usuário envia o PDF pelo frontend.
2. O backend extrai dados com o Gemini e retorna um JSON estruturado.
3. O sistema verifica automaticamente se os registros já existem no banco.
4. O botão “Salvar Movimento” persiste o movimento no PostgreSQL via Prisma.

---

# 4. Comandos Úteis

**Ver logs:**
docker compose logs -f

**Parar todos os serviços:**
docker compose stop

**Reset completo (containers + volumes):**
docker compose down -v

**Acessar o banco no pgAdmin ou outro cliente:**
Host: localhost
Porta: 5445
Usuário e senha: iguais aos do arquivo `.env`

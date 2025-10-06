# Arquitetura do Projeto — Brechó App (TP2)

Este documento apresenta (i) as escolhas de tecnologias, (ii) o projeto arquitetural no modelo C4 (níveis 1 a 3) e (iii) as justificativas do modelo escolhido.

---

## 1. Escolhas de Tecnologias

### Front-end
- React + Vite (SPA simples, rápido para desenvolvimento)
- TypeScript (maior segurança de tipos)
- Tailwind CSS (produtividade no layout responsivo)
- Deploy: GitHub Pages ou Vercel

### Back-end
- Node.js + Express
- TypeScript
- Prisma (ORM)
- Banco inicial: SQLite (fácil para dev)
- Banco planejado: PostgreSQL (para produção)
- Autenticação: JWT
- Upload de imagens: pasta local (TP2), provedor externo (TP3+)

### Testes e Qualidade
- Jest (testes unitários)
- ESLint + Prettier (padrão de código)

---

## 2. C4 Model

### 2.1 C1 — Contexto

```mermaid
flowchart TB
    Cliente([Cliente])
    Admin([Administrador])

    subgraph Sistema["Brechó App"]
      WebUI["Aplicação Web (Front-end)"]
      API["API Back-end"]
    end

    DB[(Banco de Dados)]
    Store[(Armazenamento de Imagens)]

    Cliente --> WebUI
    Admin --> WebUI
    WebUI --> API
    API --> DB
    API --> Store

### 2.2 C2 — Contêineres
flowchart LR
    %% Containers overview
    subgraph Browser["Browser (React SPA)"]
      UI["React + Vite (TypeScript)\nTailwindCSS"]
    end

    subgraph Server["Back-end (Node.js / Express)"]
      Controller["Controllers (HTTP)"]
      Service["Services (Business Rules)"]
      Repo["Repositories (Prisma)"]
      Auth["Auth (JWT)"]
    end

    DB[(SQLite / PostgreSQL)]
    Store[(Image Storage\n(local uploads / external provider))]

    %% Connections
    UI -- REST / JSON --> Controller
    Controller --> Auth
    Controller --> Service
    Service --> Repo
    Repo --> DB
    Service --> Store


---

### 2.3 C3 — Componentes do Back-end
*(insira aqui o diagrama que você vai desenhar no estilo do C1)*

O diagrama de componentes detalha o back-end em módulos internos:

- **Controllers**: recebem requisições HTTP (ex.: `ItemController`, `AuthController`).
- **Services**: aplicam regras de negócio (ex.: `ItemService`, `AuthService`).
- **Repositories**: acesso ao banco com Prisma (ex.: `ItemRepository`, `UserRepository`).
- **JWT Provider**: autenticação com tokens.
- **Uploader**: gestão de imagens.
- **Validator**: validação dos dados de entrada.

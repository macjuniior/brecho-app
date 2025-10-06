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
```
### 2.2 C2 — Contêineres
```mermaid
flowchart LR
    subgraph Browser["Browser (React SPA)"]
      UI["React + Vite (TypeScript) + TailwindCSS"]
    end

    subgraph Server["Back-end (Node.js / Express)"]
      Controller["Controllers (HTTP)"]
      Service["Services (Business Rules)"]
      Repo["Repositories (Prisma)"]
      Auth["Auth (JWT)"]
    end

    DB[(SQLite / PostgreSQL)]
    Store[(Image Storage - local or external)]

    UI -- REST / JSON --> Controller
    Controller --> Auth
    Controller --> Service
    Service --> Repo
    Repo --> DB
    Service --> Store
```

### 2.3 C3 — Componentes do Back-end
```mermaid
flowchart TB
    subgraph API["Express API"]
      subgraph Controllers
        C_Auth["AuthController"]
        C_Item["ItemController"]
      end

      subgraph Services
        S_Auth["AuthService"]
        S_Item["ItemService"]
      end

      subgraph Repositories
        R_User["UserRepository (Prisma)"]
        R_Item["ItemRepository (Prisma)"]
      end

      JWT["JWT Provider"]
      Uploader["Uploader (filesystem or external)"]
      Validator["Schema Validator"]
    end

    DB[(Database)]
    FS[(Uploads folder)]

    C_Auth --> S_Auth --> R_User --> DB
    C_Item --> Validator
    C_Item --> S_Item --> R_Item --> DB
    S_Item --> Uploader --> FS
    S_Auth --> JWT



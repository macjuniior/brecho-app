# Arquitetura do Projeto — Brechó App (TP2)

Este documento apresenta (i) as escolhas de tecnologias, (ii) o projeto arquitetural no modelo C4 (níveis 1 a 3) e (iii) as justificativas do modelo escolhido.

---

## 1. Escolhas de Tecnologias

### Front-end
- **React + Vite** (SPA simples, rápido para desenvolvimento)
- **TypeScript** (maior segurança de tipos)
- **UI**: Tailwind CSS (produtividade no layout responsivo)
- **Build/Deploy**: GitHub Pages (ou Vercel)

### Back-end
- **Node.js + Express**
- **TypeScript**
- **ORM**: Prisma
- **Banco (TP2/Dev)**: SQLite (simples, arquivo local)
- **Banco (evolução/TP3+)**: PostgreSQL (quando for publicar)
- **Autenticação**: JWT (admin)
- **Upload de imagens**: local em `uploads/` (TP2) → provedor externo na evolução (ex.: Cloudinary/S3)

### Testes e Qualidade
- **Jest** (unitários back-end)
- **ESLint + Prettier** (padrão de código)

### Observabilidade (simples, TP2)
- Logs de aplicação (winston/pino)
- Status/healthcheck em `/health`

---

## 2. C4 Model

> **Níveis utilizados**:  
> **C1 – Diagrama de Contexto**: visão geral do sistema e atores.  
> **C2 – Diagrama de Contêineres**: aplicações/serviços e dados.  
> **C3 – Diagrama de Componentes** (do back-end): camadas internas (controller/service/repository).

> **Nota**: GitHub renderiza **Mermaid** nativamente. Abaixo estão versões em Mermaid “aproximadas” do C4. Se preferir C4 fiel, gere no draw.io/Structurizr e exporte PNG para `docs/img/`.

### 2.1 C1 — Contexto (Mermaid)

```mermaid
flowchart TB
    actorCliente([Cliente])
    actorAdmin([Administrador(a) do Brechó])

    subgraph Sistema["Brechó App (Sistema)"]
      WebUI["Aplicação Web (SPA)"]
      API["API Back-end"]
    end

    DB[(Base de Dados)]
    Store[(Armazenamento de Imagens)]

    clienteCliente[(Navegador do Cliente)]
    clienteAdmin[(Navegador do Admin)]

    actorCliente --> clienteCliente --> WebUI
    actorAdmin --> clienteAdmin --> WebUI
    WebUI --> API
    API --> DB
    API --> Store

### 2.2 C2 — Contêineres (Mermaid)

flowchart LR
    subgraph Browser["Browser (React SPA)"]
      UI["React + Vite (TypeScript)\nTailwind"]
    end

    subgraph Server["Back-end (Node.js/Express)"]
      Controller["Controllers (HTTP)"]
      Service["Services (Regras de Negócio)"]
      Repo["Repositories (Prisma)"]
      Auth["Auth (JWT)"]
    end

    DB[(SQLite / PostgreSQL)]
    Store[(Uploads locais / Provedor externo futuramente)]

    UI -- REST/JSON --> Controller
    Controller --> Auth
    Controller --> Service
    Service --> Repo
    Repo --> DB
    Service --> Store

### 2.3 C3 — Componentes do Back-end (Mermaid)
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

      subgraph Repos
        R_User["UserRepository (Prisma)"]
        R_Item["ItemRepository (Prisma)"]
      end

      JWT["JWT Provider"]
      Uploader["Uploader (filesystem)"]
      Validator["DTO/Schema Validator (zod)"]
    end

    DB[(DB)]
    FS[(uploads/) ]

    C_Auth --> S_Auth --> R_User --> DB
    C_Item --> Validator
    C_Item --> S_Item --> R_Item --> DB
    S_Item --> Uploader --> FS
    S_Auth --> JWT


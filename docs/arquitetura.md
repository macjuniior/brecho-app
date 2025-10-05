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

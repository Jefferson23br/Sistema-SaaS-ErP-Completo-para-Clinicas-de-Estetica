# ERP SaaS para Clinicas de Estetica

Plataforma SaaS de alta escalabilidade para clinicas de estetica, com capacidade de adaptacao para lashing design e manicures.

Este repositorio inicia a nova versao do sistema com base no aprendizado funcional da pasta `Barbearia_Premium`, evoluindo para uma arquitetura moderna, modular e preparada para multiempresa.

## Objetivo do Produto

Construir um ERP completo em modelo SaaS para operacao clinica e comercial:

- agenda por funcionario ou por sala;
- cadastro de clientes com prontuario customizavel;
- orcamento e vendas;
- faturamento e emissao de nota fiscal;
- financeiro, bancos e conciliacao;
- relatorios estrategicos e operacionais;
- estoque;
- CRM completo.

## Identidade Visual

- Cor primaria: `#c23421`
- Cor secundaria/base clara: `#faf8f7`
- Diretriz: interface clara, elegante, foco em legibilidade e velocidade operacional.

## Stack Tecnologica

### Frontend

- React com TypeScript
- Next.js (App Router)
- Tailwind CSS
- Biblioteca de componentes padronizada (ex.: shadcn/ui + Radix)
- React Query para cache e sincronizacao de dados
- React Hook Form + Zod para formularios robustos

### Backend

- Node.js com Express
- API REST versionada (`/api/v1`)
- Estrutura por camadas: `routes -> controllers -> services -> repositories`
- Middlewares dedicados para autenticacao, autorizacao, validacao, logs e tratamento de erros

### Banco e Arquivos

- PostgreSQL como banco principal
- Estrategia multi-tenant (por `tenant_id`) para isolamento logico por empresa
- Armazenamento de fotos e anexos via servico de arquivos (local inicial + opcao S3)
- Metadados de arquivos no banco (nome, url, tipo, tamanho, dono, modulo)

### Infra e Qualidade

- Docker para ambientes padronizados
- CI/CD para testes e deploy
- Observabilidade com logs estruturados e health checks
- Documentacao de API com OpenAPI/Swagger

## Arquitetura Proposta

### Organizacao de Pastas (macro)

```text
Milla/
  frontend/
    app/
    modules/
    shared/
  backend/
    src/
      config/
      middlewares/
      modules/
        agenda/
        clientes/
        prontuarios/
        orcamentos/
        vendas/
        faturamento/
        nfe/
        financeiro/
        bancos/
        conciliacao/
        relatorios/
        estoque/
        crm/
      routes/
      utils/
  database/
    migrations/
    seeds/
    schemas/
  docs/
```

### Padrao de Endpoints (exemplo)

- `GET /api/v1/agenda`
- `POST /api/v1/agenda`
- `PUT /api/v1/agenda/:id`
- `GET /api/v1/clientes`
- `POST /api/v1/clientes/:id/prontuario`
- `GET /api/v1/financeiro/receitas`
- `POST /api/v1/financeiro/conciliacoes/importacao`

### Principios de Manutencao

- cada modulo com responsabilidade unica;
- separacao clara entre regra de negocio e acesso a dados;
- validacoes centralizadas;
- controle de permissao por papel (RBAC) e por acao;
- versionamento de API para evolucao sem quebra.

## Modulos do ERP SaaS

1. Agenda Inteligente
2. Clientes + Prontuario Dinamico
3. Orcamentos
4. Vendas e PDV
5. Faturamento
6. Emissao de NFe
7. Financeiro (receitas, despesas, contas, fluxo de caixa)
8. Bancos e Conciliacao
9. Relatorios
10. Estoque
11. CRM completo
12. Configuracoes da empresa e personalizacao de campos

## Diferenciais do Produto

- Multiempresa (SaaS real, isolado por tenant)
- Prontuario configuravel por clinica
- Agenda flexivel por profissional ou sala
- Pronto para nichos relacionados (lashing e manicure)
- Base arquitetural preparada para crescimento e integracoes

## Roadmap Inicial

O roteiro detalhado de execucao esta no arquivo `ESCOPO_ROTEIRO.md`.

## Base de Referencia

A pasta `Barbearia_Premium` foi analisada como referencia funcional para:

- agenda;
- CRM;
- financeiro;
- estoque;
- faturamento;
- emissao de nota;
- permissoes e logs.

As funcionalidades maduras dessa base serao reaproveitadas com nova identidade visual, novos fluxos e adaptacao para o segmento de estetica.

## Fase 0 - Entrega Tecnica

Pastas criadas e padronizadas:

- `backend`
- `frontend`
- `database`
- `docs`

Recursos entregues nesta fase:

- API Node/Express nova, versionada e com Swagger;
- login multi-tenant inicial;
- health check de API e banco;
- migracoes e seed inicial para PostgreSQL;
- padroes de codigo (Prettier, ESLint, Husky);
- documentacao operacional para VPS/Nginx/PM2.

## Como subir local com um comando base

1. Suba o PostgreSQL:
   - `docker compose up -d postgres`
2. Instale dependencias:
   - `npm install`
3. Crie o arquivo `backend/.env` com base em `backend/.env.example`
4. Rode estrutura inicial:
   - `npm run migrate && npm run seed`
5. Suba a API:
   - `npm run dev`

Endpoints de validacao:

- `http://localhost:3001/health`
- `http://localhost:3001/health/db`
- `http://localhost:3001/docs`

Credencial seed inicial:

- tenant: `dracamilacapeli`
- email: `admin@dracamilacapeli.com.br`
- senha: `123456`



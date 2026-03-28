# Plano de Desenvolvimento — Sistema de Orçamento e Controle de Obras

## Visão Geral

O sistema será dividido em **2 áreas principais**:

### 1. Orçamentos
- Criar orçamentos para clientes
- Selecionar materiais e serviços
- Calcular totais automaticamente
- Gerar PDF para envio
- Listar orçamentos enviados

### 2. Obras em Andamento
- Cadastrar obras aprovadas/em execução
- Lançar custos diários
- Lançar valores recebidos
- Acompanhar custo semanal, total gasto, total recebido e saldo

---

## Objetivo do Produto

Criar um sistema simples, rápido e prático para:
- montar orçamentos com agilidade
- reutilizar uma base de materiais e serviços
- gerar PDF profissional para envio ao cliente
- controlar custos reais da obra após aprovação do orçamento

---

## Arquitetura Definida

A arquitetura será separada em **2 mundos independentes**, com responsabilidades bem definidas:

### Front-end
- **Next.js**
- **TypeScript**
- **TailwindCSS**
- **shadcn/ui**

Responsável por:
- interface do usuário
- formulários
- listagens
- navegação
- dashboard
- geração de experiência rápida e fluida

### Back-end
- **Flask API**

Responsável por:
- autenticação
- regras de negócio
- cálculos
- persistência de dados
- geração de PDF
- endpoints REST

### Banco de Dados
Pode usar:
- **PostgreSQL** como principal opção
- ou **MySQL**, se preferir

### Acesso ao banco
- **Sem ORM**
- acesso via SQL direto ou camada de repositório
- separação clara entre controller, service e repository

---

## Benefícios dessa arquitetura

- separa totalmente front-end e back-end
- facilita manutenção
- permite evoluir API sem depender da interface
- facilita uso futuro de app mobile
- reduz acoplamento entre regras de negócio e telas
- deixa o back-end mais previsível para cálculos e relatórios

---

## Estrutura sugerida do projeto

## Front-end — Next.js

### Responsabilidades
- login e cadastro
- dashboard
- cadastro de orçamento
- listagem de orçamentos
- cadastro de obras
- resumo de custos
- consumo da API Flask

### Estrutura sugerida
```txt
/src
  /app
  /components
  /features
    /auth
    /clients
    /materials
    /services
    /budgets
    /projects
  /lib
    /api
    /utils
    /validators
  /types

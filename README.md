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

## Tecnologias Definidas

- **Next.js**
- **TypeScript**
- **TailwindCSS**
- **shadcn/ui**

### Sugestões complementares
- **Prisma** para ORM
- **PostgreSQL** para banco de dados
- **NextAuth** para autenticação
- **React Hook Form + Zod** para formulários e validação
- **react-pdf** ou **pdf-lib** para geração de PDF
- **TanStack Table** para listagens e tabelas

---

## Módulos do Sistema

## 1. Autenticação

### Telas
- Login
- Cadastro
- Recuperar senha

### Funcionalidades
- Criar conta
- Fazer login
- Proteger rotas privadas
- Cada usuário acessa apenas seus próprios dados

---

## 2. Dashboard

A dashboard deve ser objetiva e útil.

### Indicadores sugeridos
- Total de orçamentos no mês
- Total de orçamentos aprovados
- Total de obras em andamento
- Custo da semana
- Valor recebido na semana
- Saldo geral das obras

### Listas rápidas
- Últimos orçamentos criados
- Últimas obras em andamento

---

## 3. Cadastro de Orçamento

### Fluxo
1. Criar novo orçamento
2. Informar dados iniciais
3. Adicionar materiais
4. Adicionar serviços / mão de obra
5. Informar prazo previsto
6. Calcular total
7. Informar nome e telefone do cliente
8. Gerar PDF
9. Salvar orçamento na listagem

### Campos da tela
- Nome do cliente
- Telefone
- Título do orçamento
- Data
- Descrição geral do serviço
- Prazo previsto
- Lista de materiais
- Lista de serviços
- Observações
- Valor total

---

## 4. Base de Dados de Materiais

### Objetivo
Criar uma base reutilizável de materiais para que o usuário possa digitar, filtrar, selecionar e calcular rapidamente.

### Campos do material
- Nome
- Categoria
- Unidade
- Preço de referência (opcional)
- Status ativo/inativo

### Unidades sugeridas
- saco
- metro
- metro²
- metro³
- kilo
- grama
- litro
- unidade
- caixa
- barra
- rolo

### Funcionamento na tela
- Usuário começa a digitar
- Sistema filtra materiais da base
- Usuário seleciona um item
- Informa quantidade
- Informa valor unitário
- Sistema calcula subtotal automaticamente

### Exemplo
- Material: Cimento CP2
- Unidade: saco
- Quantidade: 20
- Valor unitário: 39,90
- Subtotal: 798,00

### Regra importante
Ao salvar no orçamento, os itens devem ser copiados como snapshot:
- nome do material
- unidade
- preço
- quantidade

Isso evita problemas caso o cadastro base seja alterado depois.

---

## 5. Base de Serviços / Mão de Obra

### Objetivo
Permitir seleção rápida de serviços a partir de uma base, mas com liberdade para inserir texto manual caso não exista.

### Campos do serviço
- Nome / descrição
- Categoria
- Unidade de cobrança (opcional)
- Preço sugerido (opcional)
- Status ativo/inativo

### Funcionamento
- Usuário digita
- Sistema busca na base
- Se encontrar, usuário seleciona
- Se não encontrar, pode usar o texto digitado manualmente

### Exemplos de serviços
- Reboco de parede
- Assentamento de piso
- Pintura interna
- Instalação elétrica
- Troca de telhado

### Campos do item no orçamento
- Descrição
- Quantidade (opcional)
- Unidade (opcional)
- Valor
- Observação
- Subtotal

---

## Estrutura do Orçamento

O orçamento deve ser dividido em 2 grupos:

### Materiais
- Nome
- Unidade
- Quantidade
- Valor unitário
- Subtotal

### Serviços / Mão de Obra
- Descrição
- Quantidade (opcional)
- Unidade (opcional)
- Valor
- Observação
- Subtotal

### Totais
- Total de materiais
- Total de mão de obra
- Desconto (opcional)
- Acréscimo (opcional)
- Total geral

---

## 6. Geração de PDF

### Objetivo
Gerar um PDF limpo e profissional para envio ao cliente.

### Conteúdo do PDF
- Nome da empresa/profissional
- Telefone / contato
- Nome do cliente
- Telefone do cliente
- Data
- Número do orçamento
- Descrição do serviço
- Prazo previsto
- Lista de materiais
- Total de materiais
- Lista de mão de obra / serviços
- Total de mão de obra
- Total geral
- Observações finais

### Estrutura visual sugerida
1. Cabeçalho
2. Dados do cliente
3. Descrição do serviço
4. Tabela de materiais
5. Tabela de mão de obra
6. Resumo financeiro
7. Prazo e observações
8. Rodapé

---

## 7. Listagem de Orçamentos

### Objetivo
Ter uma tela com todos os orçamentos enviados e um pequeno painel resumo.

### Campos da listagem
- Nome do cliente
- Telefone
- Data do orçamento
- Valor total
- Status
- Prazo
- Botão visualizar
- Botão gerar PDF novamente
- Botão duplicar

### Status sugeridos
- rascunho
- enviado
- aprovado
- recusado
- convertido em obra

### Painel no topo
- Total enviados
- Total aprovados
- Valor total orçado no mês
- Orçamento mais recente

### Clique no orçamento
Ao clicar em um orçamento, exibir:
- Nome do cliente
- Data
- Valor
- Itens de materiais
- Itens de serviços
- Observações
- Ações disponíveis

---

## 8. Obras em Andamento

### Objetivo
Após aprovação do orçamento, permitir o controle financeiro da obra.

### Fluxo
1. Selecionar orçamento aprovado ou criar obra manual
2. Cadastrar obra
3. Lançar custos diários
4. Lançar recebimentos
5. Acompanhar resumo financeiro

### Dados da obra
- Nome da obra
- Cliente
- Telefone
- Endereço (opcional)
- Data de início
- Prazo previsto
- Orçamento vinculado (opcional)
- Valor previsto
- Status

### Status sugeridos
- em andamento
- pausada
- concluída
- cancelada

---

## 9. Cadastro de Custos Diários

### Objetivo
Controlar gastos reais da obra.

### Categorias sugeridas
- material
- mão de obra
- transporte
- alimentação
- aluguel de equipamento
- outros

### Campos
- Data
- Obra
- Categoria
- Descrição
- Valor
- Observação
- Comprovante (opcional)

### Indicadores calculados
- Custo do dia
- Custo da semana
- Custo do mês
- Custo total da obra

---

## 10. Controle de Valores Recebidos

### Objetivo
Controlar entradas financeiras da obra.

### Campos
- Data
- Obra
- Valor recebido
- Forma de pagamento
- Observação

### Indicadores
- Total orçado
- Total recebido
- Total gasto
- Saldo atual
- Lucro previsto
- Lucro parcial

---

## 11. Tela de Resumo da Obra

Ao selecionar uma obra, mostrar um painel resumido.

### Cards
- Valor orçado
- Total recebido
- Total gasto
- Saldo
- Custo da semana

### Seções
- Últimos custos lançados
- Últimos recebimentos
- Comparação entre previsto e realizado
- Custos mais recorrentes

---

## Estrutura de Navegação

### Menu lateral sugerido
- Dashboard
- Orçamentos
- Novo orçamento
- Obras em andamento
- Custos diários
- Recebimentos
- Materiais
- Serviços
- Clientes
- Configurações

---

## Estrutura de Páginas

### Públicas
- `/login`
- `/cadastro`

### Privadas
- `/dashboard`
- `/orcamentos`
- `/orcamentos/novo`
- `/orcamentos/[id]`
- `/obras`
- `/obras/[id]`
- `/materiais`
- `/servicos`
- `/clientes`
- `/configuracoes`

---

## Modelagem Inicial do Banco de Dados

## Tabela `users`
- id
- name
- email
- password_hash
- created_at

## Tabela `clients`
- id
- user_id
- name
- phone
- created_at

## Tabela `materials`
- id
- user_id
- name
- category
- unit
- default_price
- is_active
- created_at

## Tabela `services`
- id
- user_id
- name
- category
- default_price
- is_active
- created_at

## Tabela `budgets`
- id
- user_id
- client_id
- title
- description
- expected_deadline
- status
- total_materials
- total_services
- discount
- addition
- total_amount
- pdf_url
- created_at

## Tabela `budget_material_items`
- id
- budget_id
- material_id (opcional)
- material_name
- unit
- quantity
- unit_price
- subtotal

## Tabela `budget_service_items`
- id
- budget_id
- service_id (opcional)
- service_name
- quantity (opcional)
- unit (opcional)
- unit_price
- subtotal
- notes (opcional)

## Tabela `projects`
- id
- user_id
- budget_id (opcional)
- client_id
- name
- status
- start_date
- expected_end_date
- estimated_value
- created_at

## Tabela `project_costs`
- id
- project_id
- date
- category
- description
- amount
- notes

## Tabela `project_incomes`
- id
- project_id
- date
- amount
- payment_method
- notes

---

## Regras de Negócio Importantes

### 1. Snapshot dos itens
Ao salvar o orçamento, copiar:
- nome do material/serviço
- unidade
- preço
- quantidade

### 2. Orçamento pode virar obra
Um orçamento aprovado pode ser convertido em obra com um clique.

### 3. Cálculos automáticos
O sistema deve recalcular sempre:
- subtotal por item
- total de materiais
- total de serviços
- total geral

### 4. Busca inteligente
Materiais e serviços precisam ter:
- busca por nome
- filtro rápido
- opção de cadastro rápido

### 5. Histórico
Guardar:
- data de criação
- data de envio
- status
- alterações principais

---

## Fluxo Ideal do Usuário

## Fluxo de orçamento
1. Entrar no sistema
2. Criar orçamento
3. Selecionar cliente ou cadastrar
4. Adicionar materiais
5. Adicionar serviços
6. Revisar total
7. Informar prazo
8. Gerar PDF
9. Marcar como enviado

## Fluxo da obra
1. Aprovar orçamento
2. Converter em obra
3. Lançar custos diários
4. Lançar recebimentos
5. Acompanhar saldo e custo semanal

---

## Melhorias de UX para Deixar o Sistema Ágil

### 1. Busca com autocomplete
Materiais e serviços devem aparecer enquanto o usuário digita.

### 2. Cadastro rápido inline
Se o item não existir:
- usar texto digitado
- ou cadastrar novo sem sair da tela

### 3. Cálculo instantâneo
Quantidade e valor devem atualizar subtotal em tempo real.

### 4. Resumo fixo na lateral
Na tela de orçamento, mostrar sempre:
- total materiais
- total mão de obra
- total geral

### 5. Duplicar orçamento
Permitir duplicar orçamentos para ganhar velocidade.

---

## MVP Recomendado

### Fase 1 — MVP
- Login e cadastro
- Dashboard básica
- Cadastro de clientes
- Base de materiais
- Base de serviços
- Criação de orçamento
- Cálculo automático
- Geração de PDF
- Listagem de orçamentos

### Fase 2
- Converter orçamento em obra
- Cadastro de custos diários
- Cadastro de recebimentos
- Resumo da obra
- Cálculo de custo semanal

### Fase 3
- Relatórios
- Gráficos
- Duplicar orçamento
- Anexos / comprovantes
- Comparação previsto x realizado
- Integração com WhatsApp

---

## Backlog Inicial

## Autenticação
- Criar login
- Criar cadastro
- Proteger rotas privadas

## Clientes
- Cadastrar cliente
- Listar clientes
- Selecionar cliente no orçamento

## Materiais
- CRUD de materiais
- Busca por nome
- Cadastro de unidade e preço padrão

## Serviços
- CRUD de serviços
- Busca por nome
- Inserção manual se não encontrar

## Orçamentos
- Criar orçamento
- Adicionar/remover itens
- Calcular totais
- Salvar rascunho
- Gerar PDF
- Listar orçamentos
- Visualizar orçamento

## Obras
- Criar obra
- Vincular orçamento
- Lançar custos
- Lançar recebimentos
- Calcular custo semanal

---

## Recomendação Final

Começar com este núcleo:

- clientes
- materiais
- serviços
- orçamento
- PDF
- listagem de orçamentos

Depois evoluir para:

- obras em andamento
- custos diários
- recebimentos
- resumo financeiro da obra

Esse caminho reduz a complexidade inicial e entrega valor mais rápido.

---

## Resumo Executivo

O sistema será um app web para orçamento e controle de obras com:

### MVP
- autenticação
- dashboard
- cadastro de clientes
- base de materiais
- base de serviços
- criação de orçamento
- cálculo automático
- geração de PDF
- listagem de orçamentos

### Segunda etapa
- obras em andamento
- custos diários
- recebimentos
- custo semanal
- resumo financeiro da obra

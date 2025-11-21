# 📋 Documentação Completa - Sistema Estacione+

## 📌 Índice
1. [Visão Geral](#visão-geral)
2. [Arquitetura do Sistema](#arquitetura-do-sistema)
3. [Tecnologias Utilizadas](#tecnologias-utilizadas)
4. [Estrutura de Diretórios](#estrutura-de-diretórios)
5. [Banco de Dados](#banco-de-dados)
6. [Funcionalidades](#funcionalidades)
7. [Rotas da Aplicação](#rotas-da-aplicação)
8. [Interface do Usuário](#interface-do-usuário)
9. [Modelos de Dados](#modelos-de-dados)
10. [Segurança](#segurança)
11. [Instalação e Configuração](#instalação-e-configuração)
12. [Como Usar](#como-usar)
13. [Melhorias Futuras](#melhorias-futuras)

---

## 🎯 Visão Geral

**Estacione+** é um sistema completo de gerenciamento de estacionamento desenvolvido em Python com Flask. O sistema permite gerenciar clientes, veículos, planos de assinatura, pagamentos e controle financeiro de forma integrada e eficiente.

### Características Principais
- ✅ Gestão completa de clientes e veículos
- ✅ Sistema de assinaturas mensais por plano
- ✅ Controle financeiro (contas a pagar/receber, fluxo de caixa)
- ✅ Dashboard administrativo com gráficos e estatísticas
- ✅ Relatórios (DRE - Demonstração de Resultado do Exercício)
- ✅ Sistema de autenticação e autorização
- ✅ Interface responsiva e moderna

---

## 🏗️ Arquitetura do Sistema

### Padrão de Arquitetura
O sistema segue o padrão **MVC (Model-View-Controller)** adaptado para Flask:

```
┌─────────────┐
│   Browser   │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────┐
│   Flask Application (app.py)│
│                             │
│  ┌──────────┐  ┌─────────┐ │
│  │  Routes  │  │  Forms  │ │
│  │(Controller)│ │(WTForms)│ │
│  └────┬─────┘  └────┬────┘ │
│       │             │       │
│  ┌────▼──────────┬──▼────┐ │
│  │   Business    │ Filtros│ │
│  │     Logic     │ Jinja2 │ │
│  └────┬──────────┴───┬───┘ │
│       │              │      │
│  ┌────▼────┐    ┌────▼────┐│
│  │ Models  │    │Templates││
│  │(Pandas) │    │ (Jinja2)││
│  └────┬────┘    └─────────┘│
└───────┼──────────────────────┘
        │
   ┌────▼────┐
   │CSV Files│
   │ (data/) │
   └─────────┘
```

### Camadas da Aplicação

#### 1. **Camada de Apresentação (Templates)**
- Templates Jinja2 para renderização HTML
- CSS customizado para estilização
- JavaScript para interatividade (Chart.js)

#### 2. **Camada de Controle (Routes)**
- Definição de rotas e endpoints
- Validação de formulários (Flask-WTF)
- Controle de autenticação e autorização

#### 3. **Camada de Lógica de Negócio**
- Processamento de dados
- Cálculos financeiros
- Validações customizadas

#### 4. **Camada de Dados**
- Armazenamento em CSV usando Pandas
- Funções de CRUD (Create, Read, Update, Delete)

---

## 💻 Tecnologias Utilizadas

### Backend
| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| **Python** | 3.x | Linguagem principal |
| **Flask** | 3.0.0 | Framework web |
| **Pandas** | 2.1.3 | Manipulação de dados |
| **Flask-Login** | 0.6.3 | Gerenciamento de sessões |
| **Flask-WTF** | 1.2.1 | Formulários |
| **WTForms** | 3.1.1 | Validação de formulários |
| **Werkzeug** | 3.0.1 | Segurança (hash de senhas) |

### Frontend
| Tecnologia | Versão | Uso |
|-----------|--------|-----|
| **Bootstrap** | 5.x | Framework CSS |
| **Bootstrap Icons** | - | Ícones |
| **Chart.js** | - | Gráficos interativos |
| **JavaScript** | ES6 | Interatividade |

### Bibliotecas Auxiliares
- **python-dateutil** 2.8.2 - Manipulação de datas
- **numpy** 1.26.2 - Cálculos numéricos
- **openpyxl** 3.1.2 - Exportação para Excel
- **plotly** 5.18.0 - Visualizações avançadas

---

## 📁 Estrutura de Diretórios

```
ProjetoCaio/
│
├── app.py                      # Aplicação principal Flask
├── requirements.txt            # Dependências Python
│
├── data/                       # Banco de dados (CSV)
│   ├── accounts_payable.csv    # Contas a pagar
│   ├── accounts_receivable.csv # Contas a receber
│   ├── cash_flow.csv           # Fluxo de caixa
│   ├── customers.csv           # Clientes
│   ├── financial_transactions.csv # Transações
│   ├── payments.csv            # Pagamentos
│   ├── plans.csv               # Planos de assinatura
│   ├── revenue_categories.csv  # Categorias de receita
│   ├── subscriptions.csv       # Assinaturas
│   ├── users.csv               # Usuários do sistema
│   ├── vehicles.csv            # Veículos
│   ├── vehicle_documents.csv   # Documentos de veículos
│   ├── vehicle_history.csv     # Histórico de alterações
│   ├── vehicle_movements.csv   # Movimentações (entrada/saída)
│   └── vehicle_services.csv    # Serviços realizados
│
├── static/                     # Arquivos estáticos
│   └── css/
│       └── custom.css          # Estilos customizados
│
└── templates/                  # Templates HTML (Jinja2)
    ├── base.html               # Template base
    ├── login.html              # Login (legado)
    │
    ├── admin/                  # Área administrativa
    │   ├── dashboard.html      # Dashboard principal
    │   │
    │   ├── customers/          # Gerenciamento de clientes
    │   │   ├── form.html       # Formulário add/edit
    │   │   ├── form_old_backup.html
    │   │   └── list.html       # Listagem
    │   │
    │   ├── vehicles/           # Gerenciamento de veículos
    │   │   ├── form.html       # Formulário add/edit
    │   │   ├── list.html       # Listagem
    │   │   └── view.html       # Visualização detalhada
    │   │
    │   ├── plans/              # Gerenciamento de planos
    │   │   ├── form.html       # Formulário add/edit
    │   │   └── list.html       # Listagem
    │   │
    │   ├── subscriptions/      # Gerenciamento de assinaturas
    │   │   ├── form.html       # Formulário add/edit
    │   │   └── list.html       # Listagem
    │   │
    │   ├── financial/          # Área financeira
    │   │   ├── accounts_payable.html    # Contas a pagar
    │   │   ├── accounts_receivable.html # Contas a receber
    │   │   └── cash_flow.html           # Fluxo de caixa
    │   │
    │   └── reports/            # Relatórios
    │       └── dre.html        # Demonstração de Resultado
    │
    ├── auth/                   # Autenticação
    │   └── login.html          # Página de login
    │
    └── customer/               # Área do cliente
        └── dashboard.html      # Dashboard do cliente
```

---

## 🗄️ Banco de Dados

O sistema utiliza **arquivos CSV** como banco de dados, gerenciados pela biblioteca **Pandas**.

### Estrutura das Tabelas

#### 1. **users.csv** - Usuários do Sistema
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- username: STRING
- password_hash: STRING
- role: STRING (admin/customer)
- name: STRING
- created_at: DATETIME
- updated_at: DATETIME
```

#### 2. **customers.csv** - Clientes
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- name: STRING
- email: STRING
- phone: STRING
- phone2: STRING (opcional)
- cpf: STRING (UNIQUE)
- rg: STRING
- birth_date: DATE
- cep: STRING
- street: STRING
- number: STRING
- complement: STRING
- neighborhood: STRING
- city: STRING
- state: STRING (UF)
- address: STRING (legado)
- notes: TEXT
- status: STRING (ativo/inativo/inadimplente)
- created_at: DATETIME
- updated_at: DATETIME
```

#### 3. **vehicles.csv** - Veículos
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- customer_id: INTEGER (FOREIGN KEY → customers.id)
- plate: STRING (UNIQUE)
- brand: STRING
- model: STRING
- color: STRING
- year: INTEGER
- type: STRING (carro/moto/utilitario)
- renavam: STRING
- chassis: STRING
- notes: TEXT
- status: STRING (ativo/inativo)
- created_at: DATETIME
- updated_at: DATETIME
```

#### 4. **plans.csv** - Planos de Assinatura
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- name: STRING
- description: TEXT
- price: DECIMAL
- duration_days: INTEGER
- is_active: BOOLEAN
- created_at: DATETIME
- updated_at: DATETIME
```

#### 5. **subscriptions.csv** - Assinaturas
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- customer_id: INTEGER (FOREIGN KEY → customers.id)
- vehicle_id: INTEGER (FOREIGN KEY → vehicles.id)
- plan_id: INTEGER (FOREIGN KEY → plans.id)
- amount: DECIMAL
- start_date: DATE
- end_date: DATE
- status: STRING (ativa/inativa/cancelada)
- created_at: DATETIME
```

#### 6. **payments.csv** - Pagamentos
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- subscription_id: INTEGER (FOREIGN KEY → subscriptions.id)
- amount: DECIMAL
- payment_date: DATE
- payment_method: STRING
- status: STRING (pendente/pago/cancelado)
- created_at: DATETIME
```

#### 7. **financial_transactions.csv** - Transações Financeiras
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- description: STRING
- amount: DECIMAL
- date: DATE
- category: STRING
- type: STRING (receita/despesa)
- related_id: INTEGER (opcional)
- created_at: DATETIME
```

#### 8. **accounts_receivable.csv** - Contas a Receber
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- subscription_id: INTEGER (FOREIGN KEY)
- customer_id: INTEGER (FOREIGN KEY)
- description: STRING
- amount: DECIMAL
- due_date: DATE
- payment_date: DATE (opcional)
- status: STRING (pendente/pago/vencido)
- payment_method: STRING
- notes: TEXT
- created_at: DATETIME
- updated_at: DATETIME
```

#### 9. **accounts_payable.csv** - Contas a Pagar
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- supplier: STRING
- description: STRING
- category: STRING
- amount: DECIMAL
- due_date: DATE
- payment_date: DATE (opcional)
- status: STRING (pendente/pago/vencido)
- payment_method: STRING
- notes: TEXT
- created_at: DATETIME
- updated_at: DATETIME
```

#### 10. **vehicle_movements.csv** - Movimentações de Veículos
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- vehicle_id: INTEGER (FOREIGN KEY)
- user_id: INTEGER (FOREIGN KEY)
- date_time: DATETIME
- type: STRING (entrada/saida)
- notes: TEXT
```

#### 11. **vehicle_services.csv** - Serviços em Veículos
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- vehicle_id: INTEGER (FOREIGN KEY)
- date: DATE
- description: STRING
- cost: DECIMAL
- provider: STRING
```

#### 12. **vehicle_documents.csv** - Documentos de Veículos
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- vehicle_id: INTEGER (FOREIGN KEY)
- document_type: STRING
- expiration_date: DATE
- notes: TEXT
```

#### 13. **vehicle_history.csv** - Histórico de Alterações
```csv
Campos:
- id: INTEGER (PRIMARY KEY)
- vehicle_id: INTEGER (FOREIGN KEY)
- user_id: INTEGER (FOREIGN KEY)
- action: STRING
- changes: JSON
- created_at: DATETIME
```

---

## ⚙️ Funcionalidades

### 🔐 Sistema de Autenticação

#### Login
- Validação de credenciais
- Hash de senha com PBKDF2-SHA256
- Gerenciamento de sessão com Flask-Login
- Redirecionamento baseado em role (admin/customer)

#### Controle de Acesso
- Decorator `@login_required` para rotas protegidas
- Decorator `@admin_required` para área administrativa
- Separação de interfaces (admin vs cliente)

---

### 👥 Gerenciamento de Clientes

#### Listagem
- **Rota:** `/admin/customers`
- **Funcionalidades:**
  - Visualização de todos os clientes
  - Busca por nome, CPF ou placa de veículo
  - Filtro por status (ativo/inativo/inadimplente)
  - Exibição de veículos vinculados
  - Formatação automática de CPF, telefone, CEP

#### Cadastro/Edição
- **Rotas:** `/admin/customers/add`, `/admin/customers/edit/<id>`
- **Validações:**
  - CPF único no sistema
  - Email válido
  - Telefone obrigatório
  - CEP no formato brasileiro
  - Estado (UF) válido
- **Campos:**
  - Dados pessoais (nome, CPF, RG, data de nascimento)
  - Contatos (email, telefone 1 e 2)
  - Endereço completo (CEP, rua, número, complemento, bairro, cidade, estado)
  - Observações
  - Status

#### Exclusão
- **Rota:** `/admin/customers/delete/<id>`
- **Validação:** Impede exclusão se houver veículos vinculados

---

### 🚗 Gerenciamento de Veículos

#### Listagem
- **Rota:** `/admin/vehicles`
- **Funcionalidades:**
  - Visualização com nome do proprietário
  - Ordenação e filtros
  - Link para visualização detalhada

#### Cadastro/Edição
- **Rotas:** `/admin/vehicles/add`, `/admin/vehicles/edit/<id>`
- **Validações:**
  - Placa única
  - Cliente válido
  - Campos obrigatórios: placa, marca, modelo, cor
- **Campos:**
  - Proprietário (cliente)
  - Placa (formatação automática)
  - Marca e modelo
  - Cor (com seletor visual)
  - Ano de fabricação
  - Tipo (carro/moto/utilitário)
  - RENAVAM e Chassi
  - Observações
  - Status

#### Visualização Detalhada
- **Rota:** `/admin/vehicles/view/<id>`
- **Informações Exibidas:**
  - Dados completos do veículo
  - Informações do proprietário
  - Fotos do veículo
  - Histórico de movimentações (entrada/saída)
  - Serviços realizados
  - Documentos vinculados
  - Histórico de alterações

#### Exclusão
- **Rota:** `/admin/vehicles/delete/<id>`
- **Validação:** Impede exclusão se houver assinatura ativa

---

### 📋 Gerenciamento de Planos

#### Listagem
- **Rota:** `/admin/plans`
- **Funcionalidades:**
  - Visualização de todos os planos
  - Indicador de plano ativo/inativo
  - Botão de ativação/desativação rápida

#### Cadastro/Edição
- **Rotas:** `/admin/plans/add`, `/admin/plans/edit/<id>`
- **Validações:**
  - Nome único
  - Preço válido (maior que zero)
  - Duração em dias
- **Campos:**
  - Nome do plano
  - Descrição
  - Preço mensal
  - Duração em dias
  - Status (ativo/inativo)

#### Ativação/Desativação
- **Rota:** `/admin/plans/toggle/<id>`
- Alterna status do plano sem exclusão

---

### 📝 Gerenciamento de Assinaturas

#### Listagem
- **Rota:** `/admin/subscriptions`
- **Funcionalidades:**
  - Visualização com cliente, veículo e plano
  - Indicador de assinatura ativa/vencida
  - Total de receita mensal
  - Modal para cadastro rápido

#### Cadastro/Edição
- **Rotas:** `/admin/subscriptions/add`, `/admin/subscriptions/edit/<id>`
- **Validações:**
  - Veículo pertence ao cliente selecionado
  - Plano ativo
  - Data de início válida
- **Cálculos Automáticos:**
  - Data de término baseada na duração do plano
  - Valor da assinatura igual ao preço do plano
- **Campos:**
  - Cliente (dropdown)
  - Veículo (filtrado por cliente)
  - Plano (apenas planos ativos)
  - Data de início
  - Status

#### Exclusão
- **Rota:** `/admin/subscriptions/delete/<id>`
- Remove assinatura

---

### 💰 Módulo Financeiro

#### Contas a Receber
- **Rota:** `/admin/financial/accounts-receivable`
- **Geração Automática:**
  - Cria conta a receber para cada assinatura
  - Atualiza status (pendente/pago/vencido)
- **Funcionalidades:**
  - Filtro por status
  - Registro de pagamento
  - Totalizadores (pendente, pago, vencido)
- **Registro de Pagamento:**
  - Rota: `/admin/financial/accounts-receivable/<id>/receive`
  - Registra pagamento
  - Atualiza status para "pago"
  - Cria transação financeira automaticamente

#### Contas a Pagar
- **Rota:** `/admin/financial/accounts-payable`
- **Funcionalidades:**
  - Cadastro de despesas
  - Filtro por status
  - Registro de pagamento
  - Totalizadores
- **Cadastro:**
  - Rota: `/admin/financial/accounts-payable/add`
  - Fornecedor, descrição, categoria
  - Valor e data de vencimento
- **Registro de Pagamento:**
  - Rota: `/admin/financial/accounts-payable/<id>/pay`
  - Marca como pago
  - Cria transação de despesa

#### Fluxo de Caixa
- **Rota:** `/admin/financial/cash-flow`
- **Funcionalidades:**
  - Consolidação de receitas e despesas
  - Separação por status (realizado/previsto/vencido)
  - Gráfico de evolução (últimos 30 dias)
  - Cálculo de saldo atual
- **Dados Exibidos:**
  - Saldo atual
  - Entradas do mês (realizadas)
  - Saídas do mês (realizadas)
  - Entradas previstas
  - Saídas previstas
  - Valores vencidos

---

### 📊 Dashboard Administrativo

#### Estatísticas Principais
- **Rota:** `/admin`
- **Cards de Resumo:**
  1. **Clientes Ativos:** Total de clientes cadastrados
  2. **Receita Mensal:** Soma das receitas do mês atual
  3. **Vencimentos Hoje:** Assinaturas que vencem hoje
  4. **Veículos Cadastrados:** Total de veículos

#### Gráficos Interativos
1. **Gráfico Financeiro (Linha):**
   - Receitas vs Despesas
   - Últimos 6 meses
   - Biblioteca: Chart.js

2. **Gráfico de Planos (Rosca):**
   - Distribuição de assinaturas por plano
   - Apenas planos ativos

#### Últimas Movimentações
- Listagem das 5 transações mais recentes
- Informações: data, cliente, descrição, valor, status
- Link para fluxo de caixa completo

---

### 📈 Relatórios

#### DRE (Demonstração de Resultado do Exercício)
- **Rota:** `/admin/reports/dre`
- **Funcionalidades:**
  - Seleção de ano
  - Receita bruta por categoria
  - Despesas detalhadas por categoria
  - Resultado líquido (receita - despesa)
  - Gráfico de evolução mensal
  - Gráficos de pizza (receitas e despesas)

---

### 🔧 Filtros Jinja2 Customizados

O sistema possui filtros personalizados para formatação de dados:

```python
@app.template_filter('format_cpf')
def format_cpf_filter(cpf):
    """Formata CPF: 123.456.789-00"""
    
@app.template_filter('format_phone')
def format_phone_filter(phone):
    """Formata telefone: (11) 98765-4321"""
    
@app.template_filter('format_cep')
def format_cep_filter(cep):
    """Formata CEP: 12345-678"""
    
@app.template_filter('format_currency')
def format_currency_filter(value):
    """Formata valor monetário: R$ 1.234,56"""
    
@app.template_filter('format_date')
def format_date_filter(date):
    """Formata data: 20/11/2025"""
    
@app.template_filter('format_datetime')
def format_datetime_filter(datetime_obj):
    """Formata data e hora: 20/11/2025 14:30"""
```

---

## 🛣️ Rotas da Aplicação

### Autenticação
| Rota | Método | Descrição |
|------|--------|-----------|
| `/login` | GET, POST | Página de login |
| `/logout` | GET | Logout do usuário |

### Dashboard
| Rota | Método | Descrição |
|------|--------|-----------|
| `/` | GET | Redireciona para dashboard |
| `/admin` | GET | Dashboard administrativo |
| `/dashboard` | GET | Dashboard do cliente |

### Clientes
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/customers` | GET | Lista clientes |
| `/admin/customers/add` | GET, POST | Adiciona cliente |
| `/admin/customers/edit/<id>` | GET, POST | Edita cliente |
| `/admin/customers/delete/<id>` | POST | Exclui cliente |

### Veículos
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/vehicles` | GET | Lista veículos |
| `/admin/vehicles/add` | GET, POST | Adiciona veículo |
| `/admin/vehicles/edit/<id>` | GET, POST | Edita veículo |
| `/admin/vehicles/delete/<id>` | POST | Exclui veículo |
| `/admin/vehicles/view/<id>` | GET | Visualiza detalhes |

### Planos
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/plans` | GET | Lista planos |
| `/admin/plans/add` | GET, POST | Adiciona plano |
| `/admin/plans/edit/<id>` | GET, POST | Edita plano |
| `/admin/plans/toggle/<id>` | POST | Ativa/desativa plano |

### Assinaturas
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/subscriptions` | GET | Lista assinaturas |
| `/admin/subscriptions/add` | GET, POST | Adiciona assinatura |
| `/admin/subscriptions/edit/<id>` | GET, POST | Edita assinatura |
| `/admin/subscriptions/delete/<id>` | POST | Exclui assinatura |

### Financeiro
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/financial/accounts-receivable` | GET | Contas a receber |
| `/admin/financial/accounts-receivable/<id>/receive` | POST | Registra recebimento |
| `/admin/financial/accounts-payable` | GET | Contas a pagar |
| `/admin/financial/accounts-payable/add` | POST | Adiciona conta a pagar |
| `/admin/financial/accounts-payable/<id>/pay` | POST | Registra pagamento |
| `/admin/financial/cash-flow` | GET | Fluxo de caixa |

### Relatórios
| Rota | Método | Descrição |
|------|--------|-----------|
| `/admin/reports/dre` | GET | Relatório DRE |

### API
| Rota | Método | Descrição |
|------|--------|-----------|
| `/api/vehicles/by_customer/<id>` | GET | Veículos por cliente (JSON) |

---

## 🎨 Interface do Usuário

### Design System

#### Paleta de Cores
```css
--color-primary: #2c3e50;      /* Azul escuro principal */
--color-secondary: #34495e;    /* Azul escuro secundário */
--color-accent: #3498db;       /* Azul de destaque */
--color-success: #27ae60;      /* Verde sucesso */
--color-warning: #f39c12;      /* Laranja aviso */
--color-danger: #e74c3c;       /* Vermelho perigo */
--color-light: #ecf0f1;        /* Cinza claro */
--color-dark: #2c3e50;         /* Azul escuro */
--color-white: #ffffff;        /* Branco */
```

#### Tipografia
- **Fonte Principal:** Inter, Segoe UI, -apple-system, BlinkMacSystemFont
- **Tamanhos:**
  - H1: 2.25rem (36px)
  - H2: 1.875rem (30px)
  - H3: 1.5rem (24px)
  - H4: 1.25rem (20px)
  - Body: 15px

#### Componentes

##### Cards
- Bordas arredondadas (12px)
- Sombra suave
- Hover com elevação
- Header com gradiente

##### Botões
- Bordas arredondadas (8px)
- Gradientes coloridos
- Animação de hover (translateY)
- Peso de fonte: 600

##### Tabelas
- Header com fundo cinza claro
- Hover nas linhas
- Bordas suaves
- Responsivas

##### Formulários
- Inputs com borda cinza
- Focus com borda azul
- Labels em negrito
- Placeholders suaves

---

## 📦 Modelos de Dados

### User (Usuário)
```python
class User(UserMixin):
    def __init__(self, id, username, role, name=''):
        self.id = id
        self.username = username
        self.role = role
        self.name = name
```

### Funções Auxiliares
```python
def get_user_by_id(user_id)
def get_customer_by_id(customer_id)
def get_vehicle_by_id(vehicle_id)
def get_plan_by_id(plan_id)
def get_subscription_by_id(subscription_id)
def get_financial_summary()
def get_next_id(filename)
```

---

## 🔒 Segurança

### Hash de Senhas
- **Algoritmo:** PBKDF2-SHA256
- **Biblioteca:** Werkzeug Security
- **Função:** `generate_password_hash()` e `check_password_hash()`

```python
from werkzeug.security import generate_password_hash, check_password_hash

# Geração de hash
password_hash = generate_password_hash('senha123', method='pbkdf2:sha256')

# Verificação
check_password_hash(password_hash, 'senha123')  # True/False
```

### Proteção de Rotas
```python
from functools import wraps
from flask_login import login_required, current_user

# Decorador para rotas protegidas
@login_required
def protected_route():
    pass

# Decorador para rotas administrativas
@admin_required
def admin_route():
    if current_user.role != 'admin':
        flash('Acesso negado', 'danger')
        return redirect(url_for('index'))
    pass
```

### Validações de Formulário
- **CSRF Protection:** Flask-WTF automático
- **Validadores WTForms:**
  - DataRequired()
  - Email()
  - Length(min, max)
  - NumberRange(min, max)
  - Optional()

### Secret Key
```python
app.config['SECRET_KEY'] = 'sua-chave-secreta-aqui'
```
⚠️ **Importante:** Em produção, usar variável de ambiente.

---

## 🚀 Instalação e Configuração

### Pré-requisitos
- Python 3.8 ou superior
- pip (gerenciador de pacotes)

### Passo a Passo

#### 1. Clone ou baixe o projeto
```bash
cd ProjetoCaio
```

#### 2. Crie um ambiente virtual (recomendado)
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

#### 3. Instale as dependências
```bash
pip install -r requirements.txt
```

#### 4. Configure a Secret Key
Edite `app.py` e altere:
```python
app.config['SECRET_KEY'] = 'sua-chave-secreta-muito-segura'
```

#### 5. Execute a aplicação
```bash
python app.py
```

#### 6. Acesse no navegador
```
http://localhost:5000
```

### Credenciais Padrão
- **Usuário:** admin
- **Senha:** admin123

⚠️ **Importante:** Altere a senha padrão após o primeiro acesso!

---

## 📖 Como Usar

### Primeiro Acesso

1. **Login:**
   - Acesse http://localhost:5000/login
   - Use as credenciais padrão (admin/admin123)

2. **Dashboard:**
   - Após login, você será redirecionado para o dashboard
   - Visualize as estatísticas principais

### Cadastrar Cliente

1. Clique em "Novo Cliente" no dashboard ou acesse `/admin/customers/add`
2. Preencha os campos obrigatórios:
   - Nome completo
   - Email
   - Telefone
   - CPF
3. Preencha o endereço (opcional mas recomendado)
4. Adicione observações se necessário
5. Clique em "Salvar"

### Cadastrar Veículo

1. Acesse "Veículos" → "Adicionar Veículo"
2. Selecione o cliente proprietário
3. Preencha os dados do veículo:
   - Placa (obrigatório)
   - Marca e modelo
   - Cor, ano, tipo
   - RENAVAM e chassi
4. Clique em "Salvar"

### Criar Plano de Assinatura

1. Acesse "Planos" → "Novo Plano"
2. Defina:
   - Nome do plano
   - Descrição
   - Preço mensal
   - Duração em dias
3. Salve e o plano ficará ativo

### Criar Assinatura

1. Acesse "Assinaturas" → "Nova Assinatura"
2. Selecione:
   - Cliente
   - Veículo (do cliente selecionado)
   - Plano
   - Data de início
3. O sistema calcula automaticamente a data de término
4. Salve a assinatura

### Gerenciar Financeiro

#### Contas a Receber
- São geradas automaticamente das assinaturas
- Clique em "Receber" para marcar como pago
- Informe o método de pagamento

#### Contas a Pagar
- Clique em "Adicionar" para criar uma nova despesa
- Preencha fornecedor, descrição, valor e vencimento
- Clique em "Pagar" quando efetuar o pagamento

#### Fluxo de Caixa
- Visualize consolidado de receitas e despesas
- Acompanhe o saldo atual
- Veja previsões e valores vencidos

### Visualizar Relatórios

#### DRE (Demonstração de Resultado)
1. Acesse "Relatórios" → "DRE"
2. Selecione o ano desejado
3. Visualize:
   - Receitas por categoria
   - Despesas por categoria
   - Resultado líquido
   - Gráficos de evolução

---

## 🔮 Melhorias Futuras

### Curto Prazo
- [ ] Exportação de relatórios em PDF
- [ ] Envio de notificações por email
- [ ] Upload de fotos de veículos
- [ ] Backup automático dos dados
- [ ] Tema escuro (dark mode)

### Médio Prazo
- [ ] Migração para banco de dados relacional (PostgreSQL/MySQL)
- [ ] API RESTful completa
- [ ] Sistema de permissões granulares
- [ ] Dashboard para clientes (área do cliente expandida)
- [ ] Aplicativo mobile (Flutter/React Native)
- [ ] Integração com gateways de pagamento
- [ ] Sistema de mensagens/chat

### Longo Prazo
- [ ] Inteligência artificial para previsão de receitas
- [ ] Sistema de reservas online
- [ ] Integração com sistemas de controle de acesso
- [ ] Câmeras e reconhecimento de placas
- [ ] Multi-tenancy (múltiplas empresas)
- [ ] Blockchain para rastreabilidade
- [ ] IoT para automação do estacionamento

---

## 📝 Notas Técnicas

### Considerações sobre CSV
**Prós:**
- ✅ Simplicidade
- ✅ Fácil visualização
- ✅ Portabilidade
- ✅ Não requer servidor de banco de dados

**Contras:**
- ❌ Performance limitada com muitos dados
- ❌ Sem transações ACID
- ❌ Concorrência limitada
- ❌ Sem integridade referencial nativa

**Recomendação:** Para produção com múltiplos usuários simultâneos, migrar para PostgreSQL, MySQL ou SQLite.

### Escalabilidade
Atual: ~1.000 registros por tabela  
Recomendado: Até ~10.000 registros totais

### Performance
- Pandas é eficiente para DataFrames pequenos
- Índices não são utilizados (limitação do CSV)
- Leitura completa do arquivo em cada operação

---

## 🤝 Contribuindo

### Como Contribuir
1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

### Padrões de Código
- Siga PEP 8 para Python
- Comente código complexo
- Escreva docstrings para funções
- Mantenha funções pequenas e focadas

---

## 📄 Licença

Este projeto é proprietário e foi desenvolvido para uso específico.

---

## 👨‍💻 Autor

**Desenvolvedor:** João Pedro  
**Data de Criação:** 2025  
**Versão Atual:** 1.0.0

---

## 📞 Suporte

Para suporte técnico ou dúvidas:
- Abra uma issue no repositório
- Entre em contato com o desenvolvedor

---

## 🎯 Changelog

### Versão 1.0.0 (Atual)
- ✅ Sistema completo de gerenciamento
- ✅ Dashboard administrativo
- ✅ Módulo financeiro
- ✅ Relatórios (DRE)
- ✅ Interface responsiva
- ✅ Autenticação e autorização

---

## 🏆 Agradecimentos

- Flask Community
- Bootstrap Team
- Chart.js Contributors
- Pandas Developers

---

**Estacione+** - Sistema de Gerenciamento de Estacionamento  
*Desenvolvido com ❤️ em Python*

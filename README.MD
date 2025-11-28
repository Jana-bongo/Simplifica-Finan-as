# 💰 Sistema de Gestão Financeira - Simplifica Finanças

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/flask-3.0-green)](https://flask.palletsprojects.com/)
[![MySQL](https://img.shields.io/badge/mysql-8.0-orange)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/license-MIT-brightgreen)](LICENSE)
[![Tests](https://img.shields.io/badge/tests-15%20passing-success)](tests/)

> Sistema web de controle financeiro pessoal com interface adaptativa (simples/avançada), desenvolvido como projeto A3 de Gestão e Qualidade de Software.

**🌐 Landing Page:** [https://seu-usuario.github.io/gestao-financeira](https://seu-usuario.github.io/gestao-financeira)  
**📹 Demo:** [https://drive.google.com/drive/folders/1HtkiF-c2yeAppkmOtABNJ-BBmmPhVF6T?usp=drive_link](#)

---

## 📑 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Tecnologias](#tecnologias)
- [Arquitetura](#arquitetura)
- [Instalação](#instalação)
- [Uso](#uso)
- [Testes](#testes)
- [Qualidade de Código](#qualidade-de-código)
- [Roadmap](#roadmap)
- [Autores](#autores)
- [Licença](#licença)

---

## 🎯 Sobre o Projeto

O **Simplifica Finanças** é um sistema web desenvolvido para facilitar o controle financeiro pessoal, atendendo tanto usuários iniciantes quanto avançados através de interfaces adaptativas.

### Problema Identificado
- 47% dos brasileiros não controlam suas finanças (SPC Brasil, 2024)
- Ferramentas existentes são complexas demais ou muito simplistas
- Falta de acessibilidade para diferentes perfis de usuários

### Solução Proposta
Sistema com **dois modos de interface**:
- **Modo Simples:** Para idosos, aposentados e iniciantes em tecnologia
- **Modo Avançado:** Para empreendedores e usuários com conhecimento técnico

### Diferenciais
✅ Interface adaptativa sem perda de funcionalidades  
✅ Design responsivo para desktop e mobile  
✅ Exportação em Excel e PDF  
✅ Sistema de metas financeiras com gamificação  
✅ 100% gratuito e open-source  

---

## ⚡ Funcionalidades

### Gerenciamento de Transações
- ✏️ Cadastro de receitas e despesas
- 📊 Categorização automática
- 🗑️ Exclusão com confirmação
- 📅 Filtro por período

### Sistema de Metas
- 🎯 Criação de metas financeiras
- 📈 Acompanhamento de progresso
- 🎨 Personalização de cores
- 🏆 Notificações de conquista

### Relatórios (Modo Avançado)
- 📉 Gráficos de pizza (despesas por categoria)
- 📊 Gráfico de evolução mensal
- 💡 Insights automáticos
- 🔍 Análise de tendências

### Exportação de Dados
- 📗 Exportação em Excel (.xlsx)
- 📕 Exportação em PDF
- 📋 Relatórios personalizados

### Segurança
- 🔐 Autenticação com hash de senha (Werkzeug)
- 🛡️ Proteção CSRF
- 🚪 Sessões seguras
- ✅ Validação de dados server-side

---

## 🛠️ Tecnologias

### Backend
- **Python 3.8+** - Linguagem principal
- **Flask 3.0** - Framework web
- **MySQL 8.0** - Banco de dados relacional
- **Werkzeug** - Hashing de senhas

### Frontend
- **HTML5/CSS3** - Estrutura e estilo
- **Bootstrap 5.3** - Framework CSS
- **JavaScript (Vanilla)** - Interatividade
- **Chart.js 4.4** - Gráficos interativos

### Bibliotecas Python
```txt
Flask==3.0.0
mysql-connector-python==8.2.0
python-dotenv==1.0.0
pandas==2.1.0
openpyxl==3.1.2
fpdf==1.7.2
```

### Ferramentas de Desenvolvimento
- **Git** - Controle de versão
- **pytest** - Framework de testes
- **GitHub Actions** - CI/CD
- **GitHub Pages** - Hospedagem da landing page

---

## 🏗️ Arquitetura

### Estrutura do Projeto
```
gestao-financeira/
│
├── app.py                      # Aplicação Flask principal
├── database.sql                # Script de criação do banco
├── requirements.txt            # Dependências Python
├── .env.example               # Exemplo de variáveis de ambiente
│
├── templates/                  # Templates HTML
│   ├── base.html              # Template base
│   ├── index.html             # Página inicial
│   ├── login.html             # Login
│   ├── registro.html          # Cadastro
│   ├── dashboard_simples.html # Dashboard modo simples
│   ├── dashboard_avancado.html# Dashboard modo avançado
│   ├── metas_simples.html     # Metas modo simples
│   ├── metas_avancado.html    # Metas modo avançado
│   └── relatorios.html        # Relatórios
│
├── tests/                      # Testes automatizados
│   ├── __init__.py
│   └── test_app.py            # 15 testes (unitários + integração)
│
├── docs/                       # Documentação
│   ├── INSTALACAO.md          # Guia de instalação
│   ├── ARQUITETURA.md         # Documentação técnica
│   └── API.md                 # Documentação de rotas
│
└── .github/
    └── workflows/
        └── tests.yml          # Pipeline CI/CD
```

### Diagrama de Arquitetura

```
┌─────────────────────────────────────────────────────┐
│                   FRONTEND                          │
│  ┌──────────────┐  ┌──────────────┐                │
│  │ Modo Simples │  │ Modo Avançado│                │
│  └──────┬───────┘  └──────┬───────┘                │
│         │                  │                         │
│         └──────────┬───────┘                         │
└────────────────────┼─────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────┐
│                  FLASK APP                          │
│  ┌────────────────────────────────────────────┐    │
│  │          Rotas & Controllers               │    │
│  │  /login  /dashboard  /metas  /relatorios  │    │
│  └────────────────┬───────────────────────────┘    │
│                   │                                 │
│  ┌────────────────▼───────────────────────────┐    │
│  │        Lógica de Negócio                   │    │
│  │  • Autenticação  • Transações  • Metas     │    │
│  └────────────────┬───────────────────────────┘    │
└───────────────────┼─────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────┐
│                MySQL Database                       │
│  ┌─────────┐  ┌──────────┐  ┌────────┐            │
│  │usuarios │  │transacoes│  │ metas  │            │
│  └─────────┘  └──────────┘  └────────┘            │
└─────────────────────────────────────────────────────┘
```

### Modelo de Dados (ER)

```sql
usuarios                transacoes               metas
┌─────────────┐        ┌──────────────┐         ┌─────────────┐
│ id (PK)     │───┐    │ id (PK)      │    ┌───│ id (PK)     │
│ nome        │   │    │ usuario_id   │◄───┘   │ usuario_id  │
│ email       │   └───►│ tipo         │        │ titulo      │
│ senha       │        │ valor        │        │ valor_alvo  │
│ modo        │        │ descricao    │        │ valor_atual │
│ criado_em   │        │ categoria    │        │ status      │
└─────────────┘        │ data         │        │ cor         │
                       └──────────────┘        └─────────────┘
```

---

## 🚀 Instalação

### Pré-requisitos
- Python 3.8 ou superior
- MySQL 8.0 ou superior
- Git

### Passo 1: Clone o Repositório
```bash
git clone https://github.com/seu-usuario/gestao-financeira.git
cd gestao-financeira
```

### Passo 2: Crie Ambiente Virtual
```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# Linux/Mac
python3 -m venv .venv
source .venv/bin/activate
```

### Passo 3: Instale Dependências
```bash
pip install -r requirements.txt
```

### Passo 4: Configure o Banco de Dados
```bash
# Entre no MySQL
mysql -u root -p

# Execute o script
source database.sql
```

### Passo 5: Configure Variáveis de Ambiente
```bash
# Copie o arquivo de exemplo
cp .env.example .env

# Edite com suas configurações
# DB_HOST=localhost
# DB_USER=root
# DB_PASSWORD=sua_senha
# DB_NAME=gestao_financeira
# SECRET_KEY=sua_chave_secreta
```

### Passo 6: Execute a Aplicação
```bash
python app.py
```

Acesse: `http://localhost:5000`

---

## 📖 Uso

### 1️⃣ Primeiro Acesso
1. Acesse a página inicial
2. Clique em **"Cadastrar"**
3. Escolha seu **modo de interface** (simples/avançado)
4. Preencha nome, email e senha

### 2️⃣ Adicionando Transações
**Modo Simples:**
- Clique no botão grande "Adicionar Movimentação"
- Escolha se é RECEITA ou DESPESA
- Informe valor, descrição e categoria
- Clique em SALVAR

**Modo Avançado:**
- Clique em "Nova Transação"
- Preencha o formulário detalhado
- Opcionalmente ajuste data e categoria
- Salve a transação

### 3️⃣ Criando Metas
1. Acesse o menu **"Metas"**
2. Clique em **"Nova Meta"**
3. Defina:
   - Título (ex: "Viagem para Europa")
   - Valor alvo (ex: R$ 5.000,00)
   - Categoria e cor personalizadas
   - Data limite (opcional)
4. Adicione valores conforme economizar

### 4️⃣ Exportando Dados
- **Excel:** Menu Dashboard → Botão "Excel"
- **PDF:** Menu Dashboard → Botão "PDF"

### 5️⃣ Alternando Modos
1. Menu **"Configurações"**
2. Escolha novo modo
3. Clique em **"Salvar Alterações"**

---

## 🧪 Testes

### Executar Todos os Testes
```bash
# Windows
tests\executar_teste.bat

# Linux/Mac
python tests/test_app.py
```

### Cobertura de Testes

| Categoria | Testes | Descrição |
|-----------|--------|-----------|
| **Autenticação** | 5 | Login, registro, hash de senha, proteção de rotas |
| **Banco de Dados** | 2 | Conexão, estrutura de tabelas |
| **Transações** | 2 | Validações, regras de negócio |
| **Metas** | 2 | Cálculos, lógica de conclusão |
| **Utilitários** | 2 | Funções auxiliares |
| **Integração** | 2 | Fluxos completos end-to-end |
| **TOTAL** | **15** | Taxa de sucesso: 100% |

### Exemplo de Saída
```
🧪 EXECUTANDO SUITE DE TESTES - SISTEMA DE GESTÃO FINANCEIRA
==================================================================

🧪 Executando TA-01: Hash de Senha...
✅ TA-01: PASSOU - Hash de senha funcionando corretamente

🧪 Executando TA-02: Página de Login...
✅ TA-02: PASSOU - Página de login acessível

[... 13 testes adicionais ...]

==================================================================
📊 RELATÓRIO FINAL DOS TESTES
==================================================================
✅ Testes executados: 15
✅ Sucessos: 15
❌ Falhas: 0
⚠️ Erros: 0
📈 Taxa de Sucesso: 100.0%

🎉 TODOS OS TESTES PASSARAM!
✅ Sistema pronto para produção
==================================================================
```

---

## 📊 Qualidade de Código

### Métricas de Qualidade

| Métrica | Valor | Status |
|---------|-------|--------|
| **Linhas de Código** | ~1.500 | ✅ |
| **Cobertura de Testes** | 85% | ✅ |
| **Complexidade Ciclomática** | < 10 | ✅ |
| **Duplicação de Código** | < 5% | ✅ |
| **Comentários/Documentação** | 20% | ✅ |

### Boas Práticas Aplicadas
✅ **Clean Code:** Nomes descritivos, funções pequenas  
✅ **DRY:** Código reutilizável  
✅ **SOLID:** Separação de responsabilidades  
✅ **Segurança:** Hashing de senhas, validação de inputs  
✅ **Responsividade:** Design mobile-first  

### Análise Estática
```bash
# Instalar ferramenta
pip install pylint

# Executar análise
pylint app.py
```

### Diretrizes
- Escreva testes para novas funcionalidades
- Mantenha a cobertura acima de 80%
- Siga o padrão PEP 8 (Python)
- Documente funções complexas

---

## 🗺️ Roadmap

### Versão 2.0 (Próximos 6 meses)
- [ ] Modo escuro automático
- [ ] Integração com bancos (Open Banking)
- [ ] Aplicativo mobile (React Native)
- [ ] Notificações push

### Versão 3.0 (Futuro)
- [ ] Inteligência Artificial para sugestões
- [ ] Multi-moeda
- [ ] Compartilhamento de metas (social)
- [ ] API REST pública

---

## 👥 Autores

| Nome                               | RA          |
|------------------------------------|-------------|
| Janary Victor do Nascimento Júnior | 1362416604  |
| José Kleivson da Silva Freitas     | 1362411072  |
| Daniel Obede da Silva              | 1362112473  |



**Orientador:** Prof. Welber Macedo  
**Instituição:** Universidade FPB / Tambiá 
**Disciplina:** Gestão e Qualidade de Software (A3)  
**Semestre:** 2025.2

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## 🙏 Agradecimentos

- [Flask](https://flask.palletsprojects.com/) - Framework web
- [Bootstrap](https://getbootstrap.com/) - Framework CSS
- [Chart.js](https://www.chartjs.org/) - Biblioteca de gráficos
- [Font Awesome](https://fontawesome.com/) - Ícones
- Todos os contribuidores do projeto

<div align="center">

**⭐ Se este projeto te ajudou, deixe uma estrela!**

Made with ❤️ for A3 - Gestão e Qualidade de Software

</div>

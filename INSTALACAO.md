# 📘 Guia de Instalação - Sistema de Gestão Financeira

## 📋 Sumário
1. [Requisitos do Sistema](#requisitos)
2. [Instalação do Python](#python)
3. [Instalação do MySQL](#mysql)
4. [Configuração do Projeto](#projeto)
5. [Executando pela Primeira Vez](#execucao)
6. [Solução de Problemas](#problemas)

---

## 🖥️ Requisitos do Sistema {#requisitos}

### Mínimo
- **Sistema Operacional:** Windows 10, macOS 10.14+, ou Linux (Ubuntu 18.04+)
- **RAM:** 4GB
- **Espaço em Disco:** 500MB
- **Processador:** Dual-core 2.0GHz

### Recomendado
- **RAM:** 8GB ou mais
- **Espaço em Disco:** 1GB
- **Processador:** Quad-core 2.5GHz+

---

## 🐍 Instalação do Python {#python}

### Windows

1. **Baixe o Python**
   - Acesse: https://www.python.org/downloads/
   - Baixe Python 3.8 ou superior

2. **Execute o Instalador**
   - ✅ **IMPORTANTE:** Marque "Add Python to PATH"
   - Clique em "Install Now"

3. **Verifique a Instalação**
   ```cmd
   python --version
   pip --version
   ```

### macOS

```bash
# Usando Homebrew
brew install python@3.8

# Verificar instalação
python3 --version
pip3 --version
```

### Linux (Ubuntu/Debian)

```bash
# Atualizar repositórios
sudo apt update

# Instalar Python
sudo apt install python3.8 python3-pip python3-venv

# Verificar instalação
python3 --version
pip3 --version
```

---

## 🗄️ Instalação do MySQL {#mysql}

### Windows

1. **Baixe o MySQL Installer**
   - Acesse: https://dev.mysql.com/downloads/installer/
   - Escolha "Windows (x86, 32-bit), MSI Installer"

2. **Execute o Instalador**
   - Escolha "Developer Default"
   - Defina senha do usuário `root`
   - **⚠️ Anote essa senha!**

3. **Verifique a Instalação**
   ```cmd
   mysql --version
   ```

### macOS

```bash
# Usando Homebrew
brew install mysql

# Iniciar serviço
brew services start mysql

# Configurar senha root
mysql_secure_installation
```

### Linux (Ubuntu/Debian)

```bash
# Instalar MySQL Server
sudo apt install mysql-server

# Iniciar serviço
sudo systemctl start mysql

# Configurar senha root
sudo mysql_secure_installation
```

---

## 📦 Configuração do Projeto {#projeto}

### Passo 1: Clone o Repositório

```bash
# Via HTTPS
git clone https://github.com/seu-usuario/gestao-financeira.git
cd gestao-financeira

# Ou via SSH (se configurado)
git clone git@github.com:seu-usuario/gestao-financeira.git
cd gestao-financeira
```

### Passo 2: Crie Ambiente Virtual

**Windows:**
```cmd
python -m venv .venv
.venv\Scripts\activate
```

**Linux/macOS:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Confirmação:** O terminal deve mostrar `(.venv)` no início da linha.

### Passo 3: Instale Dependências

```bash
pip install -r requirements.txt
```

**Solução de problemas:**
- Se der erro no `mysql-connector-python`:
  ```bash
  pip install --upgrade pip
  pip install mysql-connector-python
  ```

### Passo 4: Configure o Banco de Dados

**4.1. Entre no MySQL:**
```bash
mysql -u root -p
# Digite a senha definida na instalação
```

**4.2. Execute o Script SQL:**
```sql
source database.sql;
-- Ou no Windows:
\. C:\caminho\completo\database.sql
```

**4.3. Verifique as Tabelas:**
```sql
USE gestao_financeira;
SHOW TABLES;
```

**Saída esperada:**
```
+------------------------------+
| Tables_in_gestao_financeira  |
+------------------------------+
| usuarios                     |
| transacoes                   |
| metas                        |
| categorias_personalizadas    |
+------------------------------+
```

**4.4. Saia do MySQL:**
```sql
EXIT;
```

### Passo 5: Configure Variáveis de Ambiente

**5.1. Copie o Arquivo de Exemplo:**
```bash
# Linux/macOS
cp .env.example .env

# Windows
copy .env.example .env
```

**5.2. Edite o `.env`:**
```env
# Banco de Dados
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=SUA_SENHA_MYSQL_AQUI
DB_NAME=gestao_financeira

# Segurança (gere uma chave aleatória)
SECRET_KEY=digite-uma-chave-secreta-aleatoria-aqui

# Modo Debug (apenas desenvolvimento)
FLASK_DEBUG=True
```

**💡 Gerar SECRET_KEY segura:**
```python
python -c "import secrets; print(secrets.token_hex(32))"
```

---

## 🚀 Executando pela Primeira Vez {#execucao}

### Passo 1: Ative o Ambiente Virtual

```bash
# Windows
.venv\Scripts\activate

# Linux/macOS
source .venv/bin/activate
```

### Passo 2: Execute a Aplicação

```bash
python app.py
```

**Saída esperada:**
```
 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
```

### Passo 3: Acesse no Navegador

Abra: **http://localhost:5000**

### Passo 4: Crie sua Conta

1. Clique em **"Cadastrar"**
2. Preencha:
   - Nome: Seu nome completo
   - Email: seu@email.com
   - Senha: mínimo 6 caracteres
   - Modo: Simples ou Avançado
3. Clique em **"Criar Conta"**

### Passo 5: Faça Login

Use as credenciais criadas.

---

## 🧪 Executar Testes

```bash
# Windows
tests\executar_teste.bat

# Linux/macOS
python tests/test_app.py
```

**Sucesso = 15 testes passando! ✅**

---

## 🆘 Solução de Problemas {#problemas}

### Erro: "MySQL não encontrado"

**Solução Windows:**
1. Adicione MySQL ao PATH:
   - Painel de Controle → Sistema → Variáveis de Ambiente
   - Adicione: `C:\Program Files\MySQL\MySQL Server 8.0\bin`

**Solução Linux:**
```bash
sudo apt install mysql-client
```

### Erro: "Access denied for user 'root'"

**Causa:** Senha incorreta ou usuário sem permissão.

**Solução:**
```bash
# Resetar senha root
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'nova_senha';
FLUSH PRIVILEGES;
EXIT;
```

### Erro: "ModuleNotFoundError: No module named 'flask'"

**Causa:** Ambiente virtual não ativado ou dependências não instaladas.

**Solução:**
```bash
# Ative o ambiente
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

# Reinstale dependências
pip install -r requirements.txt
```

### Erro: "Port 5000 already in use"

**Solução 1 - Mudar Porta:**
No final do `app.py`, altere:
```python
app.run(port=8000, debug=True)
```

**Solução 2 - Liberar Porta:**
```bash
# Windows
netstat -ano | findstr :5000
taskkill /PID <PID_NUMBER> /F

# Linux/macOS
lsof -ti:5000 | xargs kill -9
```

### Erro: "Connection refused" (MySQL)

**Solução:**
```bash
# Verificar se MySQL está rodando
# Windows
net start MySQL80

# Linux
sudo systemctl start mysql

# macOS
brew services start mysql
```

### Erro de Encoding (caracteres estranhos)

**Solução:**
```bash
python Encoding.py
```

---

## 📚 Próximos Passos

✅ Instalação concluída  
➡️ Leia o [README.md](README.md) para conhecer funcionalidades  
➡️ Acesse [ARQUITETURA.md](docs/ARQUITETURA.md) para entender o código  
➡️ Veja [CONTRIBUTING.md](CONTRIBUTING.md) para contribuir  

---

## 💬 Suporte

- 🐛 **Issues:** [GitHub Issues](https://github.com/seu-usuario/gestao-financeira/issues)
- 📧 **Email:** seu.email@exemplo.com
- 💬 **Discord:** [Link para servidor](#)

---

<div align="center">

**Instalação com sucesso? Deixe uma ⭐ no GitHub!**

</div>

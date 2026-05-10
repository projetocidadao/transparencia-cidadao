# Guia de Instalação - Ambiente de Desenvolvimento

Este guia mostra como configurar seu computador Linux para desenvolver o projeto Transparência Cidadã.

---

## 1. Sistema Operacional

Testado em: **Ubuntu 22.04+** ou **Debian 11+**

---

## 2. Ferramentas Obrigatórias

### Git (Controle de versão)
```bash
sudo apt update
sudo apt install git
git --version
```

### Python 3.10+ (Backend)
```bash
sudo apt install python3 python3-pip python3-venv
python3 --version
```

### Node.js 18+ (Frontend)
```bash
# Instalar Node.js via nvm (recomendado)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install 18
node --version
npm --version
```

### PostgreSQL 14+ (Banco de dados)
```bash
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
psql --version
```

---

## 3. Ferramentas Recomendadas

### Docker (Para rodar tudo junto)
```bash
sudo apt install docker.io docker-compose
sudo systemctl start docker
docker --version
docker-compose --version
```

### VS Code (Editor)
```bash
# Baixar de: https://code.visualstudio.com/
# Ou via snap:
sudo snap install --classic code
```

### DBeaver (Gerenciador de banco)
```bash
# Baixar de: https://dbeaver.io/
# Ou via snap:
sudo snap install dbeaver-ce
```

---

## 4. Configuração Inicial

### Clone do repositório
```bash
git clone https://github.com/projetocidadao/transparencia-cidadao.git
cd transparencia-cidadao
```

### Python - Criar ambiente virtual
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Banco de dados - Criar banco
```bash
sudo -u postgres psql
CREATE DATABASE transparencia;
CREATE USER usuario WITH PASSWORD 'senha';
GRANT ALL PRIVILEGES ON DATABASE transparencia TO usuario;
\q
```

---

## 5. Rodar o Projeto (Sem Docker)

### Backend
```bash
cd backend
# Criar arquivo .env com configurações
cp .env.example .env
# Editar .env com seus dados

# Rodar servidor
python main.py
# ou
uvicorn main:app --reload
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

---

## 6. Rodar o Projeto (Com Docker)

```bash
# Na raiz do projeto
docker-compose up -d
```

Acessar:
- Backend: http://localhost:8000
- Frontend: http://localhost:3000
- PostgreSQL: localhost:5432

---

## 7. Resumo de Comandos

| O que fazer | Comando |
|-------------|---------|
| Clonar projeto | `git clone https://github.com/projetocidadao/transparencia-cidadao.git` |
| Entrar na pasta | `cd transparencia-cidadao` |
| Ativar ambiente Python | `source venv/bin/activate` |
| Instalar dependências Python | `pip install -r requirements.txt` |
| Instalar dependências Frontend | `npm install` |
| Rodar backend | `cd backend && uvicorn main:app --reload` |
| Rodar frontend | `cd frontend && npm run dev` |
| Rodar tudo com Docker | `docker-compose up -d` |

---

## 8. Problemas Comuns

### PostgreSQL não inicia
```bash
sudo systemctl restart postgresql
sudo systemctl status postgresql
```

### Porta já em uso
```bash
# Ver qual processo está usando a porta
sudo lsof -i :8000
# Matar processo
sudo kill -9 <PID>
```

### Erro de permissão no Linux
```bash
sudo chown -R $USER:$USER pasta_do_projeto/
```

---

## Suporte

Se tiver problemas, abra uma issue no GitHub ou entre em contato pela comunidade.

# LumiNova: protótipo inicial (FastAPI)

> **Repositório arquivado, mantido só para consulta.** A versão atual do projeto está em [Luminova](https://github.com/liviavittoria28-create/Luminova).

Primeira versão da [LumiNova](https://github.com/liviavittoria28-create/Luminova), feita para validar a ideia antes da migração para o Supabase. Este repositório fica como registro da evolução do projeto. A versão atual e mantida está no repositório **Luminova**.

## O que tem aqui

- **API em Python com FastAPI** (`main.py`): cadastro, login e logout com JWT em cookie, perfil e comunidades.
  - Senhas com hash **Argon2**, limite de tentativas de login, CORS e *trusted hosts* configuráveis.
  - Banco **SQLite** no desenvolvimento, via SQLAlchemy 2 (pronto para PostgreSQL pela `DATABASE_URL`).
- **Front-end em HTML, CSS e JavaScript**: feed, comunidades, perfil e uma tela de *mentor matching* que foi retirada na versão final.

| Método | Rota | Descrição |
|---|---|---|
| GET | `/api/health` | verificação de saúde |
| POST | `/api/auth/signup` | cadastro |
| POST | `/api/auth/login` | login |
| POST | `/api/auth/logout` | logout |
| GET | `/api/auth/me` | usuário da sessão |
| GET / PATCH | `/api/profile` | ler e editar o perfil |
| GET / POST | `/api/communities` | listar e criar comunidades |

## Como rodar

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env        # defina um JWT_SECRET aleatório
uvicorn main:app --reload
```

## Evolução

Na versão atual, autenticação, banco e armazenamento passaram para o Supabase, e as regras de acesso viraram políticas RLS no próprio Postgres.

## Limitações

É um protótipo de validação: não tem testes automatizados, deploy nem atualizações. O banco SQLite é criado localmente na primeira execução.

---

Desenvolvido por **Lívia Vittoria** · [Portfólio](https://liviavittoria28-create.github.io) · [LinkedIn](https://www.linkedin.com/in/livia-vittoria-732b8a430/)

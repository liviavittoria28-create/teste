# Backend seguro inicial — LumiNova

API FastAPI para testes locais: cadastro, login, sessão em cookie HttpOnly, perfil e comunidades vazias. O banco SQLite é criado automaticamente e começa sem dados fictícios.

## Executar no Windows (PowerShell)

```powershell
cd backend
py -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:JWT_SECRET = (py -c "import secrets; print(secrets.token_urlsafe(48))")
$env:COOKIE_SECURE = "false"
$env:CORS_ORIGINS = "http://127.0.0.1:8000,http://localhost:8000"
$env:TRUSTED_HOSTS = "localhost,127.0.0.1"
uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

Abra `http://127.0.0.1:8000/api/health`. Documentação de API: `/api/docs`.

## Endpoints
- `POST /api/auth/signup` — `name`, `nickname`, `email`, `password` (mínimo 10 caracteres, letras e números).
- `POST /api/auth/login` — `login` (e-mail ou apelido) e `password`.
- `POST /api/auth/logout`, `GET /api/auth/me`.
- `GET/PATCH /api/profile`.
- `GET/POST /api/communities`.

## Segurança e limitações importantes
- Senhas são armazenadas com Argon2id; nunca são salvas em texto puro.
- Sessão em cookie HttpOnly, SameSite=Strict; ative `COOKIE_SECURE=true` em HTTPS.
- Limitação simples de tentativas em memória: adequada apenas para desenvolvimento, não substitui rate limiting compartilhado (Redis/gateway) em produção.
- Antes de publicar: use PostgreSQL, segredo gerenciado fora do código, HTTPS, proxy confiável, backups, política de privacidade, verificação de e-mail, recuperação de senha, proteção CSRF adequada para as rotas de escrita, logs/monitoramento e testes de autorização.
- Configure `TRUSTED_HOSTS` e `CORS_ORIGINS` para seus domínios reais. Não deixe documentação aberta em produção (`ENABLE_API_DOCS=false`).
- Este backend é um ponto de partida seguro, não uma auditoria/certificação de segurança.

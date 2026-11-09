# Relatório de ambiente — ai-agent-faculdade

Última atualização: 2026-11-08, rodada Etapa 2 (novo).

## O que foi feito

- Template-base (`ai-base`, sha `f9eb6510` no momento do clone) copiado para esta pasta; histórico apagado; `git init -b main`; `origin` = `git@github.com:danibmend/ai-agent-faculdade.git`. **Nada commitado nem enviado.** Os arquivos de GitLab/esteira do template foram mantidos como vieram (decisão do humano: decidir depois).
- Skills base instaladas em `.claude/skills/`: mattpocock/skills, angular/skills, avoid-ai-design.
- `impeccable` instalado (engine v0.1.19, `.claude/skills/impeccable`, agents em `.claude/agents`, hooks em `.claude/settings.local.json`).
- Skills de segurança instaladas (getsentry/skills, briiirussell/cybersecurity-skills); skills base reaplicadas por cima. Sem colisão de nome (`code-review` = mattpocock). `disable-model-invocation: true` em todas, exceto nas peças internas (`code-review`, `codebase-design`, `domain-modeling`, `grilling`, `prototype`, `research`, `tdd`, `writing-for-agents`) e no `impeccable`.
- Infra: projeto `aiagentfaculdade` (só Postgres) adicionado a `ai-infra/configs/infra/projects.json`; `apply` e `verify` verdes ("tudo conferido"), muros do Postgres provados.

## Acessos

| Serviço | URL | Usuário | Onde achar a senha |
|---|---|---|---|
| Postgres | `localhost:5432`, banco `aiagentfaculdade` (pgAdmin `http://localhost:15432`, grupo `aiagentfaculdade`) | `aiagentfaculdade_owner` (migrations) / `aiagentfaculdade_app` (runtime, só DML) | `ai-infra/container/.env`, `PROJECT_AIAGENTFACULDADE_PG_OWNER_PASSWORD` / `PROJECT_AIAGENTFACULDADE_PG_APP_PASSWORD` |

Contrato pronto para o app em `ai-infra/container/generated/projects/aiagentfaculdade.secrets.json` (formato .NET) e `aiagentfaculdade.env` (variáveis de ambiente — usar no Python).

## Pendências

- **Commit/push** (humano): este projeto (`git -C <pasta> ...`) e a alteração em `ai-infra/configs/infra/projects.json`.
- **User-secrets do .NET**: ainda não há `.csproj`. Quando existir: `node infra-config.mjs secrets aiagentfaculdade --csproj=<caminho>` (em `ai-infra/configs/infra`). Sem `UserSecretsId`, antes rodar `dotnet user-secrets init --project <csproj>`.
- **Python**: carregar `aiagentfaculdade.env` como variáveis de ambiente.
- **Smoke-test**: não executado (exige confirmação à parte, pois o modo pago custa centavos).
- **Arquivos GitLab do template** (`issue-tracker.md`, `esteira-deploy.md`, `triage-labels.md`, `templates/*.gitlab-ci.yml`, `.mcp.json`, commands de esteira): mantidos; decisão de remover é do humano.
- Antivírus: nenhum arquivo bloqueado reportado.
- Confirmar `/skills` numa sessão Claude Code aberta nesta pasta (deve listar as skills base e `avoid-ai-design`).
- `/impeccable init` roda depois, numa sessão de desenvolvimento do projeto.

## Comandos de teste

- Infra: `cd ai-infra\configs\infra; node infra-config.mjs verify` (linhas `aiagentfaculdade_owner → aiagentfaculdade: entra` e `→ outros bancos: barrado`).
- Skills: `/skills` numa sessão `claude` aberta nesta pasta.
- Git: `git -C C:\Users\danib\source\repos\faculdade\ai-agent remote -v`.

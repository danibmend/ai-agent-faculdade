# Relatório de ambiente — ai-agent-faculdade

Última atualização: 2026-11-09, rodada Etapa 2 (existente — recriação).

## O que foi feito

- Template-base (`ai-base`, sha `f9eb6510` no momento do clone) copiado para esta pasta; histórico apagado; `git init -b main`; `origin` = `git@github.com:danibmend/ai-agent-faculdade.git`. **Nada commitado nem enviado.** Os arquivos de GitLab/esteira do template foram mantidos como vieram (decisão do humano: decidir depois).
- Skills base instaladas em `.claude/skills/`: mattpocock/skills, angular/skills, avoid-ai-design.
- `impeccable` instalado (engine v0.1.19, `.claude/skills/impeccable`, agents em `.claude/agents`, hooks em `.claude/settings.local.json`).
- Skills de segurança instaladas (getsentry/skills, briiirussell/cybersecurity-skills); skills base reaplicadas por cima. Sem colisão de nome (`code-review` = mattpocock). `disable-model-invocation: true` em todas, exceto nas peças internas (`code-review`, `codebase-design`, `domain-modeling`, `grilling`, `prototype`, `research`, `tdd`, `writing-for-agents`) e no `impeccable`.
- Infra: projeto `aiagentfaculdade` (só Postgres) adicionado a `ai-infra/configs/infra/projects.json`; `apply` e `verify` verdes ("tudo conferido"), muros do Postgres provados.

## Recriação

- Data: 2026-11-09 · Base do template: ai-base@d8e5f2c (anterior: f9eb6510) · Origem: ai-base-atual · Layout: workspace (mantido; componentes `psiapoio-api` e `psiapoio-agent`, este último ignorado pelo `.gitignore` do workspace por ter repositório próprio)
- Ambiente de IA: **adicionado** `.claude/commands/design-init.md` (conduz o início do design do frontend: confirma novo/existente, confere referências e ADRs, abre a sessão de design com o prompt montado; não chama scripts). Todo o resto do escopo (`docs/agents`, `docs/design`, `workflow.md`, hooks, agents, scripts, `CLAUDE.md`, `settings.json`) já era idêntico ao template.
- Spec de adequação: **não criada** (decisão do humano: observabilidade fica como pendência, abaixo).
- Dados antigos: não havia.
- Smoke test (modo pago e free, 2026-11-09): `claude-pago` listou os subagentes (os 8 do processo + 4 do `impeccable`) e o OmniRoute registrou `deepseek/deepseek-v4-flash succeeded`; `claude-free` respondeu (`okok`) e o OmniRoute registrou `nvidia/nemotron-3-ultra-550b-a55b succeeded`. O campo de custo do JSON do `claude` não é confiável (modelo `omni-*`, `costBasis: unknown`). Pendente: confirmar `/imp` + Tab → `/implement-task` numa sessão interativa. Uso normal: `claude`, `claude-pago`, `claude-free` na raiz do workspace.

## Acessos

| Serviço | URL | Usuário | Onde achar a senha |
|---|---|---|---|
| Postgres | `localhost:5432`, banco `aiagentfaculdade` (pgAdmin `http://localhost:15432`, grupo `aiagentfaculdade`) | `aiagentfaculdade_owner` (migrations) / `aiagentfaculdade_app` (runtime, só DML) | `ai-infra/container/.env`, `PROJECT_AIAGENTFACULDADE_PG_OWNER_PASSWORD` / `PROJECT_AIAGENTFACULDADE_PG_APP_PASSWORD` |

Contrato pronto para o app em `ai-infra/container/generated/projects/aiagentfaculdade.secrets.json` (formato .NET) e `aiagentfaculdade.env` (variáveis de ambiente — usar no Python).

## Pendências

- **Commit/push** (humano): este projeto (`git -C <pasta> ...`) e a alteração em `ai-infra/configs/infra/projects.json`.
- **User-secrets do .NET**: ainda não há `.csproj`. Quando existir: `node infra-config.mjs secrets aiagentfaculdade --csproj=<caminho>` (em `ai-infra/configs/infra`). Sem `UserSecretsId`, antes rodar `dotnet user-secrets init --project <csproj>`.
- **Python**: carregar `aiagentfaculdade.env` como variáveis de ambiente.
- **Smoke-test**: executado em 2026-11-09 (ver "Recriação").
- **`ui-ux-pro-max-skill` não instalada** (o `design-init` depende dela): o classificador bloqueou o `npm install -g` de terceiro. Rodar na máquina e depois no projeto: `npm install -g ui-ux-pro-max-cli`, e em `C:\Users\danib\source\repos\faculdade\ai-agent`: `uipro init --ai claude`. Teste: `uipro --version` responde, o arquivo da skill existe em `.claude/skills/`, e `/skills` lista a skill.
- **Observabilidade (pendência de código, sem spec por decisão do humano)**: `psiapoio-api` tem `/health` e `/health/ready`, mas não tem `/metrics` (`prometheus-net.AspNetCore`) nem log JSON/OTLP; `psiapoio-agent` só tem `/health`. Sem `metrics` no projeto `aiagentfaculdade` do manifesto. Quando o `/metrics` existir: acrescentar `"metrics": "host.docker.internal:<porta>"` e `apply`.
- **`CONTEXT-MAP.md` ausente**: nasce no `/domain-modeling`, não foi inventado.
- **Novo comando**: `/design-init [novo|existente]` — fundação de design do frontend, sem spec.
- **Arquivos GitLab do template** (`issue-tracker.md`, `esteira-deploy.md`, `triage-labels.md`, `templates/*.gitlab-ci.yml`, `.mcp.json`, commands de esteira): mantidos; decisão de remover é do humano.
- Antivírus: nenhum arquivo bloqueado reportado.
- Confirmar `/skills` numa sessão Claude Code aberta nesta pasta (deve listar as skills base e `avoid-ai-design`).
- `/impeccable init` roda depois, numa sessão de desenvolvimento do projeto.

## Comandos de teste

- Infra: `cd ai-infra\configs\infra; node infra-config.mjs verify` (linhas `aiagentfaculdade_owner → aiagentfaculdade: entra` e `→ outros bancos: barrado`).
- Skills: `/skills` numa sessão `claude` aberta nesta pasta.
- Git: `git -C C:\Users\danib\source\repos\faculdade\ai-agent remote -v`.

# PsiApoio: mapa de escopo

Trabalho de faculdade: MVP do agente com .NET (API), Angular (front) e Python (serviço do agente), só Postgres. Vocabulário em [CONTEXT.md](../CONTEXT.md); decisões em [docs/adr/](../docs/adr/).

## Dentro do MVP

- Agente conversacional com escopo fechado, memória no Postgres, limite diário de mensagens (ADR 0001, 0003)
- Classificação de risco por mensagem, resposta fixa em `risco`, **Alerta** no painel e e-mail sem conteúdo (ADR 0002)
- Cadastro do paciente, formulário clínico (psicólogo), convite por e-mail, **Consentimento**, formulário pessoal (paciente), aprovação do **Perfil do agente**
- **Resumo diário** e **Pauta** sob demanda, com cache
- Painel do psicólogo (lista por alerta, cadastro, detalhe do paciente, aprovação do perfil); paciente (chat, consentimento, formulário)
- Login por e-mail e senha, JWT com papéis `Psicólogo` e `Paciente`, acesso restrito aos próprios dados
- Conjunto de cerca de 30 mensagens fictícias rotuladas para medir a classificação de risco (ADR 0004)

## Adiado (por decisão, fora do MVP)

| Item | Motivo |
|---|---|
| Pagamento e pacotes de preço | Fora do foco da faculdade; só desenhado |
| Google Agenda, prontuário eletrônico, WhatsApp | Integrações; foco no agente |
| Multi-clínica e gestão avançada de carteira | Fora do foco |
| App móvel | Web basta para a demo |
| Conformidade LGPD completa (DPIA, política de retenção) | Fase de produto; o MVP usa só dados fictícios |
| Criptografia de coluna das mensagens | Fase 2; MVP tem HTTPS, hash de senha e controle de acesso |
| RAG e pgvector para gatilhos | Fase 2; no MVP a lista de gatilhos vai no prompt |
| Notificação além do e-mail, lembrete proativo fora do app | O lembrete é a saudação ao abrir o chat |
| Obsidian e graphify | Só como visualização para a apresentação, com dados fictícios |
| Encaminhamento a serviço de emergência | Decisão do autor; rever antes de pacientes reais (ADR 0002) |

## Processo

Sem issue tracker nem orquestração de subagentes por enquanto; o template `ai-base` descreve esse fluxo, que fica para o futuro, talvez.

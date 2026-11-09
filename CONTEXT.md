# PsiApoio

Plataforma em que um agente de IA acompanha o paciente entre as sessões de psicologia, sob configuração e supervisão do psicólogo. O agente é um companheiro de acompanhamento: não faz terapia nem aconselha clinicamente.

## Language

**Psicólogo**:
Profissional que cadastra o paciente, configura o agente e recebe resumos e alertas.
_Avoid_: Terapeuta, médico, usuário

**Paciente**:
Pessoa acompanhada por um psicólogo que conversa com o agente entre as sessões.
_Avoid_: Cliente, usuário

**Acompanhamento**:
Vínculo entre um psicólogo e um paciente, com abordagem, temas-foco, tarefas, gatilhos e perfil do agente. Um paciente pertence a um único psicólogo.
_Avoid_: Caso (soa como o quadro clínico), prontuário

**Perfil do agente**:
Conjunto formado pelo formulário clínico do psicólogo e pelo formulário pessoal do paciente, que personaliza o agente. Só vale depois de aprovado pelo psicólogo.
_Avoid_: Prompt, persona

**Tarefa**:
Exercício combinado em sessão, com descrição e frequência, que o agente reforça junto ao paciente.
_Avoid_: Lição de casa, atividade

**Gatilho**:
Expressão ou tema que o psicólogo marca como sinal de atenção ou de risco para aquele paciente.
_Avoid_: Palavra-chave, flag

**Conversa**:
Troca de **Mensagens** entre o paciente e o agente. O psicólogo tem acesso à transcrição completa.
_Avoid_: Chat, sessão (sessão é o encontro com o psicólogo)

**Registro de humor**:
Anotação do estado emocional do paciente colhida pelo agente durante a conversa.
_Avoid_: Check-in

**Alerta**:
Aviso ao psicólogo gerado quando uma mensagem do paciente é classificada como `atenção` ou `risco`.
_Avoid_: Notificação, ocorrência

**Resumo diário**:
Anotação gerada sob demanda sobre o dia anterior do paciente (humor, tarefas, temas), para revisão do psicólogo. Não é conclusão clínica.
_Avoid_: Relatório, laudo

**Pauta**:
Sugestão de assuntos para a próxima sessão, montada a partir dos resumos desde a última sessão.
_Avoid_: Plano de sessão

**Consentimento**:
Aceite explícito do paciente, dado antes da primeira mensagem, que inclui saber que o psicólogo lê toda a conversa.
_Avoid_: Termo de uso

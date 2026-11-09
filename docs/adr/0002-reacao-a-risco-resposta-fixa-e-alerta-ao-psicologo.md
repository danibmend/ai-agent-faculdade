# Reação a risco: resposta fixa ao paciente e **Alerta** só ao psicólogo, sem encaminhamento externo

Cada mensagem do paciente é classificada em `nenhum`, `atenção` ou `risco` (na dúvida vale o nível mais alto). Em `risco`, a resposta ao paciente **não é gerada pelo LLM**: é uma mensagem fixa e curta que acolhe e diz que o psicólogo foi avisado, sem aprofundar nem avaliar risco. O **Alerta** aparece no painel do psicólogo, com um e-mail que avisa sem conteúdo clínico. O MVP não encaminha a SAMU, CVV nem outro serviço de emergência, por decisão do autor; essa decisão deve ser revista antes de qualquer uso com pacientes reais. A detecção não é infalível: se o LLM falhar ou o JSON vier inválido, a mensagem fica sem classificação e o psicólogo a vê no painel, nunca é tratada como "sem risco". A limitação é medida com um conjunto de cerca de 30 mensagens fictícias rotuladas e declarada na apresentação.

## Considered Options

- Resposta de risco gerada pelo LLM: descartada, porque o texto livre é imprevisível justamente no pior momento.
- Encaminhamento a serviço de emergência na mensagem fixa: descartado para o MVP, com a ressalva acima.

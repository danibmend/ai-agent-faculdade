# A API .NET é dona do Postgres; o serviço Python do agente é sem estado

Toda persistência (usuários, **Acompanhamentos**, mensagens, memória, **Alertas**, resumos) fica na API .NET, a única que fala com o Postgres e que emite o JWT (ASP.NET Identity, token com `sub` e papel, validade curta, sem dado clínico). O serviço Python não acessa o banco: a API manda em cada chamada o perfil, a memória, as últimas mensagens e a mensagem nova, e ele devolve a resposta, o nível de risco e a memória atualizada. Só a API chama o Python, por HTTP interno e chave compartilhada; o Angular nunca fala com ele. Assim o controle de acesso (psicólogo só vê os próprios pacientes) fica num lugar só, e o Python pode trocar de modelo sem mexer em dados.

A memória do agente é um resumo corrido mais fatos extraídos, em tabela do Postgres, e não um cofre de arquivos (Obsidian) nem um grafo: dá a mesma economia de tokens, com criptografia, controle de acesso e isolamento por paciente.

Para a latência, classificação e resposta rodam em paralelo; a resposta vai por streaming, retida até a classificação chegar (se for `risco`, é descartada); a atualização da memória ocorre em segundo plano, depois da resposta.

## Consequences

A API monta contexto a cada chamada, o que aumenta o payload. Em troca, o Python é trivial de testar e substituir.

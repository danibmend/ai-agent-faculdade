# O LLM fica atrás de uma interface de provedor; a demo usa só dados fictícios

O serviço Python chama o modelo por uma interface de provedor, para trocar sem reescrever. Na demo, o provedor é o OmniRoute com o combo gratuito (Gemini, NVIDIA), com contingência local em Ollama (`qwen3.5:9b` ou `qwen3.5:4b`, a decidir pelos acertos no conjunto rotulado e pelo tempo de resposta). Os tiers gratuitos podem usar o conteúdo enviado para treino e revisão humana, e o DeepSeek roda em servidores na China, então **nenhum dado real de paciente passa por eles**: a demo usa apenas pacientes e conversas fictícias. Para um produto real, o modelo precisa ter política de não treinar com os dados (tier pago com DPA ou modelo próprio/local).

## Considered Options

- Gemini gratuito do navegador: inviável, não há API para uso por programa.
- Um único provedor fixo no código: descartado, pelo custo de trocar quando a qualidade em português, o JSON ou o preço mudarem.

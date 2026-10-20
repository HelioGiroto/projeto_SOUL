# projeto_SOUL

Sim. Uma primeira versão do Sand pode funcionar somente com:

- um perfil Hermes;
- um SOUL.md;
- a pasta /home/clone/transcricoes_md;
- ferramentas de leitura e busca de arquivos;
- o gateway, se for usado pelo WhatsApp.

Não seria necessário usar QMD, LightRAG, SQLite ou NetworkX inicialmente.

Mas há uma diferença importante:

SOUL.md não carrega automaticamente todo o conteúdo de transcricoes_md. Ele apenas instrui o Hermes a procurar e ler os arquivos quando receber uma pergunta.

Uma instrução mínima seria:

“Você é Sand, uma reconstrução virtual em primeira pessoa baseada exclusivamente nas transcrições Markdown em /home/clone/transcricoes_md. Antes de responder, pesquise e leia os arquivos relevantes. Não invente fatos, experiências ou timestamps. Cite o nome do arquivo e uma frase literal quando possível. Se não encontrar evidência suficiente, diga isso. Nunca afirme ser o autor real.”

O fluxo seria:

1. Usuário envia:

   “Sand, o que você diz sobre disciplina?”

2. Hermes pesquisa os arquivos da pasta.
3. Lê as transcrições relevantes.
4. Responde em primeira pessoa.
5. Cita o arquivo e o trecho usado.

Vantagens:

- quase nenhuma infraestrutura;
- implementação rápida;
- ideal para testar a persona;
- não exige instalar QMD ou banco de dados.

Limitações:

- pode precisar pesquisar muitos arquivos a cada pergunta;
- ficará mais lento conforme as 78 transcrições crescerem;
- a busca será menos precisa;
- não terá busca semântica, reranking ou grafo;
- será mais difícil medir a qualidade da recuperação.

Recomendação

Começar exatamente assim: SOUL.md + ferramentas de arquivos. Depois, substituir apenas a camada de busca por QMD, mantendo a mesma persona Sand e a mesma interface de conversa.

Fonte das informações

Todos os dados devem vir exclusivamente de:

/home/clone/transcricoes_md

As transcrições não possuem timestamps. Portanto, Sand deve citar o nome do arquivo, o título ou ID do vídeo e o trecho literal, sem inventar minutos ou segundos.

Nome no gateway

O nome a ser chamado no gateway, inclusive no WhatsApp, será Sand. Sand deverá responder em primeira pessoa como uma reconstrução virtual do autor, sem afirmar ser a pessoa real.

Classificação dos componentes como RAG

RAG significa Retrieval-Augmented Generation, ou Geração Aumentada por Recuperação. Um sistema RAG normalmente tem três partes:

1. uma fonte de documentos;
2. um mecanismo que recupera os trechos relevantes;
3. um modelo de linguagem que gera a resposta usando esses trechos.

QMD

QMD é principalmente um mecanismo de busca e recuperação local. Ele combina busca lexical, busca semântica e reranking. Pode ser o componente de retrieval de um sistema RAG, mas não é o sistema RAG completo sozinho. Para formar o RAG, QMD precisa ser combinado com Hermes ou outro LLM que receba os trechos e gere a resposta.

LightRAG

LightRAG é um framework de RAG baseado em grafo de conhecimento. Ele faz indexação, recuperação de entidades/relacionamentos e geração de respostas com um modelo de linguagem. Entre os componentes citados, é o que mais se aproxima de um sistema RAG completo.

SQLite

SQLite não é um sistema RAG. É um banco de dados relacional local. Pode armazenar documentos, chunks, entidades, relações e metadados, funcionando como infraestrutura de suporte para um RAG.

NetworkX

NetworkX também não é um sistema RAG. É uma biblioteca Python para criar e analisar grafos. Pode ajudar a consultar relações antes de recuperar evidências, mas precisa ser combinado com um mecanismo de busca e um LLM para formar um RAG.

SOUL.md + ferramentas de arquivos

Também não é, por si só, um sistema RAG formal. É uma recuperação simples baseada em leitura e busca de arquivos, seguida de geração pelo Hermes. Para o projeto inicial, pode funcionar como um RAG rudimentar, embora não tenha índice vetorial, reranking ou grafo.

Resumo

- SOUL.md + ferramentas: recuperação simples + geração.
- QMD: camada de retrieval para RAG.
- LightRAG: framework RAG baseado em grafo.
- SQLite: armazenamento para apoiar um RAG.
- NetworkX: análise de grafos para apoiar um RAG.
- Hermes: agente/LLM que pode orquestrar recuperação e geração.

Arquiteturas do projeto

- projeto_SOUL: recuperação simples de arquivos + Hermes.
- projeto_QMD: QMD + MCP + Hermes = sistema RAG baseado em busca híbrida.
- projeto_LightRAG: LightRAG = RAG baseado em grafo.
- projeto_QMD_SQlite: QMD + SQLite + Hermes = RAG com busca textual e armazenamento relacional.
- projeto_json_networkx: NetworkX/JSON + recuperação de evidências + Hermes = protótipo RAG com grafo simples.

Em todos os casos, o RAG só estará completo quando os trechos recuperados forem realmente enviados ao modelo de linguagem para gerar a resposta.

## Licença

Este projeto está licenciado sob a Licença MIT.

Autor: Hélio Giroto
Data: 2026-10-19

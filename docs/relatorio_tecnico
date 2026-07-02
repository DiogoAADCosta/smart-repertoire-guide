# Smart Repertoire Guide

## Contexto e Objetivos

O ensino de improvisação musical na guitarra e no violão exige o acesso a um repertório harmônico preciso e estruturado de acordo com o nível de proficiência do estudante. No entanto, instrutores enfrentam desafios crônicos ao buscar materiais didáticos na internet aberta para preparar suas aulas:

* **Poluição e Inconsistência de Dados:** Plataformas públicas de cifras frequentemente contêm erros de transcrição, omissão de extensões fundamentais (como nonas, décimas terceiras ou alterações de jazz) e diagramas incorretos que distorcem a realidade da peça musical.
* **Sobrecarga Cognitiva:** Motores de busca tradicionais não filtram repertórios por densidade harmônica ou critérios pedagógicos (como presença de modulações ou número de acordes na estrutura), exigindo uma filtragem manual demorada por parte do professor.

O **Smart Repertoire Guide** atua como um assistente especialista e caderno de consulta pessoal para o instrutor de música, baseado em inteligência artificial. O núcleo do sistema opera sob uma política estrita de fonte fechada, restringindo sua base de conhecimento a um acervo privado de 45 songbooks e métodos de alta fidelidade e credibilidade histórica (como as obras de Almir Chediak e Real Books de Jazz). 

O objetivo principal é servir como uma ferramenta de apoio dinâmica para as aulas do professor: você digita os conhecimentos teóricos que o seu aluno já possui no momento (se ele domina ou não campos harmônicos, extensões ou cadências como o II-V-I) e o modelo varre a base de dados confiável para sugerir repertórios sob medida. O sistema permite filtrar as sugestões escolhendo uma tonalidade específica ou um gênero musical focado (como Jazz, Choro, MPB ou Bossa Nova), entregando um roteiro analítico completo com foco em notas-alvo (*target notes*) e estratégias de escalas para o improviso.

---

## Curadoria de Fontes e Engenharia de Dados (Data Ingestion)

Para abastecer a base de conhecimento privada do assistente, foi realizada a ingestão de 46 volumes que servem como autoridade em harmonia funcional de Bossa Nova, MPB, Choro e Jazz. A base de dados foi categorizada em três grandes datasets de acordo com sua origem e perfil de digitalização dominante:

| Coleção / Dataset | Volume de Arquivos | Autores e Pilares Principais | Estado do OCR e Integridade Visual Predominante |
| :--- | :---: | :--- | :--- |
| **Coleção Lumiar (Songbooks Nacionais)** | 22 PDFs | Almir Chediak (Bossa Nova, Tom Jobim, Chico Buarque, Caetano Veloso, Ary Barroso, Djavan, João Bosco, etc.), Noel Rosa, Cartola, Gilberto Gil. | Híbrido. Mescla páginas com texto vetorial nativo de alta resolução com diagramas antigos de braço de guitarra escaneados com ruído analógico. |
| **Coleção Internacional (Jazz & Real Books)** | 18 PDFs | Hal Leonard (Real Books Vol. 1 a 4, Blues, Just Standards), Bill Evans Fake Book, Pat Metheny, Herbie Hancock, Joe Pass, Wes Montgomery, Scott Henderson. | Imagem de Alta Resolução. PDFs puramente visuais, sem texto selecionável por padrão de mouse, mas apresentando alto contraste e linhas de cifras nítidas. |
| **Métodos e Acervos de Choro** | 6 PDFs | Altamiro Carrilho, Pixinguinha, Coletâneas de Choro, Coletâneas de Canções do Século XX. | Baixa Resolução / Manuscritos. Material digitalizado de acervos antigos, partituras puras sem texto cifrado adjacente ou escritas à mão. |

> **Nota:** Essa massa de dados engloba uma tipologia mista de arquivos — variando desde PDFs com OCR 100% legível e editável até escaneamentos analógicos complexos e imagens puramente visuais —, servindo como o cenário ideal para o estresse do motor de visão computacional da IA. A presença de cancioneiros densos e métodos de virtuoses da guitarra (como Wes Montgomery e Joe Pass) garante que o sistema possua profundidade teórica tanto para triagens básicas quanto para roteiros de improvisação avançados.

---

## Fase 1: Testes de Estresse e Ingestão de Dados

Nesta fase, testamos o NotebookLM ao limite enviando vários tipos de arquivos com qualidades diferentes (desde PDFs limpos até imagens antigas e borradas). O objetivo foi descobrir exatamente onde a IA funciona bem e onde ela falha na hora de ler as letras, cifras e diagramas das músicas quando o arquivo está com qualidade ruim.

### Documentação de Testes (Perguntas vs. Resultados)

#### Caso de Teste 1: Validação de OCR Nativo & Híbrido
* **Pergunta:** *"Com base no livro Bossa Nova 1, quais os acordes utilizados para a música 'Até parece' de Carlos Lyra?"*
* **Resultado Técnico:** **Sucesso.** O modelo mapeou com precisão a sequência harmônica completa, identificando extensões complexas como `B7(b9)`, `F#m7(b5)`, `E7(13)`, `E7(b13)`, `G#m7(11)` e `G7(#11)`. A única divergência menor foi a leitura do acorde `D(6/9)` (presente no diagrama da imagem `ate_parece.png`), extraído textualmente como `D9`. O modelo conseguiu varrer as linhas iniciais e o corpo da cifra perfeitamente.

#### Caso de Teste 2: Mapeamento de Ruído e Auto-Correção
* **Pergunta:** *"Você encontrou algum caractere estranho, sequência de símbolos sem sentido (como '11111;;' ou letras embaralhadas) ou acordes com grafia corrompida ao ler a cifra de 'Desejo do mar'?"*
* *(Nota de Engenharia de Dados: Para formular esta consulta com precisão, o trecho original do PDF foi previamente copiado para um editor de texto plano para inspecionar os metadados gerados pelo OCR analógico. Isso permitiu antecipar quais strings estranhas o modelo indexaria na base de conhecimento).*
* **Resultado Técnico:** **Sucesso Avançado (Auto-Correção).** O modelo não apenas identificou os ruídos gerados pela leitura analógica dos diagramas visuais dos acordes (identificando strings estranhas como `# 11111;;` e `~i 11.,`), como usou inteligência de contexto de Bossa Nova para tratar os dados corrompidos. Em sua análise semântica, apontou que a string `GIM` correspondia a `G7M` e deduziu que `D~(9)` representava a cifragem que de fato correspondia ao acorde $D_7^4(9)$ na imagem `desejo_do_mar.png`.

#### Caso de Teste 3: Confronto de Imagem de Alta Resolução
* **Pergunta:** *"Quais os acordes da música 'In April' de Bill Evans e em que página se encontra essa música?"*
* **Resultado Técnico:** **Sucesso Parcial (Mapeamento Estrutural com Erros de Sintaxe Harmônica Complexa).** Avaliando o *Bill Evans Fake Book* (imagem `in_april.png`), o NotebookLM localizou com exatidão a página 20 e segmentou a harmonia por seções. No entanto, a análise fina dos acordes revealed os limites do modelo para decodificar convenções avançadas de arranjo e escrita musical em formato de imagem.
* **Pontos de Erro Detectados (Análise de Engenharia Harmônica):**
  1. **Omissão de Acidentes:** Na partitura original, o segundo acorde é um $Bb7(\flat13 \flat9)$, mas o modelo ignorou o símbolo de bemol da 13ª, extraindo-o como `Bb7(13 b9)`.
  2. **Confusão com Linha de Baixo Caminhando:** No trecho onde o acorde de $Db9$ se mantém enquanto o baixo faz um movimento linear de descida ($Db9/Bb \rightarrow /Ab$), o motor visual da IA se confundiu com as barras de inversão e inventou um acorde inexistente (`Ab/Eb`) na transcrição textual.
  3. **Inabilidade com Convenções Verticais (Line Cliché):** Diante da grafia de um clichê de linha harmônica — onde um acorde menor passa por uma sétima maior e cai para a sétima menor empilhada verticalmente —, a IA tentou recriar o desenho visual usando blocos matemáticos, gerando a string truncada `Bbm(#7/7)(b7)`. O modelo falhou em interpretar a semântica do movimento melódico interno do jazz, priorizando uma reconstrução gráfica aproximada (e incorreta) no texto.
* **Conclusão:** O motor de visão computacional é excelente para guias rápidos e mapeamento macro de PDFs limpos, mas falha ao processar inversões dinâmicas de baixo e empilhamentos harmônicos verticais típicos do Jazz. A validação humana de um especialista continua sendo indispensável.

#### Caso de Teste 4: Verificação de Ambiguidade e Auto-Correção Histórica
* **Pergunta:** *"Encontre a música 'Na baixa do sapateiro' de Ary Barroso. Quais os 10 primeiros acordes?"*
* **Análise do Comportamento do Modelo:** O PDF utilizado nesta ingestão possui uma estrutura complexa, unindo o Volume 1 (composto por imagens antigas e borradas) e o Volume 2 (com trechos textuais selecionáveis). 
* **Primeira Resposta da IA:** O modelo identificou que a música é mundialmente conhecida pelo título alternativo de "Bahia" e mapeou a harmonia disposta na página 36 do Volume 2 (`G7`, `C7`, `F6...`). 
* **Segunda Resposta (Refinamento):** Após uma análise mais profunda das fontes indexadas, o próprio motor do NotebookLM emitiu uma errata espontânea no chat, localizando a partitura original na página 89 do Volume 1 (zona de imagem de baixa resolução) e extraindo com sucesso a sequência harmônica real com suas respectivas extensões da melodia (`Bb7`, `E7(#9)`, `Eb7M`, `Ebm6`, `Ab7(13)`, `Dm7`, `Db7(9)`, `Cm7(9)`, `B7(9)`, `Bb7`).
* **Conclusão:** O modelo demonstrou alta resiliência visual, sendo capaz de decodificar a cifragem em uma imagem borrada e antiga, além de possuir capacidade de auto-correção textual ao cruzar volumes diferentes do mesmo autor.

#### Caso de Teste 5: Gargalo Técnico (Partitura Pura, Manuscritos e Baixa Resolução)
* **Perguntas de Estresse:**
* 1. *"Na música 'We Can Work It Out' (The Beatles), em que nota inicia a melodia da voz e em que página está essa música?"*
* 2. *"Na música 'Eu e Tu' de Altamiro Carrilho, quais os 6 primeiros acordes?"*
* **Resultado Técnico:** **Falha / Limite Operacional.** Frente a manuscritos antigos e partituras sem nenhuma cifragem textual explícita, o sistema atingiu seu limite físico de processamento de imagem. O modelo informou que as páginas correspondentes não puderam ser indexadas por falta de texto legível.
* **Conclusão de Engenharia:** LLMs baseadas em NotebookLM falham ao tentar decodificar notação musical puramente visual (pautas, claves e posições de notas na grade) caso não haja dados em texto ou cifras explícitas adjacentes para apoiar o contexto.

---

### Evidências de Teste (Auditoria de Resultados)

#### Caso de Teste 1: Até Parece (Leitura de OCR Nativo e Híbrido)
| Documento Original (PDF) | Resposta da IA |
| :---: | :---: |
| ![PDF Até Parece](images/ate_parece.png) | ![Resposta IA Até Parece](images/ate_parece_resposta.jpeg) |

#### Caso de Teste 2: Desejo do Mar (Mapeamento de Ruído e Auto-Correção)
| Documento Original (PDF) | Identificação do Ruído (IA) | Resposta com Auto-Correção (IA) |
| :---: | :---: | :---: |
| ![PDF Desejo do Mar](images/desejo_do_mar.png) | ![Resposta IA Desejo do Mar](images/desejo_do_mar_resposta.jpeg) | ![Resposta IA Desejo do Mar](images/desejo_do_mar_resposta_2.jpeg) |

#### Caso de Teste 3: In April (Confronto de Imagem de Alta Resolução)
| Documento Original (PDF) | Resposta da IA |
| :---: | :---: |
| ![PDF In April](images/in_april.png) | ![Resposta IA In April](images/in_april_resposta.jpeg) |

#### Caso de Teste 4: Na Baixa do Sapateiro (Verificação de Ambiguidade)
| Partitura Original - Vol. 1 | Partitura Original - Bahia | 
| :---: | :---: |
| ![PDF Ary Barroso](images/bahia.png) | ![PDF Ary Barroso](images/na_baixa_do_sapateiro.png) |
| Primeira Identificação (Vol. 2 / "Bahia") | Resposta Corrigida (Vol. 1 / Pág. 89) |
| ![Resposta IA Ary Barroso](images/na_baixa_do_sapateiro_resposta_1.jpeg) | ![Resposta IA Ary Barroso](images/na_baixa_do_sapateiro_resposta_2.jpeg) |

#### Caso de Teste 5: Gargalo Técnico (Partituras Puras e Manuscritos)
| Documento Original (PDF) Tu e Eu | Documento Original (PDF) We Can Work It Out | Resposta da IA (Limite Atingido) |
| :---: | :---: | :---: |
| ![PDF Beatles/Altamiro](images/tu_e_eu.png) | ![Resposta IA Limite](images/we_can_work_it_out.png) | ![Resposta IA Limite](images/tu_e_eu_resposta.jpeg) |

---

### Limitações Técnicas do Ambiente de Prototipagem (NotebookLM)

Como o escopo deste projeto para o bootcamp visa a criação de um **protótipo funcional de caderno de estudos de uso estritamente pessoal**, o ambiente do NotebookLM supriu as necessidades de indexação. Contudo, os testes de estresse revelaram limitações severas na ferramenta que inviabilizam sua abertura direta para o público geral:

* **Ausência de Camada Isolada de Sistema (System Role):** O NotebookLM não possui um painel para travar instruções de sistema. O arquivo de regras reside no mesmo nível das fontes harmônicas, competindo por atenção semântica e exigindo que o operador cole as regras manualmente como o primeiro prompt do chat para mitigar desvios de rota.
* **Degradação de Performance por Latência Unificada:** O modelo sofre com lentidão a cada nova mensagem enviada, pois precisa reavaliar o manual complexo junto com os 45 PDFs de acervo. Essa latência unificada afeta inclusive a formulação de respostas teóricas abstratas simples (que deveriam ser instantâneas), pois a ferramenta não consegue separar o tempo de processamento de regras do tempo de busca pesada nos livros.
* **Vulnerabilidade de Exposição de IP (Pirataria):** A interface de compartilhamento do NotebookLM expõe nativamente a barra de fontes lateral e as páginas originais dos PDFs nas citações das respostas. Compartilhar o link do caderno com alunos ou terceiros causaria a exposição direta de materiais protegidos por direitos autorais, inviabilizando o uso público da ferramenta neste ambiente.

---

### Roadmap de Evolução Técnica (Melhorias Futuras para Produção Comercial)

Para escalar este protótipo de um assistente de uso pessoal para uma aplicação comercial multiusuário aberta ao público de forma "plug-and-play" e segura, as seguintes implementações de engenharia de software back-end devem ser realizadas como próximos passos:

#### 1. Migração para Infraestrutura Própria em Python (FastAPI + LangChain)
* **Isolamento de Regras (System Instructions):** O conteúdo do manual de conduta será injetado diretamente no parâmetro corporativo `system_instruction` da API do Gemini. Ao rodar em camada de código oculta, as regras agem como leis físicas da IA, impedindo qualquer tentativa do usuário final de burlar as diretrizes pedagógicas.
* **Modelo Black-Box de Proteção de Direitos Autorais:** O usuário final interagirá exclusivamente com uma tela limpa de chat customizada. Os 45 PDFs originais ficarão isolados e criptografados em um servidor privado ou banco de dados vetorial corporativo. O sistema fará a busca RAG dos dados, mas ocultará os arquivos brutos, títulos e numeração de páginas, entregando ao cliente apenas as saídas textuais das análises, eliminando 100% o risco de pirataria.

#### 2. Implementação de Triagem Automatizada Multi-Estados e Banco PostgreSQL
* **Interface de Triagem por Etapas:** Acoplamento de um fluxo conversacional dinâmico onde o sistema realiza um questionário interativo de triagem (enviando uma pergunta de cada vez) para catalogar o nível do aluno.
* **Persistência e Cache Otimizado:** Armazenamento do progresso harmônico dos alunos e do histórico de cache de 20 músicas (anti-repetição) diretamente em tabelas relacionais do PostgreSQL, desonerando a janela de contexto da LLM.
* **Otimização Assíncrona de Latência:** Segregação dos tempos de resposta no back-end. Na fase de conversação teórica pura (triagem), o sistema responderá em milissegundos (consumindo apenas o prompt de sistema). O tempo de processamento de busca pesada ficará restrito exclusivamente ao momento de varredura assíncrona do banco vetorial na geração do repertório.

#### 3. Vetorização Avançada de Partituras Puras (OMR + Vector Embeddings)
* Integração de modelos de visão computacional focados em *Optical Music Recognition* (OMR) acoplados a bancos vetoriais (**ChromaDB** ou **Pinecone**). Isso permitirá transformar o desenho das notas nas pautas musicais de manuscritos antigos (gargalo do Caso de Teste 5) em vetores semânticos, estendendo a capacidade de análise harmônica para além do texto cifrado tradicional.

---

## Fase 2: Arquitetura de Prompt e Mapeamento de Estados

As diretrizes do assistente utilizam padrões avançados de engenharia de prompt para garantir previsibilidade metodológica e eliminação de alucinações teoricamente incorretas:

* **Injeção de Contexto Restrito (*Grounding*):** Bloqueio total de barramento à internet aberta para fontes harmônicas, forçando o modelo a atuar estritamente sobre a estrutura vetorial dos métodos injetados.
* **Pensamento em Cadeia Baseado em Domínio (*Domain Chain-of-Thought*):** Orientação para o modelo analisar a cadência harmônica (movimentos de II-V-I ou resoluções) antes de processar dados, permitindo a auto-correção contextual de caracteres corrompidos pelo OCR.

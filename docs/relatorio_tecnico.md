# Smart Repertoire Guide

## Contexto e Objetivos

Este projeto foi desenvolvido como parte prática integrante da formação no **Bootcamp Bradesco - GenAI, Dados & Cyber**, realizado em parceria com a **DIO (Digital Innovation One)**. O objetivo é aplicar conceitos de curadoria de dados, inteligência artificial contextualizada (RAG - *Retrieval-Augmented Generation*) e engenharia de prompts na construção de um ecossistema de aprendizagem focado no ensino musical.

O ensino de improvisação na guitarra e no violão exige o acesso a um repertório harmônico preciso e estruturado de acordo com o nível de proficiência do estudante. No entanto, instrutores enfrentam desafios crônicos ao buscar materiais didáticos na internet aberta para preparar suas aulas:

* **Poluição e Inconsistência de Dados:** Plataformas públicas de cifras frequentemente contêm erros de transcrição, omissão de extensões (como nonas, décimas terceiras ou alterações de jazz) e diagramas incorretos que distorcem a realidade da peça musical.
* **Sobrecarga Cognitiva:** Motores de busca tradicionais não filtram repertórios por densidade harmônica ou critérios pedagógicos (como presença de modulações ou número de acordes na estrutura), exigindo uma filtragem manual demorada por parte do professor.

O **Smart Repertoire Guide** atua como um assistente especialista e caderno de consulta pessoal para o instrutor de música, baseado em inteligência artificial. Para atender aos critérios pedagógicos e operacionais, o projeto foi estruturado em dois cenários de banco de dados:

1. **Cenário de Homologação (Bootcamp DIO):** Utiliza uma base de dados fundamentada em links institucionais e materiais de domínio público gratuitos localizados na internet. O objetivo é demonstrar com total segurança jurídica, fidelidade e transparência o potencial técnico e a funcionalidade prática do motor de IA. Não envolve o meu acervo pessoal pois é um conteúdo protegido por direitos autorais.
2. **Cenário de Production (Meu Uso Pessoal):** Opera sob uma política estrita de fonte fechada (*Grounding*), expandindo a base de conhecimento para o meu acervo pessoal, composto por 46 songbooks e métodos de alta fidelidade e credibilidade histórica (como as obras de Almir Chediak e Real Books de Jazz).

O objetivo principal do ecossistema é servir como uma ferramenta de apoio dinâmica para aulas de professores de música: você digita os conhecimentos teóricos que o seu aluno já possui no momento (se ele domina ou não campos harmônicos, extensões ou cadências como o II-V-I) e o modelo varre a base de dados ativa para sugerir repertórios sob medida. O sistema permite filtrar as sugestões escolhendo uma tonalidade específica ou um gênero musical focado (como Jazz, Choro, MPB ou Bossa Nova), entregando um roteiro analítico completo com foco em notas-alvo (*target notes*) e estratégias de escalas para o improviso.

### O Papel do Guia de Conduta

Para garantir que a inteligência artificial funcione exatamente como um professor de música precisa, o sistema é controlado por um arquivo rígido de regras chamado [Guia de Conduta](./guia_de_conduta.txt). Esse manual de instruções dita como a IA deve se comportar, garantindo três pontos principais:

* **Evita Alucinações:** Reforça o bloqueio do uso da internet comum para buscar cifras, obrigando a IA a ler apenas os arquivos de confiança enviados pelo professor.
* **Organiza a Dificuldade:** Define regras claras de separação para os Níveis 1, 2 e 3 (Iniciante, Intermediário e Avançado), garantindo que um aluno iniciante nunca receba uma música complexa demais.
* **Limpa Textos Ruins:** Instruções específicas ensinam a IA a ignorar sujeiras visuais e erros de leitura de PDFs antigos (como símbolos sem sentido gerados pelo escaneamento). Isso permite que ela corrija cifras quebradas usando a lógica da própria música, contornando os problemas de arquivos escaneados de baixa qualidade ou manuscritos onde o leitor visual da IA (OCR) falha em extrair o texto perfeitamente.

---

## Curadoria de Fontes e Engenharia de Dados (Data Ingestion)

Para alimentar a base de conhecimento do assistente, a estrutura de dados foi dividida de acordo com os dois cenários de operação do sistema, garantindo tanto a entrega pública do ambiente de testes quanto a profundidade do acervo pessoal:

### 1. Base de Dados Pública (Cenário de Homologação - Bootcamp DIO)
Consiste em uma seleção de fontes abertas e gratuitas de alta autoridade teórica, histórica e pedagógica. Esses materiais fornecem o embasamento necessário para que o NotebookLM localize músicas, cifras e regras sem infringir direitos autorais:

* [Música Brasilis](https://musicabrasilis.org.br/pt-br/) - Portal de referência para partituras e acervo da música brasileira.
* [Bossa Nova Fakebook Vol. 2 (PDF)](https://musicishealing.com/Bateria/Pagode/Library/BossaNovaFakebook2.pdf) - Livro de cifras focado no repertório tradicional de Bossa Nova.
* [Jazz Library](https://jazz-library.com/songs/) - Base de dados pública com estruturas harmônicas e músicas clássicas do Jazz.
* [Anais da ANPPOM - Artigo sobre Bossa Nova (PDF)](https://anppom.org.br/anais/anaiscongresso_anppom_2025/papers/182.pdf) - Estudo acadêmico sobre a estruturação e evolução harmônica nacional.
* [Análise Harmônica e Improvisação (PDF)](https://cdn.prod.website-files.com/65dcd4c1ddd64f2ee53eb284/674829d8f32b8fbebe6a6019_43114043937.pdf) - Material didático focado em técnicas de roteiros de improviso.
* [Artigo Técnico - Ritmo e Harmonia (UNICAMP)](https://www.iar.unicamp.br/wp-content/uploads/2021/07/V2_ED03_A1_BossaNova.pdf) - Documento universitário que analisa as cadências da música popular brasileira.
* [Songbook As 101 Melhores Canções do Século XX (PDF)](https://ekladata.com/kvdp5s2Kp2nEQ7-yNaJbgheQFH0/Songbook-As-101-Melhores-Cancoes-do-Seculo-XX-Vol-1.pdf) - Cancioneiro aberto contendo clássicos da música nacional e internacional.
* [Guia de Conduta do Sistema (Texto Plano)](./guia_de_conduta.txt) - O arquivo de instruções que deve ser injetado no NotebookLM para controlar o comportamento da IA.

> **Nota de Instalação:** Para ativar o assistente em seu próprio ambiente, o usuário pode baixar o arquivo `guia_de_conduta.txt` diretamente deste repositório e fazer o upload dele na barra lateral de "Fontes" do NotebookLM, ou simplesmente copiar o seu conteúdo textual e colá-lo como a primeira mensagem do chat.

### 2. Base de Dados Privada (Cenário de Produção - Meu Uso Pessoal)
Para o uso no dia a dia das aulas de guitarra, o sistema é expandido com o meu acervo pessoal de 46 volumes digitalizados. Essa base foi categorizada em três grandes grupos de acordo com a sua origem e perfil visual:

| Coleção / Dataset | Volume de Arquivos | Autores e Pilares Principais | Estado do OCR e Integridade Visual Predominante |
| :--- | :---: | :--- | :--- |
| **Coleção Lumiar (Songbooks Nacionais)** | 22 PDFs | Almir Chediak (Bossa Nova, Tom Jobim, Chico Buarque, Caetano Veloso, Ary Barroso, Djavan, João Bosco, etc.), Noel Rosa, Cartola, Gilberto Gil. | Híbrido. Mescla páginas com texto digital nativo de alta resolução com diagramas antigos de braço de guitarra escaneados com ruído visual. |
| **Coleção Internacional (Jazz & Real Books)** | 18 PDFs | Hal Leonard (Real Books Vol. 1 a 4, Blues, Just Standards), Bill Evans Fake Book, Pat Metheny, Herbie Hancock, Joe Pass, Wes Montgomery, Scott Henderson. | Imagem de Alta Resolução. PDFs puramente visuais, sem texto selecionável por padrão, mas apresentando alto contraste e linhas de cifras nítidas. |
| **Métodos e Acervos de Choro** | 6 PDFs | Altamiro Carrilho, Pixinguinha, Coletâneas de Choro, Coletâneas de Canções do Século XX. | Baixa Resolução / Manuscritos. Material digitalizado de acervos antigos, partituras puras sem texto cifrado próximo ou escritas à mão. |

> **Nota:** Essa massa mista de arquivos serviu como o cenário ideal para testarmos os limites do leitor visual (OCR) da inteligência artificial do NotebookLM. A presença de métodos densos de mestres da guitarra garante que o sistema tenha profundidade teórica tanto para triagens básicas quanto para roteiros avançados de improvisação.

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
* **Resultado Técnico:** **Sucesso Parcial (Mapeamento Estrutural com Erros de Sintaxe Harmônica Complexa).** Avaliando o *Bill Evans Fake Book* (imagem `in_april.png`), o NotebookLM localizou com exatidão a página 20 e segmentou a harmonia por seções. No entanto, a análise fina dos acordes revelou os limites do modelo para decodificar convenções avançadas de arranjo e escrita musical em formato de imagem.
* **Pontos de Erro Detectados (Análise de Engenharia Harmônica):**
  1. **Omissão de Acidentes:** Na partitura original, o segundo acorde é um $Bb7(\flat13 \flat9)$, mas o modelo ignorou o símbolo de bemol da 13ª, extraindo-o como `Bb7(13 b9)`.
  2. **Confusão com Linha de Baixo Caminhando:** No trecho onde o acorde de $Db9$ se mantém enquanto o baixo faz um movimento linear de descida ($Db9/Bb \rightarrow /Ab$), o motor visual da IA se confundiu com as barras de inversão e inventou um acorde inexistente (`Ab/Eb`) na transcrição textual.
  3. **Inabilidade com Convenções Verticais (Line Cliché):** Diante da grafia de um clichê de linha harmônica — onde um acorde menor passa por uma sétima maior e cai para a sétima menor empilhada verticalmente —, a IA tentou recriar o desenho visual usando blocos matemáticos, gerando a string truncada `Bbm(#7/7)(b7)`. O modelo falhou em interpretar a semântica do movimento melódico interno do jazz, priorizando uma reconstrução gráfica aproximada (e incorreta) no texto.
* **Conclusão:** O motor de visão computacional é excelente para guias rápidos e mapeamento macro de PDFs limpos, mas falha ao processar inversões dinâmicas de baixo e empilhamentos harmônicos verticais típicos do Jazz. A validação humana de um especialista continua sendo indispensável.

#### Caso de Teste 4: Verificação de Ambiguidade e Auto-Correção Histórica
* **Pergunta:** *"Encontre a música 'Na baixa do sapateiro' de Ary Barroso. Quais os 10 primeiros acordes?"*
* **Análise do Comportamento do Modelo:** O PDF utilizado nesta ingestão possui uma estrutura complexa, unindo o Volume 1 (composto por imagens antigas e borradas) e o Volume 2 (com trechos textuais selecionáveis). 
* **Primeira Resposta da IA:** O modelo identificou que a música é mundialmente conhecida pelo título alternativo de "Bahia" e mapeou a harmonia disposta na página 36 do Volume 2 (`G7`, `C7`, `F6...`). 
* **Segunda Resposta (Refinamento):** Após uma análise mais profunda das fontes indexadas, o próprio motor do NotebookLM emitiu uma errata espontânea no chat, localizando a partitura original na página 89 do Volume 1 (zona de imagem de baixa resolução) e extraindo com sucesso a sequência harmônica real com suas respectivas extensões (`Bb7`, `E7(#9)`, `Eb7M`, `Ebm6`, `Ab7(13)`, `Dm7`, `Db7(9)`, `Cm7(9)`, `B7(9)`, `Bb7`).
* **Conclusão:** O modelo demonstrou alta resiliência visual, sendo capaz de decodificar a cifragem em uma imagem borrada e antiga, além de possuir capacidade de auto-correção textual ao cruzar volumes diferentes do mesmo autor.

#### Caso de Teste 5: Gargalo Técnico (Partitura Pura, Manuscritos e Baixa Resolução)
* **Perguntas de Estresse:**
* 1. *"Na música 'We Can Work It Out' (The Beatles), em que nota inicia a melodia da voz e em que página está essa música?"*
* 2. *"Na música 'Tu e Eu' de Altamiro Carrilho, quais os 6 primeiros acordes?"*
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

## 🔬 Fase 2: Arquitetura de Prompt e Engenharia de Controle

Para garantir que a inteligência artificial funcione exatamente como um professor de música precisa e não invente respostas fora das fontes oficiais, o comportamento do sistema foi blindado usando uma técnica de Engenharia de Prompt Estruturada. Todo o fluxo do chat é governado pelo arquivo [Guia de Conduta](./guia_de_conduta.txt).

### 1. Inicialização por Injeção de Estado (Overriding)
Durante os testes da Fase 1, descobriu-se uma vulnerabilidade de concorrência: quando os manuais de regras são colocados apenas como arquivos na barra lateral de fontes do NotebookLM, a massa de dados dos songbooks compete de igual para igual com as regras. Perguntas diretas do usuário por músicas específicas faziam a IA buscar o dado bruto e ignorar as restrições pedagógicas (causando um *prompt bypass*).

**A Solução Técnica:** O sistema foi projetado para exigir que o usuário copie o conteúdo do `guia_de_conduta.txt` e o cole como a primeiríssima mensagem do chat. Essa ação força a IA a reescrever suas diretrizes base de comportamento (*overriding*), travando o modelo em uma máquina de estados imperativa que isola os PDFs estritamente como fontes de consulta secundárias.

### 2. Mapeamento de Estados Pedagógicos (Níveis de Alunos)
O Guia de Conduta divide o atendimento do assistente em três níveis rígidos de maturidade técnica, controlando a complexidade dos resultados que a IA tem permissão para entregar:

* **Nível 1 (Iniciante):** Restringe as sugestões a músicas com esqueletos harmônicos limpos (tríades e tétrades básicas), limite máximo de até 6 acordes por música e ausência total de inversões de baixo ou modulações. A abordagem de improvisação recomendada pela IA deve ser de **Escala Única (Centro Tonal)**, evitando que o aluno iniciante precise trocar de escala a cada acorde.
* **Nível 2 (Intermediário):** Permite músicas com mais de 6 acordes, introdução de cadências de preparação clássicas (como o II-V-I menor e maior), dominantes secundários e extensões básicas (6, 9 e 13). A estratégia de improviso muda para **uma escala direta por acorde** (Modos Gregos).
* **Nível 3 (Avançado):** Libera o acesso total ao acervo complexo, englobando modulações constantes, acordes alterados (como $\flat9$, $\sharp9$, $\flat13$) e rearmonizações avançadas. A abordagem de improvisação passa a detalhar até **10 opções teóricas por acorde** (incluindo uso de Menor Melódica, Bebop, Pentatônicas m6, Tons Inteiros, Diminuta, Dom-Dim e sobreposição de arpejos).

### 3. Máscara de Formatação de Saída (Output)
Para manter o padrão visual de um caderno de estudos limpo e profissional, o Guia de Conduta proíbe blocos longos de texto e força a IA a responder estruturando as sugestões em tabelas e tópicos divididos em 4 seções obrigatórias:

* **Identificação Macro:** Nome da música, compositor, tonalidade e links/fontes onde o arquivo foi localizado na base.
* **Análise Harmônica Detalhada:** Justificativa teórica do porquê aquela música pertence ao nível selecionado (destacando as cadências e tensões presentes).
* **Roteiro Pedagógico de Notas-Alvo (Target Notes):** Guia prático mostrando em quais notas da escala (priorizando terças e sétimas) o aluno deve repousar as frases em cima de cada acorde para marcar a mudança da harmonia.
* **Estratégia de Escalas aplicadas ao Improviso:** Mapeamento das escalas e modos que o guitarrista pode usar para criar os solos.

---

### Limitações Técnicas do Ambiente de Prototipagem (NotebookLM)

Como o escopo deste projeto para o bootcamp visa a criação de um **protótipo funcional de caderno de estudos de uso estritamente pessoal**, o ambiente do NotebookLM supriu as necessidades de indexação. Contudo, os testes de estresse revelaram limitações severas na ferramenta que inviabilizam sua abertura direta para o público geral:

* **Ausência de Camada Isolada de Sistema (System Role):** O NotebookLM não possui um painel para travar instruções de sistema. O arquivo de regras (Guia de Conduta) reside no mesmo nível das fontes harmônicas, competindo por atenção e exigindo que o operador cole as regras manualmente como o primeiro prompt do chat para mitigar desvios de rota. Isso inviabiliza o uso aberto ao público em um site, por exemplo, já que o usuário comum não teria acesso direto ao guia ou saberia como injetá-lo.
* **Degradação de Performance por Latência Unificada:** O modelo sofre com lentidão a cada nova mensagem enviada, pois precisa reavaliar o manual complexo junto com os 46 PDFs de acervo. Essa latência afeta inclusive a formulação de respostas teóricas abstratas simples (que deveriam ser instantâneas), pois a ferramenta não consegue separar o tempo de processamento de regras do tempo de busca pesada nos livros.
* **Vulnerabilidade de Exposição de IP (Pirataria):** A interface de compartilhamento do NotebookLM expõe nativamente a barra de fontes lateral e as páginas originais dos PDFs nas citações das respostas. Compartilhar o link do caderno com alunos ou terceiros causaria a exposição direta de materiais protegidos por direitos autorais, inviabilizando o uso público da ferramenta neste ambiente.

---

### Roadmap de Evolução Técnica (Melhorias Futuras para Produção Comercial)

Para escalar este protótipo de um assistente de uso pessoal para uma aplicação comercial multiusuário aberta ao público de forma "plug-and-play" e segura, as seguintes implementações de engenharia de software back-end devem ser realizadas como próximos passos:

#### 1. Migração para Infraestrutura Própria em Python (FastAPI + LangChain)
* **Isolamento de Regras (System Instructions):** O conteúdo do manual de conduta será injetado diretamente no parâmetro de configuração `system_instruction` da API do Gemini. Ao rodar em camada de código oculta, as regras agem como leis físicas da IA, impedindo qualquer tentativa do usuário final de burlar as diretrizes pedagógicas.
* **Modelo Black-Box de Proteção de Direitos Autorais:** O usuário final interagirá exclusivamente com uma tela limpa de chat customizada. Os 46 PDFs originais ficarão isolados e criptografados em um servidor privado ou banco de dados vetorial. O sistema fará a busca RAG dos dados, mas ocultará os arquivos brutos, títulos e numeração de páginas, entregando ao cliente apenas as saídas textuais das análises, eliminando 100% o risco de pirataria.

#### 2. Implementação de Triagem Automatizada Multi-Estados e Banco PostgreSQL
* **Interface de Triagem por Etapas:** Acoplamento de um fluxo conversacional dinâmico onde o sistema realiza um questionário interativo de triagem (enviando uma pergunta de cada vez) para catalogar o nível do aluno.
* **Persistência e Cache Otimizado:** Armazenamento do progresso harmônico dos alunos e do histórico de cache de 20 músicas (anti-repetição) diretamente em tabelas relacionais do PostgreSQL, desonerando a janela de contexto da LLM.
* **Otimização Assíncrona de Latência:** Segregação dos tempos de resposta no back-end. Na fase de conversação teórica pura (triagem), o sistema responderá em milissegundos (consumindo apenas o prompt de sistema). O tempo de processamento de busca pesada ficará restrito exclusivamente ao momento de varredura assíncrona do banco vetorial na geração do repertório.

#### 3. Vetorização Avançada de Partituras Puras (OMR + Vector Embeddings)
* **Processamento de Pautas Musicais:** Integração de modelos de visão computacional focados em *Optical Music Recognition* (OMR) acoplados a bancos vetoriais (**ChromaDB** ou **Pinecone**). Isso permitirá transformar o desenho das notas nas pautas musicais de manuscritos antigos (gargalo do Caso de Teste 5) em vetores semânticos, estendendo a capacidade de análise harmônica para além do texto cifrado tradicional.

---

## Miniguia de Estudo (Entrega Final)

Este guia consolida o conhecimento gerado durante o desenvolvimento do projeto, servindo como material de apoio para professores de música utilizarem o assistente com máxima eficiência.

### 1. Resumos Estruturados: O Fluxo Metodológico do Sistema
O assistente opera cruzando a teoria musical e a capacidade de leitura da IA em três etapas simples:
* **Injeção de Regras:** O professor define como o assistente deve se comportar colando o Guia de Conduta no chat.
* **Definição de Perfil:** O professor informa o nível teórico do aluno atual (Nível 1, 2 ou 3) e filtros opcionais (gênero musical ou tonalidade).
* **Varredura e Análise:** A IA lê as cifras e songbooks da base ativa, seleciona o repertório ideal e monta o roteiro analítico com as estratégias de escala e notas-alvo sem que o professor precise folhear dezenas de páginas manualmente.

### 2. Glossário de Conceitos Aprendidos

#### Termos de Tecnologia (Inteligência Artificial)
* **RAG (Retrieval-Augmented Generation):** Técnica que restringe as respostas da IA aos documentos fornecidos pelo usuário, impedindo que ela invente dados da internet comum.
* **Grounding (Ancoragem):** O ato de amarrar o conhecimento do modelo estritamente a uma base de dados real de confiança (no nosso caso, as fontes e os songbooks).
* **OCR (Optical Character Recognition):** O leitor visual que a IA usa para tentar transformar imagens de páginas escaneadas em textos e letras legíveis.
* **Prompt Bypass / Concorrência:** Erro técnico onde a IA ignora os comandos de regras para priorizar a busca direta dos dados brutos dos PDFs.

### 3. Prompts Reutilizáveis para Consulta (Casos Práticos e Templates)

Após colar o conteúdo do Guia de Conduta como a primeira mensagem do chat para ativar as regras do sistema, você pode copiar e colar qualquer uma das opções abaixo para gerar os roteiros de estudo personalizados:

#### Opção A: Gatilhos Rápidos (Exemplos de Casos Reais)
Consultas diretas que ativam as máquinas de estado e filtros do sistema de forma natural:

[PROMPT 1 - ATIVAÇÃO DE NÍVEL 1 + FILTRO TONAL]
```
Preciso de uma música no tom de Dm para um estudante iniciante em improvisação.
```

[PROMPT 2 - ATIVAÇÃO DE NÍVEL 2]
```
Preciso de uma música que possua vários dominantes secundários para um aluno.
```

[PROMPT 3 - ATIVAÇÃO DE NÍVEL 3]
```
Preciso de uma música com modulação para estudo de improvisação.
```

[PROMPT 4 - ESTRESSE HARMÔNICO AVANÇADO - NÍVEL 3]
```
Preciso de uma música com uso de mediante cromática para estudo avançado de improvisação.
```

#### Opção B: Templates Customizáveis (Para Novas Consultas)
Modelos estruturados onde você pode preencher os colchetes com os critérios exatos da sua aula:

[PROMPT TEMPLATE - REPERTÓRIO INICIANTE]
```
Filtre na base de dados uma música de [GÊNERO MUSICAL] na tonalidade de [TONALIDADE] adequada para um aluno de Nível 1 (Iniciante). Monte a tabela estruturada e o roteiro analítico com foco em escala única de centro tonal.
```

[PROMPT TEMPLATE - REPERTÓRIO INTERMEDIÁRIO]
```
Busque no acervo ativo uma peça de [GÊNERO MUSICAL] que contenha cadências de II-V-I e aplique as regras de Nível 2 (Intermediário). Entregue a análise harmônica e a estratégia de improviso indicando um modo grego específico para cada acorde.
```

[PROMPT TEMPLATE - DESAFIO AVANÇADO]
```
Selecione uma composição de [COMPOSITOR OU GÊNERO] que apresente modulações constantes ou acordes alterados, seguindo estritamente as diretrizes de Nível 3 (Avançado). Detalhe as opções de escalas avançadas (como menor melódica ou bebop) e o mapa de target notes.
```

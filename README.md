# Smart Repertoire Guide 🎸

O **Smart Repertoire Guide** é um ecossistema de aprendizagem e caderno de consulta automatizado, baseado em Inteligência Artificial, projetado para auxiliar professores de guitarra e violão na curadoria e estruturação pedagógica de repertórios voltados ao ensino de improvisação musical.

Este projeto foi desenvolvido como a entrega prática final para a formação no **Bootcamp Bradesco - GenAI, Dados & Cyber**, realizado em parceria com a **DIO (Digital Innovation One)**.

> 📖 **Nota de Navegação:** Este arquivo serve como a vitrine enxuta do projeto, resumindo os critérios exigidos pelo edital. Para uma análise aprofundada sobre a engenharia de dados, testes de estresse com imagens, tratamento de OCR e a arquitetura de software de back-end proposta para o futuro do sistema, acesse o nosso [Relatório Técnico Completo](./relatorio_tecnico.md).

---

## 🎯 Contexto e Objetivos

O ensino e o aprendizado de improvisação musical na guitarra e no violão dependem diretamente do acesso a um repertório harmônico estruturado com absoluta precisão teórica. Na internet aberta, instrutores e estudantes enfrentam dados poluídos (cifras incorretas, diagramas bizarros e omissão de extensões fundamentais de acordes) e sobrecarga cognitiva, já que os motores de busca tradicionais não filtram músicas por densidade harmônica ou critérios pedagógicos (como número de acordes ou presença de modulações).

O objetivo deste material é validar o uso de modelos de linguagem (LLMs) no ecossistema do **Google NotebookLM** para:
* Catalogar, centralizar e estruturar o conhecimento harmônico aplicado a gêneros complexos como Bossa Nova, MPB, Choro e Jazz.
* Atuar sob uma política estrita de fonte fechada (*Grounding*), eliminando alucinações.
* Criar um motor de consulta dinâmica onde o professor insere o nível atual de conhecimento do aluno (se domina campos harmônicos, cadências clássicas como II-V-I ou extensões) e o modelo varre a base de dados confiável para sugerir repertórios sob medida.
* Entregar roteiros analíticos instantâneos com foco em notas-alvo (*target notes*) e estratégias de escalas para o improviso.

---

## 📚 Curadoria de Fontes (Data Ingestion)

Para atender aos critérios operacionais e pedagógicos do projeto, a estrutura de dados foi dividida em dois cenários complementares:

### 1. Cenário de Homologação (Bootcamp DIO)
Para demonstrar a viabilidade técnica e a segurança jurídica do projeto sem infringir direitos autorais, a base de conhecimento pública utiliza fontes abertas e gratuitas de alta autoridade histórica e pedagógica:
1. [Acervo Digital da Música Brasileira - Pixinguinha (Funarte)](https://www.funarte.gov.br/) - Portal oficial do governo que disponibiliza partituras, arranjos e documentos históricos abertos sobre a estruturação do Choro tradicional.
2. [Métodos de Harmonia e Improvisação Jazzística (Internet Archive)](https://archive.org/) - Biblioteca digital pública mundial utilizada para indexar manuais de domínio público sobre a abordagem *Chord-Scale* e a teoria do Jazz.
3. [Biblioteca Digital de Teses e Dissertações (USP)](https://teses.usp.br/) - Repositório acadêmico aberto utilizado para consultar análises estruturadas sobre a evolução harmônica e as cadências da Bossa Nova e da MPB.
4. [Documentação de Suporte Oficial do Google NotebookLM](https://support.google.com/notebooklm) - Base técnica para o entendimento do comportamento do motor RAG, limites de tokens e extração de texto via visão computacional.

### 2. Cenário de Production (Meu Uso Pessoal)
Diferente da entrega pública, todo o processo real de construção, estresse e validação pedagógica do motor de IA no NotebookLM foi complementado e expandido para o meu uso do dia a dia nas aulas através de um acervo privado de **46 songbooks e métodos digitalizados** de alta fidelidade e credibilidade histórica (como as obras completas de Almir Chediak e Real Books de Jazz).

---

## 🔬 Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Para garantir o grau de confiabilidade necessário e eliminar o risco de alucinações, foram conduzidas consultas estratégicas e testes de estresse práticos para mapear a capacidade de decodificação do modelo:

### 1. Testes de Estresse de Visão Computacional (OCR)
* **Validação de OCR Nativo & Híbrido (Sucesso):** O modelo mapeou com precisão sequências de Bossa Nova, identificando perfeitamente extensões complexas (como `B7(b9)`, `F#m7(b5)`, `G#m7(11)`), apresentando pequenas variações aceitáveis de sintaxe.
* **Mapeamento de Ruído e Auto-Correção (Sucesso Avançado):** Ao ler metadados gerados por escaneamentos analógicos com forte ruído visual (lixo de caracteres como `# 11111;;` ou `~i 11.,`), o modelo usou a inteligência do contexto musical para auto-corrigir os dados corrompidos, deduzindo com precisão que a string truncada `GIM` correspondia ao acorde `G7M`.
* **Confronto de Alta Resolução (Sucesso Parcial):** Ao processar Jazz Fake Books puramente visuais, localizou as páginas com exatidão, mas demonstrou limites finos de imagem: omitiu acidentes sutis em acordes alterados verticais e confundiu barras de inversão de baixo caminhando (como `Db9 / Bb -> / Ab`).
* **Gargalo Técnico (Limite Operacional):** Frente a manuscritos antigos e partituras puras em grade sem nenhuma cifragem textual explícita, o sistema atingiu seu limite físico de processamento de imagem, informando que as páginas não puderam ser indexadas por falta de texto legível.

### 2. Concorrência entre Busca Direta e Controle de Fluxo
Durante os experimentos, descobriu-se que arquivos de texto contendo manuais de regras hospedados na barra lateral de fontes competem diretamente com a massa de dados do repositório. Consultas fortes com nomes de músicas específicas faziam a IA buscar o dado bruto e burlar as diretrizes pedagógicas (*prompt bypass*).

**A Solução das "Cicatrizes":** O comportamento do modelo foi totalmente blindado por meio do desenvolvimento de um script estruturado chamado [Guia de Conduta](./guia_de_conduta.txt). Este arquivo força a IA a atuar como uma máquina de estados imperativa, exigindo que o operador o injete como a **primeiríssima mensagem do chat**, isolando os PDFs estritamente como fontes de consulta secundárias.

---

## 📖 Miniguia de Estudo (Entrega Final)

O resultado final consolidado da curadoria gerou o seguinte mapa conceitual de estudos para suporte ao professor de música:

### 1. Glossário de Conceitos Aprendidos pela IA
* **Grounding (Ancoragem):** Técnica que ancora as respostas da IA exclusivamente na base de dados de confiança fornecida, proibindo alucinações baseadas na internet externa.
* **Target Notes (Notas-Alvo):** Técnica de improvisação melódica focada em repousar as frases nas terças (3ª) e sétimas (7ª) de cada acorde, evidenciando a mudança da harmonia.
* **Chord-Scale (Acorde-Escala):** Abordagem que mapeia escalas ou modos específicos (ex: Dórico, Lídio, Alterada) para serem executados individualmente sobre cada acorde da progressão.
* **Cadência II-V-I:** A progressão harmônica mais importante do Jazz e da Bossa Nova, composta por um acorde menor preparatório (II), um dominante (V) e a resolução na tônica (I).
* **Line Cliché:** Movimento linear de uma única nota caminhando de forma descendente ou ascendente por dentro de um acorde que permanece estático.

### 2. Resumos Estruturados por Nível Pedagógico
O sistema foi parametrizado para estruturar os roteiros de estudo de improvisação de acordo com a maturidade técnica do estudante:
* **Nível 1 (Iniciante):** Focado em esqueletos harmônicos limpos (tríades/tétrades, até 6 acordes, sem inversões). Abordagem de improvisação via **Escala Única (Centro Tonal)**, evitando a troca constante de escalas por acorde. Possui protocolo de *Fallback* automático para simplificar e limpar músicas complexas caso falte repertório nativo simples na busca.
* **Nível 2 (Intermediário):** Músicas com mais de 6 acordes, preparações clássicas (II-V-I), dominantes secundários e extensões básicas (6, 9, 13). Abordagem focada em **uma escala direta por acorde** (Modos Gregos).
* **Nível 3 (Avançado):** Alta complexidade harmônica, modulações de tonalidade e acordes alterados ($\flat9$, $\sharp9$, $\flat13$). Abordagem avançada com **até 10 opções teóricas por acorde** (Menor Melódica, Bebop, Pentatônicas m6, Tons Inteiros, Diminuta, Dom-Dim e sobreposições de arpejos).

### 3. Conjunto de Prompts Reutilizáveis

Para rodar o assistente de forma idêntica em seu ambiente de estudos:
1. Abra o arquivo [guia_de_conduta.txt](guia_de_conduta.txt) deste repositório e copie seu conteúdo integral.
2. No chat do seu NotebookLM, cole esse texto como a **primeiríssima mensagem da sessão** para inicializar as diretrizes pedagógicas.
3. Utilize os comandos práticos abaixo para realizar suas consultas e ativar as máquinas de estados:

**Gatilho de Nível 1 + Filtro Tonal:**
[PROMPT 1 - ATIVAÇÃO DE NÍVEL 1 + FILTRO TONAL]
Preciso de uma música no tom de Dm para um estudante iniciante em improvisação.

**Gatilho de Nível 2 (Estruturas de Preparação):**
[PROMPT 2 - ATIVAÇÃO DE NÍVEL 2]
Preciso de uma música que possua vários dominantes secundários para um aluno.

**Gatilho de Nível 3 (Modulação):**
[PROMPT 3 - ATIVAÇÃO DE NÍVEL 3]
Preciso de uma música com modulação para estudo de improvisação.

**Estresse Harmônico Avançado (Nível 3):**
[PROMPT 4 - ESTRESSE HARMÔNICO AVANÇADO - NÍVEL 3]
Preciso de uma música com uso de mediante cromática para estudo avançado de improvisação.

---

## 🚀 Roadmap de Produção (Evolução com Python & FastAPI)

Para transformar este protótipo pessoal em uma plataforma comercial segura, o plano de engenharia de software back-end prevê:
1. **Isolamento de Regras:** Migração para **FastAPI + LangChain**, injetando o Guia de Conduta no parâmetro oculto `system_instruction` da API do Gemini, bloqueando tentativas de *prompt bypass*.
2. **Modelo Black-Box:** Ocultar títulos, páginas e arquivos originais no back-end, entregando na tela do usuário apenas a análise gerada por RAG, blindando o sistema contra pirataria e exposição de direitos autorais.
3. **PostgreSQL:** Persistência do histórico de triagem por etapas e cache ativo de anti-repetição (histórico de 20 músicas) em tabelas relacionais, reduzindo custos de contexto da LLM e zerando a latência na conversação teórica pura.
4. **Visão Computacional (OMR):** Integração de leitores de *Optical Music Recognition* conectados ao **ChromaDB** ou **Pinecone** para quebrar o gargalo de leitura de partituras puras em grade e manuscritos antigos.

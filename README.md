# Smart Repertoire Guide

---

## 📌 Contexto e Objetivos

O ensino e o aprendizado de improvisação musical na guitarra e no violão dependem diretamente do acesso a um repertório harmônico estruturado com absoluta precisão teórica. Na internet aberta, instrutores e estudantes enfrentam dados poluídos (cifras incorretas, diagramas bizarros e omissão de extensões fundamentais de acordes) e sobrecarga cognitiva, já que os motores de busca tradicionais não filtram músicas por densidade harmônica ou critérios pedagógicos (como número de acordes ou presença de modulações).

O **Smart Repertoire Guide** é um caderno temático de aprendizagem ativa desenvolvido no Google NotebookLM para atuar como um assistente especialista e guia de consulta pessoal para o estudo de harmonia funcional e técnicas de improvisação (*Chord-Scale* e *Target Notes*).

**Objetivos de Estudo:**
* Catalogar, centralizar e estruturar o conhecimento harmônico aplicado a gêneros complexos como Bossa Nova, MPB, Choro e Jazz.
* Criar um motor de consulta dinâmica onde o professor insere o nível atual de conhecimento do aluno (se domina campos harmônicos, cadências clássicas como II-V-I ou extensões) e o modelo varre a base de dados confiável para sugerir repertórios sob medida.
* Filtrar as sugestões permitindo que o instrutor selecione tonalidades específicas ou gêneros focados (Jazz, Choro, MPB ou Bossa Nova), recebendo um roteiro analítico completo para guiar as aulas de improvisação.

---

## 📚 Curadoria de Fontes

Em conformidade com as diretrizes do desafio, foram selecionadas **fontes abertas de alta autoridade teórica e histórica** para alimentar a base de conhecimento principal do caderno temático:

1. [Artigo Acadêmico - A Harmonia da Bossa Nova (USP)](https://www.revistas.usp.br/) - Análise detalhada das progressões, cadências e extensões características do movimento da Bossa Nova.
2. [Acervo Digital Pixinguinha - Funarte](http://www.funarte.gov.br/) - Partituras e documentos históricos abertos sobre a estruturação e arranjo de Choro tradicional.
3. [Manuais Didáticos de Harmonia Funcional (Domínio Público)](https://archive.org/) - Compilados de métodos clássicos de mapeamento de Chord-Scale e improvisação jazzística.
4. [Documentação Oficial do Google NotebookLM](https://support.google.com/notebooklm) - Base técnica para o entendimento do comportamento do motor RAG e limites de extração semântica.
*(Nota: Para fins de validação pedagógica e testes de estresse privados, o protótipo foi complementarmente exposto a um ecossistema experimental de 46 songbooks digitalizados em formato híbrido e analógico).*


## 📚 Curadoria de Fontes (Fontes Abertas Utilizadas)

Em conformidade com as diretrizes do desafio, foram selecionadas fontes abertas e gratuitas de autoridade teórica, histórica e pedagógica para alimentar a base de conhecimento do caderno temático:

1. [Acervo Digital da Música Brasileira - Pixinguinha (Funarte)](https://www.funarte.gov.br/) - Portal oficial do governo que disponibiliza partituras, arranjos e documentos históricos abertos sobre a estruturação do Choro tradicional.
2. [Métodos de Harmonia e Improvisação Jazzística (Internet Archive)](https://archive.org/) - Biblioteca digital pública mundial utilizada para indexar manuais de domínio público sobre a abordagem *Chord-Scale* e a teoria do Jazz.
3. [Biblioteca Digital de Teses e Dissertações (USP)](https://teses.usp.br/) - Repositório acadêmico aberto utilizado para consultar análises estruturadas sobre a evolução harmônica e as cadências da Bossa Nova e da MPB.
4. [Documentação de Suporte Oficial do Google NotebookLM](https://support.google.com/notebooklm) - Base técnica para o entendimento do comportamento do motor RAG, limites de tokens e extração de texto via visão computacional.
*(Nota: Para fins de validação pedagógica e testes de estresse privados de uso pessoal do instrutor, o protótipo foi complementarmente exposto a um ecossistema experimental de 46 songbooks digitalizados).*

DIZER QUE PARA O BOOTCAMP FORAM USADAS FONTES PÚBLICAS MAS PARA MEU USO PESSOAL e toda a construção do modelo no notebook, validação da ferramenta, FOI USADO MEU ACERVO DE PDFs.
---

## 🔬 Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Para garantir o grau de confiabilidade necessário para o objetivo do notebook e eliminar o risco de alucinações, foram conduzidas consultas estratégicas e testes de estresse práticos para mapear a capacidade de decodificação do modelo frente a múltiplos cenários de dados:

### 1. Testes de Estresse de Visão Computacional (OCR)
* **Validação de OCR Nativo & Híbrido (Sucesso):** O modelo mapeou com precisão sequências de Bossa Nova, identificando perfeitamente extensões complexas (como `B7(b9)`, `F#m7(b5)`, `G#m7(11)`). Apresentou pequenas variações aceitáveis de sintaxe (como ler o diagrama de `D(6/9)` textualmente como `D9`).
* **Mapeamento de Ruído e Auto-Correção (Sucesso Avançado):** Ao ler metadados gerados por escaneamentos analógicos com forte ruído visual (leitura de diagramas que geravam lixo como `# 11111;;` ou `~i 11.,`), o modelo usou a inteligência do contexto musical para auto-corrigir os dados corrompidos, deduzindo com precisão que a string truncada `GIM` correspondia ao acorde `G7M`.
* **Confronto de Alta Resolução (Sucesso Parcial):** Ao processar Jazz Fake Books puramente visuais, localizou as páginas com exatidão, mas demonstrou limites finos de imagem: omitiu acidentes sutis em acordes alterados verticais e confundiu barras de inversão de baixo caminhando (como `Db9 / Bb -> / Ab`).
* **Gargalo Técnico (Limite Operacional):** Frente a manuscritos antigos e partituras puras sem nenhuma cifragem textual explícita, o sistema atingiu seu limite físico de processamento de imagem, informando que as páginas não puderam ser indexadas por falta de texto legível.

### 2. Concorrência entre Busca Direta e Controle de Fluxo
Durante os experimentos, descobriu-se que arquivos de texto contendo manuais de regras hospedados na barra lateral de fontes competem diretamente com a massa de dados do repositório. Consultas fortes com nomes de músicas específicas faziam a IA buscar o dado bruto e burlar as diretrizes pedagógicas (*prompt bypass*).

**A Solução das "Cicatrizes":** Para contornar esses problemas e garantir a previsibilidade metodológica do sistema, o comportamento do modelo foi totalmente blindado por meio do desenvolvimento de um script estruturado (`guia_de_conduta.txt`). Este arquivo força a IA a atuar como uma máquina de estados imperativa, exigindo que o operador o injete como a **primeiríssima mensagem do chat**, isolando os PDFs estritamente como fontes de consulta secundárias.

> 📊 *A documentação completa dos 5 casos de teste de estresse de imagem, relatórios de erro detalhados e o plano de transição técnica para uma **API de produção em FastAPI (Python)** estão registrados no nosso [Relatório Técnico Avançado](docs/relatorio_tecnico.md).*

---

## 📖 Miniguia de Estudo (Entrega Final)

O resultado final consolidado da curadoria e processamento do caderno temático gerou o seguinte mapa conceitual de estudos para suporte ao professor de música:

### 1. Glossário de Conceitos Aprendidos pela IA
* **Grounding (Contexto Restrito):** Técnica que ancora as respostas da IA exclusivamente em uma base de dados fornecida, proibindo alucinações baseadas na internet externa.
* **Target Notes (Notas-Alvo):** Técnica de improvisação melódica focada em repousar as frases nas terças (3ª) e sétimas (7ª) de cada acorde, evidenciando a mudança da harmonia.
* **Chord-Scale (Acorde-Escala):** Abordagem que mapeia escalas ou modos específicos (ex: Dórico, Lídio, Alterada) para serem executados individualmente sobre cada acorde da progressão.
* **Cadência II-V-I:** A progressão harmônica mais importante do Jazz e da Bossa Nova, composta por um acorde menor preparatório (II), um dominante (V) e a resolução na tônica (I).

### 2. Resumos Estruturados por Nível Pedagógico
O sistema foi parametrizado para estruturar os roteiros de estudo de improvisação de acordo com a maturidade técnica do estudante:
* **Nível 1 (Iniciante):** Focado em esqueletos harmônicos limpos (tríades/tétrades, até 6 acordes, sem inversões). Abordagem de improvisação via **Escala Única (Centro Tonal)**, evitando a troca constante de escalas por acorde.
* **Nível 2 (Intermediário):** Músicas com mais de 6 acordes, preparações clássicas (II-V-I), dominantes secundários e extensões básicas (6, 9, 13). Abordagem focada em **uma escala direta por acorde** (Modos Gregos).
* **Nível 3 (Avançado):** Alta complexidade harmônica, modulações de tonalidade e acordes alterados (b9, #9, b13). Abordagem avançada com **até 10 opções teóricas por acorde** (Menor Melódica, Bebop, Pentatônicas m6, Tons Inteiros, Diminuta, Dom-Dim e sobreposições de arpejos).

### 3. Conjunto de Prompts Reutilizáveis
Para rodar o assistente de forma idêntica em seu ambiente de estudos:
1. Abra o arquivo [guia_de_conduta.txt](guia_de_conduta.txt) deste repositório e copie seu conteúdo integral.
2. No chat do seu NotebookLM, cole esse texto como a **primeiríssima mensagem da sessão** para inicializar as diretrizes pedagógicas e travar os guardrails.
3. Utilize os comandos operacionais abaixo para realizar suas consultas de aula:
   * **Para buscar sugestões:** *"Quero sugestões de [Gênero] em [Tonalidade] para um aluno de [Nível 1, 2 ou 3]."*
   * **Para analisar uma música:** *"Gere o roteiro pedagógico completo para a música [Nome da Música] com foco em [Nível 1, 2 ou 3]."*

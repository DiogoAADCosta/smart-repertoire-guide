# Smart Repertoire Guide

[READ THIS IN ENGLISH](./README_EN.md)

O Smart Repertoire Guide é um ecossistema de aprendizagem e caderno de consulta automatizado por Inteligência Artificial, projetado para auxiliar professores de guitarra e violão na estruturação pedagógica de repertórios voltados ao ensino de improvisação musical.

Este projeto é a entrega prática final para o Bootcamp Bradesco - GenAI, Dados & Cyber, em parceria com a DIO.

> **Nota:** Este arquivo é uma vitrine resumida do projeto. Para a análise profunda de engenharia de dados, testes de imagem com OCR e arquitetura de back-end futura, acesse o [Relatório Técnico Completo](./docs/relatorio_tecnico.md).

---

## Contexto e Objetivos

Buscar materiais didáticos na internet aberta gera dados poluídos (cifras erradas e omissão de extensões) e sobrecarga cognitiva (falta de filtros por densidade harmônica).

Este projeto valida o uso do Google NotebookLM para:
* Centralizar e estruturar o conhecimento harmônico de Bossa Nova, MPB, Choro e Jazz.
* Atuar sob fonte fechada (Grounding), eliminando alucinações.
* Automatizar a triagem de músicas com base no nível teórico do aluno e gerar roteiros de improviso imediatos.

---

## Curadoria de Fontes (Data Ingestion)

A estrutura de dados foi dividida em dois cenários complementares:

### 1. Homologação (Bootcamp DIO - Fontes Abertas)
1. [Guia de Conduta do Sistema (Texto Plano)](./docs/guia_de_conduta.txt) - O arquivo de instruções estruturadas que rege o comportamento pedagógico e operacional da IA.
2. [Música Brasilis](https://musicabrasilis.org.br/pt-br/) - Portal de referência para partituras e acervo da música brasileira.
3. [Bossa Nova Fakebook Vol. 2 (PDF)](https://musicishealing.com/Bateria/Pagode/Library/BossaNovaFakebook2.pdf) - Livro de cifras focado no repertório tradicional de Bossa Nova.
4. [Jazz Library](https://jazz-library.com/songs/) - Base de dados pública com estruturas harmônicas e músicas clássicas do Jazz.
5. [Anais da ANPPOM - Artigo sobre Bossa Nova (PDF)](https://anppom.org.br/anais/anaiscongresso_anppom_2025/papers/182.pdf) - Estudo acadêmico sobre a estruturação e evolução harmônica nacional.
6. [Análise Harmônica e Improvisação (PDF)](https://cdn.prod.website-files.com/65dcd4c1ddd64f2ee53eb284/674829d8f32b8fbebe6a6019_43114043937.pdf) - Material didático focado em técnicas de roteiros de improviso.
7. [Artigo Técnico - Ritmo e Harmonia (UNICAMP)](https://www.iar.unicamp.br/wp-content/uploads/2021/07/V2_ED03_A1_BossaNova.pdf) - Documento universitário que analisa as cadências da música popular brasileira.
8. [Songbook As 101 Melhores Canções do Século XX (PDF)](https://ekladata.com/kvdp5s2Kp2nEQ7-yNaJbgheQFH0/Songbook-As-101-Melhores-Cancoes-do-Seculo-XX-Vol-1.pdf) - Cancioneiro aberto contendo clássicos da música nacional e internacional.

### 2. Produção (Uso Pessoal)

Todo o processo real de construção, testes de estresse e validação pedagógica do motor de IA foi expandido para o meu uso diário através de parte do meu acervo privado, contando com 46 songbooks e métodos digitalizados de alta fidelidade (como as obras de Almir Chediak e Real Books de Jazz).
---

## Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

### 1. Testes de Estresse de Visão Computacional (OCR)
* **OCR Híbrido (Sucesso):** Mapeou com precisão sequências de Bossa Nova e extensões complexas, com pequenas variações de sintaxe.
* **Auto-Correção de Ruído (Sucesso Avançado):** Corrigiu strings e caracteres corrompidos por escaneamentos analógicos ruins (ex: deduziu que a sujeira `GIM` correspondia a `G7M`).
* **Confronto de Alta Resolução (Sucesso Parcial):** Em Jazz Fake Books visuais, omitiu acidentes sutis e confundiu barras de inversão de baixo caminhando.
* **Gargalo Técnico (Limite):** Falhou ao tentar ler partituras puras em grade e manuscritos antigos sem nenhuma cifragem textual explícita adjacente.

### 2. Controle de Fluxo
Descobriu-se que manuais colocados na barra lateral sofrem concorrência com as músicas (prompt bypass). 

**A Solução:** O comportamento foi totalmente blindado pelo desenvolvimento do [Guia de Conduta](./docs/guia_de_conduta.txt). Ele age como uma máquina de estados imperativa e recomenda-se injetá-lo como a **primeiríssima mensagem do chat**, isolando as fontes como consulta secundária.

---

## Miniguia de Estudo (Entrega Final)

### 1. Glossário Resumido
* **RAG (Retrieval-Augmented Generation):** Técnica de arquitetura que otimiza a saída de uma LLM consultando uma base de conhecimento confiável antes de gerar a resposta.
* **Grounding (Ancoragem):** Processo de restringir o domínio de conhecimento e as respostas da IA estritamente aos documentos fornecidos na base ativa, mitigando alucinações.
* **OCR (Optical Character Recognition):** Tecnologia de visão computacional que converte imagens de texto e símbolos escaneados em caracteres de texto legíveis e indexáveis por sistemas digitais.
* **Prompt Bypass / Concorrência de Tokens:** Falha operacional onde comandos de instrução de sistema perdem peso semântico na janela de contexto e são ignorados pela IA em favor dos dados brutos consumidos.

### 2. Resumos por Nível Pedagógico
* **Nível 1 (Iniciante):** Máximo de 6 acordes, harmonia diatônica, sem modulações. Improviso via **Escala Única (Centro Tonal)**. Possui protocolo de Fallback automático para simplificar músicas complexas se faltar repertório nativo simples.
* **Nível 2 (Intermediário):** Mais de 6 acordes, cadências II-V-I, dominantes secundários e extensões básicas (6, 9, 13). Improviso por **Chord-Scale (um modo por acorde)**.
* **Nível 3 (Avançado):** Modulações constantes, acordes alterados ($\flat9$, $\sharp9$, $\flat13$) e rearmonizações. Até 10 abordagens de escalas por acorde (Menor Melódica, Bebop, arpejos sobrepostos).

### 3. Conjunto de Prompts Reutilizáveis
*Injete o Guia de Conduta na primeira mensagem do chat e utilize os comandos práticos abaixo:*

**Gatilho de Nível 1 + Filtro Tonal:**
[PROMPT 1 - ATIVAÇÃO DE NÍVEL 1 + FILTRO TONAL]
```
Preciso de uma música no tom de Dm para um estudante iniciante em improvisação.
```

**Gatilho de Nível 2 (Estruturas de Preparação):**
[PROMPT 2 - ATIVAÇÃO DE NÍVEL 2]
```
Preciso de uma música que possua vários dominantes secundários para um aluno.
```

**Gatilho de Nível 3 (Modulação):**
[PROMPT 3 - ATIVAÇÃO DE NÍVEL 3]
```
Preciso de uma música com modulação para estudo de improvisação.
```

**Estresse Harmônico Avançado (Nível 3):**
[PROMPT 4 - ESTRESSE HARMÔNICO AVANÇADO - NÍVEL 3]
```
Preciso de uma música com uso de mediante cromática para estudo avançado de improvisação.
```

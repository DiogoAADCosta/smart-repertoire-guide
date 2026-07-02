# Smart Repertoire Guide

## 🎯 Contexto e Objetivos
[Espaço para explicar o motor de recomendação e as dores da improvisação]

## 📚 Curadoria de Fontes e Engenharia de Dados (Data Ingestion)
[Lista dos Songbooks e a tipologia de arquivos testados]

## Fase 1: Teste de Estresse e Ingestão de Dados (Data Ingestion)

Inicialmente, a base de dados do projeto foi expandida para uma abordagem de estresse, submetendo o motor do NotebookLM a múltiplos formatos de arquivos PDF com diferentes níveis de integridade digital.

O objetivo desta fase foi mapear a resiliência do modelo e sua capacidade de extração de entidades (letras, cifras, diagramas e extensões harmônicas) sob condições adversas de qualidade de dados.

### Tipos de Arquivos Testados

*   **PDF com OCR Nativo:** Arquivos com camadas de texto bem definidas, de fácil leitura e seleção vetorial.
*   **PDF Híbrido:** Arquivos mesclando páginas digitalizadas textualmente com trechos escaneados e presença de caracteres corrompidos no meio da estrutura.
*   **PDF de Imagem (Alta Resolução):** Arquivos puramente visuais (sem seleção de texto por mouse), mas com alto contraste e definições de linhas nítidas.
*   **PDF de Imagem (Baixa Resolução):** Arquivos escaneados com baixo contraste, borrões de impressão e ruídos de digitalização.
*   **PDF com Manuscrito:** Partituras e cifras escritas à mão para testar o limite de visão computacional da ferramenta.
*   **PDF com Partitura Pura:** Teste focado em avaliar se o modelo é capaz de decodificar notas diretamente na pauta musical sem auxílio de texto.

---

### Documentação de Testes (Perguntas vs. Resultados)

Para validar a integridade da ingestão de dados, foram aplicadas consultas estratégicas em ambiente controlado. Os resultados demonstraram os limites práticos e as janelas de sucesso da ferramenta:

#### Caso de Teste 1: Validação de OCR Nativo & Híbrido
*   **Pergunta:** *"Com base no livro Bossa Nova 1, quais os acordes utilizados para a música 'Até parece' de Carlos Lyra?"*
*   **Resultado Técnico:** **Sucesso.** O modelo mapeou com precisão a sequência harmônica completa, identificando extensões complexas como `B7(b9)`, `F#m7(b5)`, `E7(13)`, `E7(b13)`, `G#m7(11)` e `G7(#11)`. A única divergência menor foi a leitura do acorde `D(6/9)` (presente no diagrama da imagem `image_41fd42.jpg`), extraído textualmente como `D9`. O modelo conseguiu varrer as linhas iniciais e o corpo da cifra perfeitamente.

#### Caso de Teste 2: Mapeamento de Ruído e Auto-Correção
*   **Pergunta:** *"Você encontrou algum caractere estranho, sequência de símbolos sem sentido (como '11111;;' ou letras embaralhadas) ou acordes com grafia corrompida ao ler a cifra de 'Desejo do mar'?"*
*   *(Nota de Engenharia de Dados: Para formular esta consulta com precisão, o trecho original do PDF foi previamente copiado para um editor de texto plano para inspecionar os metadados gerados pelo OCR analógico. Isso permitiu antecipar quais strings estranhas o modelo indexaria na base de conhecimento).*
* **Resultado Técnico:** **Sucesso Avançado (Auto-Correção).** O modelo não apenas identificou os ruídos gerados pela leitura analógica dos diagramas visuais dos acordes (identificando strings estranhas como `# 11111;;` e `~i 11.,`), como usou inteligência de contexto de Bossa Nova para tratar os dados corrompidos. Ele apontou que a string `GIM` correspondia a `G7M` e deduziu que `D~(9)` representava a cifragem que de fato correspondia ao acorde $D_7^4(9)$ na imagem `image_3714b8.jpg`.


#### Caso de Teste 3: Confronto de Imagem de Alta Resolução
*   **Pergunta:** *"Quais os acordes da música 'In April' de Bill Evans e em que página se encontra essa música?"*
*   **Resultado Técnico:** **Sucesso.** Avaliando o *Bill Evans Fake Book* (imagem `image_41fdfc.jpg`), que consiste em um PDF puramente de imagens de alta resolução, o NotebookLM localizou com exatidão a página 20 e segmentou a harmonia por seções (Seção A e Seção B), extraindo blocos harmônicos densos de jazz como `DbMaj9`, `Bb7(13 b9)`, `Fm11`, e `Bb7(b9 b5)`.

#### Caso de Teste 4: Verificação de Ambiguidade e Auto-Correção Histórica
*   **Pergunta:** *"Encontre a música 'Na baixa do sapateiro' de Ary Barroso. Quais os 10 primeiros acordes?"*
*   **Análise do Comportamento do Modelo:** O PDF utilizado nesta ingestão possui uma estrutura complexa, unindo o Volume 1 (composto por imagens antigas e borradas) e o Volume 2 (com trechos textuais selecionáveis). 
*   **Primeira Resposta da IA:** O modelo identificou que a música é mundialmente conhecida pelo título alternativo de "Bahia" e mapeou a harmonia disposta na página 36 do Volume 2 (`G7`, `C7`, `F6...`). 
*   **Segunda Resposta (Refinamento):** Após uma análise mais profunda das fontes indexadas, o próprio motor do NotebookLM emitiu uma errata espontânea no chat, localizando a partitura original na página 89 do Volume 1 (zona de imagem de baixa resolução) e extraindo com sucesso a sequência harmônica real com suas respectivas extensões da melodia (`Bb7`, `E7(#9)`, `Eb7M`, `Ebm6`, `Ab7(13)`, `Dm7`, `Db7(9)`, `Cm7(9)`, `B7(9)`, `Bb7`).
*   **Conclusão:** O modelo demonstrou alta resiliência visual, sendo capaz de decodificar a cifragem em uma imagem borrada e antiga, além de possuir capacidade de auto-correção textual ao cruzar volumes diferentes do mesmo autor.

#### Caso de Teste 5: Gargalo Técnico (Partitura Pura, Manuscritos e Baixa Resolução)
*   **Perguntas de Estresse:** 
    1. *"Na música 'We Can Work It Out' (The Beatles), em que nota inicia a melodia da voz e em que página está essa música?"*
    2. *"Na música 'Eu e Tu' de Altamiro Carrilho, quais os 6 primeiros acordes?"*
*   **Resultado Técnico:** **Falha / Limite Operacional.** Frente a manuscritos antigos e partituras sem nenhuma cifragem textual explícita, o sistema atingiu seu limite físico de processamento de imagem. O modelo informou que as páginas correspondentes não puderam ser indexadas por falta de texto legível.
*   **Conclusão de Engenharia:** LLMs baseadas em NotebookLM falham ao tentar decodificar notação musical puramente visual (pautas, claves e posições de notas na grade) caso não haja dados em texto ou cifras explícitas adjacentes para apoiar o contexto.

---

### Evidências de Teste (Auditoria de Resultados)

#### Caso de Teste 1: Até Parece (Leitura de OCR Nativo e Híbrido)
| Documento Original (PDF) | Resposta da IA |
| :---: | :---: |
| ![PDF Até Parece](imagens/pdf_ate_parece.png) | ![Resposta IA Até Parece](imagens/ia_ate_parece.png) |

#### Caso de Teste 2: Desejo do Mar (Mapeamento de Ruído e Auto-Correção)
| Documento Original (PDF) | Resposta com Auto-Correção da IA |
| :---: | :---: |
| ![PDF Desejo do Mar](imagens/pdf_desejo_mar.png) | ![Resposta IA Desejo do Mar](imagens/ia_desejo_mar.png) |

#### Caso de Teste 3: In April (Confronto de Imagem de Alta Resolução)
| Documento Original (PDF) | Resposta da IA |
| :---: | :---: |
| ![PDF In April](imagens/pdf_in_april.png) | ![Resposta IA In April](imagens/ia_in_april.png) |

#### Caso de Teste 4: Na Baixa do Sapateiro (Verificação de Ambiguidade)
| Partitura Original - Vol. 1 | Resposta Corrigida pela IA |
| :---: | :---: |
| ![PDF Ary Barroso](imagens/pdf_ary_barroso.png) | ![Resposta IA Ary Barroso](imagens/ia_ary_barroso.png) |

#### Caso de Teste 5: Gargalo Técnico (Partituras Puras e Manuscritos)
| Documento Original (PDF) | Resposta da IA (Limite Atingido) |
| :---: | :---: |
| ![PDF Beatles/Altamiro](imagens/pdf_limite.png) | ![Resposta IA Limite](imagens/ia_limite.png) |

---

### Lições Aprendidas & Engenharia de Mitigação (Troubleshooting)

A partir desses resultados, o repositório consolidou as seguintes decisões técnicas de arquitetura para a aplicação final:

*   **Limpeza de Dados via Prompt (Data Cleansing):** Como os PDFs analógicos trazem ruídos de OCR decorrentes de diagramas e tabelas, foi desenvolvido um prompt de sistema para instruir a IA a ignorar padrões repetitivos não-textuais (ex: `11111;;`).
*   **Restrição de Escopo:** O sistema foi blindado para **não** responder a perguntas de leitura de pauta melódica (partitura pura), focando exclusivamente no mapeamento textual-harmônico de cifras e encadeamento de acordes estruturados.

## 🛡️ Fase 2: Implementação de Guardrails (Guia de Conduta)
[Onde vai o arquivo de trancas técnicas e as regras contra alucinação]

## 🎓 Fase 3: Matriz de Nivelamento Pedagógico e Output Schema
[A regra de níveis e o formato obrigatório de saída em 3 passos]

## 🛠️ Como Executar e Reutilizar
[Passo a passo rápido para alguém replicar o caderno no próprio NotebookLM]

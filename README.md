# Smart Repertoire Guide

O **Smart Repertoire Guide** é um assistente especialista e caderno de consulta pessoal baseado em Inteligência Artificial para instrutores de guitarra e violão. O sistema opera sob uma política estrita de fonte fechada (*Grounding*), restringindo sua base de conhecimento a um acervo privado de 46 songbooks e métodos de alta fidelidade histórica (como as obras de Almir Chediak e Real Books de Jazz), eliminando alucinações e dados poluídos da internet aberta.

O professor insere o nível atual de conhecimento teórico do aluno (se domina campos harmônicos, cadências como II-V-I ou extensões) e o modelo sugere repertórios confiáveis sob medida, permitindo filtrar por tonalidades específicas e gêneros musicais focados (Jazz, Choro, MPB ou Bossa Nova).

---

## 🛠️ Tecnologias e Arquitetura

* **Camada de Inteligência:** Google NotebookLM (Ambiente de Prototipagem de Contexto Restrito).
* **Base de Dados Privada:** 46 volumes indexados e categorizados (Lumiar, Jazz/Real Books e Acervos de Choro).
* **Engenharia de Prompt:** Arquitetura orientada a estados comportamentais via diretrizes imperativas (`guia_de_conduta.txt`).

---

## 📊 Estrutura de Dados (Data Ingestion)

A base de conhecimento foi organizada em coleções temáticas para auditar a resiliência do motor de visão computacional da IA contra diferentes qualidades de arquivos:

* **Coleção Lumiar (Songbooks Nacionais - 22 PDFs):** Cancioneiros de Bossa Nova e MPB de Almir Chediak (Tom Jobim, Chico Buarque, Caetano Veloso, etc.).
* **Coleção Internacional (Jazz & Real Books - 18 PDFs):** Volumes clássicos de Real Books e transcrições de virtuoses (Pat Metheny, Wes Montgomery, Joe Pass).
* **Métodos e Acervos de Choro (6 PDFs):** Métodos históricos e partituras digitalizadas antigos (Altamiro Carrilho, Pixinguinha).

---

## 🚀 Como Executar o Protótipo (Uso Pessoal)

Como o projeto utiliza materiais protegidos por direitos autorais, os 46 PDFs originais não estão públicos no repositório. No entanto, a inteligência do sistema pode ser testada em seu próprio ambiente:

1. Acesse o [Google NotebookLM](https://notebooklm.google/) e instancie um novo caderno.
2. Faça o upload dos seus PDFs de música na barra lateral de "Fontes".
3. **Inicialização:** Abra o chat e, como a **primeiríssima mensagem da sessão**, cole o conteúdo integral do arquivo `guia_de_conduta.txt` deste repositório.
4. Digite o perfil do seu aluno (ex: *"Quero sugestões de Bossa Nova em Dó Maior para um aluno que já domina o II-V-I"*) e receba o roteiro pedagógico imediato.

---

## 📂 Documentação Completa e Relatórios

Para uma auditoria profunda de engenharia, testes de estresse de OCR e o plano de transição para o back-end, acesse as documentações satélites:

* **`guia_de_conduta.txt`:** O código-fonte do prompt de sistema com as regras, restrições e formatos de saída do motor.
* **[Relatório Técnico Completo (Fase 1 e Fase 2)](docs/relatorio_tecnico.md):** Contém os **5 casos de teste de estresse de imagem**, análise de ruídos analógicos de leitura, limitações de IP/Pirataria do NotebookLM e o desenho completo da **Arquitetura de Produção Proposta em FastAPI (Python)** para escala do projeto.

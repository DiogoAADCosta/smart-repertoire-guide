# Smart Repertoire Guide

The Smart Repertoire Guide is an AI-powered learning ecosystem and automated reference log designed to assist guitar and acoustic guitar instructors in the pedagogical structuring of repertoires for music improvisation training.

This project is the final practical submission for the Bradesco Bootcamp - GenAI, Data & Cyber, in partnership with DIO.

> **Note:** This file serves as a condensed showcase of the project. For an in-depth analysis of data engineering, OCR image stress tests, and the proposed future back-end architecture, please access the [Full Technical Report](./docs/technical_report.md).

---

## Context and Objectives

Sourcing educational materials from the open internet often results in **polluted data** (incorrect chord charts and omitted extensions) and **cognitive overload**, as traditional search engines do not filter songs by harmonic density or pedagogical criteria.

This project validates the use of Google NotebookLM to:
* Centralize and structure harmonic knowledge across Bossa Nova, MPB, Choro, and Jazz.
* Operate under a strict closed-source policy (Grounding), eliminating hallucinations.
* Automate song filtering based on the student's theoretical proficiency and generate instant improvisation roadmaps.

---

## Source Curatorial Review (Data Ingestion)

The data structure was divided into two complementary scenarios:

### 1. Homologation (DIO Bootcamp - Open Sources)
1. [Música Brasilis](https://musicabrasilis.org.br/pt-br/) - Reference portal for Brazilian sheet music and archives.
2. [Bossa Nova Fakebook Vol. 2 (PDF)](https://musicishealing.com/Bateria/Pagode/Library/BossaNovaFakebook2.pdf) - Chord charts book focused on traditional Bossa Nova repertoire.
3. [Jazz Library](https://jazz-library.com/songs/) - Public database featuring harmonic structures and Jazz classics.
4. [Anais da ANPPOM - Bossa Nova Article (PDF)](https://anppom.org.br/anais/anaiscongresso_anppom_2025/papers/182.pdf) - Academic study on national harmonic structuring and evolution.
5. [Harmonic Analysis and Improvisation (PDF)](https://cdn.prod.website-files.com/65dcd4c1ddd64f2ee53eb284/674829d8f32b8fbebe6a6019_43114043937.pdf) - Educational material focusing on improvisation roadmap techniques.
6. [Technical Article - Rhythm and Harmony (UNICAMP)](https://www.iar.unicamp.br/wp-content/uploads/2021/07/V2_ED03_A1_BossaNova.pdf) - University paper analyzing Brazilian popular music cadences.
7. [Songbook As 101 Melhores Canções do Século XX (PDF)](https://ekladata.com/kvdp5s2Kp2nEQ7-yNaJbgheQFH0/Songbook-As-101-Melhores-Cancoes-do-Seculo-XX-Vol-1.pdf) - Open songbook containing national and international classics.

### 2. Production (Personal Use)
The actual process of building, stress testing, and pedagogically validating the AI engine was expanded for the instructor's daily teaching operations by integrating a private collection of **46 digitized songbooks and methods** of high historical credibility (such as Almir Chediak's complete works and Jazz Real Books).

---

## Prompt Engineering and "Scars" (Troubleshooting)

### 1. Computer Vision Stress Tests (OCR)
* **Hybrid OCR (Success):** Accurately mapped Bossa Nova sequences and complex extensions with minor, acceptable syntax variations.
* **Noise Auto-Correction (Advanced Success):** Corrected corrupted strings and artifacts caused by poor analog scans (e.g., successfully deduced that the visual text distortion `GIM` corresponded to a `G7M` chord).
* **High-Resolution Conflict (Partial Success):** While processing purely visual Jazz Fake Books, it located pages exactly but hit fine graphical limitations, omitting subtle accidentals in vertical altered chords and misinterpreting slash bars in walking bass lines.
* **Technical Bottleneck (Limit):** Failed when attempting to process old manuscripts and raw sheet music layouts that lacked any explicit adjacent textual chord notations.

### 2. Control Flow
Experiments revealed that rule manuals hosted inside the regular source sidebar compete directly with song data for semantic attention (prompt bypass). 

**The Solution:** System behavior was completely armored by developing a structured [Code of Conduct](./docs/code_of_conduct.txt). It operates as an imperative state machine and must be injected as the **very first chat message**, isolating the PDFs strictly as secondary query sources.

---

## Study Mini-Guide (Final Delivery)

### 1. Condensed Glossary
* **RAG (Retrieval-Augmented Generation):** An architectural technique that optimizes LLM outputs by querying a trusted knowledge base before generating a response.
* **Grounding:** The process of restricting the AI's domain and answers strictly to the provided files, mitigating hallucinations.
* **OCR (Optical Character Recognition):** Computer vision technology that converts images of scanned text and symbols into machine-encoded text legibly indexed by digital systems.
* **Prompt Bypass / Token Concurrency:** An operational flaw where system instruction commands lose semantic weight within the context window and are ignored by the AI in favor of raw ingested data.

### 2. Pedagogical Level Breakdowns
* **Level 1 (Beginner):** Maximum of 6 chords, diatonic harmony, no modulations. Improvisation relies on a **Single Scale (Tonal Center)**. Features an automatic fallback protocol to simplify complex chord charts if raw beginner pieces are missing.
* **Level 2 (Intermediate):** More than 6 chords, classic cadences (II-V-I), secondary dominants, and basic extensions (6, 9, 13). Improvisation targets a **Chord-Scale approach (one mode per chord)**.
* **Level 3 (Advanced):** Continuous modulations, altered chords ($\flat9$, $\sharp9$, $\flat13$), and advanced reharmonizations. Provides up to 10 scale approaches per chord (Melodic Minor, Bebop, overlaid arpejos).

### 3. Reusable Prompt Templates
*Inject the Code of Conduct in the first chat message and use the operational commands below:*

**Level 1 Trigger + Tonal Filter:**
[PROMPT 1 - LEVEL 1 ACTIVATION + TONAL FILTER]
```
I need a song in the key of Dm for a student who is a beginner in improvisation.
```

**Level 2 Trigger (Preparation Structures):**
[PROMPT 2 - LEVEL 2 ACTIVATION]
```
I need a song that features multiple secondary dominants for a student.
```

**Level 3 Trigger (Modulation):**
[PROMPT 3 - LEVEL 3 ACTIVATION]
```
I need a song with modulation for improvisation study.
```

**Advanced Harmonic Stress Test (Level 3):**
[PROMPT 4 - ADVANCED HARMONIC STRESS - LEVEL 3]
```
I need a song featuring chromatic mediants for advanced improvisation study.
```

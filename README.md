<p align="center">
  <a href="https://kazuist.com"><strong style="font-size: 48px;">&#9878;</strong></a>
</p>

<h1 align="center"><a href="https://kazuist.com">Kazuist</a></h1>

<p align="center">
  <strong>AI-Powered Turkish Law Education Ecosystem</strong>
</p>

<p align="center">
  <a href="https://kazuist.com">kazuist.com</a> &nbsp;·&nbsp;
  <a href="spec/">Technical Specification</a> &nbsp;·&nbsp;
  <a href="ARCHITECTURE.md">Architecture Document</a> &nbsp;·&nbsp;
  <a href="spec/ai/kazu-model.md">Kazu Model</a> &nbsp;·&nbsp;
  <a href="spec/ai/kazu-career.md">Kazu Career</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-web%20%2B%20iOS-brightgreen" alt="Platform" />
  <img src="https://img.shields.io/badge/language-Turkish-blue" alt="Language" />
  <img src="https://img.shields.io/badge/AI-Kazu%20LLM-orange" alt="AI" />
  <img src="https://img.shields.io/badge/license-academic-lightgrey" alt="License" />
</p>

---

<p align="center">
  <em>A personal AI mentor for every law student. Doesn't give the answer — makes you think.</em>
  <br /><br />
  <a href="https://kazuist.com"><strong>kazuist.com</strong></a>
</p>

---

## Meet Kazu

**Kazu** is Kazuist's AI mentor. Not a generic chatbot — a specialized language model trained exclusively on Turkish law, with full command of all legislation and up-to-date case law.

```
Student: Would the perpetrator be convicted of theft in this case?

Kazu:    Great question! But let's not jump to conclusions.
         First, we need to legally characterize the perpetrator's action.
         What type of offense could the described conduct fall under?

Student: Theft?

Kazu:    It could be theft. Now let's consider the elements defined in
         Turkish Penal Code Art. 141 — "movable property" and "taking
         without the possessor's consent." Are both elements present here?
```

### What Makes Kazu Different

| | |
|---|---|
| **Turkish Law Only** | From the Constitution to the Penal Code, Civil Code to Labor Law — full command of all legislation |
| **Live Case Law** | Tracks Court of Cassation, Council of State, and Constitutional Court decisions daily |
| **Official Gazette** | Scans the Official Gazette every morning, learns legislative changes instantly |
| **Socratic Method** | Never gives the answer — guides through questions to build understanding |
| **Always Cites Sources** | Every legal claim is backed by real statute articles, never hallucinated |
| **Fun But Rigorous** | Approachable and patient, but never compromises on legal accuracy |

### How Kazu Is Trained

Kazu isn't built by adding a conversation layer on top of a general-purpose model — it's purpose-built for Turkish law from the ground up:

```
 Data Collection        Pre-training          Fine-tuning          Alignment
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│ 13 court     │   │ 120B+ tokens │   │ QLoRA on     │   │ DPO for      │
│ databases    │──►│ continued    │──►│ legal Q&A    │──►│ legal        │
│ + legislation│   │ pre-training │   │ pairs        │   │ accuracy     │
│ + Official   │   │ on Turkish   │   │              │   │ preferences  │
│   Gazette    │   │ law          │   │              │   │              │
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
       │                                                         │
       │                    RAG Layer                             │
       └──────────► Real-time legislation ◄──────────────────────┘
                    and case law retrieval
```

**Data sources:**
- [Yargi MCP](https://github.com/saidsurucu/yargi-mcp) — Programmatic access to 13 Turkish court databases
- [Mevzuat MCP](https://lobehub.com/mcp/saidsurucu-mevzuat-mcp) — Real-time access to all Turkish legislation
- [Mecellem Corpus](https://arxiv.org/abs/2601.16018) — 112.7B tokens of Turkish legal training data
- [Mevzuat Dataset](https://huggingface.co/datasets/muhammetakkurt/mevzuat-gov-dataset) — 907 laws on HuggingFace

**Training pipeline:**

| Stage | What | How |
|-------|------|-----|
| **1. Data Collection** | 13 court databases, all legislation, daily Official Gazette | Yargi MCP + Mevzuat MCP + scraper |
| **2. Continued Pre-training** | Teach Turkish legal language, terminology, patterns | Curriculum learning (Mecellem approach) |
| **3. Fine-tuning (QLoRA)** | Legal Q&A pairs with source citations | Parameter-efficient — only 0.1% of params updated |
| **4. Alignment (DPO)** | Penalize hallucinated article numbers | Good/bad legal answer preference training |
| **5. RAG Layer** | Real-time legislation and case law retrieval | Vector search over legal corpus |
| **6. Continuous Updates** | Daily cron: new decisions + legislative changes | Official Gazette 06:00, court decisions 07:00 |

Full technical document: [`spec/ai/kazu-model.md`](spec/ai/kazu-model.md)

---

## The Problem

200,000+ law students in Turkish universities study with printed practice books. Everyone solves the same questions, everyone checks the same answer key. No personalization, no feedback, no adaptation.

| Issue | Description |
|-------|-------------|
| **One-size-fits-all difficulty** | Same book, same questions for everyone |
| **No feedback** | A book can't explain where you went wrong |
| **Passive learning** | Read → Solve → Check answer key |
| **No spaced repetition** | Cram everything before exams |
| **Limited content** | Finite questions in printed books |
| **Update lag** | Legislative changes require new editions — months of delay |

---

## The Solution

### Socratic Dialogue

Like a great law professor, Kazu never gives the answer directly — it guides students through the Socratic method:

```
Turn 1-2 │ Broad, open-ended questions
         │ "How would you characterize the legal relationship in this case?"
         │
Turn 3-4 │ Narrowing questions
         │ "You mentioned criminal liability — which element is missing?"
         │
Turn 5-6 │ Targeted hints
         │ "Consider the types of intent in Penal Code Art. 21..."
         │
Turn 7+  │ Near-answer scaffolding
         │ "The distinction between dolus eventualis and conscious negligence
         │  hinges on one factor — what is it?"
```

### Three-Stage Content Pipeline

No AI-generated content reaches the student directly:

```
AI Writer → AI Editor → Academic Reviewer
  (Draft)     (Validated)    (Approved)
```

### Adaptive Difficulty (Elo Rating)

Borrowed from chess: every student and every question is rated. The system targets **70-85% success rate** — the optimal learning zone (Wilson et al., 2019).

### Scientific Spaced Repetition (FSRS)

Machine learning model trained on 700 million reviews. **20-30% fewer repetitions** than SM-2 for the same retention rate. Default algorithm in Anki since v23.10.

### Legal Source Verification (RAG)

Every legal claim is grounded in real statute articles. Kazu never fabricates article numbers.

### Kazu Career — Proactive Career Guidance

Kazu doesn't just teach law — it guides students toward their future career. Using historical alumni data from partner universities (Hacettepe, AYBU, ASBU), Kazu Career predicts career paths and proactively advises current students.

```
Student's Data                Alumni Data              Prediction
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│ GPA, grades  │         │ 10,000+ law  │         │ Career path  │
│ per course,  │────────►│ graduates,   │────────►│ probability, │
│ Kazuist      │         │ career       │         │ time-to-job  │
│ performance  │         │ outcomes     │         │ estimate     │
└──────────────┘         └──────────────┘         └──────────────┘
```

| Feature | Description |
|---------|-------------|
| **Proactive** | Doesn't wait for the student to ask — notifies and guides automatically |
| **Data-Driven** | Predictions based on real alumni outcomes, not guesswork |
| **Gamified** | Career Readiness Score (0-100), Career DNA profile, streaks, XP — makes career planning fun |
| **Complete Profile** | Enrollment year, current year, course grades, retake counts, GPA — Kazu knows everything |
| **ML Pipeline** | XGBoost (career category) + Cox PH (time-to-employment) + SHAP (explainability) |
| **iOS First** | Native Swift app, Android to follow |

Students enter their faculty exam grades into Kazuist. Combined with their platform activity and anonymized alumni records, Kazu builds a dynamic career profile that evolves with every interaction.

Full technical document: [`spec/ai/kazu-career.md`](spec/ai/kazu-career.md)

---

## Three-Space Architecture

```
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│  STUDENT SPACE   │  │  LEGAL SPACE     │  │  LEARNING SPACE  │
│                  │  │                  │  │                  │
│ • Knowledge map  │  │ • Law areas      │  │ • Adaptive       │
│ • Mastery levels │  │ • Topics         │  │   difficulty     │
│ • FSRS state     │  │ • Concepts       │  │ • FSRS scheduler │
│ • Performance    │  │ • Concept graph  │  │ • Socratic engine│
│   history        │  │ • Legislation    │  │ • Kazu engine    │
│                  │  │   references     │  │ • Recommender    │
└──────────────────┘  └──────────────────┘  └──────────────────┘
```

- **Student Space**: Personal knowledge state, strengths/weaknesses, review schedule
- **Legal Space**: Structural map of the Turkish legal system
- **Learning Space**: Pedagogical intelligence — "what should this student study next?"

---

## Security

### 5-Layer AI Defense

| Layer | Defense |
|-------|---------|
| 1 | Immutable system instructions |
| 2 | Input classification (legitimate vs. manipulation) |
| 3 | Output validation (answer leakage detection) |
| 4 | Session monitoring (repeated attempt detection) |
| **5** | **Architectural separation: the correct answer is kept in a separate environment inaccessible to the student-facing AI** |

### KVKK Compliance (Turkish GDPR)

- PII anonymization before LLM calls
- Three separate consent types
- Full audit logging
- Right to be forgotten

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js 15 + shadcn/ui + Tailwind CSS |
| Mobile | Swift (iOS first), Android planned |
| Backend | FastAPI (Python) |
| Database | PostgreSQL 16 (JSONB + Turkish FTS) |
| Cache | Redis 7 |
| AI | Kazu LLM (Kumru/Gemma-based, fine-tuned) |
| Career ML | XGBoost + Cox PH + SHAP |
| Model Routing | LiteLLM (100+ models) |
| Spaced Repetition | FSRS v5+ |
| Streaming | SSE (Server-Sent Events) |
| Observability | Langfuse |
| Deployment | Docker Compose (Raspberry Pi compatible) |

### Cost

With context window optimization:

| Metric | Value |
|--------|-------|
| AI cost per student per month | **~$0.06** |
| 1,000 students / month | ~$2,100 |
| Savings vs. naive approach | 53-84% |

---

## Project Structure

```
Kazuist/
├── ARCHITECTURE.md              # Unified architecture document
├── README.md                    # This file
└── spec/
    ├── 01-tech-stack.md         # Technology choices & justifications
    ├── 02-architecture.md       # Three-Space Architecture
    ├── 03-content-pipeline.md   # Content generation pipeline
    ├── 04-api-endpoints.md      # 30+ API endpoints
    ├── 05-database-schema.md    # PostgreSQL schema (20+ tables)
    ├── 06-deployment.md         # Docker Compose + phased rollout
    ├── ai/
    │   ├── kazu-model.md        # Kazu model — training, data, architecture
    │   ├── llm-routing.md       # Multi-model routing + cost
    │   ├── socratic-engine.md   # Socratic dialogue engine
    │   ├── prompt-security.md   # 5-layer security architecture
    │   ├── rag-pipeline.md      # Legal source verification
    │   ├── cost-management.md   # Token budget + observability
    │   └── kazu-career.md       # Proactive career guidance system
    ├── algorithms/
    │   ├── fsrs.md              # FSRS spaced repetition
    │   └── elo-adaptive.md      # Elo adaptive difficulty
    ├── security/
    │   ├── kvkk.md              # KVKK compliance
    │   └── checklist.md         # Security checklist
    └── research/
        └── references.md        # Academic references
```

---

## Development Roadmap

| Phase | Duration | Focus |
|-------|----------|-------|
| **1** | Week 1-2 | Core infrastructure, auth, KVKK |
| **2** | Week 3-5 | Legal taxonomy, case engine, RAG |
| **3** | Week 6-7 | Student space, FSRS, knowledge graph |
| **4** | Week 8-10 | Socratic AI, Kazu integration, SSE |
| **5** | Week 11-13 | Gamification, Kazu v0.5, polish |
| **6** | Week 14-16 | Kazu Career, alumni data pipeline, iOS app |

---

## Comparison

| | Traditional | Kazuist + Kazu |
|---|---|---|
| Content | Limited, static | Unlimited, AI-generated |
| Difficulty | Same for everyone | Elo-adapted per student |
| Learning | Read → Solve → Answer key | Socratic dialogue with Kazu |
| Feedback | Right / Wrong | Instant, personalized |
| Repetition | Cram before exams | FSRS scientific scheduling |
| Legal accuracy | Depends on the author | RAG-grounded in real law |
| Currency | New edition required | Kazu learns every day |
| Career guidance | None | Alumni-data-driven proactive career predictions |

---

## Team

| | Person | Institution | Expertise |
|---|------|-------|----------|
| **Academic Advisor** | Assoc. Prof. Merve Aysegul KULULAR IBRAHIM | Hacettepe University | Information Technology Law |
| **Developer** | Lect. Tarik Ismet ALKAN | Ankara Yildirim Beyazit University | Computer Programming |

---

## References

### Pedagogy
- Wilson, R. C. et al. (2019). [The 85% Rule for Optimal Learning](https://doi.org/10.1038/s41467-019-12552-4). *Nature Communications*.
- Liu, J. et al. (2024). [SocraticLM: Socratic Personalized Teaching with LLMs](http://staff.ustc.edu.cn/~huangzhy/files/papers/JiayuLiu-NeurIPS2024.pdf). *NeurIPS 2024*.

### Turkish Legal AI
- [Mecellem: Turkish Legal LLMs](https://arxiv.org/abs/2601.16018) — 112.7B tokens
- [Tailoring AI for Turkish Law](https://www.sciencedirect.com/science/article/pii/S1877050925025815) — Llama 3.1 fine-tune
- [LegalTurk BERT](https://arxiv.org/html/2407.00648v1) — NER 92.48% F1
- [NER in Turkish Legal Texts](https://www.cambridge.org/core/journals/natural-language-engineering/article/abs/namedentity-recognition-in-turkish-legal-texts/012269AA2BBD10E546F8E5043426349A)

### Algorithms
- [FSRS — Free Spaced Repetition Scheduler](https://github.com/open-spaced-repetition/fsrs4anki). 700M reviews, Anki 23.10+ default.
- [OWASP LLM01:2025 — Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/).

### Data Access
- [Yargi MCP](https://github.com/saidsurucu/yargi-mcp) — 13 Turkish courts
- [Mevzuat Dataset](https://huggingface.co/datasets/muhammetakkurt/mevzuat-gov-dataset) — 907 laws
Full reference list: [`spec/research/references.md`](spec/research/references.md)

---

## Contact

kazuisthukuk@gmail.com

---

## License

This is an academic project. License details will be determined later.

---

<p align="center">
  <sub>A joint project of Hacettepe University &amp; Ankara Yildirim Beyazit University.</sub>
</p>

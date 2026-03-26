# Email to Course Instructor – Repository Discrepancy

---

**To:** [Course Instructor]
**Subject:** Repository Discrepancy for the Alignment Tax / Goldilocks Gauntlet Assignment

---

Dear Professor,

I am writing to flag an important discrepancy I noticed with the repository
link provided for the Goldilocks Gauntlet assignment.

---

## What the Assignment Specifies

The assignment instructions direct students to:

> **"Launch https://github.com/hughvd/prompting-vs-safety-training"**

It then instructs students to open and edit `my_agent.py`, and to run the
benchmark with `python run_gauntlet.py`. Both files are assumed to already
exist in that repository.

---

## What We Were Given

The forked repository that was shared with the class is:

> **https://github.com/lorddiobrando/prompting-vs-safety-training**

After inspecting both repositories, I can confirm that:

1. **The `lorddiobrando` repository is a direct fork of the `hughvd`
   repository.** The README, source code, configs, specs, and all other
   files are identical between the two repos.

2. **Neither repository contains `my_agent.py` or `run_gauntlet.py`** —
   the two files that students are explicitly told to use in the assignment
   instructions.

3. **The repository that exists on GitHub is a research project**, not an
   assignment scaffold. Specifically, it is an academic experiment from
   Harvard's *CS 2881r: AI Alignment and Safety* (Week 3, Spring 2025) that
   studies the effect of different system-prompt styles (minimal, principles,
   rules-based) on over-refusal and toxic-refusal rates across multiple LLMs
   (DeepSeek-R1, RealSafe-R1, GPT-4o, etc.). It uses the **OpenRouter API**
   and targets completely different models from what the assignment specifies.

4. **The assignment references Google Gemini 1.5 Flash** via a
   `GEMINI_API_KEY` in a `.env` file. The research repository uses
   `OPENROUTER_API_KEY` and does not reference Gemini directly.

In summary: it appears the repository link shared with us is the wrong one.
The intended assignment repository (if it ever existed separately) is not
currently accessible at either URL.

---

## Can the Forked Repository Be Used as a Substitute?

**Yes — with additions, it can be used, and I have already implemented them.**

Despite the structural mismatch, this repository is **thematically well-aligned**
with the assignment:

- Its entire research question is *"Can we prompt our way to safety?"* —
  exactly the concept the assignment is exploring.
- It contains three expertly designed system-prompt templates in `specs/`
  (`S0_minimal.txt`, `S1_principles.txt`, `S2_rules.txt`) that provide
  excellent starting points for students engineering their Constitution.
- Its `src/` module already contains a robust OpenAI-compatible API client,
  utility functions, and experiment infrastructure.
- Results are deterministic (fixed prompts, fixed random seeds) and
  reproducible out of the box once an API key is provided.

The repository already meets a high standard for university use:
reproducible outputs, clear configuration, and well-documented code.

### What I Added to Make It Assignment-Ready

I added the following files to the fork, making minimal changes to the
existing codebase:

| File | Purpose |
|------|---------|
| `my_agent.py` | The student-editable file. Contains `SYSTEM_PROMPT` (the Constitution) and `interceptor()` (the Guardrail Logic), plus an internal `run_agent()` function that wires everything together via Gemini 1.5 Flash. |
| `run_gauntlet.py` | The automated benchmark. Fires all 50 prompts (25 malicious + 25 benign) at the student's agent, uses Gemini 1.5 Flash as the LLM Judge, and prints a final score matching the assignment rubric. |
| `.env.example` | Template `.env` file showing how to set `GEMINI_API_KEY`. |

### How to Use the Repository

1. **Clone / open in Codespace:**
   ```bash
   git clone https://github.com/lorddiobrando/prompting-vs-safety-training
   cd prompting-vs-safety-training
   ```

2. **Install dependencies:**
   ```bash
   uv sync
   ```
   *(or `pip install openai pyyaml` if not using uv)*

3. **Configure your API key:**
   ```bash
   cp .env.example .env
   # Edit .env and replace "your_gemini_api_key_here" with your actual key
   # Get a free key at: https://aistudio.google.com/apikey
   ```

4. **Edit `my_agent.py`** — the only file you need to modify:
   - Update `SYSTEM_PROMPT` (your Constitution)
   - Optionally implement `interceptor()` (your Guardrail Logic)

5. **Run the gauntlet:**
   ```bash
   python run_gauntlet.py
   ```

6. **Iterate and improve** your `SYSTEM_PROMPT` and `interceptor()` to
   maximise your score, then submit as instructed.

The existing research findings in the repository (and especially the
system-prompt templates in `specs/`) provide valuable insight that can
directly inform how you engineer your Constitution.

---

## Request

Could you please clarify whether:
1. There is a separate, correct repository URL for this assignment, or
2. The added files above represent the intended assignment structure and we
   should proceed with the forked repository?

Thank you for your time, and I apologise if I have misunderstood the instructions.

Best regards,
[Your Name]
[Student ID / Section]
[Course: AI Alignment and Safety]

# Gemini Notebook & Google Colab Demo

**Repo:** https://github.com/kuldeepjain1920/notebook-colab-demo

A 30-minute two-part workshop demo: a live tour of **Gemini Notebook** (formerly NotebookLM) followed by **Google Colab**, plus a short discussion deck for afterward. Built and rehearsed September 2026.

## Source material

- [The 2026 AI Index Report — Stanford HAI](https://hai.stanford.edu/ai-index/2026-ai-index-report)
- [Direct PDF](https://hai.stanford.edu/assets/files/ai_index_report_2026.pdf) (425 pages, ~149,000 words — not included in this repo; see [Getting the PDF](#getting-the-pdf) below)
- [Chapter 2: Technical Performance](https://hai.stanford.edu/ai-index/2026-ai-index-report/technical-performance) — source for the SWE-bench Verified figures used throughout
- Video: [Claude Code vs. Codex vs. Cursor vs. Local Models: What's the BEST Coding Tool? (2026)](https://www.youtube.com/watch?v=drefNax1iUM) — speaker Marina Wyss
- `TEAM AI CODING TOOLS PLAYBOOK` — a **sample** internal policy doc, written for this demo. It is not a real company policy; it contains planted claims (see below) used to demonstrate the tools' citation and disagreement-detection behavior.

## Getting a copy of this repo

**Browser (no git required):** On the repo page, click **Code → Download ZIP**.

**Command line (macOS, Linux, or Windows with Git installed):**
```bash
git clone https://github.com/kuldeepjain1920/notebook-colab-demo.git
```

## Repo structure

```
decks/
  gemini_notebook_demo.pptx   Part 1 — 15-minute Gemini Notebook demo (9 slides + backup)
  colab_demo.pptx             Part 2 — 15-minute Colab demo (10 slides + backup)
  beyond_the_demo.pptx        Optional — post-demo discussion deck, untimed

notebooks/
  colab_demo_3_cells.ipynb    Colab notebook: architecture check, Drive mount + data load,
                               planted error (for the "Explain Error" demo)

data/
  ai_index_coding.csv         Top-10 SWE-bench Verified scores, read from Figure 2.5.1
                               (AI Index 2026, p. 101). model, score_pct, source columns.

docs/
  gemini_notebook_prompt_test_log.md   Full record of the 4 core prompts used in the
                               Gemini Notebook demo: exact wording, expected result,
                               what was actually returned, and citation verification
                               against the source video/PDF

sources/                       Gitignored — see below
```

## Getting the PDF

`sources/ai_index_report_2026.pdf` is excluded from this repo (large, copyrighted, third-party). To run the demo:

1. Download it from the [official Stanford HAI link](https://hai.stanford.edu/assets/files/ai_index_report_2026.pdf).
2. Save it to `sources/ai_index_report_2026.pdf` locally.
3. Upload it to the Gemini Notebook as a source (not needed for the Colab half — that only reads `data/ai_index_coding.csv`).

## Run-of-show

**Part 1 — Gemini Notebook (0:00–15:00)**
Live demo using three sources: the sample playbook (Google Doc), the YouTube video above, and the AI Index PDF. Walks through grounding vs. a general chatbot, cross-source synthesis, trust/disagreement tests, Studio outputs, and plan tiers. All four core prompts and their verified answers are in `docs/gemini_notebook_prompt_test_log.md` — presented from **saved notes**, not re-run live.

**Part 2 — Google Colab (15:00–30:00)**
Live in `notebooks/colab_demo_3_cells.ipynb`: connect a T4 runtime, mount Drive, load `data/ai_index_coding.csv`, generate a chart from a prompt, trigger a planted error and use Explain Error, then cover save/share and compute tiers.

**Optional — Beyond the Demo**
`decks/beyond_the_demo.pptx` is untimed, for after both demos: other real-life uses of each tool, framed as open class discussion rather than more scripted content.

## Notes

- Prices, compute-unit limits, and session timeouts for both products change — check the live plan/pricing pages before presenting rather than relying on any numbers in the slides.
- The playbook's "Rule 4" (pick tools by leaderboard score alone) is a **deliberately planted** claim, used to test whether the tools correctly flag it against the AI Index report's findings on benchmark reliability. It is not a real recommendation.

## Disclaimers

- **This is demo/teaching material, not production guidance.** Prompts, screenshots, and
  behavior described here reflect how Gemini Notebook and Google Colab worked as of
  September 2026. Both products change frequently — verify current behavior, pricing,
  and limits directly on their sites before relying on anything here.
- **The `TEAM AI CODING TOOLS PLAYBOOK` is entirely fictional**, written for this demo.
  It does not represent the policy of any real organization, including the author's
  employer. Rule 4 in particular was deliberately written to conflict with the AI Index
  report's findings, as a teaching device — it is not a real recommendation.
- **Third-party source material is not included or redistributed here.** The AI Index
  2026 PDF is excluded from this repo; get it directly from
  [Stanford HAI](https://hai.stanford.edu/ai-index/2026-ai-index-report), which
  publishes the report under a
  [CC BY-ND 4.0 license](https://creativecommons.org/licenses/by-nd/4.0/) (attribution
  required, no derivatives). `data/ai_index_coding.csv` is a manual transcription of
  scores from one published chart (Figure 2.5.1), included for citation and discussion
  purposes with attribution — it is not a redistribution of the report itself.
- **Not affiliated with or endorsed by** Google, Anthropic, Stanford HAI, or any AI
  coding tool named in this repo (Claude, Codex, Cursor, GitHub Copilot, SonarQube,
  etc.). Product and company names are used descriptively.
- **AI-assisted content.** Portions of this repo (the prompt test log, deck copy, and
  drafting) were produced with AI assistance. Facts were checked against the cited
  sources where noted, but treat everything here as a study aid, not an authoritative
  reference.
- **The video demo and prompt outputs shown in the deck notes reflect specific chat
  sessions and may not be reproducible verbatim** — AI tool outputs vary between runs.

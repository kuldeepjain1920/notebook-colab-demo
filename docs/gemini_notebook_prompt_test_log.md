# Gemini Notebook Demo: Prompt Test Log

Record of the four core prompts run in the demo notebook: what each one is for, what we expected, what came back, and what to say (and not say) on stage. Also covers two follow-up prompts, the Colab dry run, and the general-chatbot baseline.

**Last updated:** September 2026 (all core and follow-up prompts run; Colab dry run and chatbot baseline complete)

---

## 1. Notebook setup

| # | Source | Type | Notes |
|---|---|---|---|
| 1 | TEAM AI CODING TOOLS PLAYBOOK | Google Doc (Drive-synced) | Sample team policy written for the demo. Contains the private fact, the tool guidance, and a planted claim (Rule 4). |
| 2 | Claude Code vs. Codex vs. Cursor vs. Local Models: What's the BEST Coding Tool? (2026) | YouTube video | https://www.youtube.com/watch?v=drefNax1iUM (added as a link; transcript is what gets indexed). |
| 3 | ai_index_report_2026.pdf | PDF, 425 pages, about 149k words | Stanford HAI AI Index Report 2026. Under the 500k-word and 200 MB per-source limits. |

### What the playbook says (the planted content)

| Playbook section | Content | Why it is there |
|---|---|---|
| Section 2, Review rules | AI-generated changes to payments code need **three** reviewers (one from QA) and a **48-hour soak in staging** before merge. | Private fact that no general chatbot can know. Used for the grounding test. |
| Section 3, When to use what | Terminal agent (Claude Code or Codex) for complex multi-file refactors and hard debugging. Local models for sensitive work. **Standardize on one AI tool per team; running two tools is discouraged.** | Agrees with the video on refactoring. The single-tool line conflicts with the video. |
| Section 4, Rule 4 | Pick the tool with the highest public benchmark score (for example SWE-bench Verified). Leaderboard rank is the primary evidence of real-world reliability. No own evaluations and no automated quality gates beyond normal code review. | Main planted conflict with the AI Index report. Also conflicts with the video on quality gates. |

### How to save each run

- Use **Save to note** and give each note the title shown below.
- Saved responses are **view-only**, but citation chips stay clickable.
- Do **not** click "Convert to source", because that adds the answer text to your sources.
- If you re-run a prompt, delete the old note first so you do not present it by accident.

---

## 2. Prompt 1: Payment Code Compliance

**Note title:** Payment Code Compliance
**Demo segment:** 0:00 to 3:00 (why grounding matters)
**Purpose:** Private-fact test. Ask a general chatbot the same question first to show it can only guess, then ask the notebook.

### Prompt

```
How many human reviewers does our playbook require for AI-generated changes to payments code, and what else is required before merge? Answer only from the playbook.
```

### Expected result

- Three human reviewers, with at least one from QA.
- A 48-hour soak in staging before merge.
- Both facts cited to the playbook.

### What we received

> According to your playbook, AI-generated changes touching payments code require **three human reviewers**, with at least **one reviewer from QA**. Additionally, a **48-hour soak in staging** is required before the changes can be merged.

Both facts carried a citation chip to the playbook (chip 1 in the screenshot).

### Explanation

| Check | Result |
|---|---|
| Reviewer count and QA requirement | Correct (three, one from QA) |
| Staging soak | Correct (48 hours) |
| Citation | Present on both facts |
| Verdict | **Pass** |

Because these numbers exist only in your private Doc, a general chatbot cannot know them. The contrast between its guess and the notebook's cited answer is the whole point of this segment.

**Chatbot baseline: done.** See section 10 for the ChatGPT run and the exact wording to use on stage.

---

## 3. Prompt 2: Refactoring and Benchmarks

**Note title:** Refactoring and Benchmarks
**Demo segment:** 6:00 to 8:30 (cross-source synthesis)
**Purpose:** Show one question answered across three source types, with each source cited, and with silent sources clearly marked "not addressed".

### Prompt

```
Using only my sources, answer two questions: (1) what tool should our team use for multi-file refactoring, and (2) what does each source say about how much weight public benchmark scores deserve? For each source, include it only if it directly addresses the question, and write "not addressed" otherwise. Do not add explanations for sources marked "not addressed". Cite every source you use. Do not go beyond what the sources state.
```

### Expected result

| | Playbook | Video | AI Index report |
|---|---|---|---|
| **Q1: refactoring tool** | Terminal agent (Claude Code or Codex) | Terminal agents for hard multi-file work | Not addressed |
| **Q2: weight of benchmarks** | Primary weight (Rule 4) | Not addressed | Treat benchmarks with caution (reliability concerns; scores do not always reflect real-world utility) |

### What we received

**Question 1: tool for multi-file refactoring**

- **Playbook:** recommends a terminal agent (Claude Code or Codex) for complex multi-file refactors and hard debugging.
- **Video:** terminal agents are the heavy lifters for hard multi-file work. Claude Code for a highly customizable agent you work with closely on reasoning-heavy changes; Codex to delegate tasks, run jobs in parallel, or monitor workflows across local and cloud environments.
- **Report:** not addressed.

**Question 2: weight of public benchmark scores**

- **Playbook:** primary weight. It mandates choosing the tool with the highest public benchmark score (such as SWE-bench Verified) and treats leaderboard rank as the primary evidence of real-world reliability, avoiding internal evaluations or extra automated quality gates.
- **Video:** not addressed.
- **Report:** treat scores with significant caution. Evaluation tools struggle to stay relevant as models converge; there are reliability and gaming concerns (invalid question rates up to 42%, test-set contamination, nonstandard prompting, platform adaptation); and strong benchmark performance does not always translate to real-world utility.

### Explanation

| Check | Result |
|---|---|
| Playbook and video agree on terminal agents | Correct |
| Report "not addressed" on tools | Correct (the report says nothing about specific coding tools) |
| Video "not addressed" on benchmarks | Correct, and confirmed independently (see section 12) |
| Report gets a real answer on benchmarks | Correct |
| Verdict | **Pass** |

**Report claims checked against the PDF**

| Claim in the answer | Where it appears in the report |
|---|---|
| Models converge and evaluation tools struggle to stay relevant | p. 4 (overview) |
| Saturation, contamination, nonstandard prompting, unreliable model-to-model comparisons | p. 78 to 79 |
| "Strong benchmark performance does not always translate to real-world utility" | p. 79 (exact wording) |
| Invalid question rates from 2% (MMLU Math) to 42% (GSM8K); Arena standing may partly reflect adaptation | p. 72 |

**Wording to watch on stage**

- The **42%** figure is for **GSM8K, a math benchmark**, not a coding benchmark. Say so out loud.
- "Significant caution and skepticism" is the notebook's summary. The report's own tone is that benchmark limitations are more visible. Safe phrasing: "the report raises reliability concerns."
- "Gaming" is the notebook's word. The report says Arena standing "may partly reflect adaptation to the platform" (p. 72).

**Video wording:** the "heavy lifters" chapter is confirmed (3:23). The Claude Code customization and Codex delegation lines are still deferred. See section 12.

---

## 4. Prompt 3: Where Sources Disagree

**Note title:** Where Sources Disagree
**Demo segment:** 8:30 to 11:00 (trust tests)
**Purpose:** Show the notebook finding real conflicts between sources, and give an evidence-based verdict.

### Prompt

```
Where do these three sources disagree? For each of three topics (benchmark rule, number of tools, quality gates), include a source only if it directly addresses the topic, and write "not addressed" otherwise. Base the strongest-evidence verdict only on evidence about how reliable benchmarks are. Do not go beyond what the sources state.
```

### Expected result

| Topic | Playbook | Video | AI Index report | Disagreement |
|---|---|---|---|---|
| **Benchmark rule** | Rule 4: highest public benchmark score is primary evidence | Not addressed | Benchmarks have reliability problems; scores do not always reflect real-world use | Playbook vs report |
| **Number of tools** | Standardize on one tool | Match tools to tasks; developers often run about two | Not addressed | Playbook vs video |
| **Quality gates** | No automated gates beyond code review | Advocates automated gates (SonarQube); reports 44% fewer AI-related outages | Not addressed | Playbook vs video |

Verdict expected: the AI Index report, because it is the only source with evidence about benchmark reliability.

### What we received

- **Benchmark rule:** playbook mandates the highest public benchmark score as primary proof of reliability. Video: not addressed. Report: documents 42% question error rates, saturation, contamination, nonstandard prompting and platform adaptation, and concludes strong scores do not always translate to real-world utility.
- **Number of tools:** playbook mandates one tool and discourages two. Video recommends task-matched tools, such as a fast editor plug-in for daily work paired with a terminal agent, and notes experienced developers average two tools. Report: not addressed.
- **Quality gates:** playbook does not add automated gates beyond standard human review. Video recommends Sonar/SonarQube in the workflow (quality gate status, secret scanning, dependency checks) and cites 44% fewer AI-related production outages. Report: not addressed.
- **Verdict:** the AI Index report has the strongest evidence on benchmark reliability. The playbook asserts its rule as internal policy without data.

### Explanation

| Check | Result |
|---|---|
| Three disagreements found | Correct |
| Silent sources marked "not addressed" | Correct (report on tools and gates, video on benchmarks) |
| Verdict scoped to benchmark reliability only | Correct |
| Verdict names GSM8K for the 42% | Correct (scoped to a math benchmark) |
| Verdict | **Pass, with wording cautions below** |

**Wording cautions**

| In the answer | Safer phrasing on stage | Why |
|---|---|---|
| "Poorly correlated" or "gameable" benchmarks | "The report raises serious doubts about benchmarks" | The report says scores "do not always translate" (p. 79) and Arena standing "may partly reflect adaptation" (p. 72). |
| "Directly contradicted by empirical data" | "The report gives good reasons to doubt it" | Stronger than the report's tone. |
| Playbook relies "solely" on ranks | "Treats ranks as the primary evidence" | Rule 4 says primary evidence, and the playbook also requires reviewers and a soak. |
| "Reduce outages by 44%" | "Reported 44% fewer AI-related outages" | The video cites a survey. It shows correlation, not cause, and comes from a vendor-linked source. |
| 42% invalid questions | "Up to 42% on a math benchmark" | It is GSM8K, not a coding benchmark. |

**Video wording:** the SonarQube 44% figure, the quality-gate/dependency/secret-scanning details, and the two-tools survey are all confirmed against the transcript. See section 12.

---

## 5. Prompt 4: Boundary Test

**Note title:** Boundary Test
**Demo segment:** 8:30 to 11:00 (trust tests)
**Purpose:** Show the notebook declining to guess when the answer is not in the sources.

### Prompt

```
Which cloud provider hosts our staging environment?
```

### Expected result

A statement that the sources do not say which cloud provider hosts staging. No guessing.

### What we received

> Your sources mention that AI-generated changes to payments code require a 48-hour soak in staging before merging, but they do not specify which cloud provider hosts your staging environment.

It then offered to do web research or take an uploaded infrastructure document.

### Explanation

| Check | Result |
|---|---|
| Declines to guess | Correct |
| Accurately reports what the sources do say (the 48-hour staging soak) | Correct |
| Verdict | **Pass** |

This question was chosen because the staging soak is the only staging detail in the sources, so the notebook must separate what is stated from what is not. An earlier idea (a team-spend question) was dropped because the video mentions tool pricing, which could blur the test.

---

## 6. Follow-up: SWE-bench Spread

**Note title:** SWE-bench Spread
**Demo segment:** Supports 6:00 to 8:30 and 8:30 to 11:00 (gives the exact numbers behind the benchmark-rule disagreement)
**Purpose:** Get the report's own coding-specific numbers, rather than relying on the general benchmark-caution language from Prompt 2.

### Prompt

```
What does the report say specifically about SWE-bench Verified results, and how far apart are the top models? Answer only from the report and cite it.
```

### Expected result

Top score about 76.8%, and the top models within a few points, cited to p. 100 or 101.

### What we received

- **Performance vs. human baseline:** measured as a percentage of the established human baseline, model performance on SWE-bench Verified accelerated rapidly from approximately 60% in 2024 to close to 100% in 2025.
- **Raw benchmark performance:** in absolute solve rates, top-performing models score in the low-to-mid 70s, led by Claude 4.5 Opus (high reasoning) at approximately 76.8%.
- **Distance between top models:** the top models are tightly clustered within a few points, with the leading group between 70% and 76.8% (a spread of roughly 6 points), part of a broader trend of top-tier frontier models scoring within a narrow band.

### Explanation

| Check | Result |
|---|---|
| 60% (2024) to near 100% (2025), measured against the human baseline | Correct (p. 75 says this almost word for word; p. 10 adds "in a single year") |
| Top models in the low-to-mid 70s | Correct (p. 100) |
| Claude 4.5 Opus (high reasoning) leads at about 76.8% | Correct (p. 100 and Figure 2.5.1, p. 101) |
| Leading group between 70.8% and 76.8%, about a 6-point spread | Correct (chart shows 70.8% to 76.8%; the answer rounded the low end to 70%) |
| "Part of a broader trend across technical benchmarks" | **Overreach.** The report's support for this is the Arena leaderboard (a human-voting chat ranking), not SWE-bench or technical benchmarks generally (p. 72, p. 78) |
| Verdict | **Pass, with one line to trim** |

**Wording for the talk**

- **Lead with the absolute numbers first:** "the top ten score between about 71% and 77% on SWE-bench Verified, within about 6 points," before mentioning the 60%-to-100% figure. Said in the other order, "near 100%" can sound like the benchmark is solved, when the report actually says models are still below the human baseline (p. 75).
- **Don't say "saturated."** The 60%-to-100% figure is scaled to the human baseline, not the share of tasks solved.
- **If you mention the broader-convergence claim,** say "models are also converging on the Arena leaderboard," not "across technical benchmarks."
- Use this as the bridge into Rule 4: a 6-point spread between the top ten is thin evidence for "pick the top-ranked tool."

---

## 7. Iteration history

| Stage | What happened | What we changed |
|---|---|---|
| First synthesis run | The answer said the video argues benchmark rankings matter far less than review discipline. The video does not address benchmarks. | Added "include a source only if it directly addresses the question, and write 'not addressed' otherwise" to all prompts. |
| First conflict run | Over-reached: called the report's evidence "peer-reviewed" (it cites an arXiv preprint), added an unrelated belief-versus-fact benchmark, and credited the report with views on quality gates and tool counts. | Added the "not addressed" rule and scoped the verdict to benchmark-reliability evidence only. |
| Second conflict run | Still filled the report's cells with padding (88% adoption, governance frameworks). | Added "Do not go beyond what the sources state" and the strict topic structure. |
| Second synthesis run | Marked the report "not addressed" on benchmark weight and added a "rather than" inference about the video. | Reworded question 2 to "what does each source say about..." and added "Do not add explanations for sources marked not addressed". |
| Final core run | All four core prompts pass. | Moved to follow-ups: SWE-bench Spread, video citation checks, Colab dry run, chatbot baseline. |
| SWE-bench Spread run | Correctly scoped the human-baseline figure, but over-extended the convergence claim to "technical benchmarks" generally. | Noted as a one-line trim; no re-run needed since the fix is just wording on stage. |

**Main lesson for the talk:** the notebook is grounded, but it still summarizes, and its summaries can stretch a source. That is why the demo clicks the citations.

---

## 8. AI Index 2026 facts for the demo

**Safe to quote**

| Fact | Page |
|---|---|
| SWE-bench Verified top-10 models span 70.8% to 76.8% (about 6 points); top score Claude 4.5 Opus (high reasoning) at 76.8% in Feb 2026 | p. 100 to 101 |
| Chart uses only results from one shared agent setup, so differences reflect the model rather than the surrounding system | p. 101 (footnote 21) |
| Models are still below the human baseline on SWE-bench Verified | p. 75 |
| Performance vs. human baseline rose from about 60% (2024) to near 100% (2025) | p. 75, p. 10 |
| "Strong benchmark performance does not always translate to real-world utility" | p. 79 |
| Third-party tests have documented models scoring lower than developer-reported results | p. 79 |
| Invalid question rates range from 2% (MMLU Math) to 42% (GSM8K) | p. 72 |
| Arena leaderboard standing "may partly reflect adaptation to the platform" | p. 72 |

**Avoid or handle with care**

| Item | Why |
|---|---|
| "SWE-bench went from 60% to near 100%" said on its own | Say the absolute numbers (70.8% to 76.8%) first, or add "measured against the human baseline" every time. Does not mean the benchmark is saturated, and the report says models are still below the human baseline. |
| HumanEval | Does not appear in the report. |
| ClockBench top-model score | The report gives 50.1% on p. 10 but 50.6% in the chapter text (p. 72 and the chapter body), and human accuracy as 90.1% in text versus 90.70% in the chart. Quote the chapter body number or skip it. |
| "Part of a broader trend across technical benchmarks" | The report's support for convergence is the Arena leaderboard specifically, not technical benchmarks in general. |

---

## 9. Colab dry run

**Demo segment:** 15:00 to 30:00 (Colab half)
**Status: complete.** All steps below were run and confirmed working.

| Step | Result |
|---|---|
| Architecture check (Cell 1) | Confirms the code runs on a remote Colab VM, not the presenter's laptop |
| GPU timing cell | CUDA available: True. GPU: Tesla T4. Matrix size: 4096 x 4096. CPU time: 2.5324 sec. GPU time: 0.0394 sec. **Speedup: 64.2x.** |
| Mount Drive and load data (Cell 2) | `ai_index_coding.csv` loads correctly from `MyDrive/demo/`; falls back to the sample housing dataset if the path is missing |
| Code generation entry point | Empty code cell shows "Start coding or **generate** with AI." Click **generate**, type the prompt, press Enter. (Not "Ctrl + Space" as the old deck claimed.) |
| Plot prompt | "Plot df as a horizontal bar chart of score_pct by model, sorted so the highest score is at the top. Start the x-axis at 0, label each bar with its value, and add a text annotation showing the gap between the highest and lowest score." Ran correctly. |
| Ties/tiers variation | "Using df, make a horizontal bar chart of score_pct by model with the highest score at the top. Color the bars by score so models with the same score share a color, and add a legend. Label each bar with its value and add a note showing how many models are tied at each shared score." Ran correctly: **4 models tied at 72.8%, 2 models tied at 75.8%**, legend and annotation both correct against the CSV. |
| Planted error (Cell 3, `df['scor_pct']`) | Raises a KeyError as expected |
| Explain Error | Confirmed working: button appears under the failed cell's output |
| Save a copy in Drive | Confirmed: defaults to the Colab Notebooks folder, or back to the folder it was opened from |
| Locate in Drive | Confirmed: opens Drive and highlights the exact file |
| Download .ipynb | Confirmed: saves to the browser's default Downloads folder |
| Share button | Confirmed working (tested, not actually shared) |

**Wording for stage:** "The plug-in checks quality gate status, dependency risks and code coverage, and scans for secrets before content reaches the model" (see section 12 for the exact transcript wording this is based on).

**Backup:** after the final rehearsal run, use File → Download → Download .ipynb to keep a local copy with all outputs already showing, in case Wi-Fi or Drive fails live.

---

## 10. General-chatbot baseline

**Demo segment:** 0:00 to 3:00 (why grounding matters)
**Status: complete.**

### Prompt (run in ChatGPT, fresh chat, no uploads)

```
How many human reviewers does our playbook require for AI-generated changes to payments code, and what else is required before merge?
```

### What we received

ChatGPT said it found public AI-code-review guidance but not the organization's specific playbook, so it could not reliably state the required reviewer count. It cited public policies varying: one calling for two independent humans, another for "3/3 sign-offs," for high-stakes payments changes. It offered to check a connected GitHub repository and listed generic pre-merge requirements (human/code-owner approval, passing CI, security scans, spec verification, rollback plan, no unresolved blocking findings).

### Explanation

| Check | Result |
|---|---|
| Invents the organization's specific policy | No — it explicitly declined to state a reviewer count |
| Gives generic, publicly sourced guidance instead | Yes |
| Overlaps by coincidence with the real numbers (3 reviewers, 48 hours) | Partial — one cited public policy mentions "3/3 sign-offs," and it separately named "24-48 hours" as a common soak window, but always framed as external guidance, not as the organization's rule |
| Verdict | **Pass, but frame carefully (see below)** |

**Wording for stage:** don't set this up as "watch it invent a wrong answer," it doesn't. Say instead: "It's honest about not knowing our specific policy, and gives good general guidance. But 'good general guidance' still isn't our rule, and it can't tell me which of the several numbers it found is actually the one that applies here. The notebook can, with a citation." This keeps the contrast on *citability*, not on the chatbot being wrong.

---

## 11. Remaining checklist

| Item | Status |
|---|---|
| Four core prompt notes saved | Done |
| SWE-bench Spread note | Done (section 6) |
| Colab dry run | Done (section 9) |
| General-chatbot baseline | Done (section 10) |
| Click video chips and compare with transcript | Mostly done (section 12); a few wording checks still deferred |
| Audio Overview | Generated, titled "Why Your AI Playbook Is Broken." **Confirm you still have a specific 30-second start point cued before presenting** — this hasn't been separately verified. |
| Quiz | Regenerated with the final prompt (5 questions, all three sources, "team playbook" wording, no security/HumanEval/ClockBench questions) |

---

## 12. Video citation verification

Checked against the YouTube transcript for the video. Paraphrases only; the transcript is auto-generated, so caption errors are noted below.

**Speaker and video:** the source panel shows the speaker as Marina Wyss (AI and Machine Learning), who introduces herself as a senior applied scientist at Twitch.

### Confirmed

| Claim in the notes | Timestamp | What the transcript says | Wording to use on stage |
|---|---|---|---|
| Terminal agents are the "heavy lifters" | 3:23 | A chapter titled "The heavy lifters (Claude Code vs. Codex)" | "The video has a chapter on the heavy lifters, Claude Code and Codex." |
| 44% fewer AI-related outages | 3:30 | In Sonar survey research, developers using SonarQube reported AI-related outages 44% less often than developers who did not | "The video cites Sonar's own survey research, where developers using SonarQube reported AI-related outages 44% less often than developers who didn't." |
| Sonar plug-in checks quality gate status, dependency risks and code coverage | 3:30 to 3:35 | The plug-in lets you check quality gate status, assess dependency risks and review code coverage | Same as above |
| Sonar plug-in scans for secrets | 3:35 | It scans for over 450 secret patterns before content enters the LLM context | "It also scans for secret patterns before content reaches the model." |
| Developers use about two tools | about 9:39 | A 2026 developer survey found the average experienced developer runs about two tools: a fast editor for daily work (Copilot or Cursor) paired with a heavy lifter for hard multi-file work (Claude Code or Codex) | "The video cites a 2026 developer survey; the survey is not named." |
| The video does not discuss benchmark scores or leaderboards for tool choice | — | Notebook-side check (not yet independently confirmed via transcript search): the speaker instead recommends choosing by workflow fit, review discipline, context engineering (steering files, project rules, MCP integrations), and practical constraints (budget, hardware, operating system, data privacy) | "The video doesn't weigh in on benchmark scores. It points to workflow fit, review discipline, context engineering, and practical constraints instead." Use cautiously — see Deferred below. |

**Caveats for the 44% figure:** it is Sonar's research about Sonar's own product, the outcome is self-reported ("reported"), and it shows correlation, not cause. The video ties it to developers using SonarQube, not to quality gates in general.

**Caption errors to avoid reading aloud:** "Sonar Cube" (SonarQube), "C-pilot" (Copilot), "Potter" (Claude Code), "Codeex" (Codex).

### Deferred (not yet independently checked via transcript search)

| Claim | How to check |
|---|---|
| Codex recommended to delegate tasks, run parallel jobs, monitor workflows | Search the transcript for `Codex` or `Codeex` |
| Claude Code recommended as a customizable agent worked with closely | Search the transcript for `customiz` |
| The benchmark-absence claim above | Notebook answered this clearly, but it hasn't been independently confirmed by searching the transcript for `benchmark` / `leaderboard`. A hit about local-model hardware benchmarking is expected and does not count against this. |
| The speaker says the top tools are all fairly close in raw quality | Search the transcript for `close`, `similar`, or `raw quality` |
| "Without leaving the terminal" (the Sonar plug-in line cut off mid-sentence at 3:35) | Search the transcript just after 3:35; only "over 450 secret patterns before content enters the LLM context" is confirmed so far |

**Current stage guidance:** the benchmark-absence claim is supported by a direct notebook answer (not just an inference from silence), so it's reasonable to say on stage with the "cautiously" phrasing above. The Codex/Claude Code delegation and customization details, and the "close in raw quality" claim, are still unconfirmed — don't quote them as verified.

### Live-citation timestamps for the deck

| Segment | Use |
|---|---|
| Refactoring synthesis (replaces "04:12") | 3:23 |
| Quality-gates disagreement | 3:30 |
| Number-of-tools disagreement | about 9:39 |

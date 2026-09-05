# Can we trust AI outputs?

### Learning what deterministic verifiers can, and cannot, guarantee

### Teaching materials, NeurIPS 2026 Education Track

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22313823.svg)](https://doi.org/10.5281/zenodo.22313823)

The permanent, citable archive is https://doi.org/10.5281/zenodo.22313823, the concept DOI, which always resolves to the newest version. The live development repo is https://github.com/AI-Unicamp/can_we_trust_ai_outputs.

## The concept

A model is asked to produce something under a constraint: drop the identifiers, keep the facts. The output looks right. The usual reflex is to ask a second model whether the constraint held. That is unnecessary whenever the property is **decidable** from information already in hand: a small program decides it exactly and returns a failure reason specific enough to hand back to the model. The one-shot prompt becomes a loop (model output, verifier, structured feedback, retry) in which a program, not a judge, holds the gate. This is the operational meaning of *verifiable reward* and the mechanism under RLVR (reinforcement learning from verifiable rewards), the recipe behind DeepSeek-R1 and Tülu 3.

The lesson is what that gate does and does not certify. A verifier is a claim about **coverage**: it is exact over the formats it anticipates and silent about everything else, and it reports both outcomes as the same word, PASS. The learner builds one verifier for de-identifying patient records and meets five cases: two leaks it catches, one it misses and can patch (`T.L.` for *Tomas Lindqvist*), one false alarm on clean work (`18,400` vs `18400`), and one no rule reaches (*"the only patient on the ward being treated for cystic fibrosis"*). The last two give the notebook its two names for gaps: a **string gap**, which widening the rule closes, and a **world gap**, which only closes by moving the missing fact inside the input.

Tested with 9 readers: about 60 minutes for the core (Sections 0 to 7). Six of the nine went on to the optional Section 8 and reported about 20 minutes. Three stopped after Section 7. The readers worked alone and self-paced on a near-final draft, not in a classroom, and reported their own times. The current page incorporates their feedback. See `facilitator_guide.md` before running a session.

## Run it

You only need one of the two formats. Both carry the same sections in the same order, the same records, recorded attempts and verifier code. The web page adds interaction the notebook does not have. Every code cell outside Section 8 is read-only, and each cell runs from its own Run button. Section 8 stays collapsed behind a "Challenge yourself" button. A rail on the right changes colour at each of the four stages, and each cell stays dimmed until the step above it is complete. Verifier output is coloured and also carries the text markers `[caught]` and `[missed]`. A TO DO pick stays on screen and locks once it is correct. A status indicator at the bottom right shows whether Python has loaded. Section 0 opens with an animated walkthrough of the IBAN check.

**Option A, the self-running web page (recommended).** Open `can_we_trust_ai_outputs.html` in a current desktop browser (Chrome, Firefox, Safari or Edge). Python runs inside the page via Pyodide, which is bundled into the file, so nothing is downloaded or installed. Python loads after the page opens. A status indicator at the bottom right pulses amber while it loads and turns green when it is ready. Hovering over it shows "Loading Python in your browser…" or "Python ready: you can run the cells". The Run buttons stay inactive until then. Read top to bottom, answer each decision widget, press Run on each code cell. The widgets are keyboard-navigable and four of the six figures carry text alternatives. Both were checked by the authors, not by users who rely on them.

**Option B, the Jupyter notebook.** Any Jupyter environment with `ipywidgets` works: VS Code, JupyterLab or classic Jupyter. Tested on Python 3.9.6 with ipywidgets 8.1; nothing newer is needed, nothing older has been tried.

```bash
python3 -m venv .venv
source .venv/bin/activate        # on Windows: .venv\Scripts\activate
pip install jupyter ipywidgets
jupyter lab can_we_trust_ai_outputs.ipynb
```

Run the cells in order, from the top, and pick an option in each TO DO widget before running the cell that follows it. The rule you pick in a widget is the rule the verifier runs for the rest of the notebook. A cell that needs a pick you have not made, or a pick that is wrong, stops with a message saying so. Re-running a widget cell clears its pick, so run each widget cell once. "Run All" from a fresh kernel therefore stops at the first such cell by design.

No API key, no account, no cost, no GPU. Every "model attempt" is a recording. The attempts were pre-written by Gemini 3.7 Flash and are shipped inside the notebook, so nothing calls a live model.

## Contents

| File | What it is |
|---|---|
| `README.md` | This file. Start here. |
| `can_we_trust_ai_outputs.ipynb` | The lesson as a Jupyter notebook: 47 cells, 23 of them code, five decision widgets, five inline figures (four SVG, one HTML table). Self-contained: the records, the recorded attempts and every function live in its cells. |
| `can_we_trust_ai_outputs.html` | The same lesson as a single web page that runs the Python in the browser. Nothing to install. Adds a sixth figure (the animated IBAN walkthrough), read-only code cells with a Run button, a progress rail, text markers next to the coloured output and a Python status indicator. |
| `facilitator_guide.md` | For instructors: per-section timing, where to make learners commit to a prediction, where the nine readers stalled and where others are likely to, what the reader testing did and did not cover. |
| `LICENSE-CODE` | MIT license, for the code. |
| `LICENSE-CONTENT` | CC BY 4.0 license, for the prose, figures and records. |

There are no supporting modules. The notebook's first code cells define the four patient records, their ground truth, and the recorded attempts; everything after that is built in front of the learner. Both formats end with a References section, grouped by role, and every defined term in the text links to its source.

## The arc

| Section | What happens |
|---|---|
| 0 | An IBAN checksum: what "something a computer can check" means, and the six learning objectives. |
| 1 | The task: identifiers must not survive, clinical facts must. Why asking an LLM to grade is circular. The idea in one line. |
| 2 | TO DO 1 and TO DO 2: pick the rule for identifier leaks and for lost facts. They become `verify`. It fails REC-001 (a name resurfaces) and REC-002 (a fact goes missing), and both failures are the win. |
| 3 | Close the loop. A capped repair loop prints each attempt, its verdict and the reason fed back. |
| 4 | REC-003 passes three times. One attempt says `T.L.`. REC-004 fails on clean work because of `18,400`. TO DO 3 and TO DO 4 fix both and become `verify_v2`. |
| 5 | The fix has its own blind spots: `ICU` collides with a patient's initials, `Parkinson` the diagnosis collides with `Parkinson` the patient. An eight-line audit checklist for any string-matching rule. Then the attempt no rule reaches, and a widget asking which sentence would still identify someone. |
| 6 | A ward diagnosis log closes that one gap by moving the fact inside. What a PASS is entitled to claim. A reward table where a leaking attempt and a clean one score the same: reward hacking, in three rows. |
| 7 | Back to the reader's own outputs: what is decidable from what you hold, and who reads the rest. |
| 8 (optional) | Design the coverage yourself: a two-layer verifier (schema check, then value check) for JSON extracted from an expense line, then the same shape on the reader's own material. The only place the reader writes Python. Answers sit behind "Show me the answer" disclosures. On the web page the section stays collapsed until the "Challenge yourself" button is pressed. In the notebook it follows Section 7 as a regular section. |

## Learning objectives

By the end, a learner can:

1. Explain why LLM self-grading is unreliable, and how a deterministic check differs.
2. Design a decidable verifier that returns an exact pass/fail on a specific claim.
3. Use that verifier in a generate, verify, retry loop (rejection sampling / self-correction).
4. Recognize the coverage limits of rule-based verification over free text, and why they never close.
5. Explain reward hacking and Goodhart's law: how an imperfect verifier becomes a training reward (RLVR).
6. Generalize the two-layer verification pattern (schema check, then value check) to a task.

## Level and prerequisites

First-year university through advanced undergraduate, and first-time NeurIPS attendees or researchers new to RLVR. The lesson assumes the learner can read a few lines of Python and has used an LLM. It does not assume reinforcement learning, formal verification, statistics, or prior contact with verifiable rewards, reward hacking, k-anonymity, RAG or proof assistants; each is introduced where it is needed. No coding background is required for Sections 0 to 7: the learner reads, predicts and presses Run, and every rule is picked from three options with immediate feedback. Section 8 asks for two lines of Python, with the answer available on demand.

## Honest notes

- The recordings are curated, not sampled. The attempts were generated by Gemini 3.7 Flash and selected so the verifier has something instructive to catch and something instructive to miss. Nothing here is a benchmark result.
- Everything within the notebook and html is synthetic. The four records, the names, the MRNs and the ward diagnosis log are invented for this lesson. No real person, patient or incident is represented.
- The verifier is illustrative, not production-grade. It exists to teach the pattern. A deployed de-identification gate would need far more than a handful of string checks, and the notebook's audit checklist and known gaps say exactly where this one falls short on purpose.

## License

Created for the NeurIPS 2026 Education Track by Davi Pincinato and Paula Dornhofer Paro Costa (UNICAMP, Campinas, Brazil). Code is MIT (`LICENSE-CODE`). Prose, figures, the synthetic records and the recorded attempts are CC BY 4.0 (`LICENSE-CONTENT`). Reuse and adaptation by educators is explicitly welcome under those terms; attribution is all that is asked.

**How to cite.** Pincinato, D. and Costa, P. D. P. (2026). *Can we trust AI outputs? Learning what deterministic verifiers can, and cannot, guarantee.* Teaching materials, NeurIPS 2026 Education Track. https://doi.org/10.5281/zenodo.22313823

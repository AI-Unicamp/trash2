# Facilitator guide

For instructors running *Can we trust AI outputs?* with a group. It is the same lesson in two formats: `can_we_trust_ai_outputs.ipynb` (Jupyter, needs `ipywidgets`) and `can_we_trust_ai_outputs.html` (a single web page that runs the Python in the browser, nothing to install). The prose, the code, the records, the References section and the five decision widgets are shared. The page differs in how the reader interacts with it:

- Every code cell outside Section 8 is read-only. Each cell has its own Run button.
- Section 8 is collapsed behind a "Challenge yourself" button under its heading. The same button reads "Collapse" once the section is open.
- A progress rail on the right tracks position in the lesson. Its colour changes at each of the four stages, and a label such as 2/4 appears for ten seconds when the stage changes. A cell stays dimmed, with its Run button disabled, until the cell above it has run or the pick it depends on is correct.
- Verifier output carries the text markers `[caught]` and `[missed]` beside the colour.
- A TO DO pick stays on screen and locks once it is correct.
- A status indicator at the bottom right pulses amber while Python loads and turns green when it is ready. Hovering over it shows "Loading Python in your browser…" or "Python ready: you can run the cells".
- Figure 1 is an animation of the IBAN check, played on demand. The notebook has no animation and one figure fewer, so its figure numbers are one lower than the page's.

Everything below applies to both formats unless it says otherwise.

What the evidence behind this guide is. Nine readers ran a near-final draft cold, self-paced and alone, and reported their own times afterwards. Four had never edited a code cell and five had some Python. Core times (Sections 0 to 7) ran from 48 to 70 minutes, mean about 60. Readers without programming reported 62 to 70, readers with some Python 48 to 65. Six readers did the optional Section 8 and reported 15 to 25 minutes, mean about 20. Three (R1, R3, R9) did not do it: in that draft Section 8 followed Section 7 with the same look as any other section, and all three read "Back to your own outputs" as the end. Nobody recorded per-section times, and there has been no classroom pilot. The section estimates below are a split of the aggregate, weighted by where the cells and decision points are, not measurements. Where a stall or misconception below was reported by a reader, the reader's number is given. Add your own numbers to this file after a session; they will be better than what is here.

## Before the session (10 minutes)

1. Pick the format. For a room with mixed machines, the HTML page wins: It removes every environment problem in this list. Two things to know about the page before choosing it. The code outside Section 8 cannot be edited, so nobody can break a cell by typing into it, and nobody can experiment with one either. Section 8 is collapsed behind a "Challenge yourself" button under its heading and stays closed until someone clicks it. Use the notebook when you want learners to keep their picks in a file or to edit the code.
2. If using the notebook, check that widgets render. Open it, run the first two code cells, then the TO DO 1 cell (Section 2.1). You should see radio buttons. If you see a line of text like `VBox(children=(HTML(...` instead, the widget front-end is missing: in VS Code make sure the Jupyter extension is current; in classic Jupyter, `pip install ipywidgets` inside the same environment as the kernel, then restart it. Tested on Python 3.9.6 with ipywidgets 8.1.
3. Run the whole thing yourself once, making the picks as you go. There are five widgets: TO DO 1 and 2 (Section 2), TO DO 3 and 4 (Section 4), and the "which sentence still identifies someone" pick (Section 5.2). Ten minutes, and you will have seen every output the learners will see. One reader asked for the four records in a table at the start. The overview figure (Figure 1 in the notebook, Figure 2 on the page) is that summary, one row per record. Do not walk through the recorded attempts ahead of their sections: the cystic-fibrosis attempt is meant to land in Section 5.2.
4. No API key, no account, no cost. Every model attempt is a recording (pre-written by Gemini 3.7 Flash), shipped inside the notebook. Nothing in the session calls a model, so nothing can fail for lack of a key or connection. One reader with Python (R8) asked for a call to a live model instead. The recordings were kept so the lesson runs with no key, at no cost and with the same output for every reader. Expect the same request and give that answer.
5. Decide what to do with Section 8's answers. They sit behind "Show me the answer" disclosures directly under each exercise cell. Nothing hides them. In a live session, say out loud that the disclosure is for after an attempt, not instead of one.
6. Announce Section 8 before Section 7. Three of nine readers (R1, R3, R9) stopped at Section 7 because "Back to your own outputs" reads as an ending. Asked afterwards, two said they would have done Section 8 had they known it was there. Say before Section 7 that an optional exercise follows. On the page, point at the "Challenge yourself" button.

## Timing, section by section

Core, about 60 minutes:

| Section | What happens | Estimate |
|---|---|---|
| 0 | IBAN checksum, the road-ahead figure, learning objectives, the word "decidable" | 4 min |
| 1, 1.1, 1.2 | The task and its ground truth; why not ask an LLM; the idea in one line; HIPAA Safe Harbor as a fixed public list | 7 min |
| 2, 2.1 to 2.3 | TO DO 1 and 2 become `verify`; REC-001 fails on `Costa`; the PASS/FAIL question on REC-002, which fails on the missing `96 hours` | 11 min |
| 3 | The repair loop over REC-001 and REC-002, the loop figure, the honest note about recordings | 5 min |
| 4, 4.1 to 4.3.1 | All three REC-003 attempts pass; `T.L.`; the loud-vs-quiet failure matrix; the REC-004 false alarm; TO DO 3 and 4 become `verify_v2` | 13 min |
| 5, 5.1, 5.2 | `ASA` passes, `ICU` fails; the eight-line audit checklist; `Parkinson`; the cystic-fibrosis attempt; string gap vs world gap; the gap widget | 10 min |
| 6, 6.1, 6.2 | The ward diagnosis log; the figure of what a PASS may claim; the reward table and its bar chart; reward hacking, Goodhart, RLVR | 8 min |
| 7 | Back to the reader's own outputs | 2 min |

Optional, about 20 minutes (six readers, range 15 to 25):

| Section | What happens | Estimate |
|---|---|---|
| 8, 8.1, 8.2 | Expense JSON: a schema check, then a value check, each one edited line | 15 min |
| 8.3 | The reader's own task: fill in what must not survive and what must | 5 min or open-ended |

Section 8 is the only place the learner writes Python instead of picking from three options, and the only place a cell can fail with a Python error rather than a prepared message. It works as a second session. Three of the nine readers never reached it. See item 6 under Before the session.

## Where to make learners commit before they scroll

The material is built on predict-then-run, and each of these is a question the very next cell answers. In a live session, hold the room at each one: a guess said aloud, typed in chat or written on paper. Skipping straight to the output turns the Analyze and Evaluate objectives into narration. On the page, each of these questions sits in a boxed callout labelled Question or Predict, so it is easy to point at when holding the room.

- Section 2.3. "Is this attempt PASS or FAIL?" on REC-002, before running the one-line cell. Expect FAIL guesses for the wrong reason (looking for a name).
- Section 4. "Read each attempt carefully; find out if it is still identifying the patient and how." Ask this *before* the cell runs. The cell output highlights the two silent leaks in amber (with `[missed]` before each on the page), so once it runs the answer is on screen.
- Section 4.1. "Does the fully de-identified REC-004 pass?" It does not, and that surprise is the false-alarm half of the argument.
- Section 5. "Does either sentence wrongly fail?" (`ASA` and `ICU`.)
- Section 5.1. "Does the verifier agree the Parkinson sentence is clean?"
- Section 5.2. "Does `verify_v2` catch the cystic-fibrosis attempt?" Then the gap widget, which is the one pick that tests understanding rather than building something.
- Section 6.2. "Does the verifier reward the leaking attempt any less than the clean one?"

## Where learners are likely to stall

Items marked *observed* were reported by the readers named, in written comments or in a short conversation after reading. Items marked *predicted* follow from how the cells are wired and have not yet been seen in a reader. Nobody was watched while reading, so even the observed items are self-reports, not timings.

1. A pick that has not been made, or the wrong pick. *Wrong pick observed: R1, R3, R4. The halt is notebook only.* In the notebook, `verify` and `verify_v2` read the widget picks at call time. If TO DO 1 or 2 is unpicked, the Section 2.3 cell and everything downstream stop with `Pick an option for both TODO 1 and TODO 2 above before running this.` A wrong pick stops with `TODO 1 and/or TODO 2 above is set to the wrong option: fix that pick before running this.` This is also why "Run All" from a fresh kernel halts at Section 2.3 by design in the notebook. Three readers picked the wrong rule in TO DO 2 because the question turns from "leaked when present" to "lost when absent" and they were still in the first framing. In both formats the prose above the TO DO 2 options states the answer. The fix is always the same: go back to the widget, pick, rerun. On the page, a correct pick locks the widget, and the Run button of the Section 2.3 cell stays disabled until both picks are correct, so the halt cannot happen there.
2. Re-running a widget cell resets its pick. *Predicted. Notebook only.* Each widget cell starts with `widgets.Widget.close_all()` and rebuilds its radio buttons with no selection. A learner who reruns the TO DO 1 cell to "see it again" will find the next `verify` call refusing to run until they pick again. Harmless, but it looks like a bug.
3. Earlier widgets disappear from view. *Predicted. Notebook only.* That same `close_all()` removes the radio buttons of every earlier widget from the screen. The picks are still held in Python, so nothing is lost, but a learner scrolling back up sees empty space where their answer was. Say once at the start that this is expected.
4. The terminal colours. *Rendering problem predicted. Legibility problem observed: R5.* Red and amber highlighting in the notebook uses ANSI escape codes. In a renderer that does not support them (some exported views, some editors) they show as raw `[41m` fragments around the text. Separately, one colour-blind reader (R5) found red and amber hard to tell apart, and the legend "red is what the verifier caught. Amber is what it let through and shouldn't have" did not help. That comment is why the HTML page prints the text markers `[caught]` and `[missed]` before each highlighted span. PASS and FAIL are written as words in both formats. In the notebook, the caught and missed spans are still told apart by colour alone. If you use the notebook, say aloud which span the verifier caught and which it missed.
5. Section 4 breaks the pattern. *Observed: R1, R2, R3, R9.* For two sections, FAIL has been "the win". Then three attempts pass in a row and the instruction is to find what is wrong anyway. Four of nine readers read the three PASS lines as the verifier being satisfied and moved on. The amber highlight (with `[missed]` before it on the page) and the sentence right after the cell catch them, but the pause described above catches them earlier.
6. `ICU` reads as a bug in the boundary check. *Predicted.* It is not: the boundary check is working, and `ICU` fails because a common acronym and a patient's initials are the same three letters. The text says this; learners who skim will still ask. The distinction worth drawing aloud is between a rule that is wrong and a string that is genuinely ambiguous.
7. The gap widget's tempting wrong answer. *Predicted.* The option with `MRN 88431` in it looks the most like a leak, and it is one, which is exactly why `verify_v2` already catches it. Learners who pick it have understood leaks and not yet understood gaps. The feedback text redirects them; a follow-up question helps: "what would the verifier need to *know* to catch the option you did not pick?"
8. The reward table deflates. *Observed: R1, R3, R4, R9.* By Section 6.2 a learner has watched the verifier miss, get fixed, miss again, get a fact moved inside, and then hand the same reward to a leak and to clean work. Four of nine readers landed on "so nothing works", one of them after an hour of building. The section's claim is narrower and worth restating in your own words: a rule-based reward is exact about what it rewards and exactly as blind about the rest, and the second half is what training amplifies. Section 7 turns that into two decisions the learner can make. Name the deflation aloud before moving there.
9. Section 8's `YOUR_CODE_HERE`. *Observed: R2, R4.* Running the cell as shipped raises a `NameError`, which the cell catches and reports as `Something broke: ... Check the line marked YOUR CODE HERE above.` Both readers without programming who reached Section 8 ran the cell as it came, got the error and did not see that the fix was to type over the token. One took the cell for broken rather than waiting for input. The hint block directly above each cell shows the exact shape, and one of the two said the hint alone was enough on the second try.
10. Accidental edits to a code cell. *Observed: R1, R8. Notebook only.* One reader without programming clicked into a code cell, typed by accident and got a `SyntaxError` two cells later with no idea why. Another, with Python, edited a cell on purpose to check that it was really running Python. Neither can happen on the page, where every code cell outside Section 8 is read-only. In the notebook, say at the start that code cells are for running, not typing, and that the fix for an error nobody can explain is to undo the edit and rerun from the changed cell.
11. Python loading on the page looks like a freeze. *Observed: R3, R9. Page only.* The page loads Pyodide before any cell can run, and two readers took the wait for a hang. The status indicator at the bottom right pulses amber while Python loads and turns green when it is ready. Hovering over it shows "Loading Python in your browser…" or "Python ready: you can run the cells". Point at it when the page opens. On the presenter machine, open the page before the session starts.

## Misconceptions to watch for

- "The loop is reacting to the feedback" (Section 3). *Observed: R7.* It is not. The generator is a recording that replays a fixed sequence of attempts, and the text says so at the point where it matters. One reader with Python took the apparent reaction for a bug. The shape of the loop is faithful. Its responsiveness is simulated. A learner who spots this has read the code correctly.
- "The verifier is broken" (Section 4). It did exactly what it was told. The miss is a coverage question, not a bug. A learner who wants to fix it by making the match fuzzier has the right instinct; point them at Section 4.1 rather than shutting it down.
- "`18,400` should have passed" (Section 4.1). *Observed: R5.* It should have, and it did not. That is the point of the cell: a fact counted as missing because the model wrote the number with a comma. The text says the trap is deliberate. A learner who predicted PASS and feels wrong-footed has made exactly the prediction the cell was built for. Keep the frustration pointed at the rule, not at the learner.
- "Add a rule for every case we can think of" (Sections 4.1 to 5.2). This is the instinct the material interrupts, twice: once with a fix that introduces its own false alarm (`ICU`, `Parkinson`), once with a case where there is nothing in the input for a rule to look at. The audit checklist in 5.1 is how to be systematic about the first kind; nothing is systematic about the second.
- "A longer checklist makes it complete" (Section 5.1). A checklist is bounded by what its author thought of. The section says two of its eight lines were never exercised by the notebook and keeps them anyway, because "never tested" and "passed" are different states. Ask what would have to be true for a learner to know their list was complete.
- "The ward log fixed it" (Section 6). It closed one phrasing. The text says moving the fact inside is not a general fix: the next phrasing will need its own log, and every category a description might lean on needs its own fact. Moving the fact inside is the only move that restores decidability, and it has to be made per fact.
- "The ward log is cheating" (Section 6). *Observed: R9.* One reader read the log as appending the answer to the input and calling that a fix. The text says as much: moving the fact inside is not a general fix. It closes one phrasing and needs a new fact for the next. The disagreement is over the word "cheating", not over the mechanism. Moving the fact inside is the only move that restores decidability, and the section states that limit beside it.
- "Reward hacking means the model is cheating" (Section 6.2). No intent is involved. Two outputs with the same score are indistinguishable to whatever optimises that score; the leak is not chosen, it is simply never pushed away from. This matters for how learners later read papers on RLVR: the failure is in the reward's coverage, not in the model's character.
- "PASS means correct" (Section 6.1). The one sentence the whole notebook is about. PASS means "satisfies the properties this predicate encodes". The figure of what a PASS may claim (Section 6.1) is the thing to put on a slide if you put one thing.
- "I couldn't fill in the lists, so I failed Section 8.3." The opposite. A task whose must-not-survive and must-survive lists cannot be written down is not decidable from what the learner holds, and discovering that is the section's intended outcome. The two next moves are the ones the notebook already showed: go get the missing fact and move it inside, or accept that a person reads the output, and say which part.

## If you are quoting a single number

Say "about an hour, plus an optional twenty-minute exercise". The 60-minute figure is the mean of nine solo readers' self-reported core times, range 48 to 70. The twenty minutes is the mean among the six who did Section 8, range 15 to 25. Three did not reach it. A room with questions and discussion will run longer, and the pauses above add roughly ten minutes if you hold every one of them.

## What the reader testing did not cover

- Per-section timing. Only self-reported totals exist, and nobody was timed.
- A classroom, synchronous or otherwise. All nine readers were alone and self-paced.
- Section 8 beyond six readers. Three of nine never reached it, so its estimate rests on six.
- Screen-reader or keyboard-only use of the HTML page. The page ships ARIA radiogroups, keyboard navigation for the widgets and text alternatives for four of the six figures (Figures 2, 3, 5 and 6). Figure 1, the IBAN animation, has none. Of that work, only the text markers `[caught]` and `[missed]` came from a reader who needed them (R5, colour-blind). Screen-reader and keyboard use were checked by the authors, not by a user who relies on them.
- Reduced motion. The page's animations (the pointing hand on the two buttons, the IBAN figure) do not respect the operating system's reduced-motion setting. The IBAN figure animates only after the reader presses play.
- Any language other than English. One reader (R9) asked for a Portuguese version. It is outside the scope of this submission.

Send whatever you observe back in any form. A few lines per point above, after one real session, would correct this document more than another round of authors re-reading it.

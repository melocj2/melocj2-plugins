---
name: vibe-check
description: Use when the user asks to be quizzed, tested, or checked on their understanding — "vibe check", "quiz me", "test whether I understand", "ask me multiple choice questions" — about a code change, bug fix, concept, or explanation.
---

# vibe-check

## Overview

Test the user's understanding of a topic with a **single** multiple-choice
question, then grade and explain. The point is to confirm the *reasoning* landed
— not to trick them. A good vibe-check surfaces exactly which mental step is
missing so it can be taught on the spot.

## When to use

- User says "vibe check", "quiz me", "test whether I understand", "ask me
  multiple choice questions" — on the current discussion or a topic they name.
- Default the subject to what was just discussed; if the user names a topic, use
  that instead.

## Workflow

1. **Pick the subject.** Whatever was just explained, or the named topic.
2. **Pick one facet** to probe — the one that best tests whether the reasoning
   landed. Choose from the facet set that fits the subject:

   *For a bug or code change:*
   - the **root cause**
   - the **symptom** it produces
   - the **delivery mechanism** (how the effect actually happens)
   - what the **fix changes** and why
   - a **counterfactual** ("what if we only did half the fix?")

   *For a topic/concept that was asked about, or a file/flow and how it works:*
   - the **purpose** — what problem it solves or why it exists
   - the **mechanism** — how it actually works step by step
   - **control flow / sequencing** — what calls what, and in what order
   - **data flow** — what goes in, what transforms it, what comes out
   - **boundaries & responsibilities** — which piece owns what, where one ends
     and the next begins
   - **preconditions / triggers** — what must be true for it to run
   - an **edge case or failure mode** — what happens when an assumption breaks
   - a **counterfactual** ("what if this piece were missing / configured
     differently?")

3. **Ask ONE question via `AskUserQuestion`.** Single-select, **4 options**:
   exactly one correct + three plausible distractors drawn from real
   misconceptions. Just the one question — never batch more.
4. **Grade the answer** once it's in. See Grading.

## Question design (anti-leak rules)

- **Distractors must be plausible** — draw them from mistakes a real learner
  makes. Obviously-wrong options make the quiz trivial.
- **Choose the correct slot by computation, never by feel.** LLMs can't
  randomize and default to clustering the answer in B/C. Instead, count the
  characters in your question text (letters, digits, spaces, and punctuation —
  the whole string) and take that count mod 4 → `0=A, 1=B, 2=C, 3=D`. Put the
  correct answer in that slot and build the three distractors around it.
  Character counts vary far more than word counts, so the slot spreads evenly
  instead of clustering.
- **Keep options similar in length and detail.** A longer or more-detailed
  correct option betrays the answer.
- **No hints.** Never append "(Recommended)"; never tilt an option's `description`
  toward the answer.
- **Test reasoning, not recall.** Ask *why*/*what happens if*, not "what line
  number" or exact identifier names.

## The "I don't know" path

`AskUserQuestion` auto-provides an "Other" choice. The user can answer "I don't
know — explain it." Treat that as a request to teach that concept in grading,
same as a wrong answer — no penalty framing.

## Grading

Once the answer is in:

- **Confirm the correct answer by its *text*, not slot letter** — restate the
  wording so there's no chance of grading against the wrong slot.
- If **correct**: one short line confirming it, plus a sentence on *why* it's
  right so the reasoning is reinforced.
- If a **miss or "I don't know"**: explain the correct reasoning *and* why the
  chosen distractor is wrong.
- Close with a one-line **mental-model takeaway** that situates this facet in the
  bigger picture (e.g. how the root cause leads to the symptom).

## Common mistakes

- Distractors that are obviously wrong → quiz is trivial.
- Answer leaks via a longer / more-detailed correct option.
- Picking the correct slot by feel instead of the char-count-mod-4 rule.
- Asking recall trivia (line numbers, exact names) instead of reasoning.
- Batching more than one question — ask exactly one.
- Grading without explaining a miss — the teaching moment is the point.

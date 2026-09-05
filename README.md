# vibe-check

A [Claude Code](https://claude.com/claude-code) skill that quizzes you on what you
just learned. When you ask to be "vibe checked," Claude asks **one** targeted
multiple-choice question about the current discussion — a bug fix, a code change,
or a concept — then grades your answer and explains the reasoning.

The point isn't to trick you. It's to surface exactly which mental step is missing
so it can be taught on the spot.

## What it does

- Triggers on phrases like **"vibe check"**, **"quiz me"**, **"test whether I
  understand"**, or **"ask me multiple choice questions."**
- Picks a single facet worth probing (root cause, control flow, data flow, an edge
  case, a counterfactual, …) and asks one 4-option question.
- Distractors are drawn from real misconceptions; the correct slot is chosen by
  computation (not by feel) so the answer doesn't cluster or leak.
- Grades by the answer's *text*, explains why the right answer is right — and, on a
  miss, why the distractor you picked is wrong — then leaves you with a one-line
  mental-model takeaway.

## Install

### Option A — as a Claude Code plugin (recommended)

In a Claude Code session:

```
/plugin marketplace add melocj2/vibe-check
/plugin install vibe-check@vibe-check
```

Then just say "vibe check me" after Claude explains something.

### Option B — copy the skill in manually

Clone (or download) this repo and copy the skill folder into your Claude skills
directory:

```bash
git clone https://github.com/melocj2/vibe-check.git
cp -r vibe-check/skills/vibe-check ~/.claude/skills/
```

The result should be `~/.claude/skills/vibe-check/SKILL.md`. Restart Claude Code (or
start a new session) and the skill is available.

## How to use

After Claude explains a change or concept, say any of:

- "vibe check"
- "quiz me on that"
- "test whether I understand this"

Claude asks one multiple-choice question. Answer it — or pick "I don't know" to have
it taught instead. Either way you get an explanation and a takeaway.

## License

[MIT](LICENSE) © Jacob Meloche

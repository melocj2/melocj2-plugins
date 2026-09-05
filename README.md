# melocj2-plugins

A personal [Claude Code](https://claude.com/claude-code) plugin marketplace — a
single place to publish and install my Claude Code tools. Add it once and install
any plugin from it; new tools show up here over time.

## Add the marketplace

In a Claude Code session:

```
/plugin marketplace add melocj2/melocj2-plugins
```

Then install whichever plugins you want (see below).

## Plugins

### vibe-check

Quizzes you on what you just learned. When you ask to be "vibe checked," Claude asks
**one** targeted multiple-choice question about the current discussion — a bug fix, a
code change, or a concept — then grades your answer and explains the reasoning. The
point isn't to trick you; it's to surface exactly which mental step is missing so it
can be taught on the spot.

- Triggers on phrases like **"vibe check"**, **"quiz me"**, **"test whether I
  understand"**, or **"ask me multiple choice questions."**
- Picks a single facet worth probing (root cause, control flow, data flow, an edge
  case, a counterfactual, …) and asks one 4-option question.
- Distractors are drawn from real misconceptions; the correct slot is chosen by
  computation (not by feel) so the answer doesn't cluster or leak.
- Grades by the answer's *text*, explains why the right answer is right — and, on a
  miss, why the distractor you picked is wrong — then leaves a one-line takeaway.

Install:

```
/plugin install vibe-check@melocj2-plugins
```

Then say "vibe check me" after Claude explains something.

## Adding a new plugin

Each plugin is self-contained under `plugins/<name>/`:

```
plugins/<name>/
├── .claude-plugin/
│   └── plugin.json        # plugin manifest (name, version, …)
└── skills/<skill>/SKILL.md # and/or commands/, agents/, hooks/
```

Then register it by adding one entry to `.claude-plugin/marketplace.json`:

```json
{ "name": "<name>", "source": "./plugins/<name>" }
```

Commit and push — the marketplace picks it up on the next `/plugin marketplace update`.

## License

[MIT](LICENSE) © Jacob Meloche

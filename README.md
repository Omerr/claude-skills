# Claude Code Skills

A collection of reusable [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills (slash commands) that extend what Claude can do from your terminal.

## Skills

### `/create-marp-deck` — Build Marp Slide Decks

A thinking partner for presentations, powered by [Marp](https://marp.app/) (Markdown Presentation Ecosystem).

```
/create-marp-deck API rate limiting
```

The skill starts by **talking through the presentation with you** - asking about the goal, audience, key points, data to include, and constraints. This helps you figure out the story and structure before a single slide exists. Then it generates a first draft you can iterate on.

What you get:
- A structured first draft with a narrative arc you can react to and reshape
- Styled Marp Markdown with gradient section dividers, breadcrumb navigation, and consistent formatting
- Automatic export to HTML and PPTX
- Opinionated conventions: one idea per slide, 3-5 bullet max, color-coded sections

See the [full skill file](commands/create-marp-deck.md) for all conventions and the CSS template.

**Requires**: `npm install -g @marp-team/marp-cli` (or uses `npx` as fallback)

### `/cr` — Code Review

Multi-pass code review for the current branch's open PR.

```
/cr
```

Performs 4 iterative passes:
1. **Bug hunting** — logic errors, null handling, race conditions, security issues
2. **Validation** — confirms findings, removes false positives
3. **Code smells** — duplication, complexity, naming, dead code
4. **Final sweep** — edge cases, integration issues, missing tests

Outputs findings categorized by severity (critical / warning / nit) with file paths and line numbers.

## Installation

### Option 1: Copy individual files

```bash
cp commands/create-marp-deck.md ~/.claude/commands/
cp commands/cr.md ~/.claude/commands/
```

### Option 2: Clone and symlink

```bash
git clone https://github.com/Omerr/claude-skills.git ~/claude-skills

ln -s ~/claude-skills/commands/create-marp-deck.md ~/.claude/commands/
ln -s ~/claude-skills/commands/cr.md ~/.claude/commands/
```

### Option 3: Project-level

Copy into a specific project's `.claude/` directory to scope them to that repo:

```bash
cp commands/*.md your-project/.claude/commands/
```

## Customization

These skills are meant to be forked and adapted. Some things you might want to change:

- **`create-marp-deck.md`** — Swap the color palette, adjust font sizes, add your own slide structure conventions, modify the interview questions
- **`cr.md`** — Add project-specific review criteria or coding standards

## How Claude Code Skills Work

Skills live in `~/.claude/commands/` (global) or `.claude/commands/` (per-project). When you type `/` in Claude Code, your skills appear as available slash commands.

For more on creating your own skills, see the [Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code).

## License

MIT

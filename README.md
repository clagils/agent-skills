# Vitraun Agent Skills

Public [Agent Skills](https://agentskills.io/) for integrating **Vitraun Virtual Try-On** with AI coding agents (Cursor, Claude Code, Codex, and others via [skills.sh](https://skills.sh)).

**Repository:** https://github.com/clagils/agent-skills  
**Git SSH:** `git@github.com:clagils/agent-skills.git`

## Available skills

| Skill | Description |
|-------|-------------|
| [`vitraun-integration`](./vitraun-integration/) | Install and use `@vitraun/webar` on HTML, React, Next.js, or React Native |

## Install with the Skills CLI

From any project directory. Replace `<agent>` with your harness slug — run `npx skills ls` for the full list (70+ agents):

```bash
npx skills add clagils/agent-skills --skill vitraun-integration --agent <agent> -y
```

Common examples:

```bash
# Cursor
npx skills add clagils/agent-skills --skill vitraun-integration --agent cursor -y

# Claude Code
npx skills add clagils/agent-skills --skill vitraun-integration --agent claude-code -y

# Codex
npx skills add clagils/agent-skills --skill vitraun-integration --agent codex -y

# GitHub Copilot
npx skills add clagils/agent-skills --skill vitraun-integration --agent github-copilot -y
```

Install globally (all projects on your machine):

```bash
npx skills add clagils/agent-skills --skill vitraun-integration --agent <agent> -g -y
```

Multiple agents at once:

```bash
npx skills add clagils/agent-skills --skill vitraun-integration -a cursor -a claude-code -a codex -y
```

List skills in this repository without installing:

```bash
npx skills add clagils/agent-skills --list
```

Install from Git SSH:

```bash
npx skills add git@github.com:clagils/agent-skills.git --skill vitraun-integration --agent <agent> -y
```

Full install guide: https://docs.vitraun.com/en-US/development/llm-integration/install-skill

## Sync from the Vitraun monorepo

When updating skills in the main Vitraun repository, copy `skills/` from the monorepo into this repository and push:

```bash
git clone git@github.com:clagils/agent-skills.git
rsync -av /path/to/tryon-new-version/skills/ agent-skills/
cd agent-skills && git add . && git commit -m "chore: sync vitraun-integration skill" && git push
```

Local install while developing in the monorepo:

```bash
npx skills add ./skills/vitraun-integration --agent cursor -y
```

## Related resources

- Developer docs — [AI / LLM integration guide](https://docs.vitraun.com/en-US/development/llm-integration-guide)
- Plain-text index — [llms.txt](https://docs.vitraun.com/llms.txt)
- Quickstarts — [GitHub](https://docs.vitraun.com/en-US/development/github)
- Product info (not integration) — [vitraun.com/llm](https://vitraun.com/en-US/llm)

## Repository layout

```
agent-skills/
├── README.md
└── vitraun-integration/
    ├── SKILL.md
    ├── reference.md
    └── prompt-template.md
```

## License

Same license terms as the Vitraun SDK and documentation. See the main Vitraun repository for details.

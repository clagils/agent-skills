# Vitraun integration — reference

## Documentation URLs (en-US)

| Topic | URL |
|-------|-----|
| LLM guide | https://docs.vitraun.com/en-US/development/llm-integration-guide |
| Quick start | https://docs.vitraun.com/en-US/development/quick-start |
| Integration overview | https://docs.vitraun.com/en-US/development/integration/overview |
| HTML | https://docs.vitraun.com/en-US/development/integration/html |
| React | https://docs.vitraun.com/en-US/development/integration/react |
| Next.js | https://docs.vitraun.com/en-US/development/platforms/nextjs |
| React Native | https://docs.vitraun.com/en-US/development/integration/react-native |
| E-commerce / cart | https://docs.vitraun.com/en-US/development/integration/ecommerce |
| Embed init | https://docs.vitraun.com/en-US/development/embed-init |
| Widget attributes | https://docs.vitraun.com/en-US/development/widget-api/attributes |
| Widget methods | https://docs.vitraun.com/en-US/development/widget-api/methods |
| Widget events | https://docs.vitraun.com/en-US/development/widget-api/events |
| CDN | https://docs.vitraun.com/en-US/development/cdn |
| What not to do | https://docs.vitraun.com/en-US/development/what-not-to-do |
| Go-live checklist | https://docs.vitraun.com/en-US/development/go-live-checklist |
| GitHub quickstarts | https://docs.vitraun.com/en-US/development/github |

## llms.txt

https://docs.vitraun.com/llms.txt

## Install this skill (coding agents)

Full guide: https://docs.vitraun.com/en-US/development/llm-integration/install-skill

Public repository: https://github.com/clagils/agent-skills

List supported harnesses:

```bash
npx skills ls
```

Replace `<agent>` with your harness slug (`cursor`, `claude-code`, `codex`, `github-copilot`, `opencode`, etc.):

```bash
npx skills add clagils/agent-skills --skill vitraun-integration --agent <agent> -y
```

Global install:

```bash
npx skills add clagils/agent-skills --skill vitraun-integration --agent <agent> -g -y
```

Multiple agents:

```bash
npx skills add clagils/agent-skills --skill vitraun-integration -a cursor -a claude-code -a codex -y
```

Git SSH:

```bash
npx skills add git@github.com:clagils/agent-skills.git --skill vitraun-integration --agent <agent> -y
```

Harnesses without Agent Skills: use [prompt-template.md](./prompt-template.md) or `npx skills use clagils/agent-skills --skill vitraun-integration`.

## Getting started after install

Full walkthrough: https://docs.vitraun.com/en-US/development/llm-integration/install-skill

1. Copy **merchant-id** and **widget-id** from the Vitraun Integrations panel.
2. Open your storefront project in the coding agent.
3. Ask in chat (example):

```text
Integrate Vitraun VTO on my product page using HTML and CDN.
Use merchant-id and widget-id from environment variables.
Follow the official quickstart and open the widget on "Try on" button click.
```

4. Validate with the checklist below before go-live.

## GitHub quickstart repositories

| Folder / repo slug | Stack |
|----------------------|-------|
| quickstart-vto-web-html-cdn | Plain HTML + jsDelivr |
| quickstart-vto-web-js-npm | Vite vanilla + npm |
| quickstart-vto-react | React + Vite |
| quickstart-vto-nextjs | Next.js App Router |
| quickstart-vto-react-native | Expo + WebView |

npm package (web): `@vitraun/webar`  
npm package (mobile): `@vitraun/react-native`

## Validation checklist

- [ ] `@vitraun/webar` version pinned (web) or correct mobile package
- [ ] `merchant-id` and `widget-id` from env / config — not hardcoded in public repos
- [ ] Single `import '@vitraun/webar'` on the client (React/Next)
- [ ] `open()` wired; React listeners cleaned up on unmount
- [ ] `addToCart` / checkout handlers connected to store backend
- [ ] No hardcoded `vtoUrl` or Vitraun app URL in HTML
- [ ] CDN/npm version pinned — no `@latest`
- [ ] HTTPS in production; channel allowlist configured

## Anti-patterns (never do)

| Wrong | Right |
|-------|-------|
| Embed `https://app…vitraun…` URL in iframe/WebView | Official SDK + embed-init |
| Build try-on URL manually | `open()` or `<VitraunTryOn />` |
| `@latest` in production | Pinned semver |
| `@vitraun/webar` in React Native app | `@vitraun/react-native` |
| API secrets in client bundle | Backend-only secrets |
| Trust client cart events alone | Validate SKU/qty on server |

See https://docs.vitraun.com/en-US/development/what-not-to-do

## Environment variables (web quickstarts)

| Tool | Typical vars |
|------|----------------|
| Vite | `VITE_MERCHANT_ID`, `VITE_WIDGET_ID` |
| Next.js | `NEXT_PUBLIC_MERCHANT_ID`, `NEXT_PUBLIC_WIDGET_ID` |

Copy from `.env.example` — never commit `.env`.

# Vitraun VTO — prompt template

Copy the block below into any LLM session (ChatGPT, Claude, Copilot, etc.).

```text
Integrate Vitraun VTO following the official documentation.

Context:
- Web package: @vitraun/webar (same package for HTML and React)
- Widget: custom element <vitraun-vto>
- AI guide: https://docs.vitraun.com/en-US/development/llm-integration-guide
- llms.txt: https://docs.vitraun.com/llms.txt

Before coding, decide:
1. Plain HTML / e-commerce theme → CDN or <script> (HTML guide)
2. React / Next.js client → npm install + import '@vitraun/webar' (React guide)
3. Native app → @vitraun/react-native (React Native guide)

Mandatory rules:
- merchant-id and widget-id are required (Integrations panel)
- NEVER build the try-on URL — open() calls embed-init and receives vtoUrl
- HTML: load widget.min.js via Vitraun CDN or jsDelivr with pinned version
- React: import '@vitraun/webar' once on the client; Next.js requires 'use client'
- SPA: basket-opens-in="event" and checkout-opens-in="event"
- Cart events: subscribeVitraunVTOEvents or addEventListener('addToCart')
- Production: HTTPS; domain on channel allowlist
- Do not invent attributes, methods, or URLs outside official docs

Executable references (GitHub):
- quickstart-vto-web-html-cdn
- quickstart-vto-react
- quickstart-vto-nextjs

Detailed docs:
- HTML: https://docs.vitraun.com/en-US/development/integration/html
- React: https://docs.vitraun.com/en-US/development/integration/react
- Events: https://docs.vitraun.com/en-US/development/widget-api/events
```

## Coding agent users

Install the official agent skill instead of pasting the prompt. Replace `<agent>` with your harness (`cursor`, `claude-code`, `codex`, `github-copilot`, etc.):

```bash
npx skills add clagils/agent-skills --skill vitraun-integration --agent <agent> -y
```

Install guide: https://docs.vitraun.com/en-US/development/llm-integration/install-skill

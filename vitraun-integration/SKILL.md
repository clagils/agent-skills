---
name: vitraun-integration
description: >-
  Integrates Vitraun Virtual Try-On via @vitraun/webar (HTML/React) or
  @vitraun/react-native. Use when the user mentions Vitraun, VTO, virtual
  try-on, @vitraun/webar, vitraun-vto, embed-init, merchant-id, widget-id,
  or integrating try-on in e-commerce themes, React, Next.js, or mobile apps.
---

# Vitraun VTO integration

Read this skill before generating or reviewing Vitraun integration code.

**Canonical sources (in order):**

1. Official quickstarts on GitHub (executable ground truth)
2. Developer docs — https://docs.vitraun.com/en-US/development/llm-integration-guide
3. Plain-text index — https://docs.vitraun.com/llms.txt
4. Widget API — attributes, methods, events (links in [reference.md](reference.md))

For product marketing (not integration), use https://vitraun.com/en-US/llm.

## Decision tree — pick ONE path

```
Does the host page use a React bundler (Vite, CRA, Next client)?
├─ YES → Next.js App Router?
│   ├─ YES → npm @vitraun/webar + 'use client' → quickstart-vto-nextjs
│   └─ NO  → npm @vitraun/webar + single import → quickstart-vto-react
├─ NO → Bundler without React (Vite/vanilla)?
│   └─ YES → npm @vitraun/webar → quickstart-vto-web-js-npm
└─ NO → Plain HTML / e-commerce theme / landing
    └─ CDN or <script> @vitraun/webar → quickstart-vto-web-html-cdn

Native iOS/Android app?
└─ @vitraun/react-native + VitraunTryOn → quickstart-vto-react-native
```

**HTML and React share the same web package:** `@vitraun/webar`. Only the load method differs.

## Non-negotiable invariants

1. Web package: `@vitraun/webar` — pin semver; **never** `@latest` in production.
2. Widget UI: custom element `<vitraun-vto>` — no official React widget component.
3. Required attributes: `merchant-id`, `widget-id` (Vitraun Integrations panel).
4. **Never build `vtoUrl` manually** — `open()` calls embed-init internally.
5. Production web: **HTTPS**; domain on channel allowlist when enforced.
6. SPA / React Router: `basket-opens-in="event"` and `checkout-opens-in="event"`.
7. Next.js: `import '@vitraun/webar'` only in client components; no SSR of the custom element.
8. React events: `subscribeVitraunVTOEvents` with cleanup on unmount.
9. HTML events: `addEventListener('addToCart', …)` on the `<vitraun-vto>` element.
10. Do not invent attributes, methods, or event payloads — verify in official docs.

## Minimal patterns

### HTML (CDN)

```html
<script src="https://cdn.jsdelivr.net/npm/@vitraun/webar@VERSION/dist/widget.min.js"></script>
<vitraun-vto merchant-id="…" widget-id="…" lang="en-US" platform="web"></vitraun-vto>
<script>
  const widget = document.querySelector('vitraun-vto')
  widget.addEventListener('addToCart', (e) => { /* sync cart */ })
  widget.open()
</script>
```

### React

```tsx
'use client'
import '@vitraun/webar'
import { subscribeVitraunVTOEvents } from '@vitraun/webar'

// Mount <vitraun-vto merchant-id={…} widget-id={…} … /> on the client only.
// subscribeVitraunVTOEvents(widget, handler) in useEffect with returned cleanup.
// await widget.open() on button click.
```

## GitHub quickstarts (ground truth)

| Stack | Repository |
|-------|------------|
| HTML + CDN | quickstart-vto-web-html-cdn |
| Vite vanilla | quickstart-vto-web-js-npm |
| React + Vite | quickstart-vto-react |
| Next.js | quickstart-vto-nextjs |
| React Native | quickstart-vto-react-native |

Full list: https://docs.vitraun.com/en-US/development/github

Before improvising APIs, **read the matching quickstart** and mirror its patterns.

## Agent workflow

1. Identify host stack (decision tree above).
2. Open the matching quickstart repository and read its README + main integration file.
3. Cross-check attributes/events against the widget API docs (see [reference.md](reference.md)).
4. Implement with env vars for keys (`merchant-id`, `widget-id`) — never commit production secrets.
5. Run the validation checklist in [reference.md](reference.md).

## Prompt template

For ad-hoc sessions outside Cursor, copy from [prompt-template.md](prompt-template.md).

## Additional reference

- Doc slugs, anti-patterns, env vars: [reference.md](reference.md)

# openseed.dev

Marketing site, documentation, and genome marketplace for [OpenSeed](https://github.com/openseed/openseed).

## Status

Planning phase. See `docs/` for design documents:

- [Brand Identity](docs/brand.md) - name, story, voice, visual direction
- [Site Plan](docs/site-plan.md) - pages, content, tech stack, phases

## Stack (planned)

- [Astro](https://astro.build) - static-first framework
- [Tailwind CSS](https://tailwindcss.com) - styling
- [Cloudflare Pages](https://pages.cloudflare.com) - hosting and edge functions
- [Cloudflare KV](https://developers.cloudflare.com/kv/) - cached data

## Development

```bash
pnpm install
pnpm dev        # localhost:4321
pnpm build      # production build
```

# Food Verse AI

Food Verse AI helps people identify food, review visible freshness and hygiene cues, get cooking guidance, and explore nutrition estimates.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required secret: `GEMINI_API_KEY` — server-side Gemini API access

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/food-verse` — web workspace and user interface
- `artifacts/api-server/src/routes/food-insights.ts` — validated food-insight API
- `artifacts/api-server/src/lib/food-insight.ts` — Gemini analysis and video-frame processing
- `lib/api-spec/openapi.yaml` — source of truth for API contracts

## Architecture decisions

- Gemini requests stay on the API server; the browser never receives the provider key.
- Uploaded images and sampled video frames are request-only and are not persisted.
- Hygiene videos are sampled into at most four compressed frames, then processed sequentially with retry and pacing.
- Recent analysis summaries are stored in the current browser only; no account or server-side history exists.

## Product

- Five modes: food identification, freshness cues, kitchen hygiene review, cooking guidance, and nutrition insights.
- Results include visible findings, suggested next steps, confidence estimates, and safety limitations.
- AI output is informational, not medical advice, inspection certification, or proof food is safe.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- Food or hygiene assessments must remain cautious: a photo or a few video frames cannot establish food safety or regulatory compliance.
- Re-run API codegen after changing `lib/api-spec/openapi.yaml`.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details

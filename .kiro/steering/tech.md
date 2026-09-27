# Tech Stack

## Frontend (`frontend/`)

| Category | Technology |
|---|---|
| Language | TypeScript ~6.0.2 |
| UI Framework | React 19 |
| Build Tool | Vite 8 |
| React Plugin | @vitejs/plugin-react (Oxc transformer) |
| Linting | ESLint 10 with typescript-eslint, eslint-plugin-react-hooks, eslint-plugin-react-refresh |
| Styling | Plain CSS with custom properties and modern CSS nesting (no Tailwind, no CSS-in-JS) |
| Module System | ESM (`"type": "module"`) |

## Backend (`backend/`)

| Category | Technology |
|---|---|
| Language | TypeScript ~7.0.2 |
| IaC Framework | AWS CDK 2 (aws-cdk-lib ^2.270.0) |
| Test Runner | Jest 30 |
| Jest Transform | @swc/jest (SWC for fast TS compilation) |
| CDK App Runner | tsx (runs `bin/backend.ts` directly) |
| Module Resolution | NodeNext |

---

## Common Commands

### Frontend

```bash
# From frontend/
npm run dev        # Start Vite dev server with HMR
npm run build      # Type-check (tsc -b) then bundle (vite build)
npm run lint       # Run ESLint across all files
npm run preview    # Serve the production build locally
```

### Backend

```bash
# From backend/
npm run build      # Type-check with tsc (noEmit)
npm run watch      # Watch mode type-check
npm run test       # Run Jest tests
npx cdk synth      # Emit CloudFormation template
npx cdk diff       # Compare stack with deployed state
npx cdk deploy     # Deploy stack to AWS
```

> The two sub-projects are independent — there is no root-level `package.json` or monorepo tooling. Run `npm install` and commands separately in each directory.

---

## TypeScript Configuration Notes

### Frontend (`tsconfig.app.json`)
- `moduleResolution: bundler` — Vite bundler mode, do not use `node` resolution imports
- `verbatimModuleSyntax: true` — type-only imports **must** use `import type`
- `erasableSyntaxOnly: true` — TypeScript enums and namespaces are **not allowed**
- `noUnusedLocals: true`, `noUnusedParameters: true` — strict enforcement
- `jsx: react-jsx` — no need to import React in JSX files

### Backend (`tsconfig.json`)
- `module: NodeNext`, `moduleResolution: NodeNext` — use `.js` extensions in relative imports
- `strict: true` with `noImplicitAny`, `strictNullChecks`, `noImplicitReturns`
- `experimentalDecorators: true` — CDK decorator support enabled

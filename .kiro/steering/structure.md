# Project Structure

The workspace is a two-package monorepo with no shared root tooling. Each sub-project has its own `package.json`, `node_modules`, and TypeScript config.

```
KFV/
├── frontend/                   # React SPA (Vite + TypeScript)
│   ├── src/
│   │   ├── main.tsx            # App entry point (ReactDOM.createRoot)
│   │   ├── App.tsx             # Root component
│   │   ├── App.css             # Component-scoped styles
│   │   ├── index.css           # Global CSS variables and base styles
│   │   └── assets/             # Static assets imported as ES modules
│   ├── public/
│   │   ├── favicon.svg
│   │   └── icons.svg           # SVG sprite sheet (referenced via <use href="...">)
│   ├── index.html              # HTML shell
│   ├── vite.config.ts          # Vite configuration
│   ├── eslint.config.js        # ESLint flat config
│   ├── tsconfig.json           # References tsconfig.app.json + tsconfig.node.json
│   ├── tsconfig.app.json       # Src TypeScript config (bundler mode)
│   ├── tsconfig.node.json      # Config for Vite/Node tooling files
│   └── package.json
│
└── backend/                    # AWS CDK infrastructure (TypeScript)
    ├── bin/
    │   └── backend.ts          # CDK App entry point — instantiates stacks
    ├── lib/
    │   └── backend-stack.ts    # Primary CDK stack definition
    ├── test/
    │   └── backend.test.ts     # Jest tests for CDK stacks
    ├── cdk.json                # CDK app command, feature flags, watch config
    ├── jest.config.js          # Jest config (SWC transform, node environment)
    ├── tsconfig.json           # Backend TypeScript config (NodeNext)
    └── package.json
```

## Conventions

- **Frontend components** live in `src/`. New components should be placed under `src/components/` when that directory is created.
- **New CDK stacks** are defined in `backend/lib/` and instantiated in `backend/bin/backend.ts`.
- **CDK constructs or helpers** should be organized into subdirectories under `backend/lib/` as the stack grows.
- **Static public assets** (served as-is) go in `frontend/public/`. Assets that are imported by components go in `frontend/src/assets/`.
- **CSS**: Global tokens and base styles belong in `index.css`. Component-specific styles go in a co-located `.css` file (e.g., `App.css` alongside `App.tsx`).
- No path aliases are configured — use relative imports in frontend source files.

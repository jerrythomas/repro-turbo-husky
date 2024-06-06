# internal errors encountered: receiver dropped [pre-commit] [husky]

git commit -m "chore: create repro for husky turbo"

> my-turborepo@ lint /Users/Jerry/Code/Vikalp/repro-turbo-husky
> turbo run lint

• Packages in scope: app-a, app-b, pkg-a, pkg-b, tooling-config
• Running lint in 5 packages
• Remote caching disabled
  × internal errors encountered: receiver dropped,receiver dropped,receiver dropped

 ELIFECYCLE  Command failed with exit code 1.
husky - pre-commit script failed (code 1)

## Steps to reproduce

```bash
npx create-turbo@latest -e with-shell-commands

pnpm i
```

modify package.json to add script

```json
script {
  "lint": "turbo run lint"
}
```

install husky

```bash
pnpm i --save-dev husky -w
pnpx husky init
```

modify ./husky/pre-commit

```
pnpm lint
```

Add changed files and try to commit

```bash
git add .
git commit -m "This will fail"
```

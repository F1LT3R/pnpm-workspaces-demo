# PNPM Workspaces Demo

This Repo demonstrates a Monorepo workspaces setup with [PNPM](https://pnpm.js.org/en/workspaces). 


##  Tree

```plain
❯ tree
.
├── package.json
├── packages
│   ├── apps
│   │   └── demo
│   │       ├── node_modules
│   │       │   └── @demo
│   │       │       ├── test -> ../../../../libs/demo/test
│   │       │       └── test2 -> ../../../../libs/demo/test2
│   │       ├── package.json
│   │       └── src
│   │           ├── index.js
│   │           └── pages
│   └── libs
│       └── demo
│           ├── test
│           │   ├── package.json
│           │   └── src
│           │       └── index.js
│           └── test2
│               ├── package.json
│               └── src
│                   └── index.js
└── pnpm-workspace.yaml
```

## The Setup

.npmrc

```
link-workspace-packages = true
shared-workspace-shrinkwrap = true
```

pnpm-workspace.yaml

```yaml
packages:
    - '**'
```



```shell
❯ pnpm install -r

Scope: all 4 workspace projects
Lockfile is up-to-date, resolution step is skipped
Already up-to-date
```

## Workspaces List

The command:

```shell
pnpm list -r --json
```

Yields:

```json
[
  {
    "name": "@demo/workspaces"
  },
  {
    "name": "@app/demo",
    "dependencies": {
      "@demo/test": {
        "from": "@demo/test",
        "version": "link:../../libs/demo/test"
      },
      "@demo/test2": {
        "from": "@demo/test2",
        "version": "link:../../libs/demo/test2"
      }
    }
  },
  {
    "name": "@demo/test",
    "version": "0.1.0"
  },
  {
    "name": "@demo/test2",
    "version": "0.1.0"
  }
]
```

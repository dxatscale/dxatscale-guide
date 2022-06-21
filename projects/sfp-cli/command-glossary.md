# Command Glossary

* [`sfp init`](https://github.com/Accenture/sfpowerscripts/tree/develop/packages/sfp-cli#sfp-init-caller-mode)
* [`sfp org`](https://github.com/Accenture/sfpowerscripts/tree/develop/packages/sfp-cli#sfp-org)
* [`sfp package`](https://github.com/Accenture/sfpowerscripts/tree/develop/packages/sfp-cli#sfp-package)
* [`sfp sync`](https://github.com/Accenture/sfpowerscripts/tree/develop/packages/sfp-cli#sfp-sync)
* [`sfp work`](https://github.com/Accenture/sfpowerscripts/tree/develop/packages/sfp-cli#sfp-work)

### `sfp init`

Intializes the project settings:

* Default branch
* DevHub
* Repo provider

**Needs to be run at least once per project, as other commands depend on the project settings.**

```
USAGE
  $ sfp init
```

_See code:_ [_src/commands/init.ts_](https://github.com/dxatscale/sfp-cli/blob/v0.0.38/src/commands/init.ts)

### `sfp org`

Guided workflows for working with developer orgs, such as opening, creating and deleting an org.

```
USAGE
  $ sfp org
```

_See code:_ [_src/commands/org.ts_](https://github.com/dxatscale/sfp-cli/blob/v0.0.38/src/commands/org.ts)

### `sfp package`

Helpful utilities for dealing with packages in your project:

* Managing package versions and dependency versions
* Create a new package

```
USAGE
  $ sfp package
```

_See code:_ [_src/commands/package.ts_](https://github.com/dxatscale/sfp-cli/blob/v0.0.38/src/commands/package.ts)

### `sfp sync`

Sync changes effortlessly between source repository and development environment

```
USAGE
  $ sfp sync
```

_See code:_ [_src/commands/sync.ts_](https://github.com/dxatscale/sfp-cli/blob/v0.0.38/src/commands/sync.ts)

### `sfp work`

Operations for working with work items:

* Create a new work item
* Switch to an existing work item
* Submit a work item
* Delete a work item

```
USAGE
  $ sfp work
```

_See code:_ [_src/commands/work.ts_](https://github.com/dxatscale/sfp-cli/blob/v0.0.38/src/commands/work.ts)

# Angular CDK missing Forms peer dependency reproduction

This repository reproduces the undeclared runtime dependency from
`@angular/cdk/stepper` to `@angular/forms` using pnpm's isolated dependency
layout.

```bash
pnpm install
pnpm reproduce
```

The bundle fails because `@angular/cdk/stepper` imports `ControlContainer`
from `@angular/forms`, but `@angular/forms` is not declared in the CDK package
metadata.

Installing Forms makes the same command succeed:

```bash
pnpm add @angular/forms@22.0.6
pnpm reproduce
```

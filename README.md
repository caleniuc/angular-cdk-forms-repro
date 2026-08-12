# Angular CDK missing Forms peer dependency reproduction

This repository reproduces the undeclared runtime dependency from
`@angular/cdk/stepper` to `@angular/forms` when pnpm's global virtual store is
enabled. Forms is installed directly by the application, but CDK cannot access
it because CDK does not declare it in its own package metadata.

```bash
pnpm install
pnpm reproduce
```

The bundle fails because `@angular/cdk/stepper` imports `ControlContainer`
from `@angular/forms`, but `@angular/forms` is not declared in the CDK package
metadata. With the project-local virtual store, this can be masked by accidental
access to the application's root dependency.

Adding the missing package extension makes the same command succeed:

```yaml
packageExtensions:
  '@angular/cdk@22.0.4':
    peerDependencies:
      '@angular/forms': 22.0.6
```

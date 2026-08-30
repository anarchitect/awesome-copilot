---
name: nodejs-modernization
description: 'Assess and modernize legacy Node.js applications through runtime, dependency, module-system, code, testing, and deployment upgrades.'
---

# Node.js Modernization

Use this skill to create and execute a safe, evidence-based modernization plan
for an existing Node.js application. It covers runtime upgrades, package
management, dependency compatibility, module-system migration, code updates,
tests, CI, containers, and deployment.

## When to Use This Skill

Use this skill when you need to:
- upgrade an application from an unsupported Node.js release to a supported LTS release;
- replace deprecated APIs or unmaintained dependencies;
- migrate CommonJS code toward ESM without breaking consumers or tooling;
- modernize an older JavaScript service's tests, build, CI, or deployment runtime.

## Workflow

### 1. Establish the baseline

Read `package.json`, the active lockfile, Node version files, CI workflows,
containers, deployment descriptors, and test configuration. Record the package
manager, supported Node.js versions, scripts, module type, frameworks, native
modules, and externally consumed package or service contracts.

### 2. Identify modernization risks

Check for end-of-life Node.js versions, unsupported dependencies, deprecated
APIs, CommonJS/ESM interop, peer dependency constraints, native addons, and
runtime-version drift across local development, CI, containers, and production.
Use verified project commands and vendor release notes; label uncertainty rather
than guessing.

### 3. Plan incremental upgrades

Choose a target supported LTS release compatible with hosting and dependencies.
Order changes so every phase remains buildable and testable:

1. Align runtime pins and package-manager requirements.
2. Upgrade direct dependencies and resolve peer dependency constraints.
3. Replace deprecated APIs and make focused code changes.
4. Migrate module boundaries only after verifying consumers and tooling.
5. Align CI, containers, and deployment configuration.

Include a rollback point and validation criteria for every phase.

### 4. Implement and validate

Use the repository's existing package manager to install dependencies and update
lockfiles. Do not edit lockfiles manually. After each phase, run the applicable
install, lint, typecheck, test, build, and smoke-test scripts. Update CI and
deployment configuration only after application validation passes.

## Guidelines

1. **Use configuration as evidence** - Determine runtime and package-manager
   choices from the repository and its deployment surface.
2. **Preserve compatibility deliberately** - Treat public APIs, environment
   variables, database behavior, and module exports as contracts.
3. **Keep ESM migration incremental** - Verify package `type`, exports,
   consumers, test runners, build tools, and dynamic loading before conversion.
4. **Prefer the platform responsibly** - Adopt built-in Node.js APIs when they
   meet the need and do not introduce behavior changes.

## Limitations

- This skill does not select a target release without repository and deployment
  evidence.
- Major framework, package-manager, or module-system changes may require a
  separately approved compatibility plan.
- A successful build does not replace integration, performance, or production
  rollout validation.

---
name: 'Node.js Modernization Guidelines'
description: 'Guidance for safely modernizing legacy Node.js and JavaScript applications.'
applyTo: '**/*.js, **/*.mjs, **/*.cjs, **/*.ts, **/package.json, **/package-lock.json, **/npm-shrinkwrap.json, **/yarn.lock, **/pnpm-lock.yaml, **/.nvmrc, **/.node-version, **/Dockerfile, **/Containerfile'
---

# Node.js Modernization Guidelines

## Discovery and planning

- Inspect manifests, lockfiles, runtime version files, CI workflows, containers, and deployment descriptors before proposing a target runtime.
- Use a supported Node.js LTS version compatible with the application's framework, deployment platform, and native dependencies.
- Plan changes in independently verifiable phases: runtime and tooling, dependencies, module system, application code, then deployment and CI.
- Preserve backward compatibility at public boundaries unless a breaking change is explicitly requested.

## Runtime and dependencies

- Keep `package.json` `engines`, local version files, CI setup, container base images, and deployment runtimes aligned.
- Use the repository's existing package manager and regenerate lockfiles with it; do not hand-edit generated lockfiles.
- Review changelogs and peer dependency requirements before major package upgrades.
- Prefer maintained packages and built-in Node.js APIs when they provide the required capability without weakening behavior or security.
- Remove dependencies only after confirming they have no production, development, generated-code, or transitive usage requirement.

## Code and module systems

- Prefer `async`/`await` and ensure errors and promise rejections remain handled at process and request boundaries.
- Migrate CommonJS and ESM incrementally. Verify imports, exports, dynamic loading, test tooling, build tooling, and downstream consumers before changing module type.
- Use `node:` specifiers for Node.js built-in modules in newly modified imports.
- Avoid relying on deprecated Node.js APIs or undocumented runtime behavior.
- Validate and constrain data crossing HTTP, file-system, process, database, and message boundaries.

## Validation

- Run the existing install, lint, typecheck, test, build, and smoke-test commands applicable to each change.
- Test supported Node.js versions where the repository supports more than one.
- Update CI and deployment configuration only after application validation succeeds.
- Document runtime requirements, breaking changes, rollout steps, and rollback criteria for externally visible upgrades.

# Coding and Git Standards

| Field | Value |
|-------|-------|
| **Standard ID** | STD-MERGED-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead / CI Pipeline |
| **Verification Method** | Code Review, Linter, Branch Protection, commit-lint |
| **Last Updated** | 2026-03-05 |

---

## 1. Purpose

This standard defines the coding conventions, Git workflow, branching strategy, and commit message format used across all projects. It consolidates rules from coding standards (STD-P5-001), the Git workflow standard (STD-P5-002), the branching strategy quick-reference (QR-P5-002), and the conventional commits reference (REF-P5-002) into a single operational document. All engineers are expected to follow these rules; CI pipelines and code review enforce compliance.

---

## 2. Coding Standards

### 2.1 Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Files | kebab-case | `rental-service.ts` |
| Classes | PascalCase | `RentalService` |
| Interfaces | PascalCase | `PaymentGateway` |
| Functions / Methods | camelCase | `calculateLateFee` |
| Variables | camelCase | `rentalAgreement` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_RETRY_ATTEMPTS` |
| Enums | PascalCase name, SCREAMING_SNAKE_CASE values | `RentalStatus.ACTIVE` |
| Booleans | is/has/can/should prefix | `isOverdue`, `hasLateFee` |
| Private fields | underscore or `#` prefix | `_repository`, `#cache` |

### 2.2 Formatting

- **Indentation:** 2 spaces (Prettier/ESLint auto-fix).
- **Line length:** 100 characters max.
- **Semicolons:** required.
- **Quotes:** single quotes.
- **Trailing commas:** required in multiline objects/arrays.
- **Braces:** same line (K&R style).

### 2.3 TypeScript Strictness

Enable all of the following in `tsconfig.json`:

```
strict: true
noImplicitAny: true
strictNullChecks: true
noUnusedLocals: true
noUnusedParameters: true
```

### 2.4 Import Ordering

1. Node.js built-ins
2. External packages
3. Internal modules (absolute paths)
4. Local modules (relative paths)

### 2.5 Error Handling

- Use specific error types with meaningful messages.
- Re-throw known errors; wrap unknown errors with context.
- Never leave an empty catch block.
- Log unknown errors with structured context before wrapping.

### 2.6 Async Patterns

- Use `async/await`; avoid raw `.then()` chains.
- Use `Promise.all()` for independent parallel operations.

### 2.7 Environment Variables

- Name with SCREAMING_SNAKE_CASE (`DATABASE_URL`, `MQTT_BROKER_HOST`).
- `.env` never committed; `.env.example` committed with placeholders.
- Read env vars at startup; inject into a config module.
- Never log, expose in API responses, or include secrets in error messages.

### 2.8 Logging

| Level | Use For |
|-------|---------|
| ERROR | Operation failed, requires attention |
| WARN | Unexpected but recoverable |
| INFO | Significant business events only |
| DEBUG | Detailed diagnostics |

- Use structured logging with context objects (no string concatenation).
- Never log passwords, tokens, credit cards, full PII, or secrets.

### 2.9 Security Practices

- Validate all external inputs at the controller/boundary.
- Use parameterized queries; never concatenate user input into SQL.
- Sanitize user-generated content before HTML rendering.
- Run `npm audit` weekly; fix critical/high vulnerabilities immediately.
- Use environment variables for secrets; never hardcode.
- Verify JWT on every authenticated endpoint; check expiry.
- Check user role server-side; never trust client-side claims.

### 2.10 Dependency Management

- Justify new dependencies in the PR description.
- Pin exact versions in `package.json` (no `^` or `~`) for production deps.
- Run `npm audit` in CI; fail the build on critical vulnerabilities.
- Allowed licenses: MIT, Apache 2.0, BSD, ISC. GPL requires legal review.

---

## 3. Git Workflow

### 3.1 Branching Model

| Branch | Purpose | Source | Merges Into |
|--------|---------|--------|-------------|
| `main` | Production-ready, always deployable | -- | -- |
| `develop` | Integration branch for all feature work | -- | -- |
| `feature/*` | New functionality | `develop` | `develop` |
| `bugfix/*` | Non-urgent fixes | `develop` | `develop` |
| `hotfix/*` | Urgent production fixes | `main` | `main` + `develop` |
| `release/*` | Release preparation | `develop` | `main` + `develop` |
| `refactor/*` | Technical-debt work | `develop` | `develop` |

### 3.2 Pull Request Process

1. **Title** must follow conventional commit format (see [Section 5](#5-conventional-commits)).
2. **Description** must include: what changed, why, how, and a link to the ticket.
3. **Type of change** specified (Feature / Bug fix / Refactor / Docs).
4. **Screenshots** required for UI changes.
5. **Test evidence** included.
6. **PR checklist** completed.
7. Use the [Pull Request Template](../templates/pull-request.md).

### 3.3 Merge Strategy

| Scenario | Strategy | Rationale |
|----------|----------|-----------|
| `feature/*` or `bugfix/*` to `develop` | Squash merge | Clean, linear history |
| `release/*` to `main` | Merge commit | Preserves release boundary |
| `hotfix/*` to `main` + `develop` | Merge commit | Preserves hotfix history |
| `main` back to `develop` after release/hotfix | Merge commit | Retains full history |

### 3.4 Protected Branches

| Branch | Requirements |
|--------|-------------|
| `main` | PR required, 2 approvals, CI pass, no force push, no direct commits |
| `develop` | PR required, 1 approval, CI pass, no force push |

### 3.5 Release Tagging (SemVer)

| Version Part | Trigger | Example |
|-------------|---------|---------|
| Major (X.0.0) | Breaking API changes, incompatible migrations | 1.0.0 -> 2.0.0 |
| Minor (0.X.0) | New features, backward-compatible | 1.0.0 -> 1.1.0 |
| Patch (0.0.X) | Bug fixes, backward-compatible | 1.0.0 -> 1.0.1 |

Tag format: `vX.Y.Z` (e.g., `v1.2.3`).

### 3.6 Conflict Resolution

- Pull latest `develop` into your feature branch before opening a PR.
- Resolve conflicts locally; run tests after resolution.
- Consult the original author if conflict resolution is ambiguous.

---

## 4. Branching Strategy

### 4.1 Branch Naming

| Branch Type | Pattern | Example |
|-------------|---------|---------|
| Feature | `feature/TICKET-NNN-short-description` | `feature/TICKET-123-late-fee-calc` |
| Bugfix | `bugfix/TICKET-NNN-short-description` | `bugfix/TICKET-456-fix-rounding` |
| Hotfix | `hotfix/TICKET-NNN-short-description` | `hotfix/TICKET-789-critical-payment-fix` |
| Release | `release/X.Y.Z` | `release/1.2.0` |
| Refactor | `refactor/TD-NNN-short-description` | `refactor/TD-001-optimize-rental-query` |

### 4.2 Naming Rules

- Lowercase only; hyphens to separate words.
- Always include the ticket number.
- Keep descriptions to 3-5 words.
- No personal names, dates, spaces, underscores, or dots.

### 4.3 Branch Lifecycle

1. Pull latest from the parent branch before creating a new branch.
2. Keep feature branches short-lived (days, not weeks).
3. Never commit directly to `main` or `develop`.
4. Never rebase a shared branch.
5. Delete merged branches immediately after merge.

### 4.4 Keeping Branches in Sync

| Situation | Action | Avoid |
|-----------|--------|-------|
| `develop` ahead of your **unshared** feature branch | `git rebase origin/develop` | Merging (creates noise) |
| `develop` ahead of a **shared** branch | `git merge origin/develop` | Rebasing (rewrites shared history) |

### 4.5 Hotfix Process

1. Branch from `main`.
2. Fix with minimal changes.
3. PR to `main`; expedited review.
4. After merge, PR `main` into `develop`.
5. Tag release on `main` (patch version bump).

---

## 5. Conventional Commits

Conventional commits drive automated changelogs, SemVer bumps, and readable history. Every commit and PR title must conform to this format.

### 5.1 Commit Format

```
<type>(<scope>): <description> [CU-xxxx]

[optional body]

[optional footer(s)]
```

- **type** -- one of the types listed below.
- **scope** -- the component or phase area affected.
- **description** -- imperative, present tense, lowercase start, no period, max 72 chars.
- **[CU-xxxx]** -- ClickUp task ID linking the commit to a tracked work item.

### 5.2 Type Reference

| Type | When to Use | Version Bump |
|------|-------------|-------------|
| `feat` | New feature or capability | Minor (1.x.0) |
| `fix` | Bug fix | Patch (1.0.x) |
| `docs` | Documentation only | None |
| `style` | Formatting, whitespace (no logic change) | None |
| `refactor` | Restructure code without behavior change | None |
| `test` | Adding or updating tests | None |
| `chore` | Build, tooling, deps, maintenance | None |
| `ci` | CI/CD configuration changes | None |
| `perf` | Performance improvement | Patch (1.0.x) |
| `build` | Build system or external dependency changes | None |
| `revert` | Reverts a previous commit | Depends |

### 5.3 Scopes

Scope equals the component or phase area the change touches:

| Scope | Area |
|-------|------|
| `billing` | Invoicing, payments, fees |
| `rentals` | Rental agreements, lifecycle |
| `fleet` | Equipment, maintenance |
| `customers` | Customer management |
| `auth` | Authentication and authorization |
| `iot` | IoT telemetry, MQTT |
| `api` | General API changes |
| `db` | Database migrations, schema |
| `deps` | Dependency updates |
| `config` | Configuration changes |
| `define` | SDLC Define phase artifacts |
| `design` | SDLC Design phase artifacts |
| `develop` | SDLC Develop phase artifacts |

If a change spans multiple scopes equally, use the primary scope or omit scope entirely.

### 5.4 Breaking Changes

Two conventions (both bump **major** version X.0.0):

**Exclamation mark after type:**

```
feat(api)!: change rental response format [CU-2200]
```

**BREAKING CHANGE footer:**

```
feat(api): change rental response format [CU-2200]

BREAKING CHANGE: All response fields now use snake_case instead of camelCase.
Clients must update field mappings before upgrading.
```

### 5.5 SDLC Phase Examples

| Phase | Example Commit |
|-------|---------------|
| Define | `docs(define): add BRD for Power Atlas [CU-1234]` |
| Design | `docs(design): publish API contract for billing service [CU-1300]` |
| Develop | `feat(billing): add late fee calculation [CU-1456]` |
| Develop (fix) | `fix(rentals): correct rounding in daily rate [CU-1460]` |
| Develop (refactor) | `refactor(fleet): extract maintenance scheduler [CU-1500]` |
| Test | `test(billing): add edge case for zero-day fee [CU-1510]` |
| Deploy | `ci: add staging deploy step to pipeline [CU-1600]` |
| Operate | `chore(config): rotate database credentials [CU-1700]` |

### 5.6 PR Title Convention

Every PR title **must** follow the conventional commit format:

```
feat(billing): add late fee calculation [CU-1456]
fix(rentals): correct rounding in daily rate [CU-1460]
docs(define): add BRD for Power Atlas [CU-1234]
```

This is enforced by a PR title check in CI. PRs with non-conforming titles are rejected automatically.

### 5.7 Enforcement

| Mechanism | Where | What It Checks |
|-----------|-------|---------------|
| **commit-lint** | Git hook (local) | Commit message format, type, scope, length |
| **PR title check** | CI pipeline | PR title matches `type(scope): description` pattern |
| **Code review** | Pull request | Body explains rationale; ticket referenced in footer |

### 5.8 Common Mistakes

| Mistake | Problem | Correct |
|---------|---------|---------|
| `Fixed the bug` | Past tense, no type/scope | `fix(billing): correct rounding error [CU-1234]` |
| `feat: stuff` | Vague description | `feat(billing): add late fee calculation [CU-1234]` |
| `feat(billing): Add Late Fee.` | Capital letter, trailing period | `feat(billing): add late fee [CU-1234]` |
| `update code` | No type, vague | `refactor(rentals): simplify status check [CU-1234]` |
| `WIP` | Not a valid commit message | Do not commit WIP; use branches |

---

## Cross-References

| Document | Type | Link |
|----------|------|------|
| Pull Request Template | Template | [../templates/pull-request.md](../templates/pull-request.md) |
| Code Review Checklist | Template | [../templates/code-review-checklist.md](../templates/code-review-checklist.md) |
| Implement Feature | Runbook | [../runbooks/implement-feature.md](../runbooks/implement-feature.md) |
| Code Review Standard | Standard | [code-review.md](code-review.md) |
| Phase 3: Build & Verify | Phase | [../phases/3-build-and-verify.md](../phases/3-build-and-verify.md) |

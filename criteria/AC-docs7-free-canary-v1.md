---
sdd:
  version: 1
  class: privileged
  mode: integration
  reasons:
    - cross_system
    - published_contract
    - provider_mutation
  base: "4b825dc642cb6eb9a060e54bf8d69288fbee4904"
  acceptance:
    - AC-D7-1
    - AC-D7-2
    - AC-D7-3
    - AC-D7-4
    - AC-D7-5
  authority:
    implementation: granted
    publication: granted
    runtime: granted
---

# Criteria: Docs7 Free canary

## Outcome

A separate public repository publishes a two-page VetClub documentation canary
with Docs7 Free: a public technical introduction and a sanitized catalog of 25
baseline skills plus 52 optional, task-specific Vercel skills. The repository
itself is the positive publication allowlist.

## Producer and consumer identity

- Producer: the public Git repository `Pet-dog/vetclub-docs`, production branch
  `main`, Docs7 path `docs`.
- Consumer: Docs7 Free hosted site on its generated `*.docs7.io` hostname.
- Source material: public-safe summaries derived from the current VetClub
  skills catalog; no skill bodies, live synchronization, or repository link to
  a private source.

## Versions and contract

- Docs7 CLI: `@upstash/docs7@0.1.0`, pinned for the local proof.
- Node.js: `>=20.19` as required by that release.
- Hosted tier: Free only.
- Published pages: `index` and `skills` only.

## ADDED

- One isolated public documentation repository.
- One Docs7 configuration, two MDX pages, and one explicit crawler policy.
- A sanitized catalog containing names and public summaries for exactly 77
  unique skills: 25 baseline skills and 52 optional Vercel skills.

## MODIFIED

- Nothing in existing VetClub repositories, deployments, domains, or previews.

## REMOVED

- Nothing.

## UNCHANGED

- Canonical policy, private repositories, private documentation, Vault and
  Notion remain outside Docs7.
- Vercel/GitHub remain the documentation-PR preview path.
- No custom-domain or DNS cutover.

## Retries, timeouts and idempotency

- Repository and site creation use stable names and are checked before create;
  an existing object is reused only when its identity and public-only contents
  match this contract.
- One corrective pass is allowed only after a concrete failed build or content
  check.
- Re-running the same local preview on unchanged bytes is prohibited.

## Partial failures

- If the local renderer cannot build both pages, do not publish.
- If GitHub repository creation succeeds but Docs7 publication fails, keep the
  repository public and report the site as not published; do not connect a
  private repository as a fallback.
- If any forbidden material appears on any agent-readable endpoint, remove the
  Docs7 site immediately and treat the canary as failed.

## Compatibility and rollback

- The canary uses the generated Docs7 hostname and does not replace an existing
  documentation URL.
- Rollback removes the Docs7 site. If Context7 indexing was ever enabled, its
  library must be removed separately; disconnecting alone is insufficient.
- The GitHub App is scoped to `Pet-dog/vetclub-docs` only and can be revoked
  without affecting private repositories.

## Acceptance criteria

- **AC-D7-1.** The public Git tree contains only `README.md`, this criteria
  file, `docs/docs.json`, `docs/index.mdx`, `docs/skills.mdx`, and
  `docs/robots.txt`; every item is intentionally public and no symlink exists.
- **AC-D7-2.** The pinned Docs7 CLI starts a local preview from `docs`, and both
  `/` and `/skills` return successful HTML responses with their expected
  headings.
- **AC-D7-3.** The catalog page contains exactly 77 unique skill names: 25
  baseline skills and 52 Vercel skills explicitly labeled optional and
  task-specific. It exposes no local path, source coordinate, digest, secret,
  customer or patient data, private URL, internal policy text, or private
  source file.
- **AC-D7-4.** The hosted canary uses Docs7 Free on `*.docs7.io`; Pro, custom
  domain, DNS changes, autonomous Agent, PR Review, schedule, and Context7
  indexing are not enabled.
- **AC-D7-5.** After publication, `/`, `/skills`, `/index.md`,
  `/skills.md`, `/llms.txt`, and `/llms-full.txt` are readable and contain
  only the two allowlisted pages; the previous Vercel/GitHub preview path is
  unchanged.

## Out of scope

- Migrating canonical policy, Vault, Notion, private materials, private
  repositories, source code, API references, secrets, or operational runbooks.
- Buying Docs7 Pro or reproducing its Agent/PR features.
- Automatic synchronization from a private repository.
- Custom domain, SEO migration, or replacing the current preview stack.

## Preserved behavior

All existing repositories, deployments, domains, previews, and documentation
workflows continue unchanged.

## Errors and failure states

Any repository-scope expansion, unexpected tracked file, page outside the two
declared routes, paid-plan requirement, or exposure of a forbidden content
class is a stop condition, not a reason to weaken the boundary.

## What would show this decision is wrong

The canary is rejected if Docs7 Free cannot host the two pages without granting
the service access to a private repository, or if its public agent-readable
surfaces cannot be kept equal to this repository's explicit public tree.

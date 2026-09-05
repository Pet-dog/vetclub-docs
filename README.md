# VetClub public docs canary

This repository is the complete publication boundary for the VetClub Docs7
Free canary. Everything tracked here is intentionally public.

The canary contains only:

- a short public technical introduction;
- a sanitized catalog of the 25 baseline agent skills;
- Docs7 navigation and crawler metadata.

It does not mirror or connect to private VetClub repositories. Canonical
policy, private documentation, source code, Vault, Notion, credentials,
customer data and operational material stay outside this repository.

## Local preview

Node.js 20.19 or newer is required.

```bash
npx @upstash/docs7@0.1.0 dev ./docs
```

Hosted canary settings:

- plan: Docs7 Free;
- production branch: `main`;
- docs path: `docs`;
- hostname: generated `*.docs7.io` only;
- Context7 indexing, autonomous Agent, PR Review and schedules: disabled;
- custom domain and DNS changes: not used.

Acceptance criteria live in
[`criteria/AC-docs7-free-canary-v1.md`](criteria/AC-docs7-free-canary-v1.md).

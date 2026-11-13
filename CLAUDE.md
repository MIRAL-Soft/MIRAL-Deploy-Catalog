<!-- Copied from: miralsoft-foundation-docs, projects/miral-deploy/entrypoints-for-code-repos/CLAUDE.catalog.md -->
<!-- Foundation version: 5.2.2, copied on 2026-11-13 -->

# Entrypoint: MIRAL-Deploy-Catalog

You are working on `MIRAL-Deploy-Catalog`, the package and profile data of MIRAL Deploy, its CI
checks and its signing and publishing step. No program code lives here; that is `MIRAL-Deploy`.

This repository is public. It documents only what somebody using the catalog needs to know (the
README). Everything else is the project documentation in the foundation at
`projects/miral-deploy/` (M-12, hosted).

## Before doing anything

Clone the foundation into `.foundation-docs/`, exclude it through `.git/info/exclude`, pull it at
the start of every session, and read `rules/_meta.md`, every file in `rules/`, then
`projects/miral-deploy/` (memory files first, then `project.md`, `architecture.md`,
`rules-project.md`).

## While working

- Never add signing keys or any other secret here (S-02). The private key exists only in the
  protected signing environment or with the owner.
- No customer data and no confidential customer profiles in this public repository.
- Every change reaches `main` through a pull request with the required checks (R-16).
- Update `projects/miral-deploy/status.md` at the end of every session (M-08, M-18 exception).
- Install the foundation hooks. An AI is never named as author or co-author (R-09, I-06).
- Ask before any push or pull request that starts CI (R-22).

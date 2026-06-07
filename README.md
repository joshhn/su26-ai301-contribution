# Contribution #1: Add issue template

**Contribution Number:** 1
**Student:** @joshhn
**Issue:** https://github.com/trinodb/trino-gateway/issues/992
**Status:** Phase I Complete

---

## Why I Chose This Issue

I chose [trinodb/trino-gateway#992 — "Add issue template"](https://github.com/trinodb/trino-gateway/issues/992) because it is a `good first issue` that is genuinely well-scoped: the goal is to add GitHub issue templates to the `trino-gateway` repository by adapting the existing templates from the main [Trino repo](https://github.com/trinodb/trino/tree/master/.github/ISSUE_TEMPLATE). It was opened by an active maintainer (`@ebyhr`), is currently unassigned, has no competing pull requests, and the "definition of done" is unambiguous — that gives me a high-confidence first contribution to a real, widely-used open-source project.

It also matches my skills and learning goals. trino-gateway is a large Java project (a load balancer / routing gateway for Trino clusters), but *this particular task* lives entirely in GitHub configuration: YAML-based issue forms under `.github/ISSUE_TEMPLATE/`. That means I can make a meaningful, maintainer-visible contribution without needing to fully build the Java codebase, while still learning the project's contribution workflow (CONTRIBUTING.md, fork → branch → PR, maintainer review). I want to learn how GitHub's [issue forms schema](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) works and how an established project structures contributor onboarding — this issue teaches both.

---

## Understanding the Issue

### Problem Description

The `trino-gateway` repository has no GitHub issue templates. When someone opens a new issue, they get a blank text box instead of a structured form, so bug reports and feature requests arrive with inconsistent or missing information (version, environment, reproduction steps, etc.). The issue asks us to add issue templates, reusing and adapting the ones already maintained in the main Trino repository.

### Expected Behavior

When a user clicks "New Issue" on `trino-gateway`, they should be presented with a chooser offering structured templates (at minimum a **Bug report** and a **Feature request**), each prompting for the relevant details — mirroring the experience in the main `trinodb/trino` repo but adapted to gateway-specific terminology (clusters, routing, gateway version, etc.).

### Current Behavior

`.github/ISSUE_TEMPLATE/` does not exist. "New Issue" opens an empty editor with no template selection screen, so issue quality depends entirely on the reporter.

### Affected Components

- **`.github/ISSUE_TEMPLATE/`** — new directory to be created in the `trino-gateway` repo.
  - `bug_report.yml` — adapted from Trino's bug report form.
  - `feature_request.yml` — adapted from Trino's feature request form.
  - `config.yml` — issue-chooser configuration (e.g. links to Slack/discussions, `blank_issues_enabled` setting).
- **Reference source:** [`trinodb/trino/.github/ISSUE_TEMPLATE/`](https://github.com/trinodb/trino/tree/master/.github/ISSUE_TEMPLATE) (`bug_report.yml`, `feature_request.yml`, `config.yml`).
- **For consistency review:** the existing [`.github/pull_request_template.md`](https://github.com/trinodb/trino-gateway/blob/main/.github/pull_request_template.md) and [`.github/CONTRIBUTING.md`](https://github.com/trinodb/trino-gateway/blob/main/.github/CONTRIBUTING.md) in trino-gateway.

---

## Reproduction Process

> Note: this is a *task / enhancement*, not a bug, so "reproduction" here means confirming the gap rather than triggering a defect.

### Environment Setup

*To be completed in Phase II.* Because the deliverable is YAML configuration under `.github/`, no full Java/Maven build of trino-gateway is strictly required to author and validate the templates. I will still skim `.github/CONTRIBUTING.md` for any contribution requirements (commit message format, DCO/sign-off, etc.).

### Steps to Reproduce (confirm the gap)

1. Open https://github.com/trinodb/trino-gateway and browse to `.github/`.
2. Observe there is **no** `ISSUE_TEMPLATE/` directory (only `CONTRIBUTING.md`, `pull_request_template.md`, `dependabot.yml`, `bin/`, `workflows/`).
3. On the repo, click **Issues → New issue** — a blank editor appears with no template chooser.

### Reproduction Evidence

- **Commit showing reproduction:** *N/A for a missing-feature task — gap confirmed by inspecting the live repo (see steps above).*
- **Screenshots/logs:** *To be added in Phase II (screenshot of the blank "New issue" screen vs. the Trino repo's template chooser).*
- **My findings:** trino-gateway already has a PR template and CONTRIBUTING guide but no issue templates, confirming the issue is valid and unaddressed. The main Trino repo provides three ready-made forms to adapt.

---

## Solution Approach

### Analysis

The root "cause" is simply that issue templates were never added to trino-gateway. The fix is additive (new config files) with essentially zero risk to runtime code. The main work is *adaptation*: copying Trino's forms and editing field labels, descriptions, dropdown options, and links so they make sense for the gateway (e.g. "Trino version" → gateway version + backend Trino version; routing/cluster context fields; correct community links).

### Proposed Solution

Create `.github/ISSUE_TEMPLATE/` in trino-gateway with:
1. `bug_report.yml` — structured bug form adapted from Trino's.
2. `feature_request.yml` — structured feature form adapted from Trino's.
3. `config.yml` — chooser config (decide `blank_issues_enabled`, add contact links e.g. Slack / GitHub Discussions consistent with what trino-gateway uses).

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** trino-gateway lacks `.github/ISSUE_TEMPLATE/`; add issue templates by reusing/adapting the main Trino repo's templates.

**Match:** Trino's existing `bug_report.yml`, `feature_request.yml`, and `config.yml` are the direct pattern to follow. trino-gateway's own `pull_request_template.md` and `CONTRIBUTING.md` show the project's tone and any required contributor steps to stay consistent with.

**Plan:**
1. Fork `trinodb/trino-gateway` and create a branch (e.g. `add-issue-templates`).
2. Create `.github/ISSUE_TEMPLATE/` directory.
3. Add `bug_report.yml`, adapting Trino's fields to gateway terminology.
4. Add `feature_request.yml`, similarly adapted.
5. Add `config.yml` with appropriate contact links and `blank_issues_enabled` choice.
6. Validate YAML against GitHub's issue-forms schema (lint locally; verify the chooser renders on my fork).

**Implement:** *Links to branch/commits to be added in Phase III.*

**Review:** Self-review against `.github/CONTRIBUTING.md`, confirm commit/sign-off conventions, ensure links resolve and YAML is valid.

**Evaluate:** Confirm on my fork that "New issue" shows the template chooser and each form renders all fields correctly.

---

## Testing Strategy

> This contribution is GitHub configuration (YAML issue forms), so "testing" is validation + visual verification rather than unit/integration test code.

### Validation

- [ ] YAML parses and conforms to GitHub's issue-forms schema (lint / GitHub's built-in validation on push).
- [ ] Each template appears in the "New issue" chooser on my fork.
- [ ] Required fields, dropdowns, and placeholders render and behave as intended.

### Manual Testing

- [ ] Enable Issues on my fork, open "New issue", and confirm `bug_report.yml`, `feature_request.yml`, and the `config.yml` chooser/contact links all display correctly.
- [ ] Submit a test issue using each template on the fork to confirm the rendered output is well-structured.

*Results to be recorded in Phase III.*

---

## Implementation Notes

### Week 1 Progress (Phase I — Issue Selection)

- Selected issue #992 after running the issue-selection checklist (passed all 6 checks: clear problem, well-bounded scope, matches skills, active & claimable, helpful context via the linked Trino templates, and the project has clear setup/contribution docs).
- Confirmed the gap directly in the live repo (no `.github/ISSUE_TEMPLATE/` present).
- Drafted the solution approach and implementation plan above.

### Code Changes

- **Files modified:** *(planned)* `.github/ISSUE_TEMPLATE/bug_report.yml`, `.github/ISSUE_TEMPLATE/feature_request.yml`, `.github/ISSUE_TEMPLATE/config.yml` (all new).
- **Key commits:** *To be added in Phase III.*
- **Approach decisions:** Reuse Trino's proven templates and adapt rather than design from scratch, per the maintainer's request in the issue.

---

## Pull Request

**PR Link:** *To be submitted in Phase IV.*

**PR Description:** *Draft — will adapt the "Understanding the Issue" and "Solution Approach" sections above. Will reference `Fixes #992`.*

**Maintainer Feedback:**
- *None yet — will log dates and feedback here after the PR is opened.*

**Status:** Not yet submitted (currently Phase I).

---

## Learnings & Reflections

### Technical Skills Gained

*To be completed as I progress — expecting to learn GitHub issue-forms YAML schema and an established OSS project's contribution workflow.*

### Challenges Overcome

*To be completed in later phases.*

### What I'd Do Differently Next Time

*To be completed in later phases.*

---

## Resources Used

- Issue: https://github.com/trinodb/trino-gateway/issues/992
- Reference templates: https://github.com/trinodb/trino/tree/master/.github/ISSUE_TEMPLATE
- trino-gateway CONTRIBUTING guide: https://github.com/trinodb/trino-gateway/blob/main/.github/CONTRIBUTING.md
- GitHub docs — Configuring issue templates: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository
- GitHub docs — Syntax for issue forms: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema

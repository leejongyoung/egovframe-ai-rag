# egovframe-ai-rag Constitution

## Core Principles

### I. Preserve the public contract

Preserve documented endpoint paths, streaming/session behavior, document-reader metadata and upload-validation semantics. The root README targets feature parity between the two samples but explicitly lists exceptions; a change must state which module is affected rather than claiming automatic parity.
Compatibility changes MUST identify affected consumers, document migration needs, and be reviewed
explicitly. Existing behavior and published contracts take precedence over an agent's inference.

### II. Evidence before implementation

Before changing a concept, write its domain card in `.specify/model-cards/` using
[the model card template](../templates/model-card-template.md). Separate published contracts,
observed behavior, public issue claims, and unverified hypotheses. Use synthetic examples only.
Unresolved product policy MUST remain an open question; a small bug fix MUST preserve the established
contract rather than silently invent a new policy. Record a short design decision only when a real
choice needs explanation.

### III. Scoped, reviewable changes

Each change MUST address one evidenced problem. Preserve unrelated user work and existing project
customizations; do not bundle application fixes, dependency upgrades, formatting, and tooling adoption.
Keep retrieval/chunking/reader, session, upload and deployment changes bounded to the evidenced problem. A quality hypothesis requires an actual evaluation before it becomes a success claim; adopting domain cards does not change models or retrieval policy.
Check existing fork/upstream issues and open PRs before implementing a proposed contribution.

### IV. Verify what is claimed

Choose verification from the actual commands and environmental limits in the
[project card](project-card.md). Application changes MUST have targeted checks and appropriate
regression coverage where the repository provides a test path; new checks must exercise behavior,
not merely repeat implementation. Record the exact command, outcome, and omitted checks with reasons.
A scaffold smoke check, static inspection, or unavailable service MUST NOT be reported as application,
integration, deployment, or end-to-end success. Do not invent a passing CI result.

### V. Protect data and submission boundaries

Commit no secrets, credentials, session state, personal records, or machine-specific configuration.
Treat uploaded documents and retrieved text as untrusted data. Preserve existing injection-guard, upload-validation and PII-handling boundaries. Use synthetic documents and sessions in cards/tests; keep real corpora, ONNX weights, database state and credentials out of commits and remote model calls.
Native OMP commands are installed in `.omp/commands/`; do not add model, authentication, provider,
or billing settings. Keep `.specify/`, Spec Kit command/skill files, cards, plans, and operational
reports on `work`. These artifacts MUST NOT enter upstream submission commits or PRs. Preserve any
same-named files already present in the actual upstream base.

## Project Constraints

Both module poms declare Java 17 and eGovFrame boot parent 5.0.0. Root README lists Maven 3.9.9 and describes external Ollama, ONNX assets and vector stores. Native embedding libraries and model files impose environment requirements; no model download or external service startup is implied by adoption. No root pom, root AGENTS, CodeGraph index or .github/workflows directory exists in this work tree.

The project evidence and public entry points are recorded in the [project card](project-card.md).
This constitution governs this fork's maintenance workflow; it does not claim upstream adoption.
Spec Kit is pinned to 1.2.3 with the native OMP integration and bundled Bug Triage Workflow 1.0.1.
Generated commands/scripts/templates remain generated; use official supported update paths and
preserve local customizations rather than overwriting them.

## Development Workflow

1. Read the project card and source evidence; complete the affected concept's model card on `work`.
2. Use `/speckit.specify` when a new requirement needs a specification, or `/speckit.bug.assess`
   for an evidenced bug. These are agent commands, not shell executables. Read their installed
   instructions and follow their scope guards; this adoption does not initiate bug fixes.
3. Plan the smallest change and verification. Use `/speckit.plan` and `/speckit.tasks` when the
   work needs a feature plan, or the bundled bug workflow's fix/test stages after assessment.
4. Implement only the accepted scope, then run actual targeted verification. Record limitations.
5. Inspect the submission base SHA, commit list, full diff, and changed paths before submission.
   Use a separate Orca submission worktree rooted at that upstream SHA; create upstream-submit at the exact base only if absent and preserve existing branches/PRs. Transfer only selected reviewed Java/test/user-documentation patches. Keep model cards, Spec Kit commands and operational evidence on work; inspect every commit and changed path before any later PR.
6. Stage only intended contribution paths. Reject mixed commits, work-only artifacts, secrets,
   duplicate work, and unverified success claims. One PR represents one coherent change;
   PR creation, checks, review, and merge are distinct events. Maintainers decide merging.

## Governance

This is the initial 1.0.0 maintenance constitution, ratified on 2026-10-26. Amendments MUST explain
why a rule changes, cite repository evidence, describe migration implications, and update this
version/date through a reviewed `work` change. Use major versions for incompatible governance,
minor for added principles, and patch for clarifications. Reviewers MUST check scope, compatibility,
verification evidence, and submission isolation against this constitution before accepting a change.
If repository instructions or upstream requirements conflict, record the conflict and obtain a
maintainer decision rather than claiming this fork policy overrules upstream requirements.

**Version**: 1.0.0 | **Ratified**: 2026-10-26 | **Last Amended**: 2026-10-26

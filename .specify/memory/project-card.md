# egovframe-ai-rag project context

Observed from the `work` source at `9195736cb3c56afd13152d43ba5aaf1cad02a7c5` on 2026-10-26.
This is a maintenance context card, not a claim that application checks were run during adoption.

## Role and public entry points

Two Java 17 RAG question-answering samples: `spring-ai-rag-redis-stack/` uses Spring AI and Redis Stack, while `langchain4j-ai-rag-postgre/` uses LangChain4j and PostgreSQL/PGVector. Entry points include their Maven poms, controllers/services/readers, module READMEs, Dockerfiles/Compose and Kubernetes manifests.

## Evidence and maintenance boundaries

- `README.md`: two-stack role, feature-parity table, Java/Maven and model/vector-store preparation.
- `README-spring-ai-rag-redis-stack.md`, `README-langchain4j-ai-rag-postgre.md`: endpoints, document upload and model-placement constraints.
- Both module `pom.xml` files: Java 17, Maven dependencies/plugins.
- Both module Dockerfiles: Maven/JDK 17 build, -DskipTests package and external runtime assets.
- Each module's `src/test/`: guard, reader/transformer, upload, session and retrieval tests; DbTest/Testcontainers and SpringBootTest cases have extra environment requirements. Their presence is not evidence that they ran.

Keep the change scope and workflow policy in the [constitution](constitution.md); concept cards
link there rather than repeating the policy. Author a concept card only for actual planned work.

## Build and verification commands

- Build each module independently: `mvn -f spring-ai-rag-redis-stack/pom.xml -B -ntp package` and corresponding `langchain4j-ai-rag-postgre/pom.xml`; this is the Maven entry point implied by each pom, not a root aggregate command.
- Select relevant tests with Maven -Dtest=<actual-test-class> test for targeted changes, for example EgovDocumentServiceImplUploadValidationTest in the affected module.
- Dockerfiles use `mvn -B -ntp -DskipTests package`; that packaging command explicitly skips tests.
- Full tests may require Docker/Testcontainers, vector stores, Ollama or local model assets; inspect the chosen test's annotations/config first and record skips separately. No application builds/tests, evaluation benchmarks or service integration ran for adoption.

For this tooling-only adoption, verify Spec Kit CLI/integration status, installed core/bug commands,
constitution completeness, and template resolution/scaffold presence. Full application build,
lint, tests, formatter, external services, and deployment are not part of that smoke check.

## Upstream and submission baseline

Actual upstream is `eGovFramework/egovframe-ai-rag`, default main. Fork work holds maintenance/tooling. Prepare the submission baseline from the freshly fetched actual upstream default, not from work or a fork snapshot.

Use a separate Orca submission worktree rooted at that upstream SHA; create upstream-submit at the exact base only if absent and preserve existing branches/PRs. Transfer only selected reviewed Java/test/user-documentation patches. Keep model cards, Spec Kit commands and operational evidence on work; inspect every commit and changed path before any later PR.
No PR is created by adoption. Do not merge `work` or cherry-pick its adoption commit into a submission.
Preserve existing submission branches and PRs. Inspect changed paths and commits against the exact
base before any later PR; exclude work-only scaffolding without deleting upstream-owned files.

## Working with the pinned tooling

Installed by `uvx --from specify-cli==1.2.3 specify init --here --force --non-interactive
--integration omp --script sh --extension bug` after checking for existing path conflicts.
The CLI's init metadata pins 1.2.3; native agent commands live in `.omp/commands/`, including
`speckit.bug.assess.md`, `speckit.bug.fix.md`, and `speckit.bug.test.md`.
Use official upgrade support for future changes and preserve local customizations.
The new [domain model card template](../templates/model-card-template.md) aligns concept meanings
before specification; it is not an ML performance or benchmark card.

Observed submission base: `9195736cb3c56afd13152d43ba5aaf1cad02a7c5` (eGovFramework/egovframe-ai-rag, `main`).
Submission branch status: created-remote-at-upstream-default.

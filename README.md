# backend-sample

A demo **backend** consumer of `devsecops-shared-github-actions`. It's a minimal Maven multi-module project (`pom.xml`, `service-a/`, `service-b/`) used only as sample data.

The repository has no validation logic. Its workflow `.github/workflows/build.yml` declares:

```yaml
uses: Mahesh2511/devsecops-shared-github-actions/.github/workflows/build.yml@v1
with:
  artifact_type: backend
```

On every pull request the shared framework checks that every `pom.xml` (found recursively) declares the same project `artifactId`, before the build is allowed to run.

**Demo a failure:** open a PR that changes the project `artifactId` in `service-b/pom.xml` (not the one inside `<parent>`) to `another-service`. `PR Check` fails and `Build` is skipped.

> Note: a real Maven reactor needs unique module artifactIds. See the shared repo's `docs/assumptions.md` (interpretation decision 2).

# Opsætning af en Self-Hosted GitHub Actions Runner

---

## Overblik over mappehierarkiet
- **`/opt/docker/<app-name>`** : Indeholder dine Docker-stacks (f.eks. `supermix` og `hulemanden`).
- **`/opt/runners/<repository>`** : Indeholder én selv-hosted runner pr. GitHub-repo.
- Alle runner-processer kører under samme Linux-bruger `github-runner`.

## hvis ikke brugeren allerede findes, skal den oprettes:

```
useradd --system --create-home --shell /bin/bash github-runner
```

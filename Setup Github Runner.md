# Opsætning af en Self-Hosted GitHub Actions Runner

---

## Overblik over mappehierarkiet
- **`/opt/docker/<app-name>`** : Indeholder Docker-stacks og data (f.eks. `supermix` og `hulemanden`).
- **`/opt/runners/<repository>`** : Indeholder én selv-hosted runner pr. GitHub-repo.
- Alle runner-processer kører under samme Linux-bruger `github-runner`.


## Første gang (ny server):
### hvis ikke brugeren allerede findes, skal den oprettes:

```
useradd --system --create-home --shell /bin/bash github-runner
```
### Tjek at brugeren er oprettet:
```
getent passwd github-runner
```
Det burde returnere noget som:  
github-runner:x:996:988::/home/github-runner:/bin/bash

### Hvis ikke runner mappen findes, skal den oprettes 
```
mkdir -p /opt/runners
chown root:root /opt/runners
chmod 755 /opt/runners
```

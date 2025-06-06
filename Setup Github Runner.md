# Opsætning af en Self-Hosted GitHub Actions Runner

---

## Overblik over mappehierarkiet
- **`/opt/docker/<app-name>`** : Indeholder Docker-stacks og data (f.eks. `supermix` og `hulemanden`).
- **`/opt/runners/<repository>`** : Indeholder én selv-hosted runner pr. GitHub-repo.
- Alle runner-processer kører under samme Linux-bruger `github-runner`.


## Første gang (ny server)
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

## Hver gang (nyt workflow)
Opret  mappe og sæt/skift bruger
```
mkdir -p /opt/runners/<repository>/actions-runner
chown -R github-runner:github-runner /opt/runners/<repository>
chmod 700 /opt/runners/<repository>
```
- Gå til det GitHub repository du vil oprette en runner til -> Settings -> Actions -> Runners
- Klik på New self-hostet runner
- Vælg Linux X64
- Kør "download" kommandoerne (bemærk at mappen actions-runners nok allerede er oprettet)

Inden kørsel af "configure" skal der skiftes user  
Det kan ikke gøres som sudo:
```
su - github-runner
cd /opt/runners/randomcard/actions-runner
```
Kør configure kommandoerne  
Skift tilbage til root
```
exit
```
Kør installation og start:
```
./svc.sh install
./svc.sh start
```
Tjek status:
```
./svc.sh status
```

Bekræft på GitHub:
Gå til repository → Settings → Actions → Runners. Runneren skal stå som Online eller Idle.







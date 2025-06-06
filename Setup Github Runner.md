# Opsætning af en Self-Hosted GitHub Actions Runner

Denne vejledning viser, hvordan du konfigurerer en self-hosted runner på din Hetzner-server, så du kan køre CI/CD-jobs (build, push og `docker service update`) direkte fra dine GitHub-workflows uden at åbne port 22. Vi bruger ét fælles “github-runner” systembrugerkonto, og placerer runner-installationen under `/opt/runners/<repo-navn>`.

---

## Overblik over mappehierarkiet
/opt
├─ docker
│ ├─ supermix
│ │ ├─ docker-compose.yml
│ │ └─ data/
│ └─ app 2
│ ├─ docker-compose.yml
│ └─ data/
└─ runners
  ├─ randomcard ← runner-installation til RandomCard
  │   └─ actions-runner/ ← GitHub Actions-pakker + scripts
  └─ app 2 ← runner-installation til app 2
      └─ actions-runner/

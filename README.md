# airflow-git-sync-infra
Apache Airflow Docker setup with Git-synced DAGs (no DAGs stored in this repo)

# Airflow with Git-synced DAGs (Docker)

This repository demonstrates a Docker-based Apache Airflow setup where
**DAGs are delivered from a Git repository at runtime** using `git-sync`.

The purpose of this project is to showcase **Git-based DAG management**
and the separation of Airflow infrastructure from DAG code.

---

## Scope of this repository

This repository focuses on **infrastructure and integration**, not DAG logic.

**Included**
- Airflow Docker Compose setup
- `git-sync` integration for DAG delivery
- Internal PostgreSQL metadata database
- Redis broker (CeleryExecutor)
- Custom Airflow image via Dockerfile

**Intentionally excluded**
- DAG files
- Runtime logs
- Plugins
- Secrets

These artifacts are created or provided at runtime and are not versioned here.

---

## DAG synchronization model

- DAGs live in a separate Git repository
- `git-sync` periodically pulls updates from Git
- DAG files are written to a shared volume
- Airflow reads DAGs from the synced directory

DAG changes are reflected in Airflow **without rebuilding images or restarting
services**, enabling a GitOps-style workflow.

---

## Running the setup

### 1. Configure DAG repository

Create a `.env` file in the same directory as `docker-compose.yml`:

```env
GIT_SYNC_REPO=https://github.com/<your-user>/<your-dag-repo>.git

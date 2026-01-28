# gcloud-skill

A Claude Code skill providing comprehensive Google Cloud SDK (gcloud) CLI command reference.

## Installation

Copy the `.claude/skills/gcloud` directory to your Claude Code skills location:

```bash
# For personal use (all projects)
cp -r .claude/skills/gcloud ~/.claude/skills/

# For project-specific use
cp -r .claude/skills/gcloud /path/to/your/project/.claude/skills/
```

## Usage

The skill triggers automatically when asking about:
- Google Cloud Platform (GCP) services
- gcloud CLI commands
- Cloud infrastructure management
- Kubernetes (GKE) clusters
- Serverless deployments (Cloud Run, App Engine, Cloud Functions)
- IAM and authentication
- Cloud Storage and databases

Or invoke manually with `/gcloud [service-name or command]`.

## Covered Services

| Category | Services |
|:---------|:---------|
| Compute | Compute Engine (VMs), Disks, Snapshots |
| Containers | Google Kubernetes Engine (GKE) |
| Serverless | App Engine, Cloud Functions, Cloud Run |
| Storage | Cloud Storage (gsutil), Cloud SQL |
| Messaging | Pub/Sub |
| Security | IAM, Service Accounts, Authentication |
| Networking | VPC, Firewall Rules, Subnets |

## Skill Configuration

```yaml
name: gcloud
allowed-tools: Bash(gcloud *, gsutil *)
argument-hint: "[service-name or command]"
user-invocable: true
disable-model-invocation: false
```

## License

MIT

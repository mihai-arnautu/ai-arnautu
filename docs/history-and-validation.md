# Development history and evidence

[← Project overview](../README.md) · [Models and hardware](models-and-hardware.md) · [Operations](operations.md)

## A deployment assembled over time

The AI environment is supported by separate configuration histories for the interface, model backend and monitoring stack. This portfolio brings their relationship together in one case study without merging private infrastructure repositories into it.

| Date | Configuration area | Source revision | Recorded work |
| --- | --- | --- | --- |
| 22 Dec 2025 | Monitoring | `dfc63e1` | Initial monitoring stack with Grafana, Prometheus and SES integration |
| 22 Dec 2025 | Monitoring | `4996316` | Grafana SMTP configuration through SES |
| 12 Mar 2026 | Monitoring | `b030146` | Separate versioned configuration from runtime data |
| 12 Mar 2026 | Open WebUI | `617e76b` | Initialize the interface deployment configuration |
| 12 Mar 2026 | Ollama | `33a27da` | Initialize the backend configuration repository |
| 19 Mar 2026 | Monitoring | `b40f3a4` | Add Loki and Promtail |
| 20 Apr 2026 | Monitoring | `512d8b7` | Add the daily monitoring digest |
| 20 Apr 2026 | Monitoring | `70086c4` | Improve model formatting in the digest |
| 20 Apr 2026 | Open WebUI | `de7fc83` | Add scheduled interface updates with Watchtower |
| 20 Apr 2026 | Ollama | `f1957f3` | Add host-level update timer |
| 20 Apr 2026 | Ollama | `3417456` | Correct update-script version parsing |
| 28 Apr 2026 | Open WebUI | `d1ad469` | Add SearXNG web search |

Dates and revision IDs were read from the existing source histories. They document earlier work; they are not recreated as older commits in this portfolio repository.

## November 2026 verification snapshot

| Check | Observed result | What it establishes |
| --- | --- | --- |
| Public application endpoint | HTTP 200 | Public route was serving a page |
| Fresh browser context | ARN (Open WebUI) sign-in screen | Visitor-facing entry point and branding |
| Open WebUI container | Healthy | Container health check was passing |
| Search/monitoring containers | Running | Supporting processes existed and were running |
| Ollama service | Active | Host model service was running |
| GPU inventory | RTX 3090 with 24 GB VRAM | Available GPU hardware |
| CPU inventory | Ryzen 7 9700X, 8 cores / 16 logical CPUs | Host compute topology |
| Model inventory | Five local tags | Installed artifact availability |
| Backup/report timers | Active with scheduled runs | Scheduler configuration was present and active |

These observations were collected without loading a model, generating a chat, accessing private conversations, sending a report or initiating a backup.

## Evidence and its limits

- A sign-in screenshot demonstrates the entry point, not an authenticated conversation or inference result.
- Container health is useful for service availability, not a throughput or uptime benchmark.
- Model inventory proves neither GPU residency nor task quality.
- A configured dashboard/alert proves the definition exists; delivery tests require separate evidence.
- A backup timer does not replace a repository check or a restore exercise.

## Lessons from operating the environment

**Separate application health from dependency health.** The interface, inference runtime, GPU, search and storage can fail independently.

**Treat models as artifacts, not configuration files.** Keep a small, readable configuration history and an inventory while managing weight downloads and cache outside Git.

**Make reports compare state over time.** A version/model/container change is often more useful in diagnosis than a repeated list of healthy-looking services.

**Keep recovery evidence specific.** A corrected network mount or active timer is an intermediate result, not proof of a successful restore.

## Follow-up work

| Improvement | Purpose |
| --- | --- |
| Repeatable model benchmark | Record task-specific latency, throughput and memory use |
| Explicit image/version pinning | Make rollback and reproduction more predictable |
| Periodic restore exercise | Validate recovered configuration and application data |
| Monitoring exposure review | Verify access controls for host-published services |
| Dependency-level synthetic checks | Separate page, backend and search readiness |

These are documented opportunities, not completed features or published guarantees.

## Repository activity

- [Presentation commit history](https://github.com/mihai-arnautu/ai-arnautu/commits/main/)
- [Repository activity](https://github.com/mihai-arnautu/ai-arnautu/activity)

The source-history table records earlier implementation work. This repository's own history records changes to the presentation, screenshots and technical notes from November 2026 onward. Detailed Insights graphs may depend on the GitHub plan while the repository is private.

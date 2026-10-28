# Backlog: Additional Technologies and Suggestions

Candidate additions to the stack in
[PLATFORM-MIGRATION-PLAN.md](./PLATFORM-MIGRATION-PLAN.md). None are committed
to the plan yet.

## Recommended first picks

- [ ] Longhorn (replicated storage)
- [ ] MinIO + Velero (backups, object storage)
- [ ] KEDA (queue-based autoscaling)
- [ ] Kyverno (policy engine)
- [ ] Falco (runtime detection)
- [ ] External Secrets + Vault or OpenBao
- [ ] Cilium (CNI, NetworkPolicies, mTLS, Hubble)
- [ ] Flyway (schema migrations)
- [ ] Renovate (dependency and chart updates)

## Reliability and operations

- [ ] **Backup and DR**: Velero for cluster and volume backups; MariaDB Operator
  backup CRDs and MongoDB backups to object storage. The plan mentions restore
  tests but names no tooling.
- [ ] **Object storage (MinIO)**: shared target for backups, Loki/Tempo storage,
  and Mimir blocks.
- [ ] **Persistent storage**: K3s local-path is not replicated; use Longhorn or
  Rook-Ceph for stateful workloads.
- [ ] **Autoscaling**: KEDA for queue-based scaling (optional in the plan),
  plus metrics-server and VPA.
- [ ] **Progressive delivery**: Flagger or Argo Rollouts for canaries with
  automatic rollback driven by Mimir metrics.

## Security

- [ ] **Policy engine**: Kyverno or OPA Gatekeeper (the plan already assumes
  Kyverno for cosign verification).
- [ ] **Runtime detection**: Falco for syscall-level container detection,
  complementing host-focused Wazuh.
- [ ] **Secrets**: HashiCorp Vault or OpenBao with External Secrets Operator;
  stronger than SOPS if rotation or dynamic DB credentials are needed.
- [ ] **Identity**: Keycloak or Authentik for API and Grafana SSO/OIDC.
- [ ] **CNI / mesh**: Cilium for NetworkPolicies, mTLS, and Hubble network
  observability (lighter than Istio).
- [ ] **Supply chain**: Syft and Grype for SBOMs; SLSA provenance via GitHub
  attestation actions.

## Delivery and quality

- [ ] **IaC scanning and pre-commit**: pre-commit hooks, tflint, Checkov, Trivy
  config scanning.
- [ ] **Dependency updates**: Renovate (or Dependabot) for Helm charts and
  images; works well with Flux.
- [ ] **Load and chaos testing**: k6 to replace Siege, ab, and JMeter on
  Kubernetes; Chaos Mesh for fault injection.
- [ ] **Ephemeral PR environments**: Flux or vcluster preview environments per
  pull request.

## Data

- [ ] **Schema migrations**: Flyway or Liquibase run as Kubernetes Jobs
  (ToDo.md calls for migrations but names no tool).
- [ ] **Exporters**: Prometheus exporters for MariaDB, MongoDB, Redis, and
  RabbitMQ.

## Other

- [ ] **Developer experience**: Tilt or Skaffold for local Kubernetes
  iteration; Makefile or Taskfile wrapping common commands.
- [ ] **Documentation**: architecture decision records (ADRs), e.g. RabbitMQ vs.
  NATS.

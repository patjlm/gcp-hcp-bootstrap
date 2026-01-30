# GKE Bootstrap

Bootstrap manifests for GKE clusters.

## Contents

- **ArgoCD** v3.2.6
- **External Secrets Operator** v1.3.1
- **SecretStore** for GCP Secret Manager (argocd namespace only)
- **ExternalSecrets** for cluster configuration
- **Root ApplicationSet**

## Structure

```
bootstrap/
├── argocd/
│   ├── namespace.yaml
│   ├── install.yaml
│   ├── service-account.yaml
│   ├── secret-store.yaml
│   ├── external-secret-argocd-cluster.yaml
│   ├── external-secret-git-credentials.yaml
│   └── root-applicationset.yaml
└── external-secrets/
    ├── namespace.yaml
    └── controller.yaml
```

## Updating

### ArgoCD
```bash
VERSION=v3.2.6
curl -L https://raw.githubusercontent.com/argoproj/argo-cd/${VERSION}/manifests/install.yaml \
  -o bootstrap/argocd/install.yaml
```

### External Secrets Operator
```bash
VERSION=1.3.1
helm template external-secrets external-secrets/external-secrets \
  --namespace external-secrets-system \
  --version ${VERSION} \
  > bootstrap/external-secrets/controller.yaml
```

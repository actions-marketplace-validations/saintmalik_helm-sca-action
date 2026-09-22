# helm-sca-action

GitHub Action wrapping [`saintmalik/helm-sca`](https://github.com/saintmalik/helm-sca): supply chain checks on container images your GitOps/ops repo would deploy, not app-CI image scans.

Blog: [supply chain risk in Helm charts](https://blog.saintmalik.me/helm-gitops-supply-chain-checks/)

## Usage

```yaml
- uses: saintmalik/helm-sca-action@6debf2d90e156822a8944b548eb8fd42acf1d5ae # v0.0.3
  with:
    mode: argo
    argo-apps: ./environments
    command: scan
    fail-on: high
```

Flux / gitops:

```yaml
- uses: saintmalik/helm-sca-action@6debf2d90e156822a8944b548eb8fd42acf1d5ae # v0.0.3
  with:
    mode: flux          # or: gitops, chart, manifests, terraform
    flux: ./clusters/prod
    command: scan
    fail-on: high
```

More workflows under [`examples/`](./examples/).

### Install method

- `release` (default) — download CLI from [`helm-sca` releases](https://github.com/saintmalik/helm-sca/releases) at `version` (`v0.0.1` or `latest`)
- `go-install` — `go install ...@${version}`
- `build` — clone/build from `helm-sca-ref` or `helm-sca-path`

### Inputs

| Input | Default | Notes |
|-------|---------|-------|
| `command` | `scan` | `inventory` or `scan` |
| `mode` | `argo` | `argo` \| `flux` \| `gitops` \| `manifests` \| `chart` \| `terraform` |
| `argo-apps` / `flux` / `gitops` / `chart` / `manifests` / `terraform` / `terraform-json` | | mode paths |
| `fail-on` | `none` | `none`\|`low`\|`medium`\|`high`\|`critical` |
| `out-dir` | `helm-sca-out` | scan reports |
| `install-method` | `release` | above |
| `version` | `v0.0.1` | CLI tag from helm-sca; `latest` floats |

## License

MIT

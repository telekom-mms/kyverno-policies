# A Collection of useful, reusable kyverno policies

## Installation

Add the GitHub Pages Helm repository and install the latest stable chart:

```bash
helm repo add kyverno-policies https://telekom-mms.github.io/kyverno-policies/charts
helm repo update
helm upgrade --install kyverno-policies kyverno-policies/kyverno-policies \
  --namespace [your namespace]
```

## Configure

Example `values.yaml`
```yaml
---

includePolicies:
  - require-ro-rootfs
  - require-run-as-non-root
  - disallow-privilege-escalation
  - disallow-privileged-containers
  - require-drop-all

policyRunAsNonRoot:
  validationActions:
    - Audit
  excludedNamespaces:
    - kube-system
    - my-legacy-namespace
  excludedLabels:
    exclude-from-policy: "true"
    allow-root: "yes"
```

## Currently available policies
* disallow-privilege-escalation
* disallow-privileged-containers.yaml
* require-drop-all.yaml
* require-ro-rootfs.yaml
* require-run-as-non-root.yaml

Enable GitHub Pages in the GitHub repository settings with **GitHub Actions** as the build and deployment source. The chart repository becomes available after the next non-prerelease `v*` release. Run `helm repo update` before upgrades to discover newer charts; omit `--version` to select the latest stable chart. For a fixed deployment, set `--version` on the Helm command.

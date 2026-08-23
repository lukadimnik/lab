# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal homelab / infrastructure-as-code learning repo. There is no application source code, package manager, test suite, or CI — it's a collection of Docker exercises, Kubernetes manifests, Helm values, and Terraform, used to run self-hosted services and experiment with cloud provisioning.

## Structure

- `docker-and-bash-scripts/` — standalone Docker + bash exercises (Dockerfile + script per subfolder). No shared conventions between them.
- `k8s-kubecraft-fundamentals/` — Kubernetes manifests and Helm values for a **local** cluster: `deployments/` (raw learning manifests), `helm/`, `homarr/`, `mealie/`, `audiobookshelf/`, `monitoring/` (kube-prometheus-stack values + a custom Grafana dashboard JSON).
- `kubernetes-in-the-cloud/phase-1/` — Terraform (`azurerm` provider) provisioning a **cloud** (Azure) VM, meant to become a cloud-hosted k8s node. Local state (`terraform.tfstate*`, `.terraform/`) is gitignored.

## Workflow notes

- Manifests under `k8s-kubecraft-fundamentals/` target a local cluster (e.g. `kubectl apply -f <dir>/`); `kubernetes-in-the-cloud/` targets Azure via `terraform init/plan/apply` run from `kubernetes-in-the-cloud/phase-1/`. Don't assume one context applies to both folders.
- Helm charts (`homarr`, the monitoring stack) are installed manually — only `values.yaml` files live in the repo, not install commands. Don't invent `helm install` release/repo names; ask if one is needed.
- No linter, formatter, or CI is configured anywhere. Don't assume `terraform fmt`, `yamllint`, etc. run automatically.
- `kubernetes-in-the-cloud/phase-1/vm.tf` hardcodes an Azure `subscription_id` and references local SSH key paths (`~/.ssh/mercury*`). Treat these as identifying/sensitive — don't copy them into other files, examples, or commit messages beyond what's already there.

## Commit conventions

- Use [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `chore:`, etc.) for commit messages.
- Keep commits small and logical — one change per commit, not batched unrelated edits.

# virt-controller: ReadyStack build kit

The offline build kit for the Docker image `readystack/virtcontroller:v1.9.1-CE-debian12-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.9.1-CE-debian12-r2](https://github.com/readystack-dev/virtcontroller/releases/tag/v1.9.1-CE-debian12-r2)
- Image: [`docker.io/readystack/virtcontroller:v1.9.1-CE-debian12-r2`](https://hub.docker.com/r/readystack/virtcontroller/tags), manifest digest `sha256:d19615aad99d9715a0cf91e41647795dac2d49ee7c2b6acc83d2fbed1c1212c5`
- Product page: https://readystack.dev/products/virtcontroller
- Source and build recipe: https://readystack.dev/products/virtcontroller/recipe
- Build trail: https://readystack.dev/products/virtcontroller/trail/v1.9.1-CE-debian12-r2
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=virtcontroller

## The image

the cluster-wide controller: it creates a virt-launcher Pod for each VirtualMachineInstance, tracks its lifecycle and runs live migrations, snapshots and exports.

## Who uses virt-controller and why

Kubernetes cluster administrators who run virtual machines in their clusters with KubeVirt.

virt-controller holds KubeVirt's cluster-wide virtualisation logic. It watches virtual machine instances and creates and manages the pod that each one runs in.

A typical use: When a user starts a virtual machine, virt-controller sees the new instance and creates a pod for it; Kubernetes schedules that pod onto a node, and virt-controller records the node so the virt-handler there can start the VM.

From the upstream project's own description: https://github.com/kubevirt/kubevirt/blob/main/docs/components.md, https://github.com/kubevirt/kubevirt.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-08 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 3 packages with copyleft licences (GPL, LGPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`1001`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-08; the rebuilt image digest is the published one.
- Base: Debian 12.

The current grade, measured again every day, is on https://readystack.dev/products/virtcontroller.

virt-controller is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v1.9.1-CE-debian12-r2 release](https://github.com/readystack-dev/virtcontroller/releases/tag/v1.9.1-CE-debian12-r2): `ReadyStack-virtcontroller-v1.9.1-CE-debian12-r2.tar.gz` (1.1 GB), SHA-256 `32ce793f75ae93cd275f43808a2d2365afccd5f881cac0f5958e634a0237aa26`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-virtcontroller-v1.9.1-CE-debian12-r2.rebuild.json.sigstore ReadyStack-virtcontroller-v1.9.1-CE-debian12-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-virtcontroller-v1.9.1-CE-debian12-r2.tar.gz
cd v1.9.1-CE-debian12-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-virtcontroller-v1.9.1-CE-debian12-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/virtcontroller/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev

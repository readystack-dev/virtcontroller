# Provenance — virt-controller (`v1.9.1-CE-debian12-r3`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/kubevirt/kubevirt
- Revision built: `v1.9.1` (commit `c3d19093f9c7b843b3879b18dc088911c081c39e`)
- Source tree: `de7abf04e51b6cf004d0365dfe6d8c5251edeeb69bfa0caa3d8b366b85fe6f36` over 12717 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `gcr.io/distroless/base-debian12@sha256:ca3f629c350fd1cb653caee7c5aed8967be4e43d9577fbb1cb4ed66c260e224e`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795617155` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/virtcontroller:v1.9.1-CE-debian12-r3` — index digest `sha256:bd14ffe7770328de993b4b08406c962b3458ef53a84bc5c805b571a0e93933aa` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:dd3edb1d6a2c889690e769e843601af944de1674c5ed4084a3824b27dfaefb7d` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/virtcontroller:v1.9.1-CE-debian12-r3`

## Pinned inputs, and why

- 14 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, language runtimes and toolchains 1, dependency versions readystack sets 5, pins in the kit's dockerfiles 1, readystack's build engine 1, dependencies upstream chose 1).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-virtcontroller-v1.9.1-CE-debian12-r3.trail.json`, published beside this archive and signed with the release key (`ReadyStack-virtcontroller-v1.9.1-CE-debian12-r3.trail.json.sigstore`), and readable at https://readystack.dev/products/virtcontroller/trail/v1.9.1-CE-debian12-r3.


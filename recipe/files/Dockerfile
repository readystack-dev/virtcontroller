# =====================================================================================================================
# KubeVirt v1.9.1 virt-controller: KubeVirt's OWN Bazel build, offline (docker buildx build --network=none).
# Stage kubevirt-build is KubeVirt's pinned builder (quay.io/kubevirt/builder, CentOS Stream 9, Bazel 6.5.0). It runs
# kubevirt-build.sh: the ReadyStack patch series (patches/, each patch says what it changes and why), KubeVirt's
# bootstrap and `bazel build //cmd/virt-controller:virt-controller-image` on vendored/virtcontroller-src (git archive of c3d19093f9c7), with the
# vendored Bazel repository cache (RPMs, Go SDK, rules, distroless base, libssl3 .deb: every download by sha256, none
# made here). The image Bazel builds is unpacked into /out/rootfs
# (oci-rootfs.py: config parity with the final stage below, no build path in any file); the final stage is that
# filesystem with that config, as one layer.
# Dockerfile and Dockerfile.offline are byte copies of this file. Written by
# product-kits/kubevirt-stack/kubevirt/mk-kits.py from strategies/virtcontroller.json; never edit by hand.
# =====================================================================================================================
FROM quay.io/kubevirt/builder:2606231619-4fe2cd536f@sha256:a48a7dd5a1b80602269b8c714fdaa54f729a9a4a4d096f7ee0d15c94cef343e8 AS kubevirt-build
# the commit's date as the default (as every kit declares it): assemble_kit's scratch build passes no build arguments,
# and kubevirt-build.sh refuses to build without it; the canonical build and BUILD_OFFLINE.sh pass the same value
ARG SOURCE_DATE_EPOCH=1791523273
ARG KUBEVIRT_VERSION=v1.9.1
COPY vendored/virtcontroller-src/ /root/go/src/kubevirt.io/kubevirt/
COPY vendored/bazel-repository-cache/ /kvs/cache/repo/
COPY patches/ /kvs/kit/patches/
COPY vendor/ /kvs/kit/vendor/
COPY kubevirt-build.sh oci-rootfs.py gen_rpmdb.py gomod-sbom.py gomod-virt-controller.txt kubevirt-pins.env Dockerfile.offline.pinned /kvs/kit/
# Bazel runs no ldconfig, so there is no /var/cache/ldconfig/aux-cache to strip; the rm keeps that true.
RUN bash /kvs/kit/kubevirt-build.sh build virt-controller && rm -f /out/rootfs/var/cache/ldconfig/aux-cache

FROM scratch
COPY --from=kubevirt-build /out/rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
WORKDIR /
USER 1001
ENTRYPOINT ["/usr/bin/virt-controller"]
ARG SOURCE_DATE_EPOCH=1791523273
# >>> readystack OCI labels: strategies/virtcontroller.json image_labels plus the standard OCI labels,
# the set a generated kit carries (gen_dockerfile.label_lines). Written by scripts/kit_migrations.py;
# scripts/retarget.py re-renders it with every retarget. Never edit it by hand.
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="virt-controller"
LABEL org.opencontainers.image.description="KubeVirt v1.9.1 virt-controller, built offline and bit for bit by KubeVirt's own Bazel build: the cluster controller that turns VirtualMachines into virt-launcher Pods and drives migrations."
LABEL org.opencontainers.image.source="https://github.com/kubevirt/kubevirt"
LABEL org.opencontainers.image.version="v1.9.1-CE-debian12-r2"
LABEL org.opencontainers.image.revision="c3d19093f9c7b843b3879b18dc088911c081c39e"
# <<< readystack OCI labels

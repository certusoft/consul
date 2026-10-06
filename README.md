# certusoft/consul: illumos builds

This branch only holds `.github/workflows/illumos-release.yml`, which builds an
upstream Consul release for illumos (SmartOS / Triton zones) and publishes it
as a GitHub Release here.

HashiCorp ships a `GOOS=solaris` build only. On illumos that build's
fork/exec intermittently fails with `bad address` (EFAULT), because Go uses
Oracle Solaris's `F_DUP2FD_CLOEXEC` (0x30), which illumos defines as
`F_OFD_SETLK`. A `GOOS=illumos` build uses the illumos value (0x24).

To build a release, tag this branch with `v<version>-illumos` and push the tag:

    git fetch origin certusoft/illumos-build
    git tag v2.0.4-illumos origin/certusoft/illumos-build
    git push origin v2.0.4-illumos

The workflow checks out `hashicorp/consul` at `v<version>` and builds it with
HashiCorp's release flags. Downloads:

    https://github.com/certusoft/consul/releases/download/v<version>-illumos/consul_<version>_illumos_amd64.zip
    https://github.com/certusoft/consul/releases/download/v<version>-illumos/consul_<version>_SHA256SUMS

Consul is licensed under the Business Source License 1.1 (see LICENSE in each
zip).

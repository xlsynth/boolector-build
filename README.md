## Package builds and releases

### What we do

- Build and publish a small set of packages with CI workflows
- Current packages:
  - Boolector 3.2.2 shared library (DSO)
  - Icarus Verilog (`iverilog`, `vvp` binaries)
- Produce SHA-256 checksums and include upstream license files

### How we do it

- Workflows:
  - `/.github/workflows/build-and-release-boolector.yml`
    - Debian 10 (amd64) and macOS 14 ARM64 builds; run tests; upload `.so`/`.dylib`; manual release aggregates artifacts
  - `/.github/workflows/build-and-release-iverilog.yml`
    - Debian 10 (amd64) build of `iverilog` and `vvp`; upload binaries; manual release publishes artifacts

### Conventions

- Release tag
  - Boolector: `boolector-binaries-${git-ref-built}` (commit SHA of this repo)
  - Icarus Verilog: `iverilog-binaries-${IVERILOG_REF}` (upstream ref provided to workflow)
- Artifact filename: `${package-name}-${os-name}.${platform-ext}` (or no ext for executables)
  - Examples: `libboolector-debian10.so`, `libboolector-osx-arm64.dylib`, `iverilog-rocky8`, `vvp-rocky8`
- Checksum filename: `${artifact-filename}.sha256`
- License: include upstream `COPYING`/license file with each artifact set



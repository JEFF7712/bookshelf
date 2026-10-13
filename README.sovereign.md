# Sovereign Bookshelf release

Forgejo `JEFF7712/bookshelf` on `develop` is authoritative. Woodpecker uses
homelab's server-owned `dotnet` compiler to build the frontend and .NET
projects from retained inputs, then publishes the verified OCI artifact to
Zot. Flux owns deployment after a protected homelab promotion PR.

The application Dockerfile packages the compiler's generated
`.sovereign/build/runtime` and retained SQLite library. It does not download
packages or build directly from a bare clone. The SDK and runtime base are
pinned local images. Build inputs and source provenance are recorded in
`/app/.sovereign-build.json`. Source compilation runs without publishing
credentials, and the final image runs as uid 1000.

The retained input contract, fetch manifests, clean-build evidence, and
compiler implementation live under `services/bookshelf/`,
`config/ci/applications.json`, and `scripts/ci/dotnet_release.py` in the
Forgejo homelab repository.

# AsteriskRegistry

Julia package registry for [Asterisk Labs](https://asterisk.coop), the UK's first worker-owned cooperative research lab focused on deep learning, Earth observation, and climate science.

This registry hosts Julia packages developed by Asterisk Labs that are not (yet) part of the General registry.

## Add the registry

```julia
using Pkg
Pkg.Registry.add(RegistrySpec(url = "https://github.com/asterisk-labs/AsteriskRegistry"))
```

Once added, packages from this registry can be installed with `Pkg.add` like any other Julia package.

## Available packages

| Package | Description | Source |
| ------- | ----------- | ------ |
| [`Cozip`](https://github.com/asterisk-labs/taco/tree/main/cozip/julia) | Julia bindings for `libcozip`, a writer for the Cloud-Optimized ZIP (cozip) format | `asterisk-labs/taco` |

Precompiled native binaries for `libcozip` are distributed via [`Cozip_jll`](https://github.com/asterisk-labs/taco/releases) using `Artifacts.toml` with SHA256 verification.

## Install a package

```julia
pkg> add Cozip
```

```julia
julia> using Cozip
julia> Cozip.cozip_version()
"2026.5.2"
```

## For maintainers

New versions are registered with [LocalRegistry.jl](https://github.com/GunnarFarneback/LocalRegistry.jl) from the source monorepo.

From the monorepo root:

```julia
using Pkg
Pkg.develop(path = abspath("cozip/julia"))

using LocalRegistry
register("Cozip"; registry = "AsteriskRegistry", push = true)
```

`push = true` commits to `~/.julia/registries/AsteriskRegistry` and pushes to GitHub automatically. If the push fails due to credentials:

```bash
cd ~/.julia/registries/AsteriskRegistry
git push
```

After registration, verify that `C/Cozip/{Package,Versions,Deps,Compat}.toml` and the updated entry in the root `Registry.toml` are present in this repo.

## License

MIT

# AsteriskRegistry

Julia package registry for [Asterisk Labs](https://asterisk.coop).

## Add the registry

```julia
using Pkg
Pkg.Registry.add(RegistrySpec(url = "https://github.com/asterisk-labs/AsteriskRegistry"))
```

Once added, packages from this registry can be installed with `Pkg.add` like any other Julia package.

## Available packages

| Package | Description | Latest | Source |
| ------- | ----------- | ------ | ------ |
| [`Cozip`](https://github.com/asterisk-labs/cozip/tree/main/julia) | Write Cloud-Optimized ZIP archives | `2026.11.23` | `asterisk-labs/cozip` |
| [`GeoZL`](https://github.com/asterisk-labs/geozl/tree/main/bindings/julia) | Compress raster tiles with GeoZL codecs for OpenZL | `0.31.0` | `asterisk-labs/geozl` |
| [`Rumi`](https://github.com/asterisk-labs/rumi/tree/main/bindings/julia) | Read and write Rumi Image and Cube files | `0.29.0` | `asterisk-labs/rumi` |
| [`Taco`](https://github.com/asterisk-labs/taco/tree/main/julia) | Read TACO datasets | `0.10.1` | `asterisk-labs/taco` |

Precompiled native libraries are downloaded as Julia artifacts from each project's GitHub releases.

## Install a package

```julia
pkg> add Cozip GeoZL Rumi Taco
```

```julia
julia> using Cozip
julia> Cozip.cozip_version()
```

## For maintainers

New versions are registered with [LocalRegistry.jl](https://github.com/GunnarFarneback/LocalRegistry.jl) from each source repository.

| Package | Julia project path |
| ------- | ------------------ |
| `Cozip` | `cozip/julia` |
| `GeoZL` | `geozl/bindings/julia` |
| `Rumi` | `rumi/bindings/julia` |
| `Taco` | `taco/julia` |

For example, from the `cozip` repository root:

```julia
using Pkg
Pkg.develop(path = abspath("julia"))

using LocalRegistry
register("Cozip"; registry = "AsteriskRegistry", push = true)
```

`push = true` commits to `~/.julia/registries/AsteriskRegistry` and pushes to GitHub automatically. If the push fails due to credentials:

```bash
cd ~/.julia/registries/AsteriskRegistry
git push
```

After registration, verify that `<Letter>/<Package>/{Package,Versions,Deps,Compat}.toml` and the updated entry in the root `Registry.toml` are present in this repo, and bump the `Latest` column above.

## License

MIT

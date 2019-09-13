# LibAtoms

A small Julia Package Registry for anything [JuLIP](https://github.com/libAtoms/JuLIP.jl) and [libatoms](https://libatoms.github.io) related.

To install, simply open a Julia REPL and type
```
] registry add https://github.com/cortner/LibAtoms.git
```
Afterwards use the normal package manager commands to add, remove, dev, etc the packages in this registry.

The following packages are currently registered:
* SHIPs.jl
* SKTB.jl
* JuLIPMaterials.jl
* NBodyIPs.jl
* IPFitting.jl

## Registering a Package or a new version

Registering a new package or a new version use the same process. First we require a specific fork of [`Registrator.jl`](https://github.com/GunnarFarneback/Registrator.jl), which can be installed via
```
] add https://github.com/GunnarFarneback/Registrator.jl
```

Suppose now that we want to register a new version of `IPFitting.jl`. Assume that `IPFitting` is in `dev` mode, i.e., in `~/.julia/dev/IPFitting/`. Then we first bump the version number, by manually editing `Project.toml`, commit and push.

Next, the following sequence of commands will register the new version in the `LibAtoms` registry.
```
using Registrator
using IPFitting
regpath = joinpath(homedir(), ".julia", "registries", "LibAtoms")
register(IPFitting, regpath)
```

This edits the registry files and commits the changes. If you don't have push access or are unsure about merging the updated registry, then make a PR.

Sometimes, I found that the main `v1.1` environment is incompatible with the package, and `using IPFitting` (e.g.) will fail. In that case, one first activates the package's environment  first.

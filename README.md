# MolSim

A Julia Package Registry for packages related to molecular simulation.

To install open a Julia REPL and type
```{julia}
] registry add https://github.com/JuliaMolSim/MolSim.git
```
Afterwards use the normal package manager commands to add, remove, dev, etc the packages in this registry.

## Registering a Package or a new version

Registering a new package or a new version uses the same process. First we require a specific fork of [`Registrator.jl`](https://github.com/GunnarFarneback/Registrator.jl), which can be installed via
```{julia}
] add https://github.com/GunnarFarneback/Registrator.jl
```
(`using Registrator.jl` may show a warning which you can probably ignore.)

Suppose now that we want to register a new version of `JuLIP.jl`:
1. `] dev JuLIP`; we will assume this puts `JuLIP` into  `~/.julia/dev/JuLIP/`.
2. make the changes to the package
3. Bump the version number, by manually editing `Project.toml`, commit and push.
4. Now the following sequence of commands will register the new version in the `MolSim` registry.
   ```{julia}
   using Registrator
   using JuLIP
   regpath = joinpath(homedir(), ".julia", "registries", "MolSim")
   register(JuLIP, regpath)
   ```
   This edits the registry files and commits the changes.
5. Finally, we need to push the registry
   ```{bash}
   cd ~/.julia/registries/MolSim
   git push
   ```

## Remarks

* A basic management tool for the `MolSim` registry is provided by [`MolSimReg.jl`](https://github.com/JuliaMolSim/MolSimReg.jl); With that package, Step 4 above becomes
```{julia}
using MolSimReg, JuLIP
MolSimReg.register(JuLIP)
```
* If you don't have push access or are unsure about merging the updated registry, then make a PR. (Maybe this step should be automated at some point.)
* Sometimes, I found that the main `v1.1` environment is incompatible with the package, and `using IPFitting` (e.g.) will fail. In that case, one first activates the package's environment  first.

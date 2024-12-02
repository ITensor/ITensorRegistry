# JuliaRegistry

This is the local registry containing work-in-progress versions of packages developed within the ITensors.jl ecosystem.
It is mainly meant to promote fast development and iteration, and its stability should be considered accordingly.

## Using the registry

In order to start using this registry, you can simply add it to your Julia package manager once.
After this, the package manager will automatically attempt to resolve names of packages, as long as there are no name clashes.

```julia
using Pkg: Pkg
Pkg.Registry.add(url="https://github.com/ITensor/ITensorRegistry")
```
or:
```julia
Pkg.Registry.add(url="git@github.com:ITensor/ITensorRegistry.git")
```
if you want to use SSH credentials, which can make it so you don't have to enter your Github ursername and password when registering packages.

## Registering a package

In order to register a new package, or a new version, you can simply follow the instructions [here](https://github.com/GunnarFarneback/LocalRegistry.jl/blob/master/docs/register.md).
First, you should add `LocalRegistry.jl` in your global environment.

Then, for a new package, if you only have a single additional registry which is not `General`, or for a new version, you can simply activate that package and call
```julia
using LocalRegistry: LocalRegistry
LocalRegistry.register()
```

Otherwise, you may have to specify the specific registry, for which you can follow the instructions [here](https://github.com/GunnarFarneback/LocalRegistry.jl/blob/master/docs/register.md).

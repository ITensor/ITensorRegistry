# ITensorRegistry

This is the local registry containing work-in-progress versions of packages developed within the ITensor Julia ecosystem.
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

In order to register a new package, or a new version, you can simply follow the instructions in the [LocalRegistry.jl docs](https://github.com/GunnarFarneback/LocalRegistry.jl/blob/master/docs/register.md). We will give a brief summary below:

First, you should add `LocalRegistry.jl` in your global environment.

Then, for a new package, register the package `pkgname` in the Github organization `ghuser` (`ghuser = "ITensor"` if the package is hosted in the ITensor organization) by changing to the directory of the package and registering with the URL of the package repository:
```julia
using LocalRegistry: LocalRegistry
cd(expanduser("~/.julia/dev/$pkgname")) do
  return LocalRegistry.register(; repo="https://github.com/$ghuser/$pkgname.jl.git")
end
```
This assumes you only have a single additional registry which is not `General`, otherwise you also have to specify the registry (see the [LocalRegistry.jl docs](https://github.com/GunnarFarneback/LocalRegistry.jl/blob/master/docs/register.md)).

For registering a new version, you can simply change to the directory of the package and call `LocalRegistry.register()` (the repository URL doesn't need to be specified since it is determined from the registry):
```julia
using LocalRegistry: LocalRegistry
cd(expanduser("~/.julia/dev/$pkgname")) do
  return LocalRegistry.register()
end
```

The following functions may be useful:
```julia
function register_pkg(pkgname; new, ghuser="ITensor")
  return cd(expanduser("~/.julia/dev/$pkgname")) do
    if new
      return LocalRegistry.register(; repo="https://github.com/$ghuser/$pkgname.jl.git")
    else
      return LocalRegistry.register()
    end
  end
end
```
which you can use like `register_pkg("PkgName"; new=true)` or `register_pkg("PkgName"; new=false)`.

Otherwise, you may have to specify the specific registry, for which you can follow the instructions [here](https://github.com/GunnarFarneback/LocalRegistry.jl/blob/master/docs/register.md).

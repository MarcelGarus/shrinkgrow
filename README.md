# Shrink.Grow Versioning

## Summary

<!-- TODO: Make interactive. -->

Given a version number `shrink.grow`, increment the:

* `shrink` version if you shrink the API surface
* `grow` version if you grow the API surface

Additionally, you can add labels for pre-releases and build metadata.

## Introduction

When developing software with many dependencies, you need a system to manage changes to those dependencies.
More specifically, you want to keep coupling low: If someone else makes a backwards-compatible change to their code, you should automatically be able to use that.
To be able to automate that dependency upgrade, you need a way to define whether new versions are compatible with the old one or not.

A good way to do that is by looking at the API surface of the dependency: If new methods or optional parameters got added, you can use the version.
If existing method signatures are not supported anymore, or some items got removed, you can't use the package without possibly having to upgrade your code.

The canonical solution to this problem is to use [Semantic Versioning](https://semver.org).

### What are problems of SemVer?

* Whether something is a minor version bump or a patch is sometimes subjective and it *doesn't even matter* when upgrading.  
  With Shrink.Grow Versioning, there are only two numbers, so there's no wiggle room.
* Software is never finished, so many packages are stuck with a 0.x.y version: [0ver.org](https://0ver.org/)  
  This problem occurs, because the version is not simply treated as a machine-readable number useful for automatically updating dependencies and determining compatibility, but *also* for semantic information like "Is this production ready?"
  With Shrink.Grow versioning, these information need to be delivered out-of-band, for example, using a package manager.

## Shortcuts

You can use `shrink` as a shortcut for `shrink.0`.
For example, the version `2` is the same as `2.0`.

## Pre-releases

Optionally, the numbers can be followed by a `-` followed by a dot-separated list of either numbers or strings.
They are considered to be a smaller version than only the numbered version itself.
They are compared using standard number or string comparison, respectively.

A handy property of the tags `alpha`, `beta`, `dogfood`, `fishfood`, `rc` (release candidate) is that they sort well alphabetically:

```
0.1 < 1.0-alpha < 1.0-alpha.1 < 1.0-alpha.2 < 1.0-beta < 1.0-dogfood < 1.0-fishfood < 1.0-rc < 1.0
```

## Build metadata

Optionally, the numbers (and pre-release information) can be followed by a `+` and a build number.
If the number and pre-release is the same, the build number is used for comparison:

```
0.1-alpha+1 < 0.1-alpha+2 < 0.1
```

## Ranges

In some contexts, ranges of versions may be required.

You can write explicit version ranges using `>=version <other-version`.
For example, write `>=1.0 <3.0`.

If by context, it's clear that a version range is expected, you can also simply write one version as a shortcut for the range of the version up to the next `shrink` version bump.
For example, `1.2` is the same as `>=1.2 <2.0` and `3` is the same as `>=3.0 <4.0`.

In a context where a range is expected, you can also write `=version` to fix the dependency to one specific version.

## Examples

```
2.3, 2.1-alpha.2, 49.7-beta.3
```

## Specification

In the following rules, `version` refers to either:

* A version of the form `shrink.grow`
* A version of the form `shrink`, refering to `shrink.0`

The rules:

* `>=version <version2` means any version between `version`, inclusive, and `version2`, exclusive
* `version` means any version between `version` and the next shrink version
* `=version` means exactly the `version`

## Backus-Naur Form Grammar

## Emergent behavior

## FAQ

### Why use numbered versioning at all?

Numbered versioning is useful for automatically upgrading dependencies.

## About

## License

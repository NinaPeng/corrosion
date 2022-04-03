# Unreleased

## Breaking changes

- Removed the integrator build script ([#156](https://github.com/corrosion-rs/corrosion/pull/156)).
  The build script provided by corrosion (for rust code that links in foreign code) is no longer necessary,
  so users can just remove the dependency.

## Deprecations

- Direct usage of the following target properties has been deprecated. The names of the custom properties are
  no longer considered part of the public API and may change in the future. Instead, please use the functions
  provided by corrosion.
  - `CORROSION_FEATURES`, `CORROSION_ALL_FEATURES`, `CORROSION_NO_DEFAULT_FEATURES`. Instead please use
    `corrosion_set_features()`. See the updated Readme for details.
  - `CORROSION_ENVIRONMENT_VARIABLES`. Please use `corrosion_set_env_vars()` instead.
  - `CORROSION_USE_HOST_BUILD`. Please use `corrosion_set_hostbuild()` instead.

## New features

- Add `NO_STD` option to `corrosion_import_crate` ([#154](https://github.com/corrosion-rs/corrosion/pull/154)).

## Fixes

- Improve robustness of parsing the LLVM version (exported in `Rust_LLVM_VERSION`). It now also works for
  Rust versions, where the LLVM version is reported as `MAJOR.MINOR`. ([#148](https://github.com/corrosion-rs/corrosion/pull/148))
- Fix a bug which occurred when Corrosion was added multiple times via `add_subdirectory()` 
  ([#143](https://github.com/corrosion-rs/corrosion/pull/143)).
- Set `CC` and `CXX` environment variables for the invocation of `cargo build` to the compilers selected by CMake
  (if any) ([#138](https://github.com/corrosion-rs/corrosion/pull/138)). This should ensure that C dependencies built
  in cargo buildscripts use the same compiler as CMake built dependencies.
- Fix Ninja-Multiconfig Generator support for CMake versions >= 3.20. Previous CMake versions are missing a feature,
  which prevents us from supporting the Ninja-Multiconfig generator. ([#137](https://github.com/corrosion-rs/corrosion/pull/137))


# 0.1.0 (2022-02-01)

This is the first release of corrosion after it was moved to the new corrosion-rs organization.
Since there are no previous releases, this is not a complete changelog but only lists changes since
September 2021.

## New features
- [Add --profile support for rust >= 1.57](https://github.com/corrosion-rs/corrosion/pull/130):
  Allows users to specify a custom cargo profile with 
  `corrosion_import_crate(... PROFILE <profilename>)`.
- [Add support for specifying per-target Rustflags](https://github.com/corrosion-rs/corrosion/pull/127):
  Rustflags can be added via `corrosion_add_target_rustflags(<target_name> [rustflags1...])`
- [Add `Rust_IS_NIGHTLY` and `Rust_LLVM_VERSION` variables](https://github.com/corrosion-rs/corrosion/pull/123):
  This may be useful if you want to conditionally enabled features when using a nightly toolchain
  or a specific LLVM Version.
- [Let `FindRust` fail gracefully if rustc is not found](https://github.com/corrosion-rs/corrosion/pull/111):
  This allows using `FindRust` in a more general setting (without corrosion).
- [Add support for cargo feature selection](https://github.com/corrosion-rs/corrosion/pull/108):
  See the [README](https://github.com/corrosion-rs/corrosion#cargo-feature-selection) for details on
  how to select features.


## Fixes
- [Fix the cargo-clean target](https://github.com/corrosion-rs/corrosion/pull/129)
- [Fix #84: CorrosionConfig.cmake looks in wrong place for Corrosion::Generator when CMAKE_INSTALL_LIBEXEC is an absolute path](https://github.com/corrosion-rs/corrosion/pull/122/commits/6f29af3ac53917ca2e0638378371e715a18a532d)
- [Fix #116: (Option CORROSION_INSTALL_EXECUTABLE not working)](https://github.com/corrosion-rs/corrosion/commit/97d44018fac1b1a2a7c095288c628f5bbd9b3184)
- [Fix building on Windows with rust >= 1.57](https://github.com/corrosion-rs/corrosion/pull/120)

## Known issues:
- Corrosion is currently not working on macos-11 and newer. See issue [#104](https://github.com/corrosion-rs/corrosion/issues/104).
  Contributions are welcome.
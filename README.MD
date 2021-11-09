# Jolocom DevOps CI test
# KotlinLearningMap
[GITHUB-BADGE](https://github.com/jmk47912204/devops-test/workflows/android-master/badge.svg)

[![Actions Status](https://github.com/jmk47912204/devops-test/workflows/Rust/badge.svg)](https://github.com/jmk47912204/devops-test/actions)

## Description
Create CI, which will run unit tests, build with release configuration, collect platform specific binary libraries and publish them as release artefact.
## Detailed steps
* fork this repository;
* this repository is Rust's `workspace` - should be built like one;
* each step should continue only if previous one succeeded;
* use SHELL script for post-build binaries collection step;
* can use `cargo` based snippet (may require editing), but be careful with double outputs:
```shell
cargo b -q --message-format json | jq -r '
    select (
         .reason == "compiler-artifact"
     ) | select(
         .target.kind | any(
             . == "cdylib"
         )
     ) | .filenames |
     unique | .[]
'
```
* completing this task in any other way, but with desired result is acceptable;
## Extra points (not mandatory)
* add formatter check as first step;
* CI badge[s] in the README;
* auto publish to crates.io;
* CI for different targets [Windows/Linux/MacOS/etc.];

### GL/HF

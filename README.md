# Project Descriptor Buildpack

![Version](https://img.shields.io/badge/dynamic/json?url=https://cnb-registry-api.herokuapp.com/api/v1/buildpacks/sam/project-descriptor&label=Version&query=$.latest.version)

This is a [Cloud Native Buildpack](https://buildpacks.io) that configures an image using a [project descriptor](https://github.com/buildpacks/spec/blob/main/extensions/project-descriptor.md#project-descriptor) file - `project.toml`

## Usage

This buildpack comprises of the following set of buildpacks. You can find more information and usage guide on the respective READMEs of each of the constituent buildpacks.

- [runtime-env-descriptor](https://github.com/samj1912/runtime-env-descriptor-buildpack)
- [label-descriptor](https://github.com/samj1912/label-descriptor-buildpack)
- [proc-descriptor](https://github.com/samj1912/proc-descriptor-buildpack)


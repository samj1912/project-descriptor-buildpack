# Project Descriptor Buildpack

![Version](https://img.shields.io/badge/dynamic/json?url=https://cnb-registry-api.herokuapp.com/api/v1/buildpacks/sam/project-descriptor&label=Version&query=$.latest.version)

This is a [Cloud Native Buildpack](https://buildpacks.io) that configures an image using a [project descriptor](https://github.com/buildpacks/spec/blob/main/extensions/project-descriptor.md#project-descriptor) file - `project.toml`

## Usage

This buildpack comprises of the following set of buildpacks. You can find more information and usage guide on the respective READMEs of each of the constituent buildpacks.

- [runtime-env-descriptor](https://github.com/samj1912/runtime-env-descriptor-buildpack)
- [label-descriptor](https://github.com/samj1912/label-descriptor-buildpack)
- [proc-descriptor](https://github.com/samj1912/proc-descriptor-buildpack)

## Example

For example create a project.toml file with the following content -

```toml
# You can set processes and entrypoints
[[io.buildpacks.processes]]
type = "web"
command = "echo"
args = ["hello"]
direct = true

# You can set processes and entrypoints
# which are invoked via a shell and interpolate
# environment variables
[[io.buildpacks.processes]]
type = "another-echo"
command = "echo"
args = ["$MYVAR"]
direct = false
default = false

# You can configure runtime env vars
[[io.buildpacks.run.env]]
name = "test"
value = "test"
behavior = "override"

# You can configure runtime env vars for specific processes
[[io.buildpacks.run.process-env.another-echo]]
name = "MYVAR"
value = "Hello World!"
behavior = "override"

# You can configure labels
[[io.buildpacks.labels]]
key = "label-name"
value = "<label-value>"
```

Then run - 

```bash
pack build --buildpack sam/project-descriptor myapp
docker run --entrypoint another-echo myapp
docker inspect myapp --format '{{ index .Config.Labels "label-name" }}'

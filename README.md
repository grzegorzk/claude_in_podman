# Claude in Podman

Run **Anthropic Claude Code** (`claude`) within unprivileged Podman container 

Installed directly from https://github.com/anthropics/claude-code

## Why?

 - Extra layer to ensure agent can access / modify / (or damage) what is explicitly exposed

## Requirements

- [Podman](https://podman.io/) (installed and configured)
- GNU Make

## Getting Started

### Build the image

```bash
make build
```

### Add below function at the end of your .bashrc, replace `/path/to/claude_in_podman` with full path where claude_in_podman was cloned to

```bash
function claude {
    claude_dir=/path/to/claude_in_podman
    if [ -z "$1" ]; then
        echo "Call 'claude .' or 'claude /path/to/project'";
    else
        proj_dir=$(cd "$1" && pwd);
        make -C $claude_dir run HOST_PATH_TO_PROJECT="$proj_dir" CONTAINER_PATH_TO_MOUNT_PROJECT="$proj_dir";
    fi;
}
```

Once updated:

```bash
source ~/.bashrc
```

You can then call claude as you would normally do:

```bash
cd path/to/your/project
claude .
```

### You can also run the container manually

```bash
make run HOST_PATH_TO_PROJECT=/path/to/your/project
```

## Configuration

- **`DOCKER`**: Defaults to `podman`.
- **`ARCH_BASE_IMAGE`**: Defaults to `techgk/arch:latest`.

# Thanks

ArchLinux:
* https://archlinux.org/

Podman:
* https://podman.io/

Anthropic:
* https://github.com/anthropics/claude-code

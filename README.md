# actions-use-apt-tools

![actions-use-apt-tools](https://github.com/office-tecoli/actions-use-apt-tools/actions/workflows/test.yml/badge.svg)

This Github action isntall apt packages and cache them for later use.
When executed next time with same package list, and any other
environment are not changed, installed files are extracted from the
cached archive.

Installed file list is taken by `dpkg` command.

When valid cached archive is not found, all packages are installed by
`apt-get` command.  Incremental installation is not supported.

Output is same as [`@actions/cache`](https://github.com/actions/cache).

## Usage

```yaml
# inputs:
#   tools:     { required: true,  type: string }
#   cache:     { required: false, type: string, default: yes }
#   cache-gen: { required: false, type: string, default: v1 }

- uses: office-tecoli/actions-use-apt-tools@v0
  with:

    # apt packages
    tools: ''

    # Cache strategey
    #
    # yes:      activate cache
    # no:       no cache
    # workflow: effective within same workflow (mainly for test)
    #
    cache: yes

    # Cache generation.
    # You can set any string to this parameter and different generation
    # number produces different cache key.
    #
    # Default: v1
    cache-gen: v1
```

## Example

```yaml
- uses: office-tecoli/actions-use-apt-tools@v0
  with:
    tools: bmake
```

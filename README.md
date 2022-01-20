# actions-use-apt-packages

This Github action isntall apt packages and cache them for later use.
When executed next time with same package list, and any other
environment are not changed, installed files are extracted from the
cached archive.

Installed file list is taken by `dpkg` command.

When cached archive is not found, all packages are installed by
`apt-get` command.  Incremental installation is not supported.

## usage

```
# inputs:
#   packages:  { required: true,  type: string }
#   cache:     { required: false, type: string, default: yes }
#   cache_gen: { required: false, type: string, default: v1 }

- uses: office-tecoli/actions-use-apt-packages
  with:

    # apt packages
    packages: ''

    # Cache strategey
    #
    # yes:      activate cache
    # workflow: effective within same workflow (mainly for test)
    #
    # anything else means 'no'
    cache: yes

    #
    # Cache generation.
    # You can set any string to this parameter and different generation
    # number produces different cache key.
    #
    # Default: v1
    cache_gen: v1

```

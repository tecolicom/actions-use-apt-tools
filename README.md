# actions-use-apt-tools

![actions-use-apt-tools](https://github.com/tecolicom/actions-use-apt-tools/actions/workflows/test.yml/badge.svg)

This GitHub action installs Linux APT packages and cache them for later
use.  When executed next time with same package list, and any other
environment are not changed, installed files are extracted from the
cached archive.

When valid cached archive is not found, all packages are installed by
`apt-get` command.  If you want partial install/cache behavior, use
this action multiple times.

There are two different methods to identify installed files.  Default
is **package** method, and files are taken by `dpkg -L` command.  This
method runs very fast.  For packages generate files during
installation, use **timestamp** method, and all files those have newer
timestamp are cached.  Files are searched under /etc,
/usr/{bin,sbin,lib,share} and /var/lib directory.  Search directories
can be given by **path** parameter.

Output is same as [`@actions/cache`](https://github.com/actions/cache).

## Usage

```yaml
# inputs:
#   tools:  { required: true,  type: string }
#   repos:  { required: false, type: string }
#   cache:  { required: false, type: string, default: yes }
#   key:    { required: false, type: string }
#   method: { required: false, type: string, default: package }
#   path:   { required: false, type: string,
#             default: "/etc /usr/bin /usr/sbin /usr/lib /usr/share /var/lib" }

- uses: tecolicom/actions-use-apt-tools@v1
  with:

    # apt packages
    tools: ''

    # additional repositories
    repos: ''

    # Cache strategy
    #
    # yes:      activate cache
    # no:       no cache
    # workflow: effective within same workflow (mainly for test)
    #
    cache: yes

    # Additional cache key
    key: ''

    # Method to idenfity installed files
    #   package:   use "dpkg -L" command output
    #   timestamp: use file's timestamps to check update
    method: package

    # Search path with "timestamp" method
    path: ''
```

## Example

### Normal case with default *package* method

```yaml
- uses: tecolicom/actions-use-apt-tools@v1
  with:
    tools: bmake
```

### Using *timestamp* method

For packages which generates additional files other than included in
package during installation, use *timestamp* method.  If you know
where they will be placed, provide them by a *path* parameter.

```yaml
- uses: tecolicom/actions-use-apt-tools@v1
  with:
    tools: mecab mecab-ipadic mecab-ipadic-utf8
    method: timestamp
```

### With additional repositories

```yaml
      - uses: tecolicom/actions-use-apt-tools@v1
        id: action
        with:
          tools: g++-11
          repos: ppa:ubuntu-toolchain-r/test
          method: timestamp
```

## See Also

### [tecolicom/actions](https://github.com/tecolicom/actions)

### [add-apt-repository](https://manpages.ubuntu.com/manpages/trusty/man1/add-apt-repository.1.html)

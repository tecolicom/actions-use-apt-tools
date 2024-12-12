## v1.5

- read dpkg output and archive only existing files,
  to accommodate the output of the dpkg command in ubuntu-24.04.

## v1.4

- call "apt-get update" before install

## v1.3

- uses actions/cache@v4

## v1.1

- Version 1.1

## v0.5

- use `$GITHUB_OUTPUT`
- use "method" parameter in hash seed

## v0.4

- install-and-{cache,archive} action takes run script

## v0.3

- Rename parameter "directory" to "path".

## v0.2

- Introduce **method** parameter and implement new **timestamp**
  method besides default **package** method.

## v0.1

- Version 0.1 release.

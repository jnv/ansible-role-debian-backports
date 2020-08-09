# Migrating to Newer Versions

## From v0 to v1.0.0

HTTPS transport is used for `backports_uri` by default in Ubuntu. This is supported by default in apt 1.5 which is available in Ubuntu 18.04 and Debian 10.

If you use older versions Ubuntu, you have the following options:

- Use previous version of this role.
- Install `apt-transport-https` and `ca-certificates` apt packages (this is not covered by this role).
- Set `backports_uri` manually to use http: `http://archive.ubuntu.com/ubuntu`.

If, on the other hand, you want to use HTTPS transport in Debian, make sure the `ca-certificates` package is installed (it may be missing e.g. in container) and set `backports_uri` to `https://deb.debian.org/debian`.

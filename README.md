# vfsproxy

Daemon that listens for files to be inserted into the VFS from the
local machine and forwards them to the actual vfsd(s).

vfsproxy listens on a unix socket for stream connections which obey
the following protocol:

`GET [path] [sha1]@[store] [size]\n`

after which the server responds with:

`OK [sha1] [size]\n` 

with the output in the named file, or:

`NO [error]`

if all failed.

The other command is

`PUT [path] [sha1]@[store] [size]\n`

after which the server puts the file named to the backends and
responds with:

`OK [sha1] [size]`

or

`NO [error]`

The possible values for `store` are:

* vfs (or leave blank to default to VFS)
* store$n - cyrus store name, e.g. "store23"


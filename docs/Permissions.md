-   In general, files in the cluster are owned by `vcalhoun` user and
    `trd` group.
-   Data access is controlled by access control list (ACL). To view the
    ACL, use the `getfacl` command.

`[msalman@trendslogin01 ~]$ cd /data/mialab2/`
`[msalman@trendslogin01 mialab2]$ getfacl .`
`# file: .`
`# owner: vcalhoun`
`# group: trd`
`# flags: -s-`
`user::rwx`
`user:jbockholt:rwx`
`user:msalman:rwx`
`user:nlewis26:rwx`
`group::r-x`
`mask::rwx`
`other::r-x`

The above example shows that `/data/mialab2/` is owned by
`vcalhoun:trd`. But `jbockholt`, `msalman` and `nlewis26` also have
read/write/execute (rwx) access to it. Other members of the `trd` group
have read/execute (r-x) permission. If you are the owner of a
directory/file, you can change permissions (using `chmod`) and acl
(using `setfacl`) of it.

The command to set ACL is:

`setfacl -P -m u:`<username>`:rwx `<directory>

`# recursively:`
`setfacl -RP -m u:`<username>`:rwx `<directory>

## Permissions on NFS volumes

`/data/collaboration` and `/data/users2` are NFS volumes.

The command to set permissions to a specific user is:

`nfs4_setfacl -P -a A::`<username>`@rs.gsu.edu:RWX `<directory>

The following will set permissions recursively

`nfs4_setfacl -RP -a A::`<username>`@rs.gsu.edu:RWX `<directory>

To check who has permission:

`nfs4_getfacl `<directory>

It will not show usernames, but an ID number. To know who is the user
with the particular ID, use the following:

`id `<id_number or username>
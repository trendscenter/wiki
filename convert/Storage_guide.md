## Home

-   Home directory is where you log in to.
-   Home directory quota is limited, it is not advisable to put analysis
    data here. Please use `/data/users2/`<your directory> instead.
-   You can `ls ~` from anywhere to quickly switch to the home
    directory. `pwd` will show full path to the current location.

## TReNDS storage

Please limit storing duplicate, temporary and otherwise unnecessary
data. You can check the amount of free/used storage using `df -h`
command.

### Users2 `/data/users2`

TReNDS center members own and can keep their data in
`/data/users/2`<campusID> directory.

### Mialab `/data/mialab2`, Analysis `/data/analysis` & Collaboration `/data/collaboration`

MIALab, collaboration and auto-analysis data are stored here.

### `/trdapps`

Some specific software (which are not available as modules, such as
GIFT) are installed in `/trdapps`.

### `/runjobs`

This is for short-term data, great for working environment such as
moving files during a job, storing data to be used in a job, or storing
generated files from a job. Transfer output and resulting data off
`/runjobs` after job is executed.

### `/raid`

It is a local SSD on DGX machines for fast data transfer.

### `/dev/shm`

You can directly load data on to memory by using
[`/dev/shm`](https://www.cyberciti.biz/tips/what-is-devshm-and-its-practical-usage.html)
for very fast processing. <span style="color:#ff0000">Be very careful
when using because overloading this may destroy the node.</span> It
recommended to reserve a full node when using `/dev/shm` and take
special precautions to prevent out-of-memory errors.
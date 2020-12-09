# xfs filesystem

1. `umount /dev/sdc`

2. Creating XFS filesystem with internal log on the same device

    ```shell script
    # mkfs.xfs /dev/sdc
    meta-data=/dev/sdc               isize=512    agcount=4, agsize=1310720 blks
            =                       sectsz=512   attr=2, projid32bit=1
            =                       crc=1        finobt=0, sparse=0
    data     =                       bsize=4096   blocks=5242880, imaxpct=25
            =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
    log      =internal log           bsize=4096   blocks=2560, version=2
            =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    ```

    The `-f` option forces the overwrite of an existing file system type.

    ```shell script
    # mkfs.xfs -f /dev/sdc
    ```

Reference: `https://www.thegeekdiary.com/how-to-create-an-xfs-filesystem/`

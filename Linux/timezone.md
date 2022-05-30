# Timezone

## How to Check Timezone in Linux

<https://linuxize.com/post/how-to-set-or-change-timezone-in-linux/>

### timedatectl

```shell
$ timedatectl
               Local time: Wed 2022-04-13 11:25:57 CST
           Universal time: Wed 2022-04-13 03:25:57 UTC
                 RTC time: Wed 2022-04-13 03:25:57
                Time zone: Asia/Shanghai (CST, +0800)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

### date

The timezone is CST.

```shell
$ date
Wed 13 Apr 2022 11:26:57 AM CST
```

The timezone is UTC.

```shell
$ date
Wed Apr 13 03:26:54 UTC 2022
```

### localtime

```shell
$ ls -l /etc/localtime
lrwxrwxrwx 1 root root 33 Nov 24 15:50 /etc/localtime -> /usr/share/zoneinfo/Asia/Shanghai
```

## List timezone

```shell
$ timedatectl list-timezones
Africa/Abidjan
Africa/Accra
Africa/Addis_Ababa
Africa/Algiers
Africa/Asmara
Africa/Asmera
Africa/Bamako
Africa/Bangui
Africa/Banjul
Africa/Bissau
Africa/Blantyre
Africa/Brazzaville
Africa/Bujumbura
Africa/Cairo
Africa/Casablanca
Africa/Ceuta
...
```

## Change timezone

America/New_York

```shell
timedatectl set-timezone America/New_York
```

UTC

```shell
timedatectl set-timezone UTC
```

GMT

```shell
timedatectl set-timezone GMT
```

## GMT vs UTC

<https://stackoverflow.com/questions/48942916/what-is-the-difference-between-utc-and-gmt>
<https://24timezones.com/gmt-vs-utc>

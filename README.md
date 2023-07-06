# bash
this is common bash operation


## 1. bash tips

### 1.1 bash basic commands
```bash

# list all installed packages
$ apt list --installed


# update all packages
$ apt update


# unstaill package
$ apt remove percona-xtrabackup-80

# check disk usage
$ df -h

# check all disk whatever it's mount or unmount
$ lsblk

# check last login users
$ last -10

# list file detail order by size
$ ls -lahS

# list ports are listening
# https://www.cyberciti.biz/faq/how-to-check-open-ports-in-linux-using-the-cli/
$ sudo netstat -tulpn | grep LISTEN
# on mac
# https://stackoverflow.com/a/4421674/7163137
$ lsof -i -P | grep LISTEN | grep :$PORT

# install redis-cli in ubuntu
# I. install redis cli
# https://stackoverflow.com/a/25909402/7163137
$ sudo apt-get install redis-tools

# II. connect to redis server
$ sudo redis-cli -h 127.0.0.1 -p 6379
```

### 1.2 mount new add disk in gcp instances
```bash
############################################ mount new blank disk start ############################################
$ sudo su
$ lsblk

# format disk
$ sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb

# mount disk
$ sudo mkdir -p /mnt/disks/mysql
$ sudo mount -o discard,defaults /dev/sdb /mnt/disks/mysql
$ sudo chmod a+w /mnt/disks/mysql


# create auto mount
$ sudo cp /etc/fstab /etc/fstab.backup
$ sudo blkid /dev/sdb
>>/dev/sdb: UUID="af2ec265-0da5-4c9b-9680-f4871f9aa312" TYPE="ext4"

$ vi /etc/fstab
# https://man7.org/linux/man-pages/man5/fstab.5.html
>>UUID=af2ec265-0da5-4c9b-9680-f4871f9aa312 /mnt/disks/mysql ext4 discard,defaults,nofail 0 2

# verify
$ cat /etc/fstab


############################################ mount new blank disk end ############################################
```

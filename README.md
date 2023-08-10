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


# add env variable
$ export AIRFLOW_HOME=~/git/airflow
$ echo $AIRFLOW_HOME
# unset variable
$ unset AIRFLOW_HOME


# add proxy
$ curl -x proxy:port -s -X POST -w "%{http_code}" -o .$$.tmp -H "X-User-ID: $USERID" -H "X-KM-APP-CONTEXT: $PIG_APP_CONTEXT" "$OND_REPORTS_ENDPOINT/pig-job/$1/aggregate"


# exit code 255
# https://docs.platform.sh/development/ssh/troubleshoot-ssh.html#:~:text=While%20trying%20to%20use%20SSH,problem%20with%20your%20SSH%20connection.
While trying to use SSH, you may get a response indicating permission is denied. Or if you get an error with a code of 255, it means there’s a problem with your SSH connection.

# into contianer with root access
# https://stackoverflow.com/a/43043211/7163137
$ docker exec -u root -it <container> bash
$ apt-get update
$ apt-get install vim -y


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

### 1.3 run command in remote server even after logout
```bash
https://stackoverflow.com/a/57293088/7163137

# 1. ssh into server

# 2. open screen session by
$ screen -S sessionname

# 3. Now run your command (background/foreground both works)
$ mysql -h127.0.0.1 -uroot -pauditrecon audit < /mnt/disks/mysql/audit_backup.sql


# 4. now detach to your session by command ctrl+a then press d.
# 5. Now shut your pc and enjoy
# 6. now come back ssh into server then use command screen -x sessionname to reconnect the detached session.
```

### 1.4 zip and unzip
```bash
$ sudo apt-get install zip -y
$ zip -r grafana_setup.zip grafana
$ scp -r runzhou@10.183.161.137:/home/runzhou/grafana_setup.zip  /Users/runzhou/git/argus/gcp_migration/dev52-test-apps-argus/00_DEBUG/20230712_477_upload_script
$ chown -R root:root grafana_setup.zip
$ mv /home/runzhou/rabbitmq.zip /var/cleodaemon
$ unzip rabbitmq.zip
```

### 1.5 get date from timestamp
this will display current machine time
```bash
$ date -r 1688536800
>> Wed Jul  5 14:00:00 CST 2023
```


### 1.6 restart nginx
https://www.cyberciti.biz/faq/nginx-restart-ubuntu-linux-command/
```bash
$ sudo systemctl restart nginx

$ sudo service nginx restart

```

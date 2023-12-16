## exercise

```
:~$ df -h
```

The df command displays the amount of disk space available on the filesystem with each file name's argument

in every linux installation you have to state which partition(with specifying filesystem, size) should be mounted to `/`. and in `/etc/fstab` file you can see that.

on one of the hard disk create MBR partition with xfs format and mount it on fs directory:

```
:~$ gdisk /dev/sdb
...
command (? for help): n  #creates new partition
Partition number (1-128, default 1):
First sector (34-4194270, default = 2048) or
Last sector (2048-4194270, default = 4194270) or
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
...
[Command for help): w
Final checks complete. About to write GPT data.
PARTITIONS! !
Do you want to proceed? (Y/N): y
THIS WILL OVERWRITE EXISTING
0K; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.

:~$ mkfs.xfs /dev/sdb1   #for formatting

:~$ lsblk -f    #for verifying partitioning

:~$ blkid /dev/sdb1  #also for verifying partitioning

:~$ mkdir /fs
:~$ mount /dev/sdb1 /fs
```

when you don’t want to mount every time when system boots you should open fstab file and at  the last line insert

```
[UUID=""] [where should it mount] [type] [mount option] 0 0
```

test it by unmounting and mounting

```
:~$ mount -a
```

you can mount everything in fstab with this command

now you should create some users and put them in a group and only this group can access this folder:

```
:~$ ls -l / | grep fs
drwxr-xr-x 2 rood root 6 30 13:50 fs
```

owner and group of this directory are root also others have read permission!

```
:~$ groupadd fileserver    #creating group
```

every group you create a line were added to `/etc/group` which is :`name-of-goup:x:gid(group id):user1,user2,...` (system works with gid, and x were used to be password for group but now it is deprecated) 

```
:~$ chown :fileserver /fs    #for changing group of fs
:~$ chmod 750 /fs    #so others wont have any permission and group users could read
:~$ gpasswd fileserver -a peyman    #for adding or removing a user from a group
:~$ groups peyman    #for seeing which groups a user is member of
:~$ useradd 
```

`/etc/passwd` is database of linux users, every user has a line dedicated to them: `username:x(used to be password):user-id:gid primary group of user:extra information:home directory:default shell`

<aside>
💡 every user has membership of a group that is primary group for them (only one group could be primary for a user)

when a user creates a file, permission of that comes form umask, owner would be that user, group would be primary group of user

</aside>

<aside>
⚠️ if a shell of user were `/bin/false` or `/usr/sbin/nologin` or anything that does not exist, that user **cannot** login

</aside>

`/etc/shadow` is for storing encrypted password, if instead of password there was a `!` it means that that user doesn’t have a password

<aside>
⚠️ if there was a nothing at password section that user can login without password
`ali::`

</aside>

<aside>
⚠️ if you want to disable a user’s password you add ! at the beginning of hash of password

`usermod mina -L` would do this for you

</aside>

```
:~$ useradd -m -s /bin/bash mina
```

- `-m`: creates home directory
- `-s`: defining which default shell to use

<aside>
💡 if you don’t specify a group for a new user, new group with that name would be created

</aside>

```
:~$ groupadd emp
:~$ useradd -m -s /bin/bash -g emp -G fileserver arash

:~$ passwd arash    #to specify a password for user
```

(use `-g` for primary group and `-G` for other groups)

in /etc/default/useradd you can modify start of user-id, start of group-id, default shell or …

```
:~# mkdir /fs/share
:~# chmode 770 /fs/share/    #in this case fileserver group doesn't have permission
:~# ls -l /fs/
total 0
drwxrwx--- 2 root root 6 Jul 30 14:22 share
:~# chmod 1777 /fs/share/     #now only fileserver group have permission, 1 for stickt bit

:~# mkdir /fs/download
:~# chmod 755 /fs/download/

:~# mkdir /fs/users
:~# mkdir /fs/users/mina
:~# mkdir /fs/users/arash
:~# mkdir /fs/users/peyman
:~# chmod 700 /fs/users/*
:~# ls -l /fs/users/
total 0
drwx------ 2 root root 6 Jul 30 14:31 arash
drwx------ 2 root root 6 Jul 30 14:31 mina
drwx------ 2 root root 6 Jut 30 14:31 peyman
:~# chown mina: /fs/users/mina
:~# chown arash: /fs/users/arash
:~# chown peyman: /fs/users/peyman

:~# ls -l /fs/users/
total e
drwx------ 2 arash  emp    6 Jul 30 14:31 arash
drwx------ 2 mina   mina   6 Jul 30 14:31 mina
drwx------ 2 peyman peyman 6 Jul 30 14:31 peyman
```

`:~# chown mina: /fs/users/mina` in this command mina: means that the primary group of user would be a group of that directory

if you don’t what other users to see other users directory, don’t permit read to others like:

```
:/fs/users# chmod 751 .
mina@s7:/fs$ ls users/
ls: cannot open directory 'users/': Permission denied
mina@s7:/fs/users$ cd mina
```

modify a user by `usermod`

delete a user by `userdel -r` -r to delete home directory

modify a group by `groupmod`

delete a group by `groupmod`

remove a user from a group `gpasswd -d`

### SFTP (ssh file transfer protocol)

scp [source] [destination]

```
scp -P 10007 Desktop/nima_python/geoip.py mina@Lpic1.Lab.gandotech.com:/fs/share
```

or

```
scp -P 10007 mina@Lpic1.Lab.gandotech.com:/fs/share/geoip.py .
```

- for uploading directory use `-r`
- proxy command
    
    some commands may have several forms that does the same job like `mkfs -t ext4` = `mkfs.ext4`
    

### installing a package from a source code

when you install any packages by any kind of methods you have 2 things happen: 1-every file of package copies of system and 2-it will be recorded in a database that you can get a query of that (if there were not a database you will lose the track of installed packages)

![[Untitled.png]]
for building an application, first thing is to have a compiler like gcc or GNU-make. developer with GNU-make creates a Makefile and we use `make` to compile the application the custom wey we want

configh.sh → execute with desired parameters → Makefile → make

every thing you need to compile an application are inside `build-essential` package

![[Untitled 1.png]]
for example we install SSHPass:

```
git clone git://github.com/kevinburke/sshpass.git
cd sshpass
./configure
make
apt install automake
which automake-1.16
cd /usr/bin/
ln -s automake-1.16 automake-1.15    #to create a symbolic-link(trick)
automake --add-missing
make
make install    #copy isntalled package to PATH
```

<aside>
💡 127.0.0.1 or loopback is services that server and client are at the same machine

</aside>

<aside>
👀 with `alien` you can convert `.pkg` to `.rpm`

</aside>

```
:~$ apt clean
```

to delete all archive debian binary files

```
:~$ dpkg -S [path of a file]
```

to find out which package does that file belong

inode have every thing of a file(true location of file on disk) with `ls -i` you can see the inode number 

**hard link**: A hard link always points a filename to data on a storage device. ****for example there is a on file that has two links. there is no cross-partition. cannot link to a directory. command for hard link is: `ln /etc/foo /tmp/bar`

**soft link(symbolic link)**: A soft link always points a filename to another filename, which then points to information on a storage device. you can have cross-partition and link to a directory. command for soft link is: `ln -s /fs/users /tmp/share`

![[Untitled 2.png]]
ssh port forwarding:
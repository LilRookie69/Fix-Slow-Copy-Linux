# Fix-Stack-and-Slow-Copy-Speed-Linux

Troubleshooting stuck slow copy di linux, i think it can be done on any distro, without any further ado, here it is

*do it with super user previledges*

## Step 1 - Check the /etc/rc.local
```
root@rpc-ubuntu18:/home/rdanang# file /etc/rc.local
```
if you get output like this, it means you dont have it
```
/etc/rc.local: cannot open `/etc/rc.local' (No such file or directory)
```
## Step 2 - Create the /etc/rc.local (you can skip it, if u already have it)
```
root@rpc-ubuntu18:/home/rdanang# echo "#!/bin/bash" > /etc/rc.local
root@rpc-ubuntu18:/home/rdanang# echo "/usr/bin/garbd --cfg /etc/garbd.conf &" > /etc/rc.local
root@rpc-ubuntu18:/home/rdanang# echo "exit 0" >> /etc/rc.local
root@rpc-ubuntu18:/home/rdanang# chmod 755 /etc/rc.local
```

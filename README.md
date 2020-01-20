# Fix-Stack-and-Slow-Copy-Speed-Linux

Troubleshooting stuck slow copy di linux, i think it can be done on any distro, without any further ado, here it is

*do it with super user previledges*

## Step 1 - Check the /etc/rc.local
Check the if you have the rc.local
```
root@rpc-ubuntu18:/home/rdanang# file /etc/rc.local
```
if you get output like this, it means you dont have it
```
/etc/rc.local: cannot open `/etc/rc.local' (No such file or directory)
```
## Step 2 - Create the /etc/rc.local (you can skip it, if u already have it)
you can make it with nano or any of your favorite editor
```
root@rpc-ubuntu18:/home/rdanang# nano /etc/rc.local
```
and paste this code
```
#!/bin/bash
/usr/bin/garbd --cfg /etc/garbd.conf &
exit 0
```
## Step 3 - change the permission with chmod 
change the permission 
```
root@rpc-ubuntu18:/home/rdanang# chmod 755 /etc/rc.local
root@rpc-ubuntu18:/home/rdanang# chmod +x /etc/rc.local
```
## Step 4 - Start and see status of the service
```
root@rpc-ubuntu18:/home/rdanang# systemctl start rc-local
root@rpc-ubuntu18:/home/rdanang# systemctl status rc-local
```
## Step5 - change the dirty_bytes and the dirty_background_bytes
```
root@rpc-ubuntu18:/home/rdanang# echo $((64*1024*1024)) > /proc/sys/vm/dirty_background_bytes
root@rpc-ubuntu18:/home/rdanang# echo $((192*1024*1024)) > /proc/sys/vm/dirty_bytes
```

## Step5 - restart
```
root@rpc-ubuntu18:/home/rdanang# systemctl restart rc-local
root@rpc-ubuntu18:/home/rdanang# systemctl reboot
```

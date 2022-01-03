Now, let’s see how to increase the swap file. First thing first, make sure that you have a swap file in your system.

swapon --show
It will show the current swap available. If you see the type file, it indicates that you are using a swap file.

swapon --show
NAME      TYPE SIZE USED PRIO
/swapfile file   2G   0B   -2
Now before you resize the swap file, you should turn the swap off. You should also make sure that you have enough free RAM available to take the data from swap file. Otherwise, create a temporary swap file.

You can disable a given swap file using this command. The command doesn’t produce any output and it may take a few minutes to complete:

sudo swapoff /swapfile
Now use the fallocate command in Linux to change the size of the swap file.

sudo fallocate -l 4G /swapfile
Make sure that you mark this file as swap file:

sudo mkswap /swapfile
You should see an output like this where it warns you that old swap signature is being wiped out.

sudo mkswap /swapfile
mkswap: /swapfile: warning: wiping old swap signature.
Setting up swapspace version 1, size = 4 GiB (4294967296 bytes)
no label, UUID=c50b27b0-a530-4dd0-9377-aa28eabf3957
Once you do that, enable the swap file:

sudo swapon /swapfile
That’s it. You just increased the swap size in Ubuntu from 2 GB to 4 GB. You can check swap size using the free command or the swapon --show command.

free -h
              total        used        free      shared  buff/cache   available
Mem:           7.7G        873M        5.8G        265M        1.0G        6.3G
Swap:          4.0G          0B        4.0G
You see how easy it is to resize swap size thanks to the swap files. You didn’t touch the partition, you didn’t reboot the system. Everything was done on the fly. How cool is that!

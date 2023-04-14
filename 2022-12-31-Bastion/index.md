---
layout: default
---

# Bastion

![](./01.png)

Home, home cyber range

Where geeks and enthusiasts play

Where seldom is heard a discouraging word

And ```nmap``` results are read-ay

![](./02.png)

If we look at SMB, we see that there's a share available called ```Backups```.

![](./03.png)

Let's attempt to connect to it with the guest account.

![](./04.png)

Inside is a file called ```note.txt```, so let's snag that real fast.

![](./05.png)

If we look at the contents, it's a note to sysadmins for backups.  We'll store that for later, in case we need it.

![](./06.png)

Let's now take a look through the folder ```WindowsImageBackup``` to see if we can find anything useful.

![](./07.png)

Let's mount the the SMB share.

![](./08.png)

Now let's mount the larger of the two VHD files, as the smaller is the boot partition.

![](./09.png)

Let's see if we can now browse the .vhd file.

![](./10.png)

If we browse to ```Windows/System32/Config``` we can copy the ```SAM```, ```SYSTEM```, and ```SECURITY``` files.

From there we can dump the user hash using ```secretsdump.py```.

![](./11.png)

Now that we have L4mpje's password, let's attempt to login to SSH with it.

![](./12.png)

Let's grab the user flag real fast.

![](./13.png)

Now let's see what we can do to escalate our privileges.

First, let's run ```systeminfo``` to see what we have going on.

![](./14.png)

It would appear that L4mpje has some restricted rights.

Let's run a ```whoami /priv``` to see what's going on there.

![](./15.png)

Well, not much to work with.  Let's upload a copy of winPEAS and see if we can run that.

![](./16.png)

Looks like ```certutil``` is blocked as well.  So we'll have to get the file another way.

![](./17.png)

![](./18.png)

Trying to run winPEAS will hang the session, so we'll have to keep an eye on the ```maybe.txt``` file to see if it grows in size.

![](./19.png)

Looks to be working.  However, we have no way of know when exactly it will be done.  So we'll possibly have to grab a few copies of the file.

![](./20.png)

![](./21.png)

![](./22.png)

It worked, but it's a little hard to read at first.  If you know that the color red is written as ```1;31m```, then you can search for that to find any items that would normally be red in winPEAS.

The results of winPEAS weren't particularly useful, so let's manually browse through directories.

If we go to ```Program Files (x86)``` we see an application called ```mRemoteNG```.

![](./23.png)

If we look at the ```Readme.txt``` file in ```mRemoteNG```, it says that it's used for storing remote login credentials.

![](./24.png)

Let's dig through this directory and see if we can figure out where mRemoteNG stores the credentials.

If we look online we find that credentials are stored in ```%APPDATA%\mRemoteNG\confCons.xml```.

![](./25.png)

If we look at ```confCons.xml``` we see the Administrator account stored for RDP with the password encoded as base64.

![](./26.png)

However, if we attempt to decode the base64, we get unicode characters back.  Looking online, it seems that there is a tool specifically for decrypting mRemoteNG passwods.  (https://github.com/gquere/mRemoteNG_password_decrypt)

Let's clone that repo and copy the ```confCons.xml``` file to our local machine.

First, let's toss it in an easier spot to grab with SCP.

![](./27.png)

Then copy it over.

![](./28.png)

![](./29.png)

Now that we have the Administrator password, let's log back in via SSH and go get the flag.

![](./30.png)

See you in the next box.
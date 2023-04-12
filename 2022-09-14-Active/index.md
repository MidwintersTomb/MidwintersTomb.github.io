---
layout: default
---

# Active

![](./01.png)

Here I go again on my own!  Gonna ```nmap``` this from my office in my home!

![](./02.png)

Okay, looking at the resutls, let's enumerate SMB.

![](./03.png)

The ```Replication``` share has anonymous access.  Let's access it with ```smbclient```.

![](./04.png)

Let's turn off prompting and enable recursive listing.

![](./05.png)

With that done, let's list files in the directory.

![](./06.png)

Now we'll download all the files with ```mget *```.

![](./07.png)

If we search the files downloaded, we can find ```Groups.xml```, which may contain GPP (Group Policy Preferences).

![](./08.png)

Looking at the file contents, it contains the domain Ticket Granting Service account (```active.htb\SVC_TGS```) and the ```cPassword```.

![](./09.png)

We can now use ```gpp-decrypt``` to decrypt the ```cPassword```.

![](./10.png)

Now to verify the credentials are working when passed with ```crackmapexec```.

![](./11.png)

That looks good, now let's get SPNs with ```GetUserSPNs.py```

![](./12.png)

We'll now copy the entire hash into ```hashcat``` and crack the hash.

![](./13.png)

Let's now use ```psexec.py``` to spawn a shell using our newly acquired credentials.

![](./14.png)

With our shell, let's collect the flags.

![](./15.png)

And we're done!
---
layout: default
---

# Chatterbox

![](./01.png)

I clap, you clap, we all clap for ```nmap```.

![](./02.png)

Looking at the results we have something we haven't seen before.  So let's search for AChat exploits.  (In this case, we're using https://github.com/mpgn/AChat-Reverse-TCP-Exploit)

Let's ```git clone``` the repo to our ```/opt``` directory.

![](./03.png)

To avoid using metasploit, and use a ```netcat``` listener instead, we must edit the ```AChat_Payload.sh``` file before running it:

![](./04.png)

Now, let's generate the payload.

![](./05.png)


We'll now copy the payload into ```AChat_Exploit.py```, followed by editting the server address:

![](./06.png)

Next we'll get our ```netcat``` listener setup.

![](./07.png)

Lastly, we'll launch the exploit.

![](./08.png)

Let's check our listener.

![](./09.png)

Looks good, let's grab the user flag.

![](./10.png)

Let's check if there's an autologon account on this system with ```reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"```.

![](./11.png)

Looks like we have Alfred's password now, let's keep that in mind, in case we need it later.

Let's run ```netstat -ano``` to see what all is listening on the server.

![](./12.png)

We don't see anything too interesting that's only on the inside that we didn't already see on the outside.

Let's see if Alfred is a lazy admin and reusing the password for the administrator account.  We'll attempt to browse to the SMB share.

![](./13.png)

Looks like that is indeed the case.

![](./14.png)

Let's go grab that root flag and call it a day.

![](./15.png)

![](./16.png)

And with that, we're done another box.
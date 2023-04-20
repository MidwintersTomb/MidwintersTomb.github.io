---
layout: default
---

# Blue

We're working on the machine "Blue" on Hack the Box.

![](./01.png)

Let's start with running ```nmap``` against the box.

![](./02.png)

![](./03.png)

Being that SMB is open and this machine is called "Blue," one can assume that it's probably vulnerable to Eternal Blue.

Let's go out to Google to find an Eternal Blue exploit on GitHub.  In this case we're going to use [https://github.com/worawit/MS17-010](https://github.com/worawit/MS17-010).

Now, let's clone a copy of it to our ```/opt``` directory (I'm storing it under a folder for SMB attacks, but, sort how you see fit, go wild).

![](./04.png)

Let's run the checker against the target to see if it's vulnerable to Eternal Blue.

![](./05.png)

Like we figured, it is.

Next we're going to need to take the Eternal Blue assembly shellcode and output it as a bin file.

![](./06.png)

We'll then use msfvenom to create a Windows reverse shell (being that it's Windows 7, there's a decent likelihood that it's a 64-bit install, though always keep that in mind).

We're going to want to output is a raw bin file also.

![](./07.png)

Now that we have both bin files we can merge the ```kernel.bin``` and ```shell.bin``` files into a single ```exploit.bin``` file by using ```cat``` to append ```shell.bin``` to the end of ```kernel.bin```.

![](./08.png)

Now that we have our exploit all ready to go, let's start up a ```netcat``` listener.

![](./09.png)

With the listener keeping a digital ear out, let's kick off the exploit.

![](./10.png)

All looks to have completed, let's check the status of our listener.

![](./11.png)

We'll now check the ```C:\Users``` directory to see where each flag will live.

![](./12.png)

Let's grab the user flag.

![](./13.png)

And lastly, the root flag.

![](./14.png)

Another box down, and we're moving on.

___

Findings

___

**Operating System:** Windows 7 Service Pack 1

**IP Address:** 10.10.10.40

**Open Ports:**
- 135
- 139
- 445
- 49152
- 49153
- 49154
- 49155
- 49156
- 49157

**Services Responding:**
- RPC
- SMB

**Vulnerabilities Exploited:**
- MS17-010

**Configuration Insecurities:**
- None detected in process of exploitation

**General Findings:**
- Consider replacing Windows 7 Service Pack 1 due to end of support
  - If not able to be replaced, consider installing all missing patches to limit attack surface
  - If not able to be replaced or patched, consider disabling SMBv1
  - If not able to be replaced or patched, consider restricting ports further

___

[Back](../)

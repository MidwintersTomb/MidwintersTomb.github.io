---
layout: default
---

# Optimum

![](./01.png)

```nmap``` go brrr.

![](./02.png)

Looks like the only port we have open is ```80``` which is running HttpFileServer httpd 2.3.

Let's take a look at the web interface.

![](./03.png)

Looks like a pretty simple page, so let's search for a httpfileserver 2.3 exploit.  We're going to use [https://www.exploit-db.com/exploits/39161](https://www.exploit-db.com/exploits/39161).

We'll have to edit the python file to add in our IP and port for our listener.

![](./04.png)

Once we have that saved, we will need to start our listener.

![](./05.png)

Now let's run ```hfsexploit.py``` against the target machine.

![](./06.png)

Let's check our listener to see if we got a connection.

![](./07.png)

Looks good, let's run ```systeminfo``` to learn a bit more about this box.

![](./08.png)

Let's run a search for exploits on GitHub for Server 2012 R2 6.3 Build 9600.

We see that MS16-032 comes back, however, it is not exploitable due to having only one CPU.

If we look a bit further, we find that it should also be vulnerable to MS16-098.  We'll download [https://github.com/SecWiki/windows-kernel-exploits/tree/master/MS16-098](https://github.com/SecWiki/windows-kernel-exploits/tree/master/MS16-098) for our purposes.

We are going to serve up ```bfill.exe``` using a python HTTP server.

![](./09.png)

Let's check in a browser to verify it's working.

![](./10.png)

Now let's download ```bfill.exe``` to the server using ```certutil```.

![](./11.png)

Before we run the exploit, let's go grab the user flag.

![](./12.png)

Now that the file is downloaded, and we have the user flag, let's run the exploit.

![](./13.png)

Looks like it was successful.  Now we'll go pick up the root flag.

![](./14.png)

Catch you in the next box.

___

Findings

___

**Operating System:** Windows Server 2012 R2 Standard

**IP Address:** 10.10.10.8

**Open Ports:**
- 80

**Services Responding:**
- HTTP

**Vulnerabilities Exploited:**
- CVE-2014-6287
- MS16-098

**Configuration Insecurities:**
- None detected in process of exploitation

**General Findings:**
- Consider updating HttpFileServer to HFS3 v0.43.0
- Consider installing all missing operating system patches to reduce attack surface

___

[Back](../)

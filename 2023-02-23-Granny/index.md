---
layout: default
---

# Granny

![](./01.png)

By now you know where this is going, of course it's ```nmap```.

![](./02.png)

If we look at the results, it seems that this is basically [Grandpa](../2021-06-15-Grandpa/).

We already have the IIS6 exploit for CVE-2017-7269 downloaded, but if we didn't have it, we could get it here: [https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269](https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269)

We'll setup a listener and kick off the exploit.

![](./03.png)

Let's check our listener to make sure it went through.

![](./04.png)

Let's run ```systeminfo``` to get some details.

![](./05.png)

And now ```whoami /priv``` to check our privileges.

![](./06.png)

Since we have the ```SeImpersonatePrivilege``` privilege, we'll go the Churrasco route again.

We'll make a temp folder to run it from.

![](./07.png)

Now, if we didn't already have Churrasco, we could download it from [https://github.com/Re4son/Churrasco/raw/master/churrasco.exe](https://github.com/Re4son/Churrasco/raw/master/churrasco.exe).

Now we'll share ```churrasco.exe``` and ```nc.exe``` via SMB.

![](./08.png)

Now we'll mount the share and copy both to the temp folder.

![](./09.png)

We'll now create batch file to create the reverse shell.

![](./10.png)

Next we'll start a listener and then run ```churrasco.exe``` with our batch file.

![](./11.png)

Let's check our listener.

![](./12.png)

Now that we're root, let's grab the flags.

![](./13.png)

See you in the next box.

___

Findings

___

**Operating System:** Windows Server 2003 Standard

**IP Address:** 10.10.10.15

**Open Ports:**
- 80

**Services Responding:**
- HTTP

**Vulnerabilities Exploited:**
- CVE-2017-7269
- MS09-012

**Configuration Insecurities:**
- IIS web server with WebDAV enabled

**General Findings:**
- Consider replacing Windows Server 2003 due to end of support
  - If unable to be replaced, consider installing all missing patches to reduce attack surface
  - If unable to be replaced, WebDAV should be disabled if not in use

___

[Back](../)

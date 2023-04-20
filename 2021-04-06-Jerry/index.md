---
layout: default
---

# Jerry

Hi there, Jerry, are you ready?

![](./01.png)

Let's go ```nmap```!

![](./02.png)

It seems we have a website running on port ```8080```.  Let's take a look.

![](./03.png)

Looks like an Apache Tomcat administration page.

Let's click on Manager App.

![](./04.png)

We get prompted for credentials we don't have, so let's hit cancel.

![](./05.png)

The 401 Unauthorized page gives us the username and password if configuration hasn't be changed.  So let's refresh and try it again.

![](./06.png)

Looks like that was successful.

We also have a section to deploy a ```.WAR``` file from our own machine.

![](./07.png)

Let's use ```msfvenom``` to generate a Java reverse shell as a ```.WAR``` file.

![](./08.png)

We'll then click on "Browse..." and select the file we created.

![](./09.png)

Now let's set up a ```netcat``` listener.

![](./10.png)

Once that's done, we'll deploy our ```.WAR``` file, which now shows up as an application in the list.

![](./11.png)

Let's check out our listener to see if it worked, as well as to see who are.

![](./12.png)

Looks like we're the system account.  Let's go pick up the flags.

![](./13.png)

If we look in the usual location, it seems we have a directory called ```flags``` which contains a file called ```2 for the price of 1.txt```.

Let's take a look in that file and see if it contains both flags.

![](./14.png)

Looks like that's the case, and this box is done.

___

Findings

___

**Operating System:** Windows Server 2012 R2 Standard

**IP Address:** 10.10.10.95

**Open Ports:**
- 8080

**Services Responding:**
- HTTP

**Vulnerabilities Exploited:**
- Weak authentication
- Service running as elevated account

**Configuration Insecurities:**
- Apache configuration exposed
- Apache configuration using default administrator credentials
- Apache web service running as NT Authority\System

**General Findings:**
- Consider restricting access to Apache configuration page
- Consider strengthening authentication scheme for Apache
- Consider running Apache as a limited service account

___

[Back](../)

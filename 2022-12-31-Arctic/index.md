---
layout: default
---

# Arctic

![](./01.png)

Pssst... Hey... You got any of that ```nmap```?

![](./02.png)

Port ```8500``` in the results thinks it's ftmp based on port number, however, it's not confirmed.  Let's try opening it in a web browser.

![](./03.png)

Based on the CF in each folder, it looks like it's probably a ColdFusion server.

If we go into ```CFIDE``` and then ```Administrator```, we can confirm this.

![](./04.png)

It is an Adobe ColdFusion 8 server.

If we run ```searchsploit``` for ColdFusion, we see that there's a remote code execution python script for ColdFusion 8.

![](./05.png)

Let's copy that python script over to our current directory.

![](./06.png)

Let's edit the python script to specify our IP, the server's IP, and the appropriate ports.

![](./07.png)

Now, let's run the script.

![](./08.png)

![](./09.png)

Let's grab the user flag before we move on to escalation.

![](./10.png)

Let's run ```systeminfo``` to see what we can learn about this box.

![](./11.png)

Let's copy the contents of ```systeminfo``` to a text file and use Windows Exploit Suggester.

![](./12.png)

We see that there's a kernel exploit that can potentially elevate privileges.

![](./13.png)

We've seen this before.  Let's browse out to https://github.com/SecWiki/windows-kernel-exploits/tree/master/MS10-059, download the executable, and copy it over to our victim.

![](./14.png)

![](./15.png)

Now let's grab the root flag.

![](./16.png)

See you in the next box.

___

[Back](../)

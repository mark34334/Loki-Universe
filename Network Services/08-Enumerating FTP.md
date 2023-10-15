----
**Lets Get Started**

Before we begin, make sure to deploy the room and give it some time to boot. Please be aware, this can take up to five minutes so be patient!

**![](https://cdn4.iconfinder.com/data/icons/database-and-server-pixel-prefect-set-3/80/network__computer__connection__sharing_-512.png)Enumeration**

By now, I don't think I need to explain any further how enumeration is key when attacking network services and protocols. You should, by now, have enough experience with **nmap** to be able to port scan effectively. If you get stuck using any tool\- you can always use **"tool \[\-h / \-help / \-\-help\]"** to find out more about it's function and syntax. Equally, man pages are extremely useful for this purpose. They can be reached using **"man \[tool\]"**.

**Method**

We're going to be exploiting an anonymous FTP login, to see what files we can access\- and if they contain any information that might allow us to pop a shell on the system. This is a common pathway in CTF challenges, and mimics a real\-life careless implementation of FTP servers.

**Resources**

As we're going to be logging in to an FTP server, we will need to make sure an FTP client is installed on the system. There should be one installed by default on most Linux operating systems, such as Kali or Parrot OS. You can test if there is one by typing "ftp" into the console. If you're brought to a prompt that says: "ftp>", then you have a working FTP client on your system. If not, it's a simple matter of using "sudo apt install ftp" to install one.

**Alternative Enumeration Methods**

It's worth noting  that some vulnerable versions of in.ftpd and some other FTP server variants return different responses to the "cwd" command for home directories which exist and those that don’t. This can be exploited because you can issue cwd commands before authentication, and if there's a home directory\- there is more than likely a user account to go with it. While this bug is found mainly within legacy systems, it's worth knowing about, as a way to exploit FTP.

This vulnerability is documented at: [https://www.exploit\-db.com/exploits/20745](https://www.exploit-db.com/exploits/20745)

Now we understand our toolbox, let's do this.

Answer the questions below

Run an **nmap** scan of your choice.

How many **ports** are open on the target machine?


----

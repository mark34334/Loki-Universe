
Time to turn things up another notch!

Client\-side filters are easy to bypass \-\- you can see the code for them, even if it's been obfuscated and needs processed before you can read it; but what happens when you *can't* see or manipulate the code? Well, that's a server\-side filter. In short, we have to perform a lot of testing to build up an idea of what is or is not allowed through the filter, then gradually put together a payload which conforms to the restrictions.

For the first part of this task we'll take a look at a website that's using a blacklist for file extensions as a server side filter. There are a variety of different ways that this could be coded, and the bypass we use is dependent on that. In the real world we wouldn't be able to see the code for this, but for this example, it will be included here:

`<?php
    //Get the extension
    $extension = pathinfo($_FILES["fileToUpload"]["name"])["extension"];
    //Check the extension against the blacklist -- .php and .phtml
    switch($extension){
        case "php":
        case "phtml":
        case NULL:
            $uploadFail = True;
            break;
        default:
            $uploadFail = False;
    }
?>
`

In this instance, the code is looking for the last period (`.`) in the file name and uses that to confirm the extension, so that is what we'll be trying to bypass here. Other ways the code could be working include: searching for the first period in the file name, or splitting the file name at each period and checking to see if any blacklisted extensions show up. We'll cover this latter case later on, but in the meantime, let's focus on the code we've got here.

We can see that the code is filtering out the `.php` and `.phtml` extensions, so if we want to upload a PHP script we're going to have to find another extension. The [wikipedia page](https://en.wikipedia.org/wiki/PHP) for PHP gives us a few common extensions that we can try; however, there are actually a variety of other more rarely used extensions available that webservers may nonetheless still recognise. These include: `.php3`, `.php4`, `.php5`, `.php7`, `.phps`, `.php-s`, `.pht` and `.phar`. Many of these bypass the filter (which only blocks`.php` and `.phtml`), but it appears that the server is configured not to recognise them as PHP files, as in the below example:

![](https://i.imgur.com/yzOGVob.png)

This is actually the default for Apache2 servers, at the time of writing; however, the sysadmin may have changed the default configuration (or the server may be out of date), so it's well worth trying.

Eventually we find that the `.phar` extension bypasses the filter \-\- and works \-\- thus giving us our shell:

![](https://i.imgur.com/Aigaz4R.png)

---

Let's have a look at another example, with a different filter. This time we'll do it completely black\-box: i.e. without the source code.

Once again, we have our upload form:

![](https://i.imgur.com/STsI51E.png)

Ok, we'll start by scoping this out with a completely legitimate upload. Let's try uploading the `spaniel.jpg` image from before:

![](https://i.imgur.com/tp6T2WH.png)

Well, that tells us that JPEGS are accepted at least. Let's go for one that we can be pretty sure will be rejected (`shell.php`):

![](https://i.imgur.com/hk4inJ2.png)

Can't say that was unexpected.

From here we enumerate further, trying the techniques from above and just generally trying to get an idea of what the filter will accept or reject.

In this case we find that there are no shell extensions that both execute, and are not filtered, so it's back to the drawing board.

In the previous example we saw that the code was using the `pathinfo()` PHP function to get the last few characters after the `.`, but what happens if it filters the input slightly differently?

Let's try uploading a file called `shell.jpg.php`. We already know that JPEG files are accepted, so what if the filter is just checking to see if the `.jpg` file extension is somewhere within the input?

Pseudocode for this kind of filter may look something like this:

`ACCEPT FILE FROM THE USER -- SAVE FILENAME IN VARIABLE userInput
IF STRING ".jpg" IS IN VARIABLE userInput:
    SAVE THE FILE
ELSE:
    RETURN ERROR MESSAGE
`

When we try to upload our file we get a success message. Navigating to the `/uploads` directory confirms that the payload was successfully uploaded:

![](https://i.imgur.com/K55eu9o.png)

Activating it, we receive our shell:

![](https://i.imgur.com/VVAKZfw.png)

---

This is by no means an exhaustive list of upload vulnerabilities related to file extensions. As with everything in hacking, we are looking to exploit flaws in code that others have written; this code may very well be uniquely written for the task at hand. This is the really important point to take away from this task: there are a million different ways to implement the same feature when it comes to programming \-\- your exploitation must be tailored to the filter at hand. The key to bypassing any kind of server side filter is to enumerate and see what is allowed, as well as what is blocked; then try to craft a payload which can pass the criteria the filter is looking for.

---

Now your turn. You know the drill by now \-\- figure out and bypass the filter to upload and activate a shell. Your flag is in `/var/www/`. The site you're accessing is `annex.uploadvulns.thm`.

Be aware that this task has also implemented a randomised naming scheme for the first time. For now you shouldn't have any trouble finding your shell, but be aware that directories will not always be indexable...

Answer the questions below

What is the flag in /var/www/?
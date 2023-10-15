When files are uploaded to the server, a range of checks should be carried out to ensure that the file will not overwrite anything which already exists on the server. Common practice is to assign the file with a new name -- often either random, or with the date and time of upload added to the start or end of the original filename. Alternatively, checks may be applied to see if the filename already exists on the server; if a file with the same name already exists then the server will return an error message asking the user to pick a different file name. File permissions also come into play when protecting existing files from being overwritten. Web pages, for example, should not be writeable to the web user, thus preventing them from being overwritten with a malicious version uploaded by an attacker.  

If, however, no such precautions are taken, then we might potentially be able to overwrite existing files on the server. Realistically speaking, the chances are that file permissions on the server will prevent this from being a serious vulnerability. That said, it could still be quite the nuisance, and is worth keeping an eye out for in a pentest or bug hunting environment.  

Let's go through an example before you try this for yourself.

### ❗❗ Warning ❗❗  

_Please note that_ `demo.uploadvulns.thm` _will be used for all demonstrations; however, **this site is not available in the uploaded VM**. It is purely for demonstrative purposes._

_Attempts to access this subdomain will have amusing consequences... you have been warned.  
_

In the following image we have a web page with an upload form:

![](https://i.imgur.com/7KmsrTW.png)

You may need to enumerate more than this for a real challenge; however, in this instance, let's just take a look at the source code of the page:

![](https://i.imgur.com/BeqAZ3s.png)

Inside the red box, we see the code that's responsible for displaying the image that we saw on the page. It's being sourced from a file called "spaniel.jpg", inside a directory called "images".

Now we know where the image is being pulled from -- can we overwrite it?

Let's download another image from the internet and call it `spaniel.jpg`. We'll then upload it to the site and see if we can overwrite the existing image:

![](https://i.imgur.com/8PiIuiu.png)

![](https://i.imgur.com/TIoA2DR.png)

And our attack was successful! We managed to overwrite the original `images/spaniel.jpg` with our own copy.  

---

Now, let's put this into practice.

Open your web browser and navigate to `overwrite.uploadvulns.thm`. Your goal is to overwrite a file on the server with an upload of your own.  



Answer the questions below

What is the name of the image file which can be overwritten?

Overwrite the image. What is the flag you receive?
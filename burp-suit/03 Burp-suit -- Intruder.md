#burp-suit #burp-suit/intruder 

---

***What is intruder?***

Intruder allows us to automate requests, which is very useful when fuzzing or bruteforcing. We will be looking at how to use Intruder to perform both of these functions in conjunction with the other tools we have already covered.


![[Pasted image 20230622102750.png]]

Intruder is Burp Suite's in-built fuzzing tool. It allows us to take a request (usually captured in the Proxy before being passed into Intruder) and use it as a template to send many more requests with slightly altered values automatically.

There are four other Intruder sub-tabs:

- **Positions** allows us to select an Attack Type (we will cover these in an upcoming task), as well as configure where in the request template we wish to insert our payloads.  
    
- **Payloads** allows us to select values to insert into each of the positions we defined in the previous sub-tab. For example, we may choose to load items in from a wordlist to serve as payloads. How these get inserted into the template depends on the attack type we chose in the Positions tab. There are many payload types to choose from (anything from a simple wordlist to regexes based on responses from the server). The Payloads sub-tab also allows us to alter Intruder's behaviour with regards to payloads; for example, we can define pre-processing rules to apply to each payload (e.g. add a prefix or suffix, match and replace, or skip if the payload matches a defined regex).  
    
- **Resource Pool** is not particularly useful to us in Burp Community. It allows us to divide our resources between tasks. Burp Pro would allow us to run various types of automated tasks in the background, which is where we may wish to manually allocate our available memory and processing power between these automated tasks and Intruder. Without access to these automated tasks, there is little point in using this, so we won't devote much time to it.
- As with most of the other Burp tools, Intruder allows us to configure attack behaviour in the **Options** sub-tab. The settings here apply primarily to how Burp handles results and how Burp handles the attack itself. For example, we can choose to flag requests that contain specified pieces of text or define how Burp responds to redirect (3xx) responses.

Let's see the positions:

![[Pasted image 20230622105100.png]]

![Screenshot of the positions sub-tab](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/c286bd89e92aab284460ab9302b3b18c.png)

Notice that Burp will attempt to determine the most likely places we may wish to insert a payload automatically -- these are highlighted in green and surrounded by silcrows (`§`).

On the right-hand side of the interface, we have the buttons labelled "Add §", "Clear §", and "Auto §":

- **Add** lets us define new positions by highlighting them in the editor and clicking the button.
- **Clear** removes all defined positions, leaving us with a blank canvas to define our own.
- **Auto** attempts to select the most likely positions automatically; this is useful if we cleared the default positions and want them back.


**Attack types in [burpsuit]

There are four attack types available:

    Sniper
    Battering ram
    Pitchfork
    Cluster bomb

***Sniper attack***

When conducting a sniper attack, we provide _one_ set of payloads. For example, this could be a single file containing a wordlist or a range of numbers. From here on out, we will refer to a list of items to be slotted into requests using the Burp Suite terminology of a "Payload Set". Intruder will take each payload in a payload set and put it into each defined position in turn.

![[Pasted image 20230622110204.png]]


There are two positions defined here, targeting the `username` and `password` body parameters.

In a sniper attack, Intruder will take each position and substitute each payload into it in turn.

For Example:

![[Pasted image 20230622110301.png]]

Notice how Intruder starts with the first position (username) and tries each of our payloads, then moves to the second position and tries the same payloads again. We can calculate the number of requests that Intruder Sniper will make as ***requests = numberOfWords * numberOfPositions.**

This quality makes Sniper very good for single-position attacks (e.g. a password bruteforce if we know the username or fuzzing for API endpoints).

**_Battering Ram_ Attack type:**

Like Sniper, Battering ram takes _one_ set of payloads (e.g. one wordlist). _Un_like Sniper, the Battering ram puts the same payload in _every_ position rather than in each position in turn.

![[Pasted image 20230622110650.png]]


	If we use Battering ram to attack this, Intruder will take each payload and substitute it into every position _at once._  

With the two positions that we have above, Intruder would use the three words from before (`burp`, `suite`, and `intruder`) to make _three_ requests:  

|   |   |
|---|---|
|**Request Number**|**Request Body**|
|1|`username=burp&password=burp`|
|2|`username=suite&password=suite`|
|3|`username=intruder&password=intruder`|

As can be seen in the table, each item in our list of payloads gets put into _every_ position for each request. True to the name, Battering ram just throws payloads at the target to see what sticks.


***Pitchfork attack** :*

Pitchfork is the attack type you are most likely to use. It may help to think of Pitchfork as being like having numerous Snipers running simultaneously. Where Sniper uses one payload set (which it uses on every position simultaneously), Pitchfork uses one payload set per position (**up to a maximum of 20**) and iterates through them all at once.

This type of attack can take a little time to get your head around, so let's use our brute-force example from before, but this time we need two word lists:

   *- Our first wordlist will be usernames. It contains three entries: `joel`, `harriet`, `alex`.*
*- Let's say that Joel, Harriet, and Alex have had their passwords leaked: we know that \ Joel's password is `J03l`, Harriet's password is `Emma1815`, and Alex's password is`Sk1ll`.*

We can use these two lists to perform a pitchfork attack on the login form from before. The process for carrying out this attack will not be covered in this task, but you will get plenty of opportunities to perform attacks like this later!

When using Intruder in pitchfork mode, the requests made would look something like this:

![[Pasted image 20230622111725.png]]

it takes the username and the password from two different list and put it together into as a payload in the position, if the list A has 90 payload and list B has 100 payload then only 90 request will be made.

***Cluster Bomb:***

Like Pitchfork, Cluster bomb allows us to choose multiple payload sets: 
one per position, up to a maximum of 20;
however, whilst Pitchfork iterates through each payload set **simultaneously**, 
**Cluster bomb** iterates through each payload set individually, 
making sure that **every possible combination** of payloads is tested.

Let's use the same wordlists as before:

    Usernames: joel, harriet, alex.
    Passwords: J03l, Emma1815, Sk1ll.


But, this time, let's assume that we don't know which password belongs to which user. We have three users and three passwords, but we don't know how to match them up. In this case, we would use a cluster bomb attack; this will try _every_ combination of values. The request table for our username and password positions looks something like this:


|**Request Number**|**Request Body**|
|1|`username=joel&password=J03l`|
|2|`username=harriet&password=J03l`|
|3|`username=alex&password=J03l`|
|4|`username=joel&password=Emma1815`|
|5|`username=harriet&password=Emma1815`|
|6|`username=alex&password=Emma1815`|
|7|`username=joel&password=Sk1ll`|
|8|`username=harriet&password=Sk1ll`|
|9|`username=alex&password=Sk1ll`|



Cluster Bomb will iterate through every combination of the provided payload sets to ensure that every possibility has been tested.  
	(equal to the number of lines in each payload set multiplied together





---


links:
[[00 Burp-suit]]
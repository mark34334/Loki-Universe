#burp-suit #burp-suit/other-moduls 

---

we will be looking at the _Decoder, Comparer_ and _Sequencer_ tools. These allow us to: work with encoded text; compare sets of text; and analyse the randomness of captured tokens, respectively. Being able to perform these relatively straightforward tasks directly within Burp Suite can save a lot of time, so it is well worth the time spent learning to use these modules efficiently.

The Burp Suite Decoder module allows us to manipulate data.

![[Pasted image 20230623074651.png]]

This interface offers us a number of options.

1. The box on the left is where we would paste or type text to be encoded or decoded. As with most other modules of Burp Suite, we can also send data here from other sections of the framework by right-clicking and choosing _Send to Decoder._  
    
2. We have the option to select between treating the input as text or hexadecimal byte values at the top of the list on the right.
3. Further down the list, we have dropdown menus to _Encode_, _Decode_ or _Hash_ the input.
4. Finally, we have the "Smart Decode" feature, which attempts to decode the input automatically.
![[Pasted image 20230623074753.png]]


![[Pasted image 20230623074759.png]]


![[Pasted image 20230623075732.png]]

**Plain:** Plaintext is what we have before performing any transformations.
**URL:** URL encoding is used to make data safe to transfer in the URL of a web request. It involves exchanging characters for their ASCII character code in hexadecimal format, preceded by a percentage symbol (`%`). Url encoding is an extremely useful method to know for any kind of web application testing.  

**HTML:** Encoding text as HTML Entities involves replacing special characters with an ampersand (`&`) followed by either a hexadecimal number or a reference to the character being escaped, then a semicolon (`;`). For example, a quotation mark has its own reference: `&quot;`. When this is inserted into a webpage, it will be replaced by a double quotation mark (`"`). This encoding method allows special characters in the HTML language to be rendered safely in HTML pages and has the added bonus of being used to prevent attacks such as [XSS](https://owasp.org/www-community/attacks/xss/) (Cross-Site Scripting).

**Base64:** Another widely used encoding method, base64 is used to encode any data in an ASCII-compatible format. It was designed to take binary data (e.g. images, media, programs) and encode it in a format that would be suitable to transfer over virtually any medium.

**ASCII Hex:** This option converts data between ASCII representation and hexadecimal representation. For example, the word "ASCII" can be converted into the hexadecimal number "4153434949". Each letter in the original data is taken individually and converted from numeric ASCII representation into hexadecimal. For example, the letter "A" in ASCII has a decimal [character code](https://www.asciitable.com/) of 65. In hexadecimal, this is 41. Similarly, the letter "S" can be converted to hexadecimal 53, and so on.

**Hex**, **Octal**, and **Binary:** These encoding methods all apply only to numeric inputs. They convert between decimal, hexadecimal, octal (base eight) and binary.

**Gzip:** Gzip provides a way to _compress_ data. It is widely used to reduce the size of files and pages before they are sent to your browser. Smaller pages mean faster loading times, which is highly desirable for developers looking to increase their SEO score and avoid annoying their customers. Decoder allows us to manually encode and decode gzip data, although this can be hard to process as it is often not valid ASCII/Unicode.

**Smart Decode:**
This feature of Decoder attempts to automatically decode encoded text. For example, `&#x42;&#x75;&#x72;&#x70;&#x20;&#x53;&#x75;&#x69;&#x74;&#x65;`, is automatically recognised as being HTML encoded and is automatically decoded accordingly:

_**Hashing in Decoder:**_
Decoder allows us to generate hashsums for data directly within Burp Suite; this works in much the same way as the encoding/decoding options we saw in the previous task. Specifically, we click on the "Hash" dropdown menu and select an algorithm from the list:

![[Pasted image 20230624081654.png]]

![[Pasted image 20230624081718.png]]

**_Comparer:_**

_Comparer_ allows us to compare two pieces of data, either by ASCII words or by bytes.

![[Pasted image 20230624081850.png]]

This interface can be split into three main parts:

1. On the left, we have the items being compared. When we load data into Comparer, it will appear as rows in these tables -- we would then select two datasets to compare.
2. On the upper right, we have options for pasting data in from the clipboard (Paste), loading data from a file (Load), removing the current row (Remove) and clearing all datasets (Clear).
3. Finally, on the bottom right, we have the option to compare our datasets by either words or bytes. Don't worry about which of these buttons you select as this can be changed later on. These are the buttons we click when we are ready to compare the data we have selected.
![[Pasted image 20230624081910.png]]

Once again, there are three distinct parts to this window:

1. The compared data takes up most of the window; this can be viewed in either text or hex format. The initial format is determined by whether we chose to compare by words or by bytes in the previous window, but this can be overwritten by using the buttons above the comparison boxes.
2. The key for comparisons is at the bottom left, showing which colours denote modified, deleted, and added data between the two datasets.
3. At the bottom right of the window is the "Sync views" checkbox. When selected, this means that both sets of data will sync formats -- i.e. if you change one of them into Hex view, the other will do the same to match.

***Sequencer:***

Sequencer allows us to measure the _entropy_ (or randomness, in other words) of "tokens" -- strings that are used to identify something and should, in theory, be generated in a cryptographically secure manner. For example, we may wish to analyse the randomness of a session cookie or a **C**ross-**S**ite **R**equest **F**orgery (CSRF) token protecting a form submission. If it turns out that these tokens are not generated securely, then we can (in theory) predict the values of upcoming tokens. Just imagine the implications of this if the token in question is used for password resets.

![[Pasted image 20230624082024.png]]

There are two main methods we can use to perform token analysis with Sequencer:

- **Live capture** is the more common of the two methods -- this is the default sub-tab for Sequencer. Live capture allows us to pass a request to Sequencer, which we know will create a token for us to analyse. For example, we may wish to pass a POST request to a login endpoint into Sequencer, as we know that the server will respond by giving us a cookie. With the request passed in, we can tell Sequencer to start a live capture: it will then make the same request thousands of times automatically, storing the generated token samples for analysis. Once we have accumulated enough samples, we stop Sequencer and allow it to analyse the captured tokens.

- **Manual load** allows us to load a list of pre-generated token samples straight into Sequencer for analysis. Using Manual Load means we don't have to make thousands of requests to our target (which is both loud and resource intensive), but it does mean that we need to obtain a large list of pre-generated tokens!

***Sequencer analysis:***

Burp performs dozens of tests on the token samples that it captured. We won't be looking at all of these as it would take far more than a single task to do so (and it would get very maths-intensive to break each technique apart). Instead, we will focus on the generated summary; however, you are encouraged to look through all of the test results for yourself.

![[Pasted image 20230624082203.png]]

Collectively, these will often be enough to determine whether the token is generated safely or not; however, in some instances, we may need to have a look at the test results directly -- this can be done in the "Character-level analysis" and "Bit-level analysis" tabs. As mentioned previously, we will not be going into these to avoid delving into the depths of statistical-analysis mathematics in a beginner-friendly room. In short, with an estimated 1% chance of being incorrect based on the data provided (Significance level: 1%), Burp has calculated that the effective entropy of our token _should_ be around 117 bits. This is an excellent level of entropy to have in a secure token, although it should be noted that it is impossible to say with absolute assurance that this calculation is entirely accurate, simply due to the nature of the topic.





























---

links:
[[00 Burp-suit]]
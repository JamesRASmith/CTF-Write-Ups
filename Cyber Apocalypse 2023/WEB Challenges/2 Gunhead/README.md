# Gunhead

This was the second challenge in the web part of the CTF.

As usual, I spin up the docker instance and download the files provided by the challenge.

Over the course of this CTF I found it best to first visit the instance that had been spun up, before reviewing any files that were included as I could potentially narrow my focus later on.

![image](https://user-images.githubusercontent.com/57868272/227778510-936d0467-453b-496d-9fc4-846566208ddf.png)

A look over the site shows that this contains a lot of diagnostic information for the 'robot'. Further review shows that there is the ability to open a terminal, this seems like the best chance I have of exploiting this site to get the flag for the challenge.

![image](https://user-images.githubusercontent.com/57868272/227778718-81c5008d-a6ac-48b7-8508-3b984855a730.png)

Running the help command shows that there are only 3 commands that can be run in this terminal (clear, ping & storage) of the 3 available commands '/ping' seems to me to have the best chance of exploiting.

Now that I have found what I believe to be the best chance of infiltration I can go back and look at the files provided by the challenge.

![image](https://user-images.githubusercontent.com/57868272/227779545-0011e2ba-9656-45e3-8207-3752e3c8acd2.png)

From looking at previous years CTF write-ups I found that most of the important information is stored in the 'challenge' folder.

![image](https://user-images.githubusercontent.com/57868272/227779625-acafa667-5330-45ce-94fd-43204a4ea6cc.png)

I spent some time looking through the files included in the challenge folder and found that they were all written in PHP. This is a language I have 0 experience in and have never actually seen code for before. However a basic understanding of Python helped me to at least understand the flow of the code and the code in this challenge seems pretty self explanatory.

Each of the folders seen in the above image contain PHP scripts, however I am largely interested in finding the code that operates the ping command to see if this has any flaws that can be exploited. Fortunately this was not hard to find and the ping command was handled by the 'ReconModel.php' file. The code within is seen below:

```
<?php
#[AllowDynamicProperties]

class ReconModel
{   
    public function __construct($ip)
    {
        $this->ip = $ip;
    }

    public function getOutput()
    {
        # Do I need to sanitize user input before passing it to shell_exec?
        return shell_exec('ping -c 3 '.$this->ip);
    }
}
```

As with many of the easier challenges within CTF's comments are used to guide the player towards the right solution. As the code mentions the sanitisation of user input this is where I started online and found the following useful link.

https://www.acunetix.com/websitesecurity/php-security-2/

This notes that if PHP code is using shell_exec() without proper input sanitsation we can make execute multiple commands inline through the use of a simple semicolon (within Linux this is the delimiter used to execute multiple commands inline) I also made use of chatGPT here to show sanity check this a short while later as I was having issues crafting the exploit.

Comparing the evidence in the above link with chatGPT and my own input, I found the issue to be one of my own causing as I was including a colon rather than a semicolon in my input to the program. Inputting the following command returned the flag

```
ping 192.168.0.1; cat flag.txt
```

This returned the following flag:

**HTB{4lw4y5_54n1t1z3_u53r_1nput!!!}**

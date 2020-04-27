# Table of Content

- [Useful Linux Command](#linux)
- [Reconnaissance](#recon)
   - [Nmap](#nmap)
   - [Nikto](#nikto)
- [Web App](#webapp)
   - [SQL Injection](#sqlinj)
   - [XSS](#xss)
   - [Subdomain Takeover](#subdomain)
- [Privilege Escalation](#privesc)
   - [SUID[(#suid)



<a name="linux"></a>
# Useful Linux Command

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
# Reconnaissance

<a name="nmap"></a>
### Nmap

- ```nmap -p- -oA full-nonscripts [Target IP] --max-retries 0```: 
-```nmap -sC -sV -O -oA [file] [target ip]```:




<a name="nikto"></a>
### Nikto













<a name="webapp"></a>
# Web App 

<a name="sqlinj"></a>
### SQL Injection

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


<a name = "xss"></a>
### XSS

<a name ="subdomain"></a>
### Subdomain Takeover

<a name ="privesc"></a>
# Privilege Escalation

<a name="suid"></a>
### SUID

If you type ```ls -al``` in console, there are something like ```rwxr--rwx root root``` next to your file name. So, what does it mean? It 

To find file with SUID bit. Simply use following command:

```
find [directory] -perm -u=s -type f 2>/dev/null
```


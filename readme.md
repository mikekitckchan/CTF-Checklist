This file containes a checklist for myself to use in CTF challenge.

# Table of Content
1. [Web-app Testing](#webapp)
- [SQL Injection](##sqlinj)














<a name="webapp"></a>
# Web-app testing

</a name="sqlinj"></a>
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






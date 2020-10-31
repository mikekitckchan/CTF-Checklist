1. Search for useful information using search engine (e.g. google, baidu):

For example
```
site:target.com inurl:admin|login
site:target.com intitle:"index of"
site:target.com ext:php
site:target.com ext:csv
```

2. Search for information using below site:

zoomeye.org
```
hostname:target.com
```
shodan.io
```
target.com
```
fofa.so
```
domain:"target.com"
```
dnsdb.io
```
target.com
```

3. Find subdomain
http://tool.chinaz.com/subdomain/
sublist3r
https://phpinfo.me/domain/
lijiejie
wydomain
https://securitytrails.com

4. SSL search
https://crt.sh

5. Port scan
Yujian portscan
nmap

6. Try source code leak
e.g.
```
www.target.com/.git/config
www.target.com/.ds_store
www.target.com/CVS/root
www.target.com/.svn/entries
```

Other useful leak:
```
/WEB-INF/web.xml：Web应用程序配置文件，描述了 servlet 和其他的应用组件配置及命名规则。



/WEB-INF/classes/：含了站点所有用的 class 文件，包括 servlet class 和非servlet class，他们不能包含在 .jar文件中。



/WEB-INF/lib/：存放web应用需要的各种JAR文件，放置仅在这个应用中要求使用的jar文件,如数据库驱动jar文件。



/WEB-INF/src/：源码目录，按照包名结构放置各个java文件。



/WEB-INF/database.properties：数据库配置文件。
```

4. Find endpoints:
- Use bruteforce directories
- Use linkfinder for js files




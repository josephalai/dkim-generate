# DKIM TXT Record Generator Script (generate-dkim.sh)

### About

Generate a DKIM from private and public RSA keys to be used for TXT Records. Prevent your emails from going to SPAM! 
This script is intended for use with PowerMTA, but can be used with any system that uses RSA, TXT, etc. 


#### Intended Output

- Generates RSA Private Key
- Generates RSA Public Key
- Generates TXT Record in proper format


#### Requirements
1. `openssl` is the only requirement. If you do not have `openssl` on your machine, you need to download and install it.



### Instructions

#### Option 1

1. Edit `generate-dkim.sh` and set the `SELECTOR` and `DOMAIN` variables.
```bash
DOMAIN=example.com
SELECTOR=default
```
2. Run the script: `./generate-dkim.sh`
3. Collect your keys from `./$DOMAIN/$SELECTOR.$DOMAIN.dkim.txt`
4. Place them in your server and point your configs to them
5. Update TXT Record


#### Option 2

1. Run `./generate-dkim.sh example.com default` (`example.com` is the domain and `default` is the selector).
2. Collect your keys from `./$DOMAIN/$SELECTOR.$DOMAIN.dkim.txt`


### TXT Records

1. Add a new, unique TXT Records with a unique selector.
2. Set Host to: `default._domainkey.example.com` (`example.com` is the domain and `default` is the selector).
3. Set TTL to `86400`.
4. Set the TXT to `v=DKIM1; k=rsa; p=MIGfMA0GCSqGSx...;`


Inside your dkim file will be the full txt record.

```
default._domainkey.example.com. 86400 IN TXT "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSxl3DQEBAXUAAZGNADCBiX2kcmM33JHa01Zm51O1MG9vXcnXApfm/a0IMm5s97n9cNdzOSfxNFa7SLBzs8KKZgUmx775w5FDWIwaZk1SNzOg0CML68t2Bds9XWZzR85uxgVxMOXXb8aU/cRXixBMnMaxxzBIZy8fgE9xlVK7rZfPycxdwIDAXAB"
```


Copy the following directly into your text record.

Host: 
```
	default._domainkey.example.com
```

TXT
```
	v=DKIM1; k=rsa; p=MIGfMA0GCSXGSxl3lmEBAXUAAZGNADCBiX2kcmM33JHa01Zm51O1MG9vXcnXApfm/a0IMm5s97n9cNdzOSfxNFa7SLBzs8KKZgUmx775w5FDWIwaZk1SNzOg0CML68t2Bds9XWZzR85uxgVxMOXXb8aU/cRXixBMnMaxxzBIZy8fgE9xlVK7rZfPycxdwIDAXAB
```

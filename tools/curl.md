Curl
=====

## General syntax

### curl

```bash
curl http://google.com
```

### Request: Header (-H)
```
curl -H "Host:" http://www.example.com
```

### Response: Headers (-i)
```bash
curl -i http://google.com
```

### Verbs (-X)
```
curl -X POST http://example.org/
```

### Post Data (--data, --data-binary)

```
curl --data "birthyear=1905&press=%20OK%20" http://www.example.com/when.cgi
(form) curl --data-urlencode "name=I am Daniel" http://www.example.com
```

Json
```
curl --data-binary=@filename.json -H "Content-type: application/json" http://url1.example.com
```

### Follow redirects (-L)
```
curl -L http://google.com
```

## Certificates
```
curl --cacert ca-bundle.pem https://example.com/
curl --cert mycert.pem https://secure.example.com
```

## Advanced

### Host Header via resolver
```
curl --resolve www.example.org:80:127.0.0.1 http://www.example.org/
```

### Basic Authentication
```
curl -u user:password http://example.org/
```

### Upload file via PUT
```
curl --upload-file uploadfile http://www.example.com/receive.cgi
```

# References

https://curl.haxx.se/docs/httpscripting.html

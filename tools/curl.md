Curl
=====

Ref: https://curl.haxx.se/docs/httpscripting.html

General syntax:

```bash
curl http://google.com
```

Request with headers:

```bash
curl -i http://google.com
```

Header
curl -H "Host:" http://www.example.com
curl --header "Host:" http://www.example.com

Verbs
curl -X POST http://example.org/

Post
curl --data "birthyear=1905&press=%20OK%20" http://www.example.com/when.cgi
(form) curl --data-urlencode "name=I am Daniel" http://www.example.com
(json) curl --data-binary=@filename.json -H "Content-type: application/json" http://url1.example.com

Follow redirects
curl -L http://google.com
curl --location http://www.example.com

Certificates
curl --cacert ca-bundle.pem https://example.com/
curl --cert mycert.pem https://secure.example.com

curl --resolve www.example.org:80:127.0.0.1 http://www.example.org/
curl -u user:password http://example.org/
curl --upload-file uploadfile http://www.example.com/receive.cgi (PUT)

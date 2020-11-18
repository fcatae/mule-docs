
Requisitos do load balancer:
- An unencrypted, PEM-encoded (Privacy-Enhanced Mail) certificate file.
- A second file containing the private key of your PEM certificate.
The private key file must be passphraseless.

## Gerar chave self-signed

openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 3000 -out cert.pem

## Gerar um certificado Wildcard

CN = *.example.com

## Use Config File (-config)

openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 3000 -out cert.pem -config domain-com.cfg

```
[ req ]
default_bits       = 2048
distinguished_name = req_distinguished_name
req_extensions     = req_ext
prompt = no
[ req_distinguished_name ]
countryName                 = US
stateOrProvinceName         = California
localityName               = San Francisco
organizationName           = MuleSoft
commonName                 = example.com

[ req_ext ]
subjectAltName = @alt_names
[alt_names]
DNS.1   = app1.example.com
DNS.2   = app2.example.com
```

### Generating CSR

openssl req -nodes -newkey rsa:4096 -keyout myserver.key -out server.csr

openssl req -newkey rsa:2048 -keyout <chave>.key -keyform PEM -SHA512 -out requisicao.csr

### Convert to PKCS12

openssl pkcs12 -export -in cacert.pem -inkey cakey.pem -out identity.p12 -name "mykey"

### Convert from PFX

openssl pkcs12 -in myfile.pfx -nocerts -out private-key.pem -nodes
openssl pkcs12 -in myfile.pfx -nokeys -out certificate.pem


# PKCS #12
https://tools.ietf.org/html/rfc7292

A simpler, alternative format to PKCS #12 is PEM which just lists the certificates and possibly private keys as Base 64 strings in a text file. 

# curl

Note -k option is to tell curl to accepted self-signed certificates.

# troubleshoot

https://help.mulesoft.com/s/article/SSL-certificate-verification

curl -v https://<SERVER_NAME>;

openssl s_client -connect <SERVER_NAME>:443 -showcerts -servername <SERVER_NAME>

curl -v -H "Host: <SERVER_NAME>" https://127.0.0.1
openssl s_client -connect 127.0.0.1:443 -showcerts -servername <SERVER_NAME>

curl -v --cert ./Client_cert.p12 https://<SERVER_NAME>/order-service/order
curl -v --cacert ./CA_Cert.pem https://<SERVER_NAME>/order-service/order

###

openssl req –out certificatesigningrequest.csr -new -newkey rsa:2048 -nodes -keyout privatekey.key

openssl req -in server.csr -noout -text

CSR
openssl req -out CSR.csr -key privateKey.key -

Regenerate CSR
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key

self-signed
The –days parameter is set to 365, meaning that the certificate is valid for the next 365 days. The x509 parameter indicates that this will be a self-signed certificate. A temporary CSR is generated, and it is used only to gather the necessary information.

openssl x509 \ -signkey domain.key \ -in domain.csr \ -req -days 365 -out domain.crt

ref: many commands 
https://phoenixnap.com/kb/openssl-tutorial-ssl-certificates-private-keys-csrs
https://www.keycdn.com/blog/openssl-tutorial
https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs
https://gist.github.com/Soarez/9688998


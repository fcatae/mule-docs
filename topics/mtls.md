Gerar os certificados self-signed

    openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 3000 -out cert.pem

Problemas

SSL certificate problem: self signed certificate

    curl -k https://lb-fcatae2.lb.anypointdns.net/simple-app-fcatae/mulesoft

    curl https://lb-fcatae2.lb.anypointdns.net/simple-app-fcatae/mulesoft --cacert cert.pem


SSL: certificate subject name 'self.mule.run' does not match target host name 'lb-fcatae2.lb.anypointdns.net'



---
openssl s_client -showcerts -connect 946-BAD-289.mktorest.com:443
---


#Server private key = Certificate Authority (CA)
openssl genrsa -out server-private-key.pem 1024

#Server certificate = CA certificate
openssl req -new -x509 \
-key server-private-key.pem \
-out server-public-key.crt \
-subj "/C=UK/ST=London/L=London/O=IT/CN=api.igorrepka.com"

#Key for client certificate
openssl genrsa -out client-private-key.pem 1024

#Certificate Signing Request (CSR) for client certificate
openssl req -new -key client-private-key.pem -out client-cert.csr

#Signing CSR
openssl x509 -req -days 365 -in client-cert.csr -CA server-public-key.crt -CAkey server-private-key.pem -set_serial 01 -out client-cert.crt

#Creating a PKCS #12 (PFX)
openssl pkcs12 -export -out client.pfx -inkey client-private-key.pem -in client-cert.crt -certfile server-public-key.crt
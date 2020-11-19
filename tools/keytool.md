https://docs.mulesoft.com/mule-runtime/4.3/tls-configuration

Mule


https://help.mulesoft.com/s/article/How-to-create-a-self-signed-Keystore-and-Trustore-SSL-Certificate

keytool -v -genkeypair -keyalg RSA -dname "cn=MuleSoft, ou=MuleSoft, o=MuleSoft,L=San Francisco, st=CA, c=US" -ext SAN="DNS:localhost,IP:127.0.0.1" -validity 1825 -alias mule -keystore keystore.jks -keypass mule123 -storepass mule123

 
2. Export the Certificate to add it into Truststore:  
    Export the certificate so that we can use it in the Truststore.
 

keytool -export -alias mykeyalias -file localhost.cer -keystore keystore.jks

 
3. Create a Trustore certificate:
    Truststore is a client-side asset that serves as a repository of certificates (CA or simple) that the client should trust.
 

keytool -import -v -trustcacerts -alias mykeyalias -file localhost.cer -keystore truststore.jk


keytool -importkeystore -srckeystore <sistema>.pfx -destkeystore <sistema>.keystore -deststoretype JKS -srcstoretype PKCS12 


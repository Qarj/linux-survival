# SSL

## Ubuntu 16.04

View SSL info for a website:
```
openssl s_client -connect pypi.python.org:443
```

Download a .crt and covert it to a .pem:
```
wget http://cacerts.digicert.com/DigiCertHighAssuranceEVRootCA.crt 
openssl x509 -inform DES -in DigiCertHighAssuranceEVRootCA.crt -out DigiCertHighAssuranceEVRootCA.pem -text
```

Make that cert the Python PIP cert:
```
sudo mkdir /usr/share/ca-certificates/custom
sudo chmod 755 /usr/share/ca-certificates/custom
mv DigiCertHighAssuranceEVRootCA.crt usr/share/ca-certificates/custom
cd /usr/share/ca-certificates/custom
sudo chmod 644 DigiCertHighAssuranceEVRootCA.pem
export PIP_CERT=`pwd`/DigiCertHighAssuranceEVRootCA.pem
```

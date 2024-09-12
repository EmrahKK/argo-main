## Create CA certificate for cert-manager cluster issuer

openssl genrsa -out ca.key 4096

openssl req -x509 -new -nodes -sha512 -days 3650 \
 -subj "/C=CN/ST=Istanbul/L=Istanbul/O=k3dlocal/OU=Personal/CN=k3d.local" \
 -key ca.key \
 -out ca.crt

## Create TLS secret from key and certificate files

kubectl create secret tls cluster-tls --cert=ca.crt --key=ca.key -n cert-manager
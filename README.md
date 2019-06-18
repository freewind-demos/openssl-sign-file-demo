OpenSSL Sign File Demo
=======================

https://raymii.org/s/tutorials/Sign_and_verify_text_files_to_public_keys_via_the_OpenSSL_Command_Line.html

## Generate Keys:

```
openssl req -nodes -x509 -sha256 -newkey rsa:4096 \
  -keyout "Demo Sign Key.key" \
  -out "Demo Sign Key.crt" \
  -days 365 \
  -subj "/C=NL/ST=AAA/L=BBB/O=CCC/OU=DDD/CN=Demo Sign Key"
```

## Sign file

```
echo "Hello, World!" > sign.txt
```

```
openssl dgst -sha256 -sign "Demo Sign Key.key" -out sign.txt.sha256 sign.txt 
```

## Verify Signature

```
openssl dgst -sha256 -verify  <(openssl x509 -in "Demo Sign Key.crt" -pubkey -noout) -signature sign.txt.sha256 sign.txt
```

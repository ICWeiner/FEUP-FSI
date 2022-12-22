# Public-Key Infrastructure (PKI)

## Logbook Week 11

### Lab Environment

```shell
# input the content below
10.9.0.80   www.l11g03.com
```

### Task 1: Becoming a Certificate Authority (CA)

In this task, we will make ourselves a root CA, and generate a certificate for this CA. First we started by copying openssl.cnf to our working directory, so then we can change it.

```shell
# cd path/to/Labsetup
cp /usr/lib/ssl/openssl.cnf ./openssl.cnf
```

Then, like resquested, uncomment the unique subject line, under [CA default], inside the openssl.cnf file to allow creation of certifications with the same subject.

```shell
dir = ./demoCA
certs = $dir/certs
crl_dir = $dir/crl
database = $dir/index.txt
unique_subject = no
new_certs_dir = $dir/newcerts
serial = $dir/serial
```

Next, create the necessary files, like an empty file (index.txt) and the serial file with a number in the string format in it ("1000").

```shell
mkdir demoCA
cd demoCA
mkdir certs crl newcerts
touch index.txt
echo "1000" > serial
cd .. # return to Labsestup
```

To finish, we need to generate a self-signed certificate for our CA, by running the following comand.

```shell
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout ca.key -out ca.crt -subj "/CN=www.modelCA.com/O=Model CA LTD./C=US" -passout pass:dees
```

With this we already specified the all the information of the subject and the password needed, so any additional information will not be promted.

### Questions

```shell
openssl x509 -in ca.crt -text -noout
openssl rsa  -in ca.key -text -noout
```

First we run this commands so we can look the content into plain text.

**What part of the certificate indicates this is a CA’s certificate?**

CA:TRUE
```shell
```

**What part of the certificate indicates this is a self-signed certificate?**

The Subject Key Identifier and the Authority Key Identifier are the same.

```shell
```

**In the RSA algorithm, we have a public exponent, a private exponent `d`, a modulus `n`, and two secret numbers `p` and `q`, such that `n=pq`. Please identify the values for these elements in your certificate and key files.**

p and q are prime1 and prime2

```shell
```

### Task 2: Generating a Certificate Request for Your Web Server

We need to generate a Certificate Signing Request (CSR) with this command:

```shell
openssl req -newkey rsa:2048 -sha256 -keyout server.key -out server.csr -subj "/CN=www.l11g03.com/O=L11g03 Inc./C=US" -addext "subjectAltName = DNS:www.l11g03.com, DNS:www.l11g03A.com, DNS:www.l11g03B.com" -passout pass:dees
```

To the "subjectAltName" we added to alternative names, pointing to the same web server.

```shell
```

### Task 3: Generating a Certificate for your server

Using the files created at Task 1(ca.crt and ca.key ), we generate the X509 certificate, with the follwing command:

```shell
openssl ca -config openssl.cnf -policy policy_anything \
-md sha256 -days 3650 \
-in server.csr -out server.crt -batch \
-cert ca.crt -keyfile ca.key
```

```shell
```

For security reasons, the default setting in openssl.cnf does not allow the "openssl ca" command to copy the extension field from the request to the final certificate, so we need to enable it:

```shell
copy_extensions = copy
```

```shell
openssl x509 -in server.crt -text -noout
```

```shell
```

The alternative names are included.

### Task 4: Deploying Certificate in an Apache-based HTTPS Website





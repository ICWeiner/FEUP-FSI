# Public-Key Infrastructure (PKI)

### Lab Environment

```shell
sudo nano /etc/hosts
```
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img1.png "Title")

### Task 1: Becoming a Certificate Authority (CA)

In this task, we will make ourselves a root CA, and generate a certificate for this CA. First we started by copying openssl.cnf to our working directory, so that we can change it.

```shell
# cd path/to/Labsetup
cp /usr/lib/ssl/openssl.cnf ./openssl.cnf
```

Then, like requested, we uncomment the unique subject line, under [CA default], inside the openssl.cnf file to allow the creation of certifications with the same subject.

```shell
dir = ./demoCA
certs = $dir/certs
crl_dir = $dir/crl
database = $dir/index.txt
unique_subject = no
new_certs_dir = $dir/newcerts
serial = $dir/serial
```

Next, we create the necessary files, like an empty file (index.txt) and the serial file with a number in the string format in it ("1000").

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

With this we already specified all the information of the subject and the password needed, so any additional information will not be prompted.

### Questions

```shell
openssl x509 -in ca.crt -text -noout
openssl rsa  -in ca.key -text -noout
```

First we run these commands so we can look at the content as plain text.

**Question 1**

What part of the certificate indicates this is a CA’s certificate?
- CA:TRUE

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img2.png "Title")

**Question 2**

What part of the certificate indicates that this is a self-signed certificate?
- The Subject Key Identifier and the Authority Key Identifier are the same.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img3.png "Title")

**Question 3**

In the RSA algorithm, we have a public exponent, a private exponent `d`, a modulus `n`, and two secret numbers `p` and `q`, such that `n=p*q`. Please identify the values for these elements in your certificate and key files.
- p and q are prime1 and prime2

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img4.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img5.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img6.png "Title")


### Task 2: Generating a Certificate Request for Your Web Server

We need to generate a Certificate Signing Request (CSR) with this command:

```shell
openssl req -newkey rsa:2048 -sha256 -keyout server.key -out server.csr -subj "/CN=www.l11g03.com/O=L11g03 Inc./C=US" -addext "subjectAltName = DNS:www.l11g03.com, DNS:www.l11g03A.com, DNS:www.l11g03B.com" -passout pass:dees
```

With the "subjectAltName", we added two alternative names, pointing to the same web server.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img8.png "Title")


### Task 3: Generating a Certificate for your server

Using the files created (ca.crt and ca.key), we generate the certificate, with the following command:

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img9.png "Title")

For security reasons, the default setting in openssl.cnf doesn´t allow the "openssl ca" command to copy the extension field from the request to the final certificate, so we need to enable it:

```shell
copy_extensions = copy
```

### Task 4: Deploying Certificate in an Apache-based HTTPS Website

For this task we had to deploy a webiste with a certificate (https connection).

To achieve that, we start by editing the folder image_www updating the certs, dockerfile, and the config file.

Dockerfile:
```shell
FROM handsonsecurity/seed-server:apache-php

ARG WWWDIR=/var/www/l11g03

COPY ./index.html ./index_red.html $WWWDIR/
COPY ./l11g03_apache_ssl.conf /etc/apache2/sites-available
COPY ./certs/server.crt ./certs/server.key /certs/

RUN chmod 400 /certs/server.key \
    && chmod 644 $WWWDIR/index.html \
    && chmod 644 $WWWDIR/index_red.html \
    && a2ensite l11g03_apache_ssl

CMD tail -f /dev/null
```

l11g03_apache_sll.conf:
```shell
<VirtualHost *:443>
    DocumentRoot /var/www/l11g03
    ServerName www.l11g03.com
    ServerAlias www.l11g03A.com
    ServerAlias www.l11g03B.org
    DirectoryIndex index.html
    SSLEngine On
    SSLCertificateFile /certs/server.crt
    SSLCertificateKeyFile /certs/server.key
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot /var/www/l11g03
    ServerName www.l11g03.com
    DirectoryIndex index_red.html
</VirtualHost>
```

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img10.png "Title")

Now we can build and run the container. We can start the server after configure the apache.

```shell
docker-compose build 
docker-compose up
```

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img11.png "Title")

Searching for our server we can find:

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img12.png "Title")

This means that our certificate has an unknown (or untrusted) CA. Firefox only has highly secure certificates in its bank of certificates, which means a self-signed certificate is a reason to launch a warning in a modern browser. We need to add our CA in the list of truted CAs within Firefox. To do this we can go to need to Preferences -> Private & Security -> View Certificates and add the file "ca.crt".

Now, our connection is secure.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img13.png "Title")

### Task 5: Launching a Man-In-The-Middle Attack

In this task we can test public-key encryption based on Certification Authority signature capability´s to handle MITM attacks as long as the certification keys are not compromised. For this, we need to setup a fake "www.fsi.com" changing the config file and the hosts folder.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img14.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img15.png "Title")

Now, we can rebuild docker and start apache once again.

The server is running but when we try to access it gives us a different warning:

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img16.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img17.png "Title")

This happens because we are trying to use the certificate we generate for "www.l11g03.com" with "www.fsi.com". Firefox recognizes that something isn´t right and gives us this warning.

The MITM attack was not successful. The Browser was able to pick it up.

### Task 6: Launching a Man-In-The-Middle Attack with a Compromised CA

When CA is compromised, the attacker can generate its own certificates for the fake website.
So, the first step is generate a certificate for www.fsi.com using our CA.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img18.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img19.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img20.png "Title")

After that, we change the docker and the config file.
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img21.png "Title")
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img22.png "Title")

Rebuilding and starting the apache again...

We can acess the site and see that is secure.
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/logbook11img23.png "Title")

Firefox still shows us a message but we get no warnings this time.

This time the MITM attack was successful. From this we conclude that if the CA is compromised, then an attacker can create a certificate for themselves and impersonate a website. 

## Challenge 1: Number Station

For this CTF, we know that the public exponent is 0x10001 and that p and q that make up n are prime numbers.

p is close to 2^512 and q is close to 2^513.

Our first objective is to find the exact values for p and q. 

This is easily achived with the following python code.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img1.PNG "Title")

Next we need to get the value of d, which is used to decode the flag.

We get d with the following code.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img2.PNG "Title")

Now we just need to get the enconded flag from the server...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img3.PNG "Title")

And decode using the script.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img4.PNG "Title")

Flag obtained.

## Challenge 2:

For this challenge we know that there are two different values of e but only one value of n.

We did some research on possible attacks on RSA and found some general ideias on how to attack RSA, which we´ll explain along the guide

We start by saving this data to a python script, somewhat inspired by the last challenge, which we will use to decode the flag.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img5.PNG "Title")

We then find that if the gcd of e1 and e2 = 1, then there exists 2 values, a and b such that e1 * a + e2 * b = 1

So we implement egcd in our script.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img5.PNG "Title")

And run it, finding the values for a and b.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img6.PNG "Title")

Since b is negative...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img7.PNG "Title")

 We need an i equal to c2(encrypted message) to the power of -1 modulus(%) of n (c2^-1 % n)

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img8.PNG "Title")

Finally, we have all the values we need to decrypt the message and obtain the value.

The final computation is as follows

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img9.PNG "Title")

Now we just run the code and obtain the flag.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf6img10.PNG "Title")

We also noticed that the code took quite a bit to run, and so we re-ran it using "time", for curiosity´s sake and found that on our machine it took almost 2 minutes(!), perhaps there is some more efficient way of running this attack?

Also, since this script was written mostly from the ground up, just taking some general ideias from the provided one, we´ll provide it in full below so as to get a better look.

```
def egcd(a, b):
    if a == 0:
        return b, 0, 1
    gcd ,x1,y1 = egcd(b%a,a)
    
    x = y1 - (b//a) *x1
    y = x1
    
    return gcd,x,y

n = 29802384007335836114060790946940172263849688074203847205679161119246740969024691447256543750864846273960708438254311566283952628484424015493681621963467820718118574987867439608763479491101507201581057223558989005313208698460317488564288291082719699829753178633499407801126495589784600255076069467634364857018709745459288982060955372620312140134052685549203294828798700414465539743217609556452039466944664983781342587551185679334642222972770876019643835909446132146455764152958176465019970075319062952372134839912555603753959250424342115581031979523075376134933803222122260987279941806379954414425556495125737356327411
e1 = 0x10001
e2 = 0x10003

gcd , a ,b = egcd(e1,e2)

c1 = 0xc1f4e67f3b08817245592e142426d71ed5741d69e90ceb6a264090d04b735ae9d1d8fef1c9c70c2d05bd514bfd5661c72ec26bd813953e3a01aa34d6aceb937e3d563a5e77922b2216679dd1839e15867903090f12a13b4752c3568083d8098e271f8be4c0a7bc3021ee66af15c392ff8dde40857d26f0ff20169894d22535901b65da94a54c573a2633a0ada76874f14ec0b20f452d9cf24a5730a6f3b209208fd070811eec8b587ffb9c038ddf1d5e2027bcfee7268a17f2164add87287aed2e50cbfaaad4d615e6982927ee33efd666bcc66ae1fdcca9b2a1704f4dcce0216fa12bc2c47bd87657b77afcafc7dd9d09ec7e3458024211b03f26c712af8a87

c2 = 0x7926baf45d630ae095419b8965f5d7843a4bcaf861703ef61b3d0e010e75617bb370cfa3413da2f23a30bc507c250b9701276d110ed72eee502d3c27a9120b91df5dca0a5ad4705a981ba906a576bccdc0894e70954c37bcdc68e241ebac7b911a2565e13a84ceb734b757944dd71317a706b9742e4eefa831d4bf8893065f7938d4e2be5965908588d8c8bea2f3293cb9f68d9d184b45f962e1ab7f45e359bee36691ed53e899e16a6d54a0cabd7a9bbd108e1332d8ea62124f76023f38d130cda11d6d18ef2c4d65968c1fa87973f6a3cb6a05858139343b6dcdfd6fba0a88082c3c358e9fec49146f59430f6ac56df4ca68fac653a43533f4820351c27b15

i = pow(c2,-1,n)

m = c1**a * i**(-b) % n

print(m.to_bytes(256,'big').decode())


``` 

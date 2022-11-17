# CTF 3


## Task 1

### Checksec

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img1.PNG "Title")

### Obtendo a flag

Neste desafio, os endereços de memoria são estaticos e a flag é carregada num buffer global, utilizamos o exploit fornecido que le a flag visto que sabemos o endereço, que obtivemos usando o gdb

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img2.PNG "Title")

Correndo o script fornecido contra o servidor do ctf, obtemos imediatamente a flag.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img3.PNG "Title")

## Task 2

### Checksec

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img4.PNG "Title")

### Desafio

Desta vez, em vez de imprimir um valor de um buffer, temos de alterar um valor de uma variavel local para um valor especifico 0xbeef, a semelhança do logbook do tema "format strings".

Primeiro precisamos do endereço

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img5.PNG "Title")

# DIO-Cibersecurity-Project
Entrega de Projeto para o bootcamp da DIO Cibersecurity

## Fazendo varredura de alvos dentro da rede destino com nmap para descobrir possíveis alvos ativos e com portas abertas dentro da rede do Virtual Box:
``` bash
nmap 192.168.56.103/24
```
Com esse comando irá listar todos os hosts encontrados nessa rede, nesse caso nossa máquina com vulnerabilidades será listada nos resultados, juntamente com suas portas que estão abertas, nesse caso o ip do host seria 192.168.56.103. E suas portas que estão abertas são:
```
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
```


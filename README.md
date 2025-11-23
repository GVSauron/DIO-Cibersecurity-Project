# DIO-Cibersecurity-Project
Entrega de Projeto para o bootcamp da DIO Cibersecurity
# Força bruta DIO 
## Ferramentas e OS a serem ultilizadas
- VirtualBox
- Kali Linux(já vem com as ferramentas instaladas)
- Metasploitable(máquina virtual com vulnerabilidades) [Download](https://sourceforge.net/projects/metasploitable/)
- Nmap
- Medusa
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
Agora que já sabemos quais portas estão abertas, é hora de explorar as vulnerabilidades, nesse caso iremos explorar um cenário onde as senhas dos serviços desse servidor serão fracas e previsivéis e utilizaremos de força bruta para tentar invadir esse host. Iremos iremos explorar conexão SSH, para teste, digite no terminal o seguinte para que se certificar se o protocolo está aceitando requisição de login(substitua o IP pelo IP da máquina em sua rede):
```
ssh 192.168.56.103
```
Caso solicite credenciais de user e password, é sinal de serviço está aceitando requisição de logins, é aqui onde iremos ultilizar a Medusa para quebrar a senha na força bruta.

## Medusa
A Medusa é uma ferramente muito útil para ataques de força bruta em serviços que podem ser acessados via autenticação remota(SSH, FTP...) e suporta vários protocolos, e tem um objetivo ser muito rápida nas requisições, cabe a cada um testar a extensão da sua força. Para maiores informações pode-ser obter detalhas nesta [Documentação](http://foofus.net/goons/jmk/medusa/medusa.html)




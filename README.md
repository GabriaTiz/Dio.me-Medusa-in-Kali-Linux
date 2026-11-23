# Dio.me-Medusa-in-Kali-Linux
Aprendendo sobre brute force com Medusa no Kali Linux e metasploitable em VMs seguindo o curso Santander - Cibersegurança do Zero a prática da DIO.me

Primeiramente baixei o Kali Linux (linux com ferramentas de pentest e etc) e o MetaExplitable (sistema Linux com vulnerabilidades para testar ataques) e rodei ambos em maquinas virtuais usando o Oracle Virtual Box, configurei para que fiquem na mesma rede.

 Comandos usados no terminal :

no Metasploitable:
ip a 
para ver o endereço de IP da maquina virtual.

no Kali linux:
para ver se o metasploitable estava online e visivel pelo Kali na rede rodei o comando de ping com o IP da maquina metasploitable: ping - c 3 192.168.56.102

apos isso verifiquei se todos pacotes foram recebidos com sucesso no terminal


feito isso seguimos para o a enumeração para ver quais portas estavam abertas com comando do NMAP:

nmap -sV -p 21,22,80,445,139 192.168.56.102

todas portas do comando (21,22,80,445,139) estavam abertas.

apos isso o curso nos guiava para tentar descobrir a senha do FTP via brute force com listas de Usuarios e Senhas simples para entendermos o conceito.

comando usado : ftp 192.168.56.102

que pedia usuario e senha para entrar via FTP.

utilizei o comando: echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

e : echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

com isso foi criado arquivos de texto que chamamos de wordlist com senhas e nomes de usuarios prováveis para o teste de força bruta.

com isso rodei o medusa com comando: medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ftp -t 6

isso faz o medusa testar cada nome de usuario e senhas contidas nos aquivos de texto pass.txt e users.txt e o programa retornou sucesso com a senha mfsadmin e usuarios msfadmin.

com isso foi possivel logar com ftp com sucesso na maquina metasploitable via FTP do Kali linux.

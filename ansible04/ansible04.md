## Inventory File

Arquivo de texto comum onde você vai identificar e cadastrar seus alvos. Pode utilizar qualquer nome.

opção **-i** informa o arquivo inventory para ser utilizado.

comando all
```bash
ansible -i hosts all -m ping -u edemir -k
```

ou informar um IP

```bash
ansible -i hosts 192.168.0.102 -m ping -u edemir -k
```
### Grupos e Subgrupos

No arquivo de inventário podemos dividir em grupos e subgrupos.

basta abrir colchetes e definir o grupo

arquivs hosts - invetory file

```bash
[servidores_web]
192.168.0.101

[servidores_bd]
192.168.0.102
```

comando com o grupo servidores_web

```bash
ansible -i hosts servidores_web -m ping -u edemir -k
```

Cadastrando subgrupos

no arquivo hosts incluir subgrupo [nome_grupo:children]

```bash
[servidores_web]
192.168.0.101

[servidores_bd]
192.168.0.102

[servidores:children]
servidores_web
servidores_bd
```

comando com subgrupo

```bash
ansible -i hosts servidores -m ping -u edemir -k
```

### Variaveis hosts

```bash
[servidores_web]
192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102

[servidores:children]
servidores_web
servidores_bd
```

linha de comando 

```bash
ansible -i hosts mysql -m ping -u edemir -k
```

incluindo usuário e senha no arquivo de inventário.

```bash
[servidores_web]
192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102 ansible_ssh_user=edemir ansible_ssh_pass=123qwe ansible_become=yes ansible_become_method=sudo ansible_become_user=edemir ansible_become_pass=123qwe

[servidores:children]
servidores_web
servidores_bd
```

comando:

```bash
ansible -i hosts mysql -m ping
```

vamos elevar o privilégio com o comando **become** alterando o arquivo de inventário **hosts**

```bash
[servidores_web]
192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102 ansible_ssh_user=edemir ansible_ssh_pass=123qwe ansible_become=yes ansible_become_method=sudo
ansible_become_user=edemir ansible_become_pass=123qwe

[servidores:children]
servidores_web
servidores_bd 
```

```bash
ansible -i hosts mysql -m shell -a "sudo apt update"
```

 caso queira alterar o bash que será executado

 ```bash
[servidores_web]
192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102 ansible_ssh_user=edemir ansible_ssh_pass=123qwe ansible_become=yes ansible_become_method=sudo
ansible_become_user=edemir ansible_become_pass=123qwe ansible_sheel_executable=/bin/bash

[servidores:children]
servidores_web
servidores_bd
 ```

 ### Variaveis no arquivo de inventário - Grupos

 alterando o arquivo de hosts

 ```bash
[servidores_web]
www ansible_ssh_host=192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102

[servidores:children]
servidores_web 
servidores_bd

[servidores_bd:vars]
ansible_ssh_port=22
ansible_ssh_user=edemir
ansible_ssh_pass=123qwe
ansible_become=yes
ansible_become_method=sudo
ansible_become_user=edemir
ansible_become_pass=123qwe
ansible_connection=ssh
 ```


 comando de teste

 ```bash
ansible -i hosts mysql -m ping
 ```
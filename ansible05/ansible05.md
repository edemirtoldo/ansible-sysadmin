## Roles e Tasks

O que são Roles ?

Roles
“As roles (funções) são um conjunto de itens independentes destinados
a provisionar uma determinada aplicação/infraestrutura...”

Itens.:
- Variáveis
- Módulos
- Modelos
- Tarefas
- Ações

>Nota.: Pode-se associar-se roles com projetos.

Roles
As roles possuem uma estrutura padrão de diretórios para seus
projetos:

```bash
playbook.yml

roles/
└── common
    ├── defaults
    ├── files
    ├── handlers
    ├── meta
    ├── tasks
    ├── templates
    └── vars
```
para isso devemos criar os diretorios

comandos:

```bash
mkdir roles
cd roles/
mkdir common/{defaults,files,handlers,meta,tasks,templates,vars} -p
cd ..
tree roles/
```
Roles

- tasks – lista de tarefas para serem executadas em uma role.
- handlers – são manipuladores/eventos acionados por uma task.
- files – arquivos utilizados para deploy dentro de uma role.
- templates – modelos para deploy dentro de uma role (permite o uso de
variáveis)
- vars – variáveis adicionais de uma role.
- defaults – variáveis padrão de uma role. Prioridade máxima.
- meta – trata dependências de uma role por outra role – primeiro
diretório a ser analisado.

>Nota.: dentro dos diretórios tasks, handlers, vars, defaults e meta,
deverá existir um arquivo com o nome de main.yml para que o mesmo
seja interpretado.

O caminho tradicional para utilizar-se de uma role pode ser definido
basicamente por.:

```bash
---
- hosts: webservers
  roles:
    - common
    - nginx
    - php
    - mysql
```

> Nota.: O que determina a execução de uma role são as tasks,
cadastradas no arquivo tasks/mail.yml.

## Variáveis

“… variáveis são utilizadas pelo ansible para lhe ajudar a trabalhar com
diferentes tipos de sistemas, arquiteturas e/ou lhe auxiliar no processo
de repetição durante a execução de uma role...”

O ansible interpreta as variáveis de diferentes arquivos. Para isso, o
mesmo mantém a seguinte ordem de prioridades (do menor pro maior).:

1. role/defaults/main.yml
2. inventory file
3. host_vars/*
4. group_vars/all
5. roles/vars/main.yml

> Doc: https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html

As variáveis são comumente utilizadas pelos SysAdmin para facilitar no
provisionamento de seus sistemas/infraestrutura. Entretanto, o ansible
permite através do módulo setup obter o que chamamos de Systems
Facts.

Os Systems Facts são descobertos pelo ansible através do módulo
setup, trazendo informações de todo o sistema. Experimente executar o
comando.:

< ansible hostname -m setup >

## Variáveis no arquivo Inventory

arquivo hosts - inventory

```bash
[servidores_web]
www ansible_ssh_host=192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102

[servidores:children]
servidores_web 
servidores_bd

[servidores:vars]
ansible_ssh_port=22
ansible_ssh_user=edemir
ansible_ssh_pass=123qwe
ansible_become=yes
ansible_become_method=sudo
ansible_become_user=edemir
ansible_become_pass=123qwe
ansible_connection=ssh
```
comando para executar um teste

```bash
ansible -i hosts www -m ping
```
mensagem de retorno:

```bash
www | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}

```

###  Teste prioridade no inventory file - grupos e hosts.

Para testar a prioridade no arquivo de inventário vamos alterar o arquivo hosts, trocando a porta ssh no grupo.

```bash
[servidores_web]
www ansible_ssh_host=192.168.0.101

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102

[servidores:children]
servidores_web 
servidores_bd

[servidores:vars]
ansible_ssh_port=2222
ansible_ssh_user=edemir
ansible_ssh_pass=123qwe
ansible_become=yes
ansible_become_method=sudo
ansible_become_user=edemir
ansible_become_pass=123qwe
ansible_connection=ssh
```
Executando novamente o mesmo comaando com o arquivo hosts alterar agora apresentou erro.

```bash
www | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.0.101 port 2222: No route to host",
    "unreachable": true
}
```

Vamos testar variáveis de grupos e variáveis de hosts no arquivo de inventário (hosts), na variavel de grupos retornamos a porta de ssh para 22 e no host incluimos **ansible_ssh_port=2222**.

```bash
[servidores_web]
www ansible_ssh_host=192.168.0.101 ansible_ssh_port=2222

[servidores_bd]
mysql ansible_ssh_host=192.168.0.102

[servidores:children]
servidores_web 
servidores_bd

[servidores:vars]
ansible_ssh_port=22
ansible_ssh_user=edemir
ansible_ssh_pass=123qwe
ansible_become=yes
ansible_become_method=sudo
ansible_become_user=edemir
ansible_become_pass=123qwe
ansible_connection=ssh
```
será apresentado o erro na porta de ssh 2222, confrmando que a prioridade é do host.

```bash
www | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.0.101 port 2222: No route to host",
    "unreachable": true
}
```

#### Teste de prioridade no host_vars/*

Vamos criar os diretórios host_vars e group_vars

#### Teste de prioridade no group_vars/all

#### Teste de prioridade no roles/vars/main.yml
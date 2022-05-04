# Playbooks

## O que são Playbooks?

Playbooks são maneiras completamente diferente de usar o
modo de execução de tarefa ansible do que no modo adhoc e são
particularmente poderosos. Simplificando, os playbooks são a base
para um sistema de gerenciamento de configuração e multi-
máquina realmente simples, diferente de qualquer um que já exista,
e um que seja muito adequado para implantar aplicativos
complexos.
>Documentação Oficial

- As Playbooks são expressadas em YAML como mínimo de linguagem possível;

- De forma intencional, tenta não ser uma linguagem de programação e/ou script, e sim uma sequência de instruções e/ou processo.
Playbooks são compostos por um ou mais Plays (tarefas);

- O objetivo é reunir um conjunto de hosts (alvos) para roles pré-definidas, representadas por tarefas.

- De forma simplificada, uma tarefa nada mais é que uma chamada para um módulo ansible.

- Com a utilização de múltiplas Plays/Tarefas, o ansible orquestra as implementações ali pré-definidas.
ansible
> Documentação Oficial 
> https://docs.ansible.com/ansible/2.4/ansible-playbook.html

> Working with playbooks
> https://docs.ansible.com/ansible/latest/user_guide/playbooks.html

> Introdução a Playbooks
> https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html#about-playbooks

## Linha de comando - ansible-playbook

``` bash
ansible-playbook --help
```
### --limit - Em caso de falhas

Quando o ansible nao ache um host ele cria um arquivo playbook.retry para poder se executado novamente.

Ele criou um inventario dos hoss que apresentaram falha.

``` bash
ansible-playbook -i hosts playbook.yml --limit @/home/edemir/ansible-sysadmin/playbook.retry
```
ou

``` bash
ansible-playbook -i hosts playbook.yml -l www
```
### check / --syntax-check

para validar sua syntax

```bash
ansible-playbook -i hosts playbook.yml --syntax-check
```
simular a playbook, teste da sequencia

``` bash
ansible-playbook -i hosts playbook.yml --check
```

### -f passar numero de processos - padrão 5

### quais são os alvos --list-hosts

```bash
ansible-playbook -i hosts playbook.yml --list-hosts
```

### quais as tarefas cadastradas --list-tags

``` bash
ansible-playbook -i hosts playbook.yml --list-tasks
```

### alterar argumentos timeout usuario senha

##  Criando e executando uma Playbook - Parte 01

Vamos escrever playbooks

playbook2.yml

```bash
---

- hosts: www
  tasks: 
  - name: Instalação do Ngnix
    yum:
      name: nginx
      state: latest
    notify: stop apache
    notify: restart nginx
  handlers:
    - name: stop apache
      systemd:
        name: httpd
        state: stop
    - name: restart nginx
      systemd:
        name: nginx
        state: restarted

...

```

vamos rodas os testes e depois a playbook

```bash
ansible-playbook -i hosts playbook2.yml --syntax-check

ansible-playbook -i hosts playbook2.yml --check

ansible-playbook -i hosts playbook2.yml
```

outra forma de playbook

```bash
---

- hosts: www
  remote_user: edemir
  become: yes
  become_user: root
  order: sorted
  tasks: 
  - name: Instalação do Ngnix
    yum:
      name: nginx
      state: latest
    notify: stop apache
    notify: restart nginx
  handlers:
    - name: stop apache
      systemd:
        name: httpd
        state: stop
    - name: restart nginx
      systemd:
        name: nginx
        state: restarted
...

```

### Nova playbook

```bash
---

- hosts: www
  remote_user: edemir
  become: yes
  become_user: root
  order: sorted
  tasks: 
  - name: Remocao de pacotes
    yum:
      name: "[u'httpd']"
      state: absent

...
```

 instalando pacotes exemplo

 ``` bash
---

- hosts: www
  remote_user: edemir
  become: yes
  become_user: root
  order: sorted
  tasks: 
  - name: Remocao de pacotes
    yum:
      name: "{{ packages }}"
      state: absent
    vars:
      packages:
        - httpd
        - nginx
  - name: Instalação de pacotes
    yum:
      name: "{{ packages }}"
      state: latest
    vars:
      packages:
        - nmap
        - tcpdump
        - vim        

... 
 ```

 
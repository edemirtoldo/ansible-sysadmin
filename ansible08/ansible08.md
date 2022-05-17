## Features Ansible

### O que é o Ansible Galaxy?

O Ansible Galaxy é um site aonde você pode compartilhar roles para qualquer tipo de atividade: subir um servidor de Zimbra? montar uma infra inteira de OpenShift? Instalar e configurar um banco de Redis? Tudo isso e muito mais. Isso acaba facilitando sua vida, já que ninguém quer ficar criando servidores manualmente, ou até mesmo escrevendo roles que já existem no Ansible Galaxy, né? Num comparativo, o site seria um repositório de roles, e o comando ansible-galaxy o apt/yum do Ansible.

>Site Oficial https://galaxy.ansible.com/


### Comand Line - ansible-galaxy

### ansible-doc

Ansible-doc exibe informações sobre módulos instalados em bibliotecas Ansible. Ele exibe uma lista sucinta de plugins e suas descrições curtas, fornece uma impressão de suas strings de DOCUMENTAÇÃO e pode criar um pequeno “snippet” que pode ser colado em um playbook.

consultar o modulo AWS S3

``` bash
ansible-doc aws_s3
```

Consultar modulo yum

```bash
ansible-doc yum
```

Opção -F para listar os modulos existentes.

```bash
ansible-doc -F
```
Parametro -s mostra uma especie de playbook de um determinado modulo.

```bash
ansible-doc -s yum
```


### Ansible Vault

Pode criptografar qualquer arquivo de dados estruturados usado pelo Ansible. Isso pode incluir variáveis ​​de inventário group_vars/ ou host_vars/ , variáveis ​​carregadas por include_vars ou vars_files ou arquivos de variáveis ​​passados ​​na linha de comando ansible-playbook com -e @file.yml ou -e @file.json . Variáveis ​​de função e padrões também estão incluídos!

Como as tarefas, manipuladores e outros objetos do Ansible são dados, eles também podem ser criptografados com o vault. Se não quiser expor quais variáveis ​​você está usando, você pode manter um arquivo de tarefa individual totalmente criptografado.

> Artigo Ansible Vault https://www.minasnetworking.com.br/index.php?title=Ansible_Vault


> Documentação Oficial Ansible Vault https://docs.ansible.com/ansible/latest/user_guide/vault.html

### Criando um arquivo

Para realizar a criação de um arquivo através do ansible-vault, basta realizar a execução do comando.

``` bash
$ ansible-vault create arquivo.yml
```

Ao executar, será solicitado a criação de uma senha para criptografar os dados. Em seguida, o arquivo abrirá normalmente para edição. Finalizada a criação do arquivo, ao salvar, o conteúdo do arquivo será algo como.:

```bash
bash-5.0$ cat arquivo.yml
$ANSIBLE_VAULT;1.1;AES256
36653333643631373131613033666366383065343035393265643865383364383964623239383062
3666303236656530616330383331396466633937656662350a646264306239393662643738373231
64346235613766353165316365666465326630333064636564386437383835623966643635306361
3533613462633765610a663738353933356364666463323933343736356361643038646364386335
34383364646335646335616536396531313564623333313639363430313061393866
```

### Editando um arquivo

Para editar um arquivo criptografado com o ansible-vault, basta executar o comando

```bash
 $ ansible-vault edit arquivo.yml
 ```

 Feito isso, será solicitado a senha utilizado de criptografia do arquivo.

### Visualizando um arquivo

Uma forma de visualizar o conteúdo do arquivo criptografado é através do comando

```bash
$ ansible-vault view arquivo.yml
```

Feito isso, será solicitado a senha utilizado de criptografia do arquivo.

### Criptografando arquivos

Uma característica bem interessante do ansible-vault, é que ele permite realizar a criptografia de um ou mais arquivos (já existente) simultaneamente. Para realizar tal ação, basta executar

```bash
$ ansible-vault encrypt arquivo1.yml arquivo2.yml
```

Feito isso, será solicitado a senha utilizado para criptografia do arquivo.

### Decriptografando arquivos

Para decriptar um ou mais arquivos, execute.

```bash
$ ansible-vault decrypt arquivo.yml
```

Feito isso, será solicitado a senha utilizado de criptografia do arquivo.

### Executando Playbooks com Vault

Após criar, alterar seus arquivos com o ansible-vault, você já pode realizar a execução de sua Playbook contendo os dados sensíveis e criptografados de seu ambiente. para isso, você deve adicionar um dos parâmetros abaixo em sua execução.:

- **--vault-password-file**: esta opção é utilizada para você adicioar a senha de Vault em um arquivo. Esta pode ser uma boa saída para integrações contínuas, por exemplo. A sintaxe ficaria algo parecido como.

```bash
$ ansible-playbook -i hosts -u user
--vault-password-file password_file playbook.yml
```

- **--ask-vault-pass**: esta opção é utilizada para digitar a senha durante a execução da Playbook. Quando executar, abrirá no prompt para você especificar a senha utilizada para criptografar o ambiente. uma possível sintaxe seria.

```bash
$ ansible-playbook -i hosts -u user --ask-vault-pass playbook.yml
```

> Nota.: É importante ressaltar que e a forma de executar a Playbook (sintaxe) irá variar de acordo com seu ambiente e configurações. O importante são os parâmetros **--vault-password-file** e **--ask-vault-pass**

FIM xx

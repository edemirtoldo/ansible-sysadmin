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


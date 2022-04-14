## Ansible para Sysadmin - repositório

Este é um repositório para estudos do Ansible voltado para Sysadmin.
este

Esse repositório apresenta o Desafio do Docker do curso Kubedev!

- [1- Introdução ao Ansible ](ansible01/ansible01.md)






O Laboratório será composto por 3 maquinas criadas no virtualbox:

| Sistema Operacional | IP            |
|---------------------|:-------------:|
| Windows Server 2012 | 192.168.0.100 |
|- Centos 8           | 192.168.0.101 |
|- Debian 10          | 192.168.0.102 |


## Instalação do Ansible

[Guia de instalação](lhttps://docs.ansible.com/ansible/2.7/installation_guide/intro_installation.html)

## Configurando o ansible (ansible.cfg)

[Documentação ansible.cfg](https://docs.ansible.com/ansible/2.4/intro_configuration.html)

ansible.cfg
- Principal arquivo de configuração do ansible
- Sua localização padrão é /etc/ansible/ansible.cfg
- Alterações e configurações são interpretadas respeitando a
seguinte ordem.:
- Variável ANSIBLE_CONFIG
- ansible.cfg no diretório corrente
- .ansible.cfg no diretório home
- /etc/ansible/ansible.cfg

Doc: https://docs.ansible.com/ansible/latest/reference_appendices/config


### ansible.cfg - padrão

```bash
# config file for ansible -- https://ansible.com/
# ===============================================

# nearly all parameters can be overridden in ansible-playbook
# or with command line flags. ansible will read ANSIBLE_CONFIG,
# ansible.cfg in the current working directory, .ansible.cfg in
# the home directory or /etc/ansible/ansible.cfg, whichever it
# finds first

[defaults]

# some basic default values...

#inventory      = /etc/ansible/hosts
#library        = /usr/share/my_modules/
#module_utils   = /usr/share/my_module_utils/
#remote_tmp     = ~/.ansible/tmp
#local_tmp      = ~/.ansible/tmp
#plugin_filters_cfg = /etc/ansible/plugin_filters.yml
#forks          = 5
#poll_interval  = 15
#sudo_user      = root
#ask_sudo_pass = True
#ask_pass      = True
#transport      = smart
#remote_port    = 22
#module_lang    = C
#module_set_locale = False

# plays will gather facts by default, which contain information about
# the remote system.
#
# smart - gather by default, but don't regather if already gathered
# implicit - gather by default, turn off with gather_facts: False
# explicit - do not gather by default, must say gather_facts: True
#gathering = implicit

# This only affects the gathering done by a play's gather_facts directive,
# by default gathering retrieves all facts subsets
# all - gather all subsets
# network - gather min and network facts
# hardware - gather hardware facts (longest facts to retrieve)
# virtual - gather min and virtual facts
# facter - import facts from facter
# ohai - import facts from ohai
# You can combine them using comma (ex: network,virtual)
# You can negate them using ! (ex: !hardware,!facter,!ohai)
# A minimal set of facts is always gathered.
#gather_subset = all

# some hardware related facts are collected
# with a maximum timeout of 10 seconds. This
# option lets you increase or decrease that
# timeout to something more suitable for the
# environment.
# gather_timeout = 10

# Ansible facts are available inside the ansible_facts.* dictionary
# namespace. This setting maintains the behaviour which was the default prior
# to 2.5, duplicating these variables into the main namespace, each with a
# prefix of 'ansible_'.
# This variable is set to True by default for backwards compatibility. It
# will be changed to a default of 'False' in a future release.
# ansible_facts.
# inject_facts_as_vars = True

# additional paths to search for roles in, colon separated
#roles_path    = /etc/ansible/roles

# uncomment this to disable SSH key host checking
#host_key_checking = False

# change the default callback, you can only have one 'stdout' type  enabled at a time.
#stdout_callback = skippy


## Ansible ships with some plugins that require whitelisting,
## this is done to avoid running all of a type by default.
## These setting lists those that you want enabled for your system.
## Custom plugins should not need this unless plugin author specifies it.

# enable callback plugins, they can output to stdout but cannot be 'stdout' type.
#callback_whitelist = timer, mail

# Determine whether includes in tasks and handlers are "static" by
# default. As of 2.0, includes are dynamic by default. Setting these
# values to True will make includes behave more like they did in the
# 1.x versions.
#task_includes_static = False
#handler_includes_static = False

# Controls if a missing handler for a notification event is an error or a warning
#error_on_missing_handler = True

# change this for alternative sudo implementations
#sudo_exe = sudo

# What flags to pass to sudo
# WARNING: leaving out the defaults might create unexpected behaviours
#sudo_flags = -H -S -n

# SSH timeout
#timeout = 10

# default user to use for playbooks if user is not specified
# (/usr/bin/ansible will use current user as default)
#remote_user = root

# logging is off by default unless this path is defined
# if so defined, consider logrotate
#log_path = /var/log/ansible.log

# default module name for /usr/bin/ansible
#module_name = command

# use this shell for commands executed under sudo
# you may need to change this to bin/bash in rare instances
# if sudo is constrained
#executable = /bin/sh

# if inventory variables overlap, does the higher precedence one win
# or are hash values merged together?  The default is 'replace' but
# this can also be set to 'merge'.
#hash_behaviour = replace

# by default, variables from roles will be visible in the global variable
# scope. To prevent this, the following option can be enabled, and only
# tasks and handlers within the role will see the variables there
#private_role_vars = yes

# list any Jinja2 extensions to enable here:
#jinja2_extensions = jinja2.ext.do,jinja2.ext.i18n

# if set, always use this private key file for authentication, same as
# if passing --private-key to ansible or ansible-playbook
#private_key_file = /path/to/file

# If set, configures the path to the Vault password file as an alternative to
# specifying --vault-password-file on the command line.
#vault_password_file = /path/to/vault_password_file

# format of string {{ ansible_managed }} available within Jinja2
# templates indicates to users editing templates files will be replaced.
# replacing {file}, {host} and {uid} and strftime codes with proper values.
#ansible_managed = Ansible managed: {file} modified on %Y-%m-%d %H:%M:%S by {uid} on {host}
# {file}, {host}, {uid}, and the timestamp can all interfere with idempotence
# in some situations so the default is a static string:
#ansible_managed = Ansible managed

# by default, ansible-playbook will display "Skipping [host]" if it determines a task
# should not be run on a host.  Set this to "False" if you don't want to see these "Skipping"
# messages. NOTE: the task header will still be shown regardless of whether or not the
# task is skipped.
#display_skipped_hosts = True

# by default, if a task in a playbook does not include a name: field then
# ansible-playbook will construct a header that includes the task's action but
# not the task's args.  This is a security feature because ansible cannot know
# if the *module* considers an argument to be no_log at the time that the
# header is printed.  If your environment doesn't have a problem securing
# stdout from ansible-playbook (or you have manually specified no_log in your
# playbook on all of the tasks where you have secret information) then you can
# safely set this to True to get more informative messages.
#display_args_to_stdout = False

# by default (as of 1.3), Ansible will raise errors when attempting to dereference
# Jinja2 variables that are not set in templates or action lines. Uncomment this line
# to revert the behavior to pre-1.3.
#error_on_undefined_vars = False

# by default (as of 1.6), Ansible may display warnings based on the configuration of the
# system running ansible itself. This may include warnings about 3rd party packages or
# other conditions that should be resolved if possible.
# to disable these warnings, set the following value to False:
#system_warnings = True

# by default (as of 1.4), Ansible may display deprecation warnings for language
# features that should no longer be used and will be removed in future versions.
# to disable these warnings, set the following value to False:
#deprecation_warnings = True

# (as of 1.8), Ansible can optionally warn when usage of the shell and
# command module appear to be simplified by using a default Ansible module
# instead.  These warnings can be silenced by adjusting the following
# setting or adding warn=yes or warn=no to the end of the command line
# parameter string.  This will for example suggest using the git module
# instead of shelling out to the git command.
# command_warnings = False


# set plugin path directories here, separate with colons
#action_plugins     = /usr/share/ansible/plugins/action
#become_plugins     = /usr/share/ansible/plugins/become
#cache_plugins      = /usr/share/ansible/plugins/cache
#callback_plugins   = /usr/share/ansible/plugins/callback
#connection_plugins = /usr/share/ansible/plugins/connection
#lookup_plugins     = /usr/share/ansible/plugins/lookup
#inventory_plugins  = /usr/share/ansible/plugins/inventory
#vars_plugins       = /usr/share/ansible/plugins/vars
#filter_plugins     = /usr/share/ansible/plugins/filter
#test_plugins       = /usr/share/ansible/plugins/test
#terminal_plugins   = /usr/share/ansible/plugins/terminal
#strategy_plugins   = /usr/share/ansible/plugins/strategy


# by default, ansible will use the 'linear' strategy but you may want to try
# another one
#strategy = free

# by default callbacks are not loaded for /bin/ansible, enable this if you
# want, for example, a notification or logging callback to also apply to
# /bin/ansible runs
#bin_ansible_callbacks = False


# don't like cows?  that's unfortunate.
# set to 1 if you don't want cowsay support or export ANSIBLE_NOCOWS=1
#nocows = 1

# set which cowsay stencil you'd like to use by default. When set to 'random',
# a random stencil will be selected for each task. The selection will be filtered
# against the `cow_whitelist` option below.
#cow_selection = default
#cow_selection = random

# when using the 'random' option for cowsay, stencils will be restricted to this list.
# it should be formatted as a comma-separated list with no spaces between names.
# NOTE: line continuations here are for formatting purposes only, as the INI parser
#       in python does not support them.
#cow_whitelist=bud-frogs,bunny,cheese,daemon,default,dragon,elephant-in-snake,elephant,eyes,\
#              hellokitty,kitty,luke-koala,meow,milk,moofasa,moose,ren,sheep,small,stegosaurus,\
#              stimpy,supermilker,three-eyes,turkey,turtle,tux,udder,vader-koala,vader,www

# don't like colors either?
# set to 1 if you don't want colors, or export ANSIBLE_NOCOLOR=1
#nocolor = 1

# if set to a persistent type (not 'memory', for example 'redis') fact values
# from previous runs in Ansible will be stored.  This may be useful when
# wanting to use, for example, IP information from one group of servers
# without having to talk to them in the same playbook run to get their
# current IP information.
#fact_caching = memory

#This option tells Ansible where to cache facts. The value is plugin dependent.
#For the jsonfile plugin, it should be a path to a local directory.
#For the redis plugin, the value is a host:port:database triplet: fact_caching_connection = localhost:6379:0

#fact_caching_connection=/tmp



# retry files
# When a playbook fails a .retry file can be created that will be placed in ~/
# You can enable this feature by setting retry_files_enabled to True
# and you can change the location of the files by setting retry_files_save_path

#retry_files_enabled = False
#retry_files_save_path = ~/.ansible-retry

# squash actions
# Ansible can optimise actions that call modules with list parameters
# when looping. Instead of calling the module once per with_ item, the
# module is called once with all items at once. Currently this only works
# under limited circumstances, and only with parameters named 'name'.
#squash_actions = apk,apt,dnf,homebrew,pacman,pkgng,yum,zypper

# prevents logging of task data, off by default
#no_log = False

# prevents logging of tasks, but only on the targets, data is still logged on the master/controller
#no_target_syslog = False

# controls whether Ansible will raise an error or warning if a task has no
# choice but to create world readable temporary files to execute a module on
# the remote machine.  This option is False by default for security.  Users may
# turn this on to have behaviour more like Ansible prior to 2.1.x.  See
# https://docs.ansible.com/ansible/become.html#becoming-an-unprivileged-user
# for more secure ways to fix this than enabling this option.
#allow_world_readable_tmpfiles = False

# controls the compression level of variables sent to
# worker processes. At the default of 0, no compression
# is used. This value must be an integer from 0 to 9.
#var_compression_level = 9

# controls what compression method is used for new-style ansible modules when
# they are sent to the remote system.  The compression types depend on having
# support compiled into both the controller's python and the client's python.
# The names should match with the python Zipfile compression types:
# * ZIP_STORED (no compression. available everywhere)
# * ZIP_DEFLATED (uses zlib, the default)
# These values may be set per host via the ansible_module_compression inventory
# variable
#module_compression = 'ZIP_DEFLATED'

# This controls the cutoff point (in bytes) on --diff for files
# set to 0 for unlimited (RAM may suffer!).
#max_diff_size = 1048576

# This controls how ansible handles multiple --tags and --skip-tags arguments
# on the CLI.  If this is True then multiple arguments are merged together.  If
# it is False, then the last specified argument is used and the others are ignored.
# This option will be removed in 2.8.
#merge_multiple_cli_flags = True

# Controls showing custom stats at the end, off by default
#show_custom_stats = True

# Controls which files to ignore when using a directory as inventory with
# possibly multiple sources (both static and dynamic)
#inventory_ignore_extensions = ~, .orig, .bak, .ini, .cfg, .retry, .pyc, .pyo

# This family of modules use an alternative execution path optimized for network appliances
# only update this setting if you know how this works, otherwise it can break module execution
#network_group_modules=eos, nxos, ios, iosxr, junos, vyos

# When enabled, this option allows lookups (via variables like {{lookup('foo')}} or when used as
# a loop with `with_foo`) to return data that is not marked "unsafe". This means the data may contain
# jinja2 templating language which will be run through the templating engine.
# ENABLING THIS COULD BE A SECURITY RISK
#allow_unsafe_lookups = False

# set default errors for all plays
#any_errors_fatal = False

[inventory]
# enable inventory plugins, default: 'host_list', 'script', 'auto', 'yaml', 'ini', 'toml'
#enable_plugins = host_list, virtualbox, yaml, constructed

# ignore these extensions when parsing a directory as inventory source
#ignore_extensions = .pyc, .pyo, .swp, .bak, ~, .rpm, .md, .txt, ~, .orig, .ini, .cfg, .retry

# ignore files matching these patterns when parsing a directory as inventory source
#ignore_patterns=

# If 'true' unparsed inventory sources become fatal errors, they are warnings otherwise.
#unparsed_is_failed=False

[privilege_escalation]
#become=True
#become_method=sudo
#become_user=root
#become_ask_pass=False

[paramiko_connection]

# uncomment this line to cause the paramiko connection plugin to not record new host
# keys encountered.  Increases performance on new host additions.  Setting works independently of the
# host key checking setting above.
#record_host_keys=False

# by default, Ansible requests a pseudo-terminal for commands executed under sudo. Uncomment this
# line to disable this behaviour.
#pty=False

# paramiko will default to looking for SSH keys initially when trying to
# authenticate to remote devices.  This is a problem for some network devices
# that close the connection after a key failure.  Uncomment this line to
# disable the Paramiko look for keys function
#look_for_keys = False

# When using persistent connections with Paramiko, the connection runs in a
# background process.  If the host doesn't already have a valid SSH key, by
# default Ansible will prompt to add the host key.  This will cause connections
# running in background processes to fail.  Uncomment this line to have
# Paramiko automatically add host keys.
#host_key_auto_add = True

[connection]

# ssh arguments to use
# Leaving off ControlPersist will result in poor performance, so use
# paramiko on older platforms rather than removing it, -C controls compression use
#ssh_args = -C -o ControlMaster=auto -o ControlPersist=60s

# The base directory for the ControlPath sockets.
# This is the "%(directory)s" in the control_path option
#
# Example:
# control_path_dir = /tmp/.ansible/cp
#control_path_dir = ~/.ansible/cp

# The path to use for the ControlPath sockets. This defaults to a hashed string of the hostname,
# port and username (empty string in the config). The hash mitigates a common problem users
# found with long hostnames and the conventional %(directory)s/ansible-ssh-%%h-%%p-%%r format.
# In those cases, a "too long for Unix domain socket" ssh error would occur.
#
# Example:
# control_path = %(directory)s/%%h-%%r
#control_path =

# Enabling pipelining reduces the number of SSH operations required to
# execute a module on the remote server. This can result in a significant
# performance improvement when enabled, however when using "sudo:" you must
# first disable 'requiretty' in /etc/sudoers
#
# By default, this option is disabled to preserve compatibility with
# sudoers configurations that have requiretty (the default on many distros).
#
#pipelining = False

# Control the mechanism for transferring files (old)
#   * smart = try sftp and then try scp [default]
#   * True = use scp only
#   * False = use sftp only
#scp_if_ssh = smart

# Control the mechanism for transferring files (new)
# If set, this will override the scp_if_ssh option
#   * sftp  = use sftp to transfer files
#   * scp   = use scp to transfer files
#   * piped = use 'dd' over SSH to transfer files
#   * smart = try sftp, scp, and piped, in that order [default]
#transfer_method = smart

# if False, sftp will not use batch mode to transfer files. This may cause some
# types of file transfer failures impossible to catch however, and should
# only be disabled if your sftp version has problems with batch mode
#sftp_batch_mode = False

# The -tt argument is passed to ssh when pipelining is not enabled because sudo 
# requires a tty by default. 
#usetty = True

# Number of times to retry an SSH connection to a host, in case of UNREACHABLE.
# For each retry attempt, there is an exponential backoff,
# so after the first attempt there is 1s wait, then 2s, 4s etc. up to 30s (max).
#retries = 3

[persistent_connection]

# Configures the persistent connection timeout value in seconds.  This value is
# how long the persistent connection will remain idle before it is destroyed.
# If the connection doesn't receive a request before the timeout value
# expires, the connection is shutdown. The default value is 30 seconds.
#connect_timeout = 30

# The command timeout value defines the amount of time to wait for a command
# or RPC call before timing out. The value for the command timeout must
# be less than the value of the persistent connection idle timeout (connect_timeout)
# The default value is 30 second.
#command_timeout = 30

[accelerate]
#accelerate_port = 5099
#accelerate_timeout = 30
#accelerate_connect_timeout = 5.0

# The daemon timeout is measured in minutes. This time is measured
# from the last activity to the accelerate daemon.
#accelerate_daemon_timeout = 30

# If set to yes, accelerate_multi_key will allow multiple
# private keys to be uploaded to it, though each user must
# have access to the system via SSH to add a new key. The default
# is "no".
#accelerate_multi_key = yes

[selinux]
# file systems that require special treatment when dealing with security context
# the default behaviour that copies the existing context or uses the user default
# needs to be changed to use the file system dependent context.
#special_context_filesystems=nfs,vboxsf,fuse,ramfs,9p,vfat

# Set this to yes to allow libvirt_lxc connections to work without SELinux.
#libvirt_lxc_noseclabel = yes

[colors]
#highlight = white
#verbose = blue
#warn = bright purple
#error = red
#debug = dark gray
#deprecate = purple
#skip = cyan
#unreachable = red
#ok = green
#changed = yellow
#diff_add = green
#diff_remove = red
#diff_lines = cyan


[diff]
# Always print diff when running ( same as always running with -D/--diff )
# always = no

# Set how many context lines to show in diff
# context = 3
```

### ansible.cfg - modelo para os estudos

```bash
[defaults]

#--- General settings
forks                   = 5
log_path                = /var/log/ansible.log
module_name             = command
executable              = /bin/bash
ansible_managed         = Ansible managed

#--- Files/Directory settings
inventory               = /etc/ansible/hosts
library                 = /usr/share/my_modules
remote_tmp              = ~/.ansible/tmp
local_tmp               = ~/.ansible/tmp
roles_path              = /etc/ansible/roles

#--- Users settings
remote_user             = root
#sudo_user               = root
ask_pass                = no
ask-sudo_pass           = no

#--- SSH settings
remote_port             = 22
timeout                 = 10
host_key_checking       = False
ssh_executable          = /usr/bin/ssh
private_key_file        = ~/.ssh/id_rsa

[privilege_scalation]

become                  = True
become_method           = sudo
become_user             = root
become_ask_pass         = False

[ssh_connection]

scp_if_ssh              = smart
transfer_method         = smart
retries                 = 3
```
Introdução a linha de comando ad-hoc

[Introdução aos comandos ad hoc - documentação](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html)

Local onde está o binario do ansible

```bash
which ansible
```
> /usr/local/bin/ansible

## Comanddos AD-HOC

Fazer uma copia do arquivos hosts no ansible

```bash
cd /etc/ansible
sudo cp hosts hosts_original
```
editar arquivo de hosts

```bash
sudo vim hosts
```
primeiros comandos

-u usuario
-k para exigir senha
-m ping modulo de ping

comando 

```bash
ansible 192.168.0.102 -u edemir -k -m ping
```
retorno do comando
```bash
SSH password: 
192.168.0.34 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

```bash
ansible 192.168.0.34 -u edemir -k -m setup
```

resultado do setup da maquina

```bash
SSH password: 
192.168.0.34 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "192.168.0.34"
        ],
        "ansible_all_ipv6_addresses": [
            "2804:14d:7839:9d7d:a00:27ff:feff:2f6e",
            "fe80::a00:27ff:feff:2f6e"
        ],
        "ansible_apparmor": {
            "status": "enabled"
        },
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "12/01/2006",
        "ansible_bios_vendor": "innotek GmbH",
        "ansible_bios_version": "VirtualBox",
        "ansible_board_asset_tag": "NA",
        "ansible_board_name": "VirtualBox",
        "ansible_board_serial": "NA",
        "ansible_board_vendor": "Oracle Corporation",
        "ansible_board_version": "1.2",
        "ansible_chassis_asset_tag": "NA",
        "ansible_chassis_serial": "NA",
        "ansible_chassis_vendor": "Oracle Corporation",
        "ansible_chassis_version": "NA",
        "ansible_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-4.19.0-19-amd64",
            "quiet": true,
            "ro": true,
            "root": "UUID=0a15368c-266b-4443-8e01-2250ece99c7b"
        },
        "ansible_date_time": {
            "date": "2022-03-10",
            "day": "10",
            "epoch": "1646947331",
            "epoch_int": "1646947331",
            "hour": "18",
            "iso8601": "2022-03-10T21:22:11Z",
            "iso8601_basic": "20220310T182211813317",
            "iso8601_basic_short": "20220310T182211",
            "iso8601_micro": "2022-03-10T21:22:11.813317Z",
            "minute": "22",
            "month": "03",
            "second": "11",
            "time": "18:22:11",
            "tz": "-03",
            "tz_dst": "-03",
            "tz_offset": "-0300",
            "weekday": "quinta",
            "weekday_number": "4",
            "weeknumber": "10",
            "year": "2022"
        },
        "ansible_default_ipv4": {
            "address": "192.168.0.34",
            "alias": "enp0s3",
            "broadcast": "192.168.0.255",
            "gateway": "192.168.0.1",
            "interface": "enp0s3",
            "macaddress": "08:00:27:ff:2f:6e",
            "mtu": 1500,
            "netmask": "255.255.255.0",
            "network": "192.168.0.0",
            "type": "ether"
        },
        "ansible_default_ipv6": {
            "address": "2804:14d:7839:9d7d:a00:27ff:feff:2f6e",
            "gateway": "fe80::ea20:e2ff:fe29:2706",
            "interface": "enp0s3",
            "macaddress": "08:00:27:ff:2f:6e",
            "mtu": 1500,
            "prefix": "64",
            "scope": "global",
            "type": "ether"
        },
        "ansible_device_links": {
            "ids": {
                "sda": [
                    "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795"
                ],
                "sda1": [
                    "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part1"
                ],
                "sda2": [
                    "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part2"
                ],
                "sda5": [
                    "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part5"
                ],
                "sr0": [
                    "ata-VBOX_CD-ROM_VB2-01700376"
                ]
            },
            "labels": {},
            "masters": {},
            "uuids": {
                "sda1": [
                    "0a15368c-266b-4443-8e01-2250ece99c7b"
                ],
                "sda5": [
                    "88095b80-e2d9-4561-bd24-7a0706e29c42"
                ]
            }
        },
        "ansible_devices": {
            "sda": {
                "holders": [],
                "host": "SATA controller: Intel Corporation 82801HM/HEM (ICH8M/ICH8M-E) SATA Controller [AHCI mode] (rev 02)",
                "links": {
                    "ids": [
                        "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795"
                    ],
                    "labels": [],
                    "masters": [],
                    "uuids": []
                },
                "model": "VBOX HARDDISK",
                "partitions": {
                    "sda1": {
                        "holders": [],
                        "links": {
                            "ids": [
                                "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part1"
                            ],
                            "labels": [],
                            "masters": [],
                            "uuids": [
                                "0a15368c-266b-4443-8e01-2250ece99c7b"
                            ]
                        },
                        "sectors": "14774272",
                        "sectorsize": 512,
                        "size": "7.04 GB",
                        "start": "2048",
                        "uuid": "0a15368c-266b-4443-8e01-2250ece99c7b"
                    },
                    "sda2": {
                        "holders": [],
                        "links": {
                            "ids": [
                                "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part2"
                            ],
                            "labels": [],
                            "masters": [],
                            "uuids": []
                        },
                        "sectors": "2",
                        "sectorsize": 512,
                        "size": "1.00 KB",
                        "start": "14778366",
                        "uuid": null
                    },
                    "sda5": {
                        "holders": [],
                        "links": {
                            "ids": [
                                "ata-VBOX_HARDDISK_VB9bc593ba-13bbb795-part5"
                            ],
                            "labels": [],
                            "masters": [],
                            "uuids": [
                                "88095b80-e2d9-4561-bd24-7a0706e29c42"
                            ]
                        },
                        "sectors": "1996800",
                        "sectorsize": 512,
                        "size": "975.00 MB",
                        "start": "14778368",
                        "uuid": "88095b80-e2d9-4561-bd24-7a0706e29c42"
                    }
                },
                "removable": "0",
                "rotational": "1",
                "sas_address": null,
                "sas_device_handle": null,
                "scheduler_mode": "mq-deadline",
                "sectors": "16777216",
                "sectorsize": "512",
                "size": "8.00 GB",
                "support_discard": "0",
                "vendor": "ATA",
                "virtual": 1
            },
            "sr0": {
                "holders": [],
                "host": "IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)",
                "links": {
                    "ids": [
                        "ata-VBOX_CD-ROM_VB2-01700376"
                    ],
                    "labels": [],
                    "masters": [],
                    "uuids": []
                },
                "model": "CD-ROM",
                "partitions": {},
                "removable": "1",
                "rotational": "1",
                "sas_address": null,
                "sas_device_handle": null,
                "scheduler_mode": "mq-deadline",
                "sectors": "2097151",
                "sectorsize": "512",
                "size": "1024.00 MB",
                "support_discard": "0",
                "vendor": "VBOX",
                "virtual": 1
            }
        },
        "ansible_distribution": "Debian",
        "ansible_distribution_file_parsed": true,
        "ansible_distribution_file_path": "/etc/os-release",
        "ansible_distribution_file_variety": "Debian",
        "ansible_distribution_major_version": "10",
        "ansible_distribution_release": "buster",
        "ansible_distribution_version": "10",
        "ansible_dns": {
            "nameservers": [
                "192.168.0.1"
            ]
        },
        "ansible_domain": "",
        "ansible_effective_group_id": 1000,
        "ansible_effective_user_id": 1000,
        "ansible_enp0s3": {
            "active": true,
            "device": "enp0s3",
            "ipv4": {
                "address": "192.168.0.34",
                "broadcast": "192.168.0.255",
                "netmask": "255.255.255.0",
                "network": "192.168.0.0"
            },
            "ipv6": [
                {
                    "address": "2804:14d:7839:9d7d:a00:27ff:feff:2f6e",
                    "prefix": "64",
                    "scope": "global"
                },
                {
                    "address": "fe80::a00:27ff:feff:2f6e",
                    "prefix": "64",
                    "scope": "link"
                }
            ],
            "macaddress": "08:00:27:ff:2f:6e",
            "module": "e1000",
            "mtu": 1500,
            "pciid": "0000:00:03.0",
            "promisc": false,
            "speed": 1000,
            "type": "ether"
        },
        "ansible_env": {
            "HOME": "/home/edemir",
            "LANG": "pt_BR.UTF-8",
            "LANGUAGE": "pt_BR:pt:en",
            "LOGNAME": "edemir",
            "MAIL": "/var/mail/edemir",
            "PATH": "/usr/local/bin:/usr/bin:/bin:/usr/games",
            "PWD": "/home/edemir",
            "SHELL": "/bin/bash",
            "SHLVL": "1",
            "SSH_CLIENT": "192.168.0.46 41382 22",
            "SSH_CONNECTION": "192.168.0.46 41382 192.168.0.34 22",
            "SSH_TTY": "/dev/pts/0",
            "TERM": "xterm-256color",
            "USER": "edemir",
            "XDG_RUNTIME_DIR": "/run/user/1000",
            "XDG_SESSION_CLASS": "user",
            "XDG_SESSION_ID": "18",
            "XDG_SESSION_TYPE": "tty",
            "_": "/usr/bin/python"
        },
        "ansible_fibre_channel_wwn": [],
        "ansible_fips": false,
        "ansible_form_factor": "Other",
        "ansible_fqdn": "debian",
        "ansible_hostname": "debian",
        "ansible_hostnqn": "",
        "ansible_interfaces": [
            "lo",
            "enp0s3"
        ],
        "ansible_is_chroot": false,
        "ansible_iscsi_iqn": "",
        "ansible_kernel": "4.19.0-19-amd64",
        "ansible_kernel_version": "#1 SMP Debian 4.19.232-1 (2022-03-07)",
        "ansible_lo": {
            "active": true,
            "device": "lo",
            "ipv4": {
                "address": "127.0.0.1",
                "broadcast": "",
                "netmask": "255.0.0.0",
                "network": "127.0.0.0"
            },
            "ipv6": [
                {
                    "address": "::1",
                    "prefix": "128",
                    "scope": "host"
                }
            ],
            "mtu": 65536,
            "promisc": false,
            "type": "loopback"
        },
        "ansible_local": {},
        "ansible_lsb": {
            "codename": "buster",
            "description": "Debian GNU/Linux 10 (buster)",
            "id": "Debian",
            "major_release": "10",
            "release": "10"
        },
        "ansible_machine": "x86_64",
        "ansible_machine_id": "5d05d0ca1e90414598d96ca57b1a61e3",
        "ansible_memfree_mb": 832,
        "ansible_memory_mb": {
            "nocache": {
                "free": 901,
                "used": 86
            },
            "real": {
                "free": 832,
                "total": 987,
                "used": 155
            },
            "swap": {
                "cached": 0,
                "free": 974,
                "total": 974,
                "used": 0
            }
        },
        "ansible_memtotal_mb": 987,
        "ansible_mounts": [
            {
                "block_available": 1347755,
                "block_size": 4096,
                "block_total": 1801369,
                "block_used": 453614,
                "device": "/dev/sda1",
                "fstype": "ext4",
                "inode_available": 423962,
                "inode_total": 462384,
                "inode_used": 38422,
                "mount": "/",
                "options": "rw,relatime,errors=remount-ro",
                "size_available": 5520404480,
                "size_total": 7378407424,
                "uuid": "0a15368c-266b-4443-8e01-2250ece99c7b"
            }
        ],
        "ansible_nodename": "debian",
        "ansible_os_family": "Debian",
        "ansible_pkg_mgr": "apt",
        "ansible_proc_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-4.19.0-19-amd64",
            "quiet": true,
            "ro": true,
            "root": "UUID=0a15368c-266b-4443-8e01-2250ece99c7b"
        },
        "ansible_processor": [
            "0",
            "GenuineIntel",
            "Intel(R) Core(TM) i5-8350U CPU @ 1.70GHz"
        ],
        "ansible_processor_cores": 1,
        "ansible_processor_count": 1,
        "ansible_processor_nproc": 1,
        "ansible_processor_threads_per_core": 1,
        "ansible_processor_vcpus": 1,
        "ansible_product_name": "VirtualBox",
        "ansible_product_serial": "NA",
        "ansible_product_uuid": "NA",
        "ansible_product_version": "1.2",
        "ansible_python": {
            "executable": "/usr/bin/python",
            "has_sslcontext": true,
            "type": "CPython",
            "version": {
                "major": 2,
                "micro": 16,
                "minor": 7,
                "releaselevel": "final",
                "serial": 0
            },
            "version_info": [
                2,
                7,
                16,
                "final",
                0
            ]
        },
        "ansible_python_version": "2.7.16",
        "ansible_real_group_id": 1000,
        "ansible_real_user_id": 1000,
        "ansible_selinux": {
            "status": "disabled"
        },
        "ansible_selinux_python_present": true,
        "ansible_service_mgr": "systemd",
        "ansible_ssh_host_key_ecdsa_public": "AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMcOFy1ADTKgs/WEmdobmpBFojqgTx2DqcJjdT2EQTHN/KCpi9xiG09CrIZ/T8vjGg4D2mJGdlZ/dl8n+11D2zo=",
        "ansible_ssh_host_key_ecdsa_public_keytype": "ecdsa-sha2-nistp256",
        "ansible_ssh_host_key_ed25519_public": "AAAAC3NzaC1lZDI1NTE5AAAAILsv0D2GJwRevpq6xnDp8EhAzQaVoCysCW0FCPzXmrKI",
        "ansible_ssh_host_key_ed25519_public_keytype": "ssh-ed25519",
        "ansible_ssh_host_key_rsa_public": "AAAAB3NzaC1yc2EAAAADAQABAAABAQDL2KFBsmhbQpzdqZvSZGx5gRLzI9RVl/zQLyZ1MUrSq2ipM+1rLT3FRn4YxkBiDV0nu/nUBzFVaehV9ttTeud6+AHY4SmpwNpd3sb+zgMdFRnxcBdqZZF3VuJee9AOEinoE9Vqqm1VI6BiVFFFD1q7qzYFPa+8PBL2LcEmlJOFGMQR5Cen1Gzrsclb2l/xt/qyJTQ2d3ZF1tL4RCOr1BgoCesUVZ+2ULBoe4KFtrNgYA6rmQiGrVjFIXZzK6wG/IrlST2ybFuFS40HuFqlBK378AwNGwoO7Mi2qqQy7BXkimpINiPhZySaKJJidmmyzb+M/lLqZtRKkW5XsYYqP1KT",
        "ansible_ssh_host_key_rsa_public_keytype": "ssh-rsa",
        "ansible_swapfree_mb": 974,
        "ansible_swaptotal_mb": 974,
        "ansible_system": "Linux",
        "ansible_system_capabilities": [
            ""
        ],
        "ansible_system_capabilities_enforced": "True",
        "ansible_system_vendor": "innotek GmbH",
        "ansible_uptime_seconds": 3085,
        "ansible_user_dir": "/home/edemir",
        "ansible_user_gecos": "edemir,,,",
        "ansible_user_gid": 1000,
        "ansible_user_id": "edemir",
        "ansible_user_shell": "/bin/bash",
        "ansible_user_uid": 1000,
        "ansible_userspace_architecture": "x86_64",
        "ansible_userspace_bits": "64",
        "ansible_virtualization_role": "guest",
        "ansible_virtualization_tech_guest": [
            "virtualbox"
        ],
        "ansible_virtualization_tech_host": [],
        "ansible_virtualization_type": "virtualbox",
        "discovered_interpreter_python": "/usr/bin/python",
        "gather_subset": [
            "all"
        ],
        "module_setup": true
    },
    "changed": false
}
```
modulo systemd iniciando o serviço de ssh

-m systemd -a "name=ssh state=restarted"

ansible 192.168.0.34 -u edemir -k -m systemd -a "name=ssh state=restarted"

elevar o privilegio opção:

-b 

ansible 192.168.0.34 -u edemir -k -b -m systemd -a "name=ssh state=restarted"

notamos que o resultado vem na cor amarela por que foi alterado quando não ocorre alteração o resultado é verde

podemos consultar o status do serviço ssh

```bash
ansible 192.168.0.34 -u edemir -k -b -m shell -a "systemctl status ssh"
```
opção -K (maiusculo) digitar senha elevação de provilegio

```bash
ansible 192.168.0.34 -u edemir -k -K -b -m shell -a "systemctl status ssh"
```
executando o mudulo comand por padrão
comando pwd

```bash
ansible 192.168.0.34 -u edemir -k -a "pwd"
```

executar em modo verbose
```bash
ansible 192.168.0.34 -u edemir -k -a "pwd" -vvv
```

alterar o 
ask_pass = yes
ask-sudo_pass = no



texto

```bash

```
[-nome do link-](teste)

correção do texto


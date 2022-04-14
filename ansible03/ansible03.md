# Comandos ad-hoc

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

ansible 192.168.0.101 -u edemir -k -m systemd -a "name=ssh state=restarted"

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

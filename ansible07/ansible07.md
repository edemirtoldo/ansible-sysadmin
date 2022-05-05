## Targets Micrososoft Windows

> Documentação 
> https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#winrm-setup


Para que o Ansible se comunique com um host Windows e use módulos do Windows, o host Windows deve atender a estes requisitos:

- O Ansible geralmente pode gerenciar versões do Windows sob suporte atual e estendido da Microsoft. O Ansible pode gerenciar sistemas operacionais de desktop, incluindo Windows 7, 8.1 e 10, e sistemas operacionais de servidor, incluindo Windows Server 2008, 2008 R2, 2012, 2012 R2, 2016 e 2019.

- O Ansible requer que o PowerShell 3.0 ou mais recente e pelo menos o .NET 4.0 seja instalado no host do Windows.

- Um ouvinte WinRM deve ser criado e ativado. Mais detalhes para isso podem ser encontrados abaixo.

### Atualizando o PowerShell e o .NET Framework

O Ansible requer o PowerShell versão 3.0 e .NET Framework 4.0 ou mais recente para funcionar em sistemas operacionais mais antigos, como Server 2008 e Windows 7. A imagem base não atende a esse requisito. Você pode usar o script Upgrade-PowerShell.ps1 para atualizá-los.

Este é um exemplo de como executar este script do PowerShell:

Deve informar a senha no campo **$password**.

``` sh
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Upgrade-PowerShell.ps1"
$file = "$env:temp\Upgrade-PowerShell.ps1"
$username = "Administrator"
$password = "Password"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force

# Version can be 3.0, 4.0 or 5.1
&$file -Version 5.1 -Username $username -Password $password -Verbose
```

Windows Server 

como descobrir 

winrm enumered winrm/config/Listener


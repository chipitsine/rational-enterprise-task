# automatic nginx on Windows installation


# SSL Certificates

SSL certificates were created using an [XCA](https://hohnstaedt.de/xca/) tool

# Sensitive info

sensitive info is kept within ansible-vault protected group_vars/all, vault password is `tiajIddAiWamjoogerOc`

# Conventions

the idea is to keep as simple as possible. Everything is installed to `c:\rational`, nginx is bound to 443 port. SSL configuration prepared in [Mozilla generator](https://ssl-config.mozilla.org/). No parametrization unless explicitly mentioned in task.

# Server preparation (user and winrm)

user creation:

```
$UnsecurePassword = 'bayshnocdunmovvijiv4'
$SecurePassword = ConvertTo-SecureString $UnsecurePassword -AsPlainText -Force

New-LocalUser 'taskadmin' -Password $SecurePassword -FullName 'task local admin' -Description 'Temporary local admin'
Add-LocalGroupMember -Group 'Administrators' -Member 'taskadmin'
```

winrm was enabled by the following [script](https://raw.githubusercontent.com/psconfeu/2018/e41a7dbc5af61976f48000882840bd65e3e11c45/Wojciech%20Sciesinski/Ansible/Demo-1/ConfigureRemotingForAnsible.ps1)

# playbook invocation (on WSL)

```
ansible-playbook -i hosts playbook.yaml
```
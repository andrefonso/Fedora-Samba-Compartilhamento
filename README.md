# Fedora-Samba-Compartilhamento
#### **Tutorial para instalação do Samba e Configuração de compartilhamento de arquivos no Fedora**
---

<img src="/imagens/samba.png">      <img src="/imagens/fedora.png">

1) Instalação e ativação do Samba:</br>
```
sudo dnf install samba
sudo systemctl enable smb --now
firewall-cmd --get-active-zones
sudo firewall-cmd --permanent --zone=FedoraWorkstation --add-service=samba
sudo firewall-cmd --reload
```

2) Compartilhamento de pasta:

 - Criar usuário:</br>
   ``sudo smbpasswd -a andre``
   
 - Digitar os comandos abaixo para compartilhar a pasta Documentos na minha hoje:</br>
 ```
   sudo semanage fcontext --add --type "samba_share_t" "/home/andre/Documentos(/.*)?"
   sudo restorecon -R ~/Documentos
```
  
 - Editar o arquivo smb.conf e inserir o seguinte conteúdo:</br>
```
[Documentos]
comment = pasta compartilhada
path = /home/andre/Documentos
valid users = andre
read only = no
browseable = yes
writeable = yes
guest ok = no
create mask = 0765
directory mask = 0755
write list = user
```
        
- Restartar o Samba para que as mudanças surtam efeito:</br>
 ``sudo systemctl restart smb nmb``
 
 Fonte de pesquisa: https://docs.fedoraproject.org/en-US/quick-docs/samba/



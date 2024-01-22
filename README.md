# Fedora-Samba-Compartilhamento
### **Tutorial para instalação do Samba e Configuração de compartilhamento de arquivos no Fedora**
---

**1) Instale o Samba:**</br>
   `sudo dnf install samba`
   
**2) Configure o compartilhamento:**</br>
   - Abra o arquivo de configuração do Samba:</br>
   `sudo nano /etc/samba/smb.conf`

   - Adicione o seguinte bloco no final do arquivo para compartilhar a pasta "Documentos":

   ```
   [Documentos]
   path = /home/andre/Documentos
   read only = no
   guest ok = yes
   ```
   - Salve e feche o arquivo.

**3) Adicione seu usuário ao grupo Samba:**</br>
   `sudo usermod -aG smbusers andre`
   
**4) Configure uma senha para o usuário no Samba:**</br>
  `sudo smbpasswd -a andre`

**5) Habilite a inicialização automática do serviço Samba:**</br>
   `sudo systemctl enable smb`

**6) Reinicie o serviço Samba:**</br>
  ```
  sudo systemctl restart smb.service
  sudo systemctl restart nmb.service
```

**7) Abra as portas necessárias no firewall (se estiver ativado):**</br>
  ```
sudo firewall-cmd --permanent --add-service=samba
sudo firewall-cmd --permanent --zone=public --add-service=samba
sudo firewall-cmd --reload
```


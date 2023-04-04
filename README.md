Tutorial para criar um servidor Samba no Ubuntu Server
======================================================

O Samba é uma ferramenta que permite compartilhar arquivos e impressoras entre sistemas Linux e Windows. 
Este tutorial irá guiá-lo através dos passos para instalar e configurar um servidor Samba em um sistema com Ubuntu Server.

Instalando o Ubuntu Server
--------------------------

Antes de começar, você precisará instalar o Ubuntu Server em seu sistema. Você pode encontrar um guia passo a passo de como instalar o Ubuntu Server [aqui](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview).

Instalando o Samba
------------------

Para instalar o Samba, abra o terminal e execute o seguintes comandos:

```
sudo apt-get update
```
```
sudo apt-get install samba
```

Criando um usuário Samba
------------------------

Agora, você precisa criar um usuário Samba para acessar a pasta compartilhada. Para criar um usuário sem uma conta de login, execute o seguinte comando:

```
sudo adduser --no-create-home --disabled-login smb-usuario
```

Substitua ```smb-usuario``` pelo nome de usuário que deseja usar.

Para permitir que o usuário Samba acesse a pasta compartilhada, defina uma senha para ele com o seguinte comando:

```
sudo -s smbpasswd -a smb-usuario
```

Substitua `smb-usuario` pelo nome de usuário que você criou anteriormente. Digite uma senha segura quando solicitado.

Criando uma pasta compartilhada
-------------------------------

Crie uma pasta na qual deseja compartilhar arquivos. Por exemplo:

```
sudo mkdir -p /share/smb-pasta-compartilhada
```

Agora, defina o usuário e o grupo de proprietários da pasta para o usuário Samba que criamos anteriormente:

```
sudo chown smb-usuario:smb-usuario /share/smb-pasta-compartilhada
```

Finalmente, defina as permissões da pasta:

```
sudo chmod 770 /share/smb-pasta-compartilhada
```

Configurando o compartilhamento Samba
-------------------------------------

Abra o arquivo de configuração do Samba com o seguinte comando:

```
sudo nano /etc/samba/smb.conf
```

Role para a seção `[homes]` e adicione as seguintes linhas abaixo dela:

```
[smb-pasta-compartilhada] 
path = /share/smb-pasta-compartilhada 
valid users = smb-usuario 
read only = no
```

Substitua `/share/smb-pasta-compartilhada` pelo caminho da pasta que deseja compartilhada.

Salve e saia do arquivo de configuração do Samba.


Reiniciando o serviço Samba
---------------------------

Para que as alterações entrem em vigor, reinicie o serviço Samba com o seguinte comando:

```
sudo systemctl restart smbd.service
```

Conclusão
---------

Pronto! Agora você tem um servidor Samba configurado e uma pasta compartilhada para usar em seu sistema Ubuntu Server. Você pode se conectar a esta pasta a partir de outros sistemas usando um cliente Samba ou explorador de arquivos.

Contribuição
------------

Contribuições são bem-vindas! Se você encontrar algum problema ou tiver sugestões para melhorar o tutorial, sinta-se à vontade para abrir uma issue ou enviar um pull request.

Se você gostou do meu trabalho e quer me agradecer, você pode me pagar um café :)

<a href="https://www.paypal.com/donate/?hosted_button_id=SFR785YEYHC4E" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 40px !important;width: 150px !important;" ></a>


Licença
-------

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo LICENSE para obter mais informações.

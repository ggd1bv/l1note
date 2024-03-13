# UPDATE
sudo apt update

sudo apt upgrade

# CAMBIAR PORT SSH
/etc/ssh/sshd_config

port 13970 o 2223

sudo /etc/init.d/ssh restart

ssh -p 13970 ubuntu@ip...

# HABILITAR FIREWALL
sudo ufw allow OpenSSH

sudo ufw allow 13970/tcp (el port ssh)

sudo ufw enable

# CAMBIAR PASS ROOT
sudo passwd root

# CAMBIAR USUARIO DEFAULT
Permite que las cuentas ejecuten comandos como otras cuentas, incluida la raíz . 

* Usuarios que forman parte del grupo Sudo
cat /etc/group | grep "sudo"
*Crear grupo:
sudo groupadd sudousers
*Añadir cuentas
 sudo usermod -a -G sudousers user1
 sudo usermod -a -G sudousers user2

*Copia de seguridad del archivo de configuración de sudo /etc/sudoers
 sudo cp --archive /etc/sudoers /etc/sudoers-COPY-$(date +"%Y%m%d%H%M%S")

* En caso de que no hayamos instalado el sistema nosotros
 sudo adduser newUser  
 sudo adduser newUser sudo  ( usermod -aG sudo lau ) 
 ssh -p 13970 newUser@ip...

- - - RESTRICCIONES SSH
 sudo vi /etc/ssh/sshd_config
 LoginGraceTime : 2m
 StrictMode : yes
 MaxAuthTries: 5
 MaxSessions: 2 ( o la cantidad de usuarios que van a acceder)
 sudo /etc/init.d/ssh restart

- - - LIMITAR QUIÉNES USAN SU
Permite que las cuentas ejecuten comandos como otras cuentas, incluida la raíz .
 sudo groupadd suusers
 sudo usermod -a -G suusers user1
* Solo los usuarios de este grupo puedan ejecutar /binsu:
 sudo dpkg-statoverride --update --add root suusers 4750 /bin/su



- - - FORZAR INICIO CON SSH

La clave pública se transfiere al servidor mientras que la clave privada permanece en nuestra computadora local.

# Generar clave en CLIENTE (no en el servidor)
 ssh-keygen -t rsa -b 4096 -C "your@email.com"
- Default: /home/newUser/.ssh/id_rsa
 Resguadar la clave
 chmod 600 id_rsa

# En el Servidor
 mkdir ~/.ssh (Crear carpeta)
 vim ~/.ssh/authorized_keys (Crear archivo)

- Pegar el contenido de la clave pública, si se usa el nombre default:
 id_rsa.pub
 /etc/ssh/sshd_config
 PubkeyAuthentication: yes
 sudo /etc/init.d/ssh restart
 exit
- Verificar acceso:
 ssh -p 13970 -i path/to/your/private/key/id_rsa newUser@ip...

- En caso que se pueda entrar sin que pida la clave procedemos a deshabilitar el acceso con contraseña:
 /etc/ssh/sshd_config
 PasswordAuthentication: no
 /etc/init.d/ssh restart

- - - FAIL2BAN
 sudo apt install fail2ban
- Archivos de configuración en: 
 /etc/fail2ban
  fail2ban.conf
 jail.conf (Servicios a monitorear)
 sudo cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
 sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

 sudo nano /etc/fail2ban/jail.local
 bantime
 findtime
 maxretry  (intentos fallidos)

 En la Sección Jail se mencionan muchos servicios sshd, dropbear, selinux-ssh, cada uno es una "carcel"

SSH es el servicio más importante en el servidor porque permite el acceso al servidor. fail2ban por defecto, monitorea sshd en busca de fallas de autenticación

 sudo fail2ban-client status


- - - CLIENTE NTP

- Usamos el cliente NTP en el servidor para actualizar la hora del servidor con la hora oficial extraída de los servidores oficiales. 
 sudo apt install ntp

- Copia de seguridad del archivo de configuración del cliente NTP /etc/ntp.conf:
 sudo cp --archive /etc/ntp.conf /etc/ntp.conf-COPY-$(date +"%Y%m%d%H%M%S")

Nos asegurarnos que usamos la directiva  pool y no cualquier otro server. Esto permite que el cliente NTP deje de usar un servidor si no responde o cumple una mala hora. 

*** Recomendacioens para SV offline ? ( está pensado para vps o servers con acceso a inet)

 Comentando TODAS las directivas Server y solo agregar en etc/ntp.conf: 
 pool pool.ntp.org iburst

** Bonus: 
sudo sed -i -r -e "s/^((server|pool).*)/# \1         # commented by $(whoami) on $(date +"%Y-%m-%d @ %H:%M:%S")/" /etc/ntp.conf
echo -e "\npool pool.ntp.org iburst         # added by $(whoami) on $(date +"%Y-%m-%d @ %H:%M:%S")" | sudo tee -a /etc/ntp.conf

- Configurar Timezone
  sudo timedatectl set-timezone America/Buenos_Aires

  sudo service ntp restart


- - - 

A DEBATIR - EN DESARROLLO


- - - ACTUALIZACIONES AUTOMÁTICAS ??

- - - CAMBIAR PORT FTP ?? 

- - - UPDATE KERNEL SIN REINICIAR ??

- - - ENMASCARAR IP DEL SV DETRAS DE UN FW EN LA NUBE
Cuando aloja un sitio web en su servidor, el nombre de dominio puede revelar la dirección IP del servidor. Se recomienda enmascarar la dirección IP detrás de un firewall en la nube como Cloudflare . Cloudflare y otros cortafuegos en la nube similares pueden enmascarar la dirección IP del servidor de origen detrás de su dirección IP.

- - - CON CPANEL USAR 2FA

- - - SPAMASSASSIN (para correo electrónico)
 sudo apt install spamassassin


- - - Seguridad en AUTOMATIZACIÓN Ansible , Chef , Jenkins , Puppet 

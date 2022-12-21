# GLPI-Installation-Guide-Ubuntu_22.04
GLPI Installation Guide Ubuntu 22.04

### 0.666 CONCLUSIONES FINALES

### 1. INSTALACIÓN DE APACHE

```shell
apt-get install apache2
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190367570-093d6ac2-c0b4-4a21-b824-cae5bb0f524e.png)</kbd>

En un navegador, accedemos a la URL de nuestro máquina virtual y comprobamos si funciona:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190367841-1938c201-9728-45b7-85e6-ec12a9243a86.png)</kbd>

### 2. INSTALACIÓN DE PHP 8

```shell
sudo apt install ca-certificates apt-transport-https software-properties-common
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368199-ff183676-8553-48b7-a5f1-d292dcc2c886.png)</kbd>

```shell
sudo add-apt-repository ppa:ondrej/php
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368451-23265c03-e5ef-4f68-b0bf-31f9cd753b5d.png)</kbd>


```shell
sudo apt install php8.0 libapache2-mod-php8.0
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368692-aac9c322-5e4f-49cc-8958-a81dd3dacc53.png)</kbd>


```shell
sudo systemctl restart apache2
```

```shell
php -v
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190368901-e0382902-a13d-4cd1-b787-579ea2a61183.png)</kbd>

#### 2.1 INSTALACIÓN DE LA EXTENSIÓN MYSQLI PARA PHP 8

```shell
sudo apt install php8.0-mysqli 
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190369709-a8a97c4f-1566-4406-b1f3-9002e1756e64.png)</kbd>

Para comprobar que funciona, creamos un fichero en /var/www/html llamado info.php por ejemplo

```shell
nano /var/www/html/info.php
```

y escribimos estas líneas:

 ```shell
<?php
phpinfo();
?>
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190370162-be39a198-143b-4dce-9141-5c5c39810069.png)</kbd>

Desde nuestro navegador, visitamos la URL de nuestro servidor Apache y añadimos el nombre del fichero que hemos creado:

```shell
http://192.168.46.214/info.php
```

Si todo está correcto hasta ahora, veremos algo similar a esto:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190371854-5b08c8a9-bea8-4078-a629-b43c2156a28b.png)</kbd>

#### Warning - :skull: Haz un Snapshot :eyes:

### 3. INSTALACIÓN DE MYSQL DATABASE

```shell
sudo apt install mysql-server
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190381304-84dea3a9-69d8-4e68-8cda-6aca37be3508.png)</kbd>

#### 3.1 CONFIGURACIÓN DE MYSQL

```shell
sudo mysql_secure_installation
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190381413-b33bebe1-d0a4-474a-97ac-a24967ba3693.png)</kbd>

Si nos aparece este error:

<kbd>![image](https://user-images.githubusercontent.com/20743678/190382549-7923d3a9-928b-4ba9-ac7b-1f673b9f3916.png)</kbd>

Tendremos que cerrar el terminal a la brava, del aspa en la esquina. Luego abrimos un nuevo terminal y ejecutamos el comando:

```shell
sudo su
```

```shell
mysql
```

```shell
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'mynewpassword';
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190383805-69981a35-ec36-4a59-97b9-06e54cfcea03.png)</kbd>

Salimos con exit:

```shell
exit
```

Y probamos de nuevo el comando y seguimos el asistente:

```shell
sudo mysql_secure_installation
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190384498-6d7eaec6-cec5-4b84-8c30-7b9ea87c0510.png)</kbd>

Probamos si MySQL funciona:

```shell
systemctl status mysql.service
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/190384728-a043ed3b-e1ab-4614-a8a2-96c50c9c8618.png)</kbd>

#### Warning - :skull: Haz un Snapshot :eyes:

### 4. DESCARGA E INSTALACIÓN DE GLPI

Desde su repositorio ofical descargamos el fichero:

https://github.com/glpi-project/glpi/releases/

<kbd>![image](https://user-images.githubusercontent.com/20743678/191053727-2177da39-eb70-4e42-8b25-e64518196073.png)</kbd>

El día de redacción de este manual, la última versión es la 10.0.0.5. Podemos descargarlo con el comando:

```shell
wget https://github.com/glpi-project/glpi/releases/download/10.0.5/glpi-10.0.5.tgz
```

```shell
tar xzvf glpi-10.0.5.tgz
```

Lo descomprimimos en "Descargas" por ejemplo, y lo copiamos con 'sudo' en /var/www/html

```shell
cp -r glpi /var/www/html/
```

Asignamos permisos de escritura al servidor web a la carpeta 'files' y 'config' dentro de '/var/www/html/glpi':

```shell
cd /var/www/html/glpi
```

```shell
chown www-data config
```

```shell
chown www-data:www-data files
```

Desde un navegador, accedemos a la URL de nuestro servidor:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191054247-1bf5e278-5997-46d1-adc1-160eae73def0.png)</kbd>

#### Warning - :skull: Sería un buen momento para hacer un Snapshot :eyes:

En la siguiente ventana nos pregunta si vamos a hacer una instalación o una actualización:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191054662-9f933bb2-6a6a-4bed-9f95-371c2033e350.png)</kbd>

Como siempre con estos asistentes de instalación, nos saldrá un listado de compatibilidad que tendremos que ir saneando antes de proseguir con la instalación:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191054938-9cad8ab5-53c4-4fd6-8e19-f53706ff72b7.png)</kbd>

Comenzamos por el principio y vamos arreglando:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191055301-861b3623-32a1-406b-ab8d-66a29a6606db.png)</kbd>

```shell
sudo apt install php8.0-dom
```

```shell
systemctl restart apache2
```

Siguientes errores:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191056014-438b0ba5-58c7-4474-80ad-36098ca1c30a.png)</kbd>

```shell
sudo apt install php8.0-curl
```

```shell
sudo apt install php8.0-gd
```

```shell
sudo apt install php8.0-intl
```

```shell
systemctl restart apache2
```

Continuamos con los errores de permisos, que no estaban muy finos de antes:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191056992-5d50096d-0a3a-47df-82e4-72b56fe101e6.png)</kbd>

```shell
chown www-data:www-data files
```

```shell
chmod -R 755 files
```

```shell
systemctl restart apache2
```

Siguientes errores, calentad, que salís:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191206354-adb88416-5923-4206-9cb2-ac0e0e14204b.png)</kbd>

Editamos el siguiente fichero:

> /etc/apache2/apache2.conf

```shell
sudo nano /etc/apache2/apache2.conf
```

Y alrededor de la línea 172, cambiamos "AllowOverride None" por "AllowOverride All"

<kbd>![image](https://user-images.githubusercontent.com/20743678/191207442-511914c8-3221-472e-8532-b04056e7c0bb.png)</kbd>

Reiniciamos apache:

```shell
sudo systemctl restart apache2
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/191208104-945bbce7-ab14-4811-a683-95085405b74c.png)</kbd>

Problema solucionado. Vamos a por el siguiente.

Editamos el siguiente fichero

> /etc/php/8.0/apache2/php.ini

```shell
sudo nano /etc/php/8.0/apache2/php.ini
```

Y alrededor de la línea 1399, cambiamos "session.cookie_httponly =" por "session.cookie_httponly = On"

<kbd>![image](https://user-images.githubusercontent.com/20743678/191209677-f8b15ccb-2331-4b04-8a7c-e46205119847.png)</kbd>

Reiniciamos apache:

```shell
sudo systemctl restart apache2
```

Problema solucionado. A por los siguientes:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191211107-d50cf4b4-0008-44c7-b72b-48553be2cb86.png)</kbd>

#### Warning - :skull: Sería un buen momento para hacer un Snapshot :eyes:

Instalamos las extensiones que nos faltan (ldap, zip, bz2, ctype, iconv, sodium y mbstring)

```shell
sudo apt install php8.0-ldap
```

```shell
sudo apt install php8.0-zip
```

```shell
sudo apt install php8.0-bz2
```

```shell
sudo apt install php8.0-ctype
```

```shell
sudo apt install php8.0-iconv
```

```shell
sudo apt install php8.0-mbstring
```

```shell
sudo systemctl restart apache2
```

> La extensión sodium se instala aparentemente con alguna de las instalaciones anteriores, ya que con el comando "sudo apt install php8.0-sodium" nos sale un error. Buscando en Google, aparentemente hay que descargarlo a mano , compilar y copiar en su carpeta de destino, pero instalando las otras anteriormente mencionadas, el error de falta de esta extensión desaparece:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191215309-7bbf6c55-c807-4d6c-aa96-cf6ff23cadd8.png)</kbd>

Continuamos con el último warning, los permisos para el directorio /var/www/html/marketplace

<kbd>![image](https://user-images.githubusercontent.com/20743678/191215757-b7cdf3e7-99a4-4f6a-a92b-97957fd37461.png)</kbd>

```shell
chown www-data:www-data marketplace
```

```shell
chmod -R 755 marketplace
```

Refrescamos el navegador de nuestra instalación y voilà, momento satisfactorio :sunglasses:. Podemos proseguir la instalación con la conciencia tranquila.

<kbd>![image](https://user-images.githubusercontent.com/20743678/191221262-42633b49-885e-4b08-aa66-230560344a30.png)</kbd>

Rellenamos los datos de nuestra conexión a la base de datos. EL usuario y contraseña de MySQL lo definimos anteriormente en la instalación de MySQL

<kbd>![image](https://user-images.githubusercontent.com/20743678/191222258-9f103912-a6cc-4612-9ee7-ba9df91fc5aa.png)</kbd>

Creamos una nueva BD. Yo la he llamado "glpi"

<kbd>![image](https://user-images.githubusercontent.com/20743678/191222459-d5b0692c-d725-490c-a0e6-1f5b71f1d894.png)</kbd>

<kbd>![image](https://user-images.githubusercontent.com/20743678/191222613-fb9dbb9f-ddfc-471d-91fb-0d687b8ad5a3.png)</kbd>

Configuramos nuestras preferencias de compartición de datos con GLPI:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191223003-605e8b81-632b-4df8-b162-a88e366ebbae.png)</kbd>

La instalación nos ofrece la posibilidad de contratar un servicio comercial mediante una URL para la puesta en marcha y/o resolución de errores y bugs

<kbd>![image](https://user-images.githubusercontent.com/20743678/191223470-56245ef6-dc98-4bdc-b8e5-8d03900e272a.png)</kbd>

En el último paso nos muestra un resumen de las contraseñas por defecto para poder empezar a trabajar, las cuales tendremos que modificar por unas personalizadas mediante el frontend, pero es conveniente apuntarlas o tenerlas a mano en los primeros momentos de uso.

</kbd>![image](https://user-images.githubusercontent.com/20743678/191223749-b362f507-d6be-4165-83d3-5e4c54483003.png)</kbd>

Nos logueamos como admin con glpi/glpi y nos aparece una advertencia de seguridad en la que nos recomienda:

* Cambiar la contraseña por defecto de los usuarios: glpi, post-only, tech y normal
* Eliminar el fichero install/install.php

<kbd>![image](https://user-images.githubusercontent.com/20743678/191227152-03e361ff-fea8-4ded-853a-fe8d9fc24e03.png)</kbd>

Para eliminar el fichero install/install.php, usamos el comando siguiente:

```shell
sudo rm /var/www/html/install/install.php
```

<kbd>![image](https://user-images.githubusercontent.com/20743678/191227577-088c0823-078c-49cf-bb4b-27462c00ecd9.png)</kbd>

Y para cambiar las contraseñas de los usuarios, en el frontend, vamos al menú "Administración" y dentro de él, "usuarios". Accedemos a cada uno de ellos y cambiamos el password:

<kbd>![image](https://user-images.githubusercontent.com/20743678/191227960-cb5c1057-632a-4e5b-a1a6-e19dc1eae3f9.png)<kbd>

Una vez hecho esto ya no nos sale ninguna advertencia al entrar al panel de control, y podemos comenzar a alimentar nuestro sistemas con usuarios, departamentos, sistemas, redes, ...
 
 <kbd>![image](https://user-images.githubusercontent.com/20743678/191228944-17ebfbeb-022f-4050-95a0-3760bc6a0d31.png)</kbd>

### 5. FIN

 Hacemos un snapshot de nuestra máquina con todo limpio y escoscado y a usarlo
 
 #### Warning - :skull: Haz un Snapshot :eyes:

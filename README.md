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

<kbd>![image](https://user-images.githubusercontent.com/20743678/191053727-2177da39-eb70-4e42-8b25-e64518196073.png)</kbd>

Lo descomprimimos en "Descargas" por ejemplo, y lo copiamos con 'sudo' en /var/www/html

Asignamos permisos de escritura al servidor web a la carpeta 'files' y 'config':

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

Instalamos las extensiones que nos faltan (Ldap, zip, bz2, ctype, iconv, sodium y mbstring)

```shell
sudo apt install php8.0-ldap
```



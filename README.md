# Docker3

## 1. Utiliza la imagen de Ubuntu , tag 22 y apoyandote en esta guía sigue sus instrucciones para instalar LAMP en dicho contenedor.

   Para empezar descargamos la imagen y creamos el contenedor llamado dam2_lamp y lo iniciamos.
   
```
sudo docker pull Ubuntu:22

sudo docker run -it --name dam2_lamp -p 8080:80 ubuntu:22.04

sudo docker start dam2_lamp 
```
 ![](https://github.com/VictorQuinoa/Docker3/blob/main/Captura%20de%20pantalla%20de%202024-10-24%2011-25-32.png?raw=true)

 Una vez iniciado entramos en el contenedor.

```
sudo docker exec -it dam2_lamp
```
![](https://github.com/VictorQuinoa/Docker3/blob/main/Captura%20de%20pantalla%20de%202024-10-24%2011-38-50.png?raw=true)

Dentro, seguimos la guia introduciendo los comandos indicados.

```
apt update

apt install -y apache2 apache2-utils

```
Si intentamos continuar con el último comando, no deja continuar con la instalacción. Para solucionarlo comprobamos el estado del servicio mysql y lo activamos en caso de que no este activo.

```
service mysql status

service mysql start

sudo mysql_secure_installation
```

 ![](https://github.com/VictorQuinoa/Docker3/blob/main/Captura%20de%20pantalla%20de%202024-10-24%2011-33-17.png?raw=true)

Para comprobar si PHP se ha instalado bien necesitamos crear la información que se muestre en el navegador.

```
echo "" | tee /var/www/html/info.php
```
Y apareceria lo siguiente:

![](https://github.com/VictorQuinoa/Docker3/blob/main/php.png?raw=true)

## 2. Utiliza esta guía para instalar wordpress en el contenedor.

Para comenzar la instalacion de wordpress, instalamos las dependencias con el siguiente comando.

```
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip

```

A continuación para obtener wordpress en si usaremos:

```
sudo mkdir -p /srv/www

sudo chown www-data: /srv/www

(necesitamos instalar curl con "apt install curl")

curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```

Una vez instalado wordpress necesitamos configurarlo, para ello creamos un documento que contenga la configuracion proporcionada en la guia en un documento nano.

```
nano /etc/apache2/sites-available/wordpress.conf
```

![](https://github.com/VictorQuinoa/Docker3/blob/main/NANO.png?raw=true)

A continuación habilitaremos la página.

```
a2ensite wordpress

a2enmod rewrite

a2dissite 000-default

Y por ultimo

service apache2 reload

```

El próximo paso sera crear una base de datos accediendo a mysql.

![](https://github.com/VictorQuinoa/Docker3/blob/main/SQL.png?raw=true)

```
CREATE DATABASE wordpress;

CREATE USER wordpress@localhost IDENTIFIED BY '<your-password>';

GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wordpress.* TO wordpress@localhost;

FLUSH PRIVILEGES;

quit
```


## 3. Comprueba que puedes acceder a wordpress

Una vez realizados los pasos anteriores, podemos comprobar que aparece la siguiente página.

![](https://github.com/VictorQuinoa/Docker3/blob/main/wordpress.png?raw=true)

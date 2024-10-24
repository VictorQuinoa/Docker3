# Docker3

## 1. Utiliza la imagen de Ubuntu , tag 22 y apoyandote en esta guía sigue sus instrucciones para instalar LAMP en dicho contenedor.

   Para empezar descargamos la imagen y creamos el contenedor llamado dam2_lampy  lo iniciamos.
   
```
sudo docker pull Ubuntu:22

sudo docker run dam2_lamp Ubuntu:22

sudo docker start dam2:lamp 
```
  ///////
  ///////

 Una vez iniciado entramos en el contenedor.

```
sudo docker exec -it dam2_lamp
```
 ///////
 ///////

 Una vez dentro, seguimos la guia introduciendo los comandos indicados.

```
apt update

apt install -y apache2 apache2-utils

```
Si intentamos continuar con el ultimo comando, no deja continuar con la instalacción. Para solucionarlo comprobamos el estado del servicio mysql y lo activamos en caso de que no este activo.

```
service mysql status

service mysql start

sudo mysql_secure_installation
```

////////
////////

Y ya estaria instalado lamp.

## 2. Utiliza esta guía para instalar wordpress en el contenedor.

## 3. Comprueba que puedes acceder a wordpress

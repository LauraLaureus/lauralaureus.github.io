---
title: Tutorial Cómo instala WordPress en tu Raspberry Pi sin morir por tutorial obsoleto
category: Personal
---

Raspberry Pi es una marca de miniordenadores portátiles, casi que se puede decir que de bolsillo, muy versátil sobre todo para hacer experimentos locos. Uno de estos experimentos puede ser montarnos nuestro propio servidor de WordPress para alojar un blog o una página web. Por suerte para nosotros la página oficial de Raspberry Pi ofrece un tutorial completo para hacerlo, pero está desactualizado. En el post de hoy realizo un tutorial con algunas claves para que (espero que ) nunca esté desactualizado.
Antes que nada
Tenemos que tener nuestra Raspberry Pi con el sistema operativo Raspbian.
Comprobamos que tenemos el sistema actualizado para realizar las siguientes instalaciones con la siguiente sentencia de la terminal:
sudo apt-get update
 
1.Intalación del servidor Web
Nuestra nueva página de WordPress se ejecutará sobre un servidor web ampliamente conocido que es el servidor Apache. Para instalarlo ejecutamos la siguiente sentencia:
sudo apt-get install apache2 -y
Si ahora accedemos a la dirección ip de nuestra Raspberry Pi podremos ver la página de prueba del servidor Apache.  En caso de que no sepamos cuál es la ip de nuestra Raspberry podemos utilizar el siguiente comando :
ifconfig
Y buscamos un apartado donde ponga ip adress relacionado con la interfaz lan.
 
2.Instalación de PHP
PHP es el lenguaje clásico de creación de páginas web dinámicas. WordPress se apoya sobre él así que procedemos a instalarlo
sudo apt-get install php libapache-mod-php -y
Este es el primer comando que si volvemos a la página web del tutorial oficial ya se ha quedado desfasado puesto que en la página oficial indica explícitamente en este comando que la versión de PHP que busca es la 5, que ya no está disponible para su descarga a través de apt-get . El anterior comando no especifica la versión así que deja a apt-get que busque en los repertorios un candidato similar al propuesto, de esta forma no nos tenemos que preocupar de que cambien las versiones.
 
3.Instalación de MySQL
Los comentarios y las entradas se almacenan en una base de datos. Lo más usual es tener una base de datos MySQL, para instalarlo hacemos uso de los siguientes comandos.
sudo apt-get install mysql-server php-mysql -y
Al final de la instalación se nos preguntará por una contraseña, esta contraseña tenemos que guardarla porque la vamos a utilizar en pasos posteriores. En ese momento tenemos que reiniciar el servidor web Apache para que se conecte a la base de datos MySQL. La siguiente instrucción se encarga de ello
sudo service apache2 restart
 
4.Instalación de WordPress
En este momento estamos en disposición de instalar WordPress en nuestro servidor de Apache. El primer paso es movernos en la terminal a la carpeta donde va a residir nuestro WordPress así que utilizamos:
cd /var/www/html/
Para ello. En esta carpeta se situa por defecto todo lo que use el servidor web Apache, como la página de prueba que hemos visto antes que aún sigue existiendo y que eliminamos de la siguiente manera:
sudo rm *
Ahora procedemos a descargarnos la última versión de WordPress.
sudo wget http://wordpress.org/latest.tar.gz
La descomprimimos
sudo tar xzf latest.tar.gz
Movemos su contenido a la carpeta de Apache
sudo mv wordpress/* .
Y nos cargamos el archivo comprimido
sudo rm -rf wordpress latest.tar.gz
Ahora solamente nos queda darle permiso al servidor de apache para poder ejecutar todo lo que acabamos de añadir. Esto lo hacemos sabiendo que el usuario interno que se creó Apache cuando lo instalamos pertenece al grupo de usuarios www-data. Para darle permisos a este grupo para que utilice el contenido ejecutamos:
sudo chown -R www-data: .
 
5.Configurando la base de datos
Ha llegado el momento de hacerle un huequito a WordPress en MySQL, esto significa que vamos a crear una base de datos que podrá usar WordPress. Primeramente iniciamos sesión en MySQL de la siguiente manera:
mysql -uroot -ppassword
Donde el sufijo password es la contraseña que creamos antes. Para aquellos con conocimientos en administración de sistemas a los que  no les gustaría tener que introducir la contraseña en la línea de comandos (porque se queda en el historial y cualquiera podría acceder a dicha contraseña) siempre nos queda la opción de introducir únicamente el usuario y que nos pidan después la contraseña.
mysql -uroot -p
En este momento podemos crear la base de datos utilizando el siguiente comando:
mysql> create database wordpress;
Una vez aparezca en pantalla OK escribimos
mysql>exit;
 
6.Configuración de WordPress
Llegados hasta aquí accedemos con la IP de nuestra Raspberry Pi desde nuestro navegador favorito. Nos aparecerá el asistente de configuración de WordPress. Seguimos los pasos y tenemos configurado nuestro WordPress.
El único paso delicado es cuando nos pregunta por los datos de la base de datos que se rellenan de la siguiente manera.
Database Name:      wordpress

User Name:          root

Password:           <YOUR PASSWORD>

Database Host:      localhost

Table Prefix:       wp_
Felicidades ya tienes alojado tu blog WordPress en tu Raspberry Pi
 
7.Edición de enlaces permanentes 
La dirección URL que aparece en la barra del navegador puede ser modificable desde wordpress pero necesita de una configuración especial que seguiremos en este apartado.
Lo primero que hay que hacer es habilitar  el módulo de  reescritura de Apache, para ello usamos la siguiente sentencia:
sudo a2enmod rewrite
Ahora la cosa se pone peliaguada, puesto tenemos que editar un archivo de configuración de Apache.  Para abrirlo usamos la siguiente sentencia:
sudo nano /etc/apache2/sites-available/000-default.conf
Y añadimos las siguientes líneas en la segunda línea del fichero:
<Directory "/var/www/html">    
    AllowOverride All
</Directory>
De forma que el archivo comience así:
<VirtualHost *:80>    
    <Directory "/var/www/html">
        AllowOverride All    
    </Directory>    
...
Ahora sí que sí, ya tenemos nuestro servidor completamente personalizable de  WordPress en nuestra Raspberry Pi.  Solo resta reiniciar el servidor con la sentencia
sudo service apache2 restart
Y ya está.
 
Otras cosas que hacer desde aquí:
Las páginas personales no suelen tener mucha carga de trabajo ni demandar espacios muy grandes, lo que hace de una Raspberry Pi una herramienta ideal para alojar este tipo de páginas web. Una vez hecho todo lo anterior quedaría “librerar” o publicar nuestro sitio, es decir que esté accesible desde cualquier punto de Internet, para ello recomiendo buscar tutoriales sobre NoIP y su configuración en Raspbian.
 

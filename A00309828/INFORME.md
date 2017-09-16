<h1>WORKSHOP 1 SISTEMAS DISTRIBUIDOS

Nombre Estudiante: Emmanuel Bolaños 

Código Estudiante: A00309828
</h1>


<h1>1.	Consigne los comandos de Linux necesarios para el aprovisionamiento de los servicios solicitados. 
En este punto no debe incluir recetas solo se requiere que usted identifique los comandos o acciones que debe automatizar</h1>

<h1>Load Balancer</h1>
La máquina de balanceo de carga se encargará de recibir las peticiones y de re direccionar dichas peticiones (equitativamente) hacia las máquinas web. Para esto se usará el servicio de balanceo de carga haproxy.

•	Instalación de haproxy

•	yum install haproxy

•	Configuración de haproxy
Modificar archivo /etc/haproxy/haproxy.cfg con los datos de los servidores web con sus respectivas ip.

<h1>Máquinas Web</h1>

•	Instalar dependencias de tecnologías

yum install httpd -y
yum install php -y
yum install php-mysql -y
yum install mysql –y

•	Abrir puerto 80 para recibir peticiones http

firewall-cmd --zone=public --add-port=80/tcp –permanent

•	Crear el script de php que consultará la base de datos de mysql.

<h1>Máquina base de datos</h1>


•	Instalar dependencias de tecnologías

•	yum install mariadb-server
•	service firewalld start

•	Abrir puerto 3306 para recibir las peticiones dirigidas al motor de base de datos

•	firewall-cmd --zone=public --add-port=3306/tcp --permanent
•	firewall-cmd --reload
•	service mariadb.service start


•	Configuración de la base de datos

•	/usr/bin/mysql_secure_installation

Se ejecuta un script para la configuración de la base de datos de forma automática sin tener que ingresar todos los parámetros.

o	Enter current password for root (enter for none):
o	Set root password? [Y/n] y
o	New password:  distribuidos
o	Re-enter new password: distribuidos
o	Remove anonymous users? [Y/n] n
o	Disallow root login remotely? [Y/n] n
o	Remove test database and access to it? [Y/n] n
o	Reload privilege tables now? [Y/n] y

•	mysql -u root –pdistribuidos


•	create database database1
•	use database1
•	create table WebServer(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), ip VARCHAR(30))
•	INSERT INTO WebServer (name,ip) VALUES ('WebServer1',' 192.168.66.666');
•	INSERT INTO WebServer (name,ip) VALUES ('WebServer2',' 192.168.66.667');



•	Configuración de permisos

Una vez creado el esquema, la tabla y los datos de la misma, se debe dar permiso de consulta a los servidores web.

•	GRANT ALL PRIVILEGES ON *.* to 'WebServer1'@' 192.168.66.666' IDENTIFIED by 'WebServer1';
•	GRANT ALL PRIVILEGES ON *.* to 'WebServer2'@' 192.168.66.667' IDENTIFIED by 'WebServer2';

<h1>2.	Escriba el archivo Vagrantfile para realizar el aprovisionamiento, teniendo en cuenta definir: 
maquinas a aprovisionar, interfaces solo anfitrión, interfaces tipo puente, declaración de cookbooks, 
variables necesarias para plantillas. Incluya el Vagrantfile añadiendo comentarios en cada línea encargada del 
aprovisionamiento de la infraestructura. </h1>



Creación del archivo Vagrantfile

Para crear el archivo se debe ejecutar el comando de inicio de vagrant:

vagrant init

<h1> Vagrantfile</h1>

![imagen1](https://user-images.githubusercontent.com/17281732/30509197-29fc85ce-9a70-11e7-91a1-dee34abdd883.png)

![imagen2](https://user-images.githubusercontent.com/17281732/30509204-3d049170-9a70-11e7-9f0b-ebbb6f893c02.png)


<h1> 3.	Escriba los cookbooks necesarios para realizar la instalación de los servicios solicitados. 
Incluya una tabla como se muestra a continuación explicando la función de cada archivo o directorio en los cookbooks.
No incluya código fuente en el informe para esta sección. </h1>


![imagen3](https://user-images.githubusercontent.com/17281732/30509227-03a65430-9a71-11e7-9a09-eca1339ba03b.PNG)
![imagen4](https://user-images.githubusercontent.com/17281732/30509228-0d96d0f0-9a71-11e7-94c9-bca0c2bcb908.PNG)
![imagen5](https://user-images.githubusercontent.com/17281732/30509229-1904dad6-9a71-11e7-8fe4-4b92c223367f.PNG)


<h1>4. Incluya evidencias gráficas que muestran el funcionamiento de lo solicitado<h1/>

![imagen6](https://user-images.githubusercontent.com/17281732/30509237-69d1503e-9a71-11e7-8af5-27c02305828b.jpg)

![imagen7](https://user-images.githubusercontent.com/17281732/30509240-7235aa68-9a71-11e7-9b6f-47885bc4f685.jpg)





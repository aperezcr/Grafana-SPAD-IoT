# Grafana-SPAD-IoT
En este repositorio se da una explicacion de la herramienta de visualizacion grafica Grafana, los requerimientos para realizar pruebas de forma local, su conexion con la base de datos no relacional Cassandra y los pasos de conexion necesarios para conectar Grafana con la aplicacion SPAD-IoT y su posterior visualizacion de datos.

## Index

1. [Descripción](#Descripción)
2. [Grafana en el entorno local con datos de prueba](#Grafana-en-el-entorno-local-con-datos-de-prueba)
3. [Grafana como herramienta de visualizacion en SPAD-IoT](#Grafana-como-herramienta-de-visualizacion-en-SPAD-IoT)


## Descripción

Grafana permite la visualización de datos métricos y es un software de versión libre con licencia de Apache 2.0. Con esta herramienta se puede monitorizar los datos provenientes de diferente tipo de fuentes, por ejemplo, bases de datos relacional como MySQL, InfluxDB o bases no Relacional como MongoDB. Para este proyecto se hara especial enfasis en la base de Datos Cassandra CQL.

## Grafana en el entorno local con datos de prueba

Lo primero que debemos instalar para familiarizarnos con el entorno de Grafana es la aplicación Grafana Lab con la edición Enterprise, para los usuarios de linux-Ubuntu, seguir los siguientes pasos:

` sudo apt-get install -y adduser libfontconfig1 musl`

` wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.3.3_amd64.deb`

` sudo dpkg -i grafana-enterprise_10.3.3_amd64.deb`

Una vez instalado Grafana correctamente, podra acceder a su interfaz escribiendo en el navegador:

`localhost:3000"`

Si la instalacion fue correcta vera la siguiente ventana:

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/cJqrbDs9/Captura-de-pantalla-2024-02-23-131130.png)

El usuario y contraseña por defecto son:

` username:admin`

` password:admin`

Una vez logueado podra ver el home de Grafana.

El siguiente paso es instalar la base de datos usada como prueba Cassandra DB, para esto se recomienda usar la interfaz de Datastax.

` sudo apt install apt-transport-https wget gnupg`

` sudo apt install openjdk-8-jdk`

` wget -q -O - https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -`

`sudo sh -c 'echo "deb http://www.apache.org/dist/cassandra/debian 311x main" > /etc/apt/sources.list.d/cassandra.list'`

`sudo apt-get update`

`sudo apt install cassandra`

Una vez instalado CassandraDB en la computadora, es necesario instalar el conector de la BD en Grafana y configurarlo.

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/hvFHTdg5/Captura-de-pantalla-2024-02-23-132952.png)

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/J4RXM7BN/Captura-de-pantalla-2024-02-23-133342.png)

Una vez configurado el conector, podra hacer consultas CQL con editor de query o usar la intefaz de Grafana para visualizar los datos de la DB Cassandra:

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/cH9fbVFq/1.png)

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/zGZK6wFf/2.png)

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/sD2xDT3X/3.png)


## Grafana como herramienta de visualizacion en SPAD-IoT

Se usa la versión 9.5.14 de grafana ya que la ultima versión aun genera algunos errores con el conector de cassandra, la versión usada del conector es la 2.3.0 

Conector de [Cassandra 2.3.0](https://github.com/HadesArchitect/GrafanaCassandraDatasource/releases/download/2.3.0/cassandra-datasource-2.3.0.zip)

Para el despliegue de la herramienta se usan dos volumenes, uno para pasarle la conexion con cassandra y la otra para establecer la conexion segura con la base de datos.

Docker compose Grafana.

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/Vv7g8J4N/Captura-de-pantalla-2024-02-23-141018.png)

Se deben realizar tres configuraciones para el correcto funcionamiento de la herramienta:

### 1. Paso 1
Se debe configurar el conector de Cassandra en el DataSource de Grafana.

`Host: 54d91226-1193-4ef8-963e-cd02b29c5874-useast1.db.astra.datastax.com:29042`

`User: fxTAPZquKNbYycaKZhDcdxTg `

`Password:4zpbTvjZ.6.XK+g_20wk65hItrFcDBZG3zQIN.lZU5R85UZr3JIy_cPfXkq9uc7k.Qz0Gsr_W21RdLKpwsZyPZ2P2.HI,7Eu,ZnBT75WWyvNi_wiL.T6jXdOEy-B.6SU`

### 2. Paso 2
La segunda configuracion permite que la aplicacion sea visible desde el nginx de SPAD, para ello se debe ingresar al docker y en la ruta /etc/grafana/ ingresar al archivo grafana.ini, dejar las siguientes lineas de código igual a la imagen:

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/wB7n1dnM/Captura-de-pantalla-2024-02-23-142335.png)

### 3.Paso 3
La tercera configuración es la que permite ingresar desde la url de spad sin la necesidad de autenticarnos en la aplicación, se debe configurar el mismo archivo anterior /etc/grafana ingresar al archivo grafana.ini

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/QxYbHWDg/Captura-de-pantalla-2024-02-23-142449.png)

A los cambios anteriores se deben sumar los siguientes:

`enforce_domain = false `

![Descripción de la imagen](Capturas/enforce_domain.png)

`allow_embedding = true`

![Descripción de la imagen](Capturas/allow_embedding.png)

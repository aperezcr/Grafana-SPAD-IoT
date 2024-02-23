# Grafana-SPAD-IoT
En este repositorio se da una explicacion de la coneccion entre la herramienta de visualizacion Grafana y la aplicacion SPAD-IoT.

## Grafana en el entorno local, datos de prueba.

Grafana permite la visualización de datos métricos y es un software de versión libre con licencia de Apache 2.0. Con esta herramienta se puede monitorizar los datos provenientes de diferentes fuentes, por ejemplo, bases de datos como MySQL, InfluxDB y para el proyecto CassandraDB.

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

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/cJqrbDs9/Captura-de-pantalla-2024-02-23-131130.png](https://i.postimg.cc/hvFHTdg5/Captura-de-pantalla-2024-02-23-132952.png)https://i.postimg.cc/hvFHTdg5/Captura-de-pantalla-2024-02-23-132952.png)

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://i.postimg.cc/cJqrbDs9/Captura-de-pantalla-2024-02-23-131130.png](https://i.postimg.cc/hvFHTdg5/Captura-de-pantalla-2024-02-23-132952.png)https://i.postimg.cc/hvFHTdg5/Captura-de-pantalla-2024-02-23-132952.png)











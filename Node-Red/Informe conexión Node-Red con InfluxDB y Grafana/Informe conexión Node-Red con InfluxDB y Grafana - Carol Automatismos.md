Como crear una conexión de Node-Red con InfluxDB y Grafana:
Primero descargamos Node.js desde su página oficial:
https://nodejs.org/en
Después podremos descargar Node-RED desde su página oficial siguiendo los
pasos (hay que tener en cuenta que sistema operativo tenemos instalado en nuestro
computador para poder instalar el correcto, en nuestro caso para este ejemplo
usaremos un sistema operativo Windows por lo cual instalaremos con npm, también,
hay que abrir una pestaña de cmd para poder instalarlo para hacer esto podemos o
pulsar en el botón Windows de abajo a la izquierda de nuestra pantalla y luego
escribir “cmd” para buscarlo o podemos pulsar las teclas Windows+R y escribir
“cmd” para ir directamente también):
https://nodered.org/docs/getting-started/local
Una vez instalado podemos ejecutarlo para ello podemos hacerlo creando otra
pestaña de cmd o en la misma de la instalación escribir “node-red” para iniciar el
programa.
Una vez iniciado el programa tendremos que abrir nuestro navegador de preferencia
para poner en el buscador nuestra dirección IP(La que usaremos para la red de
PLCs) y el puerto que vamos a abrirle a Node-RED. En nuestro caso como ejemplo
sería 192.168.0.1 con el puerto 1880 por lo cual escribimos en el buscador
“http://192.168.0.1:1880/” (cuando iniciamos Node-RED nos enseña también un
ejemplo utilizando la IP interna de nuestro dispositivo como se ve a continuación):

Una vez en la página de Node-RED en el buscador tendremos que añadir unas
paletas que permitan la comunicación de InfluxDB con Node-RED. Si no quiere
buscar unos puede usar los mismos que usamos en la guía(Tenga en cuenta que si
utiliza unos distintos a los de la guía tal vez no funcionen igual).
Paleta de InfluxDB:
https://flows.nodered.org/node/node-red-contrib-influxdb
Ahora descargamos InfluxDB, para ello iremos a la página oficial de InfluxDB(Nos
pedirán un nombre de usuario y un mail asociado de los cuales se tendrá que
acordar mas adelante:
https://www.influxdata.com/downloads/
Para descargar pondremos la plataforma correcta de dispositivo en (nuestro caso es
windows) y copiaremos el código de descarga que nos pone abajo y lo ponemos
donde pertoque (en nuestro caso como usamos windows lo tenemos que poner en
powershell).
(Cabe aclarar que para esta guía se usa InfluxDB 2.7.10 por lo cual tal vez no sea
de utilidad en futuras versiones como las 3.X).
Para abrir Powershell podemos presionar el icono “Windows” y escribir “Powershell”
o podemos pulsar Ctrl+R y escribir “Powershell” para ir de una forma más directa.
Una vez en powershell solo queda pegar el código y esperar a que se descargue.
Una vez descargado podemos abrir un CMD y podremos la ruta de la carpeta en la
que esta guardado el ejecutable de InfluxDB. En el caso de que no lo modifiques a
la hora de poner el codigo de descartesa en powershell tendria que estas en

“C:\Program Files\InfluxData\influxdb” por lo cual en el CMD pondremos “cd
“C:\Program Files\InfluxData\influxdb”” una vez en la carpeta tendremos que iniciar
el ejecutable para ello pondremos “.\influxd.exe” y nos saldrá mucho texto
“aleatorio”. El resultado final se verá parecido a este:
Una vez iniciado influxDB tendremos que ir a nuestro navegador y poner la ip de
nuestra red y el puerto 8086 (en nuestro caso 192.168.0.1:8086).
Cuando tengas iniciado te pedirán crear un usuario, crea un usuario el cual usarás
para poder iniciar sesión en la organización que introduzcas.

Luego tendremos que crear un Bucket y una API Key los cuales recordaremos para
más tarde para más tarde.
Para crear el Bucket iremos a la flecha de subida de datos y elegiremos la sección
buckets como se muestra a continuación:
Una vez dentro le daremos a create bucket y le daremos un nombre que
guardaremos para más adelante.
Para crear la API Key iremos a la seccion de API Tokens y crearemos un nuevo
toquen de tipo all access.
Una vez creado copiaremos la key y la guardaremos para más adelante.

Ahora en Node-Red pondremos un bloque de conexión in de influxDB y le
pondremos los siguientes datos:
Una vez hecho, pondremos nuestra organización y el bucket que hemos creado
antes para guardar la información en sus recuadros respectivos y pondremos el
nombre que queramos que tenga nuestra medición en el apartado “Medición”.
Si queremos visualizar el dato podemos crear una dashboard y poner nuestro dato
en, por ejemplo, una gráfica la cual nos mostrará la evolución a lo largo del tiempo.
Para hacerlo solo tenemos que añadir una nueva celda introducir el bucket y elegir
nuestro valor de medidia( si no se muestra nada despues de esto pulsad el boton de
“submit”.

Ahora descargaremos grafana para ello iremos a la paguina oficial de descarga
( https://grafana.com/grafana/download?platform=windows ) seleccionamos la opción
de nuestro sistema operativo y lo instalamos.
Una vez descargado abrimos el instalador de Grafana y lo instalamos.
Tras instalarlo vamos a abrir nuestro navegador y buscar nuestra ip de servidor mas
el puerto 3000 (ejemplo: 192.168.0.1:3000).
Ahora tendremos que iniciar sesion la cual si no se a modificado en las
configuraciones de Grafana sera “admin” de contraseña “admin” (si quiere modificar
el usuario no hace falta que entre a las configuraciones de Grafana ya que una vez
iniciada sesión con el usuario “admin2 nos dara la opcion de cambiar el nombre y
contraseña de usuario).
Una vez iniciada sesion entraremos en dashboards y creamos una nueva
visualizacion en la cual en data source abriremos el menu avanzado y crearemos
una nueva data source la cual sera influx DB

Como data source usaremos influxdb lo cual abrira un menu como este:

Pondremos como qwerty lenguaje flux y rellenaremos con la informacion de nuestro
influxDB y le daremos a save and test lo cual nos tendria que dar un mensaje como
este:

Ahora para hacer los gráficos de la dashboard tendremos que poner el influxDB
como data source y tendremos que poner el script de la variable que queremos
medir. Ejemplo:


Como crear una conexión por Node-RED entre un plc NX1P2 y un S71200:
Primero descargamos Node.js desde su página oficial:
https://nodejs.org/en
Después podremos descargar Node-RED desde su página oficial siguiendo los pasos (hay que tener
en cuenta que sistema operativo tenemos instalado en nuestro computador para poder instalar el
correcto, en nuestro caso para este ejemplo usaremos un sistema operativo Windows por lo cual
instalaremos con npm, también, hay que abrir una pestaña de cmd para poder instalarlo para hacer
esto podemos o pulsar en el botón Windows de abajo a la izquierda de nuestra pantalla y luego
escribir “cmd” para buscarlo o podemos pulsar las teclas Windows+R y escribir “cmd” para ir
directamente también):
https://nodered.org/docs/getting-started/local
Una vez instalado podemos ejecutarlo para ello podemos hacerlo creando otra pestaña de cmd o en
la misma de la instalación escribir “node-red” para iniciar el programa.
Una vez iniciado el programa tendremos que abrir nuestro navegador de preferencia para poner en el
buscador nuestra dirección IP(La que usaremos para la red de PLCs) y el puerto que vamos a abrirle
a Node-RED. En nuestro caso como ejemplo sería 192.168.0.1 con el puerto 1880 por lo cual
escribimos en el buscador “http://192.168.0.1:1880/” (cuando iniciamos Node-RED nos enseña
también un ejemplo utilizando la IP interna de nuestro dispositivo como se ve a continuación):

Una vez en la página de Node-RED en buscador tendremos que añadir unas paletas que permitan la
comunicación de los PLCs con Node-RED. Si no quiere buscar unos puede usar los mismos que
usamos en la guía(Tenga en cuenta que si utiliza unos distintos a los de la guía tal vez no funcionen
igual).
Paleta de Omron:
https://flows.nodered.org/node/node-red-contrib-omron-fins
Paleta de Simatic:
https://flows.nodered.org/node/node-red-contrib-s
Una vez tengamos preparado todos los elementos en Node-RED podemos pasar a configurar los
PLCs para poder comunicar.
Comenzaremos con el PLC de Omron para el cual crearemos un nuevo documento en el que
habilitaremos el área de memoria DM. Para ello iremos a “Configuración de Operación” luego a
“Configuración de memoria” y por último activaremos el área DM como se muestra a continuación:
Después activaremos las comunicaciones vía FINS, ya que la paleta que utilizamos utiliza FINS para
poder comunicar. Para ello iremos a “Configuración de Operación” luego a “Configuración de puerto
Ethernet/IP integrado” y bajaremos hasta encontrar el apartado de las comunicaciones FINS, en este
apartado lo activaremos pulsando en “FINS/UPD Utilizar”:

Luego crearemos dos variables globales que representaran la memoria de escritura y la memoria de
lectura en nuestro caso las hemos llamado “D0” y “D1” y se ubican en las memorias D00 y D01 (hay
que recordar activarlas como retentivas, ya que si no no dejarán utilizarse).
Tras esto ya tendríamos todo hecho en el PLC de Omron ahora pasaremos al de Simatic.
Primero hay que activar el acceso con PUT/GET para ello iremos a las propiedades del PLC
“Protección y seguridad” luego “Mecanismo de conexionado” y activaremos la opción de activar
PUT/GET:
Después creamos un DB en el cual ponemos nuestras memorias que se comunicaran con el PLC de
Omron (En nuestro caso usaremos memorias WORD que nombramos DB0 y DB1 como en el PLC
de Omron).
Ahora tocaría añadir los inputs y outputs en el node red. Si se ha estado siguiendo la guía su
conexionado se tendrá que ver más o menos como el siguiente:

A continuación se enseña una foto de como deben estar configuradas las paletas de Simatic:

A continuación se enseña una foto de como deben estar configuradas las paletas de Omron:
Read:

Write:

También hay que utilizar una paleta de funciones entre el reading de Omron y el input de Simatic con
la siguiente función:
:
Hecho todo esto solo quedaría darle arriba a la derecha en recuadro rojo que pone “instanciar” para
guardarlo todo y conectar con los PLCs.
Podemos para acabar probar a mandar un mensaje a cada PLC para ver si el conexionado está
hecho correctamente.
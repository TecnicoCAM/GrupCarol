Cómo conectar con un servidor MQTT privado con mosquitto:
Primero descargamos mosquitto desde su página oficial(hay que tener en cuenta la versión de
Windows que tiene usted, 32 o 64 bits):
https://mosquitto.org/download/
Una vez descargado solo hace falta instalarlo (se recomienda que cuando le pida una ruta de
descarga deje la predeterminada).
Para comprobar que mosquitto se ha instalado correctamente nos iremos al botón Windows de
nuestro ordenador abajo a la izquierda de la pantalla y escribiremos “Servicios” para acceder a los
servicios del sistema. Una vez abierto bajaremos hasta encontrar un servicio llamado “Mosquitto
broker”
Tras encontrarlo le haremos doble clic y presionaremos iniciar si todavía no se está ejecutando.

Una vez esté en ejecución podemos cerrar “Servicios” y abrir una ventana de cmd, podemos buscarla
como hemos hecho con los servicios o podemos pulsar Windows+R y escribir cmd.
Tras abrir el cmd hay que ir a la carpeta de mosquitto escribiendo cd y su ruta por ejemplo si dejas la
ruta por defecto que te crea el instalador serÍa “cd “c:/program files/mosquitto””. Se tienen que crear
dos ventanas de mosquitto en cmd puedes crear otra ventana y volver a escribir la ruta o escribir
“start” en la ya creada para crear otra automáticamente.
En la primera pestaña crearemos un subscribe para ello escribiremos “mosquitto_sub -d -t
topico_ejemplo” y para la otra pestaña crearemos un publisher en host local escribiendo
“mosquitto_pub -h localhost -t topico_ejemplo -m “mensaje de prueba””. Si usted quiere saber que
hace cada comando puede escribir en la ruta de mosquitto “mosquitto -h”
Tras escribir el publisher tendría que salir en el subscribe el mensaje que usted ha escrito, si no es
así compruebe que haya seguido correctamente los pasos o si le hace falta una guía más visual le
dejamos un video aquí abajo para que lo siga.

https://www.youtube.com/watch?v=4CIUBtMNnKU
Tras todo esto las dos ventanas de cmd se tendrían que ver algo parecido a esto:
Tras la prueba hay que abrir la carpeta de mosquitto desde el explorador de archivos de Windows
(Es la misma ruta que hemos utilizado para buscar la carpeta de mosquitto en cmd).
Una vez dentro tenemos que buscar un archivo llamado “mosquitto.conf” lo abrimos y buscamos un
apartado llamado “PSK based SSL/TLS support” (puedes buscarlo con más facilidad pulsado Ctrl+R.
En este apartado hay que añadirle dos líneas en las que ponga “listener 1883” y “allow_anonymous
true” tras introducir estas líneas guardamos el archivo y cerramos. Si no nos dejara guardar en la
carpeta de mosquitto guardamos el archivo en el escritorio para luego borrar el que hay en la carpeta
mosquitto y pegamos el que hemos dejado en el escritorio.

Ahora vamos otra vez al botón Windows y escribimos “firewall” y abrimos el firewall de Windows
defender. Una vez abierto le pulsamos en “Configuración avanzada”.
Luego pulsamos en “Reglas de entrada” y creamos una nueva regla. Esta nueva regla será de tipo
“Puerto” número 1883 con permiso de la conexión y la llamaremos “mosquitto_regla_entrada”. Luego
hay que hacer lo mismo pero para las “Reglas de salida” y tras crearlas y comprobar que estén
activas reiniciamos el ordenador.
Cuando ya tengamos reiniciado el ordenador volveremos a probar que funcione correctamente
mosquitto poniendo otra vez el publisher y el subscribe, pero esta vez con la IP de nuestro ordenador
(si no sabes la IP de tu ordenador escribe “ipconfig” para poder ver tus IPs) en nuestro caso es
192.168.5.225. Aquí un ejemplo de como quedaría(si no funcionase compruebe que tenga el
Mosquitto broker en ejecución en los servicios del sistema):
Ahora podemos abrir sysmac studio para crear nuestro publisher(para este ejemplo aprovechamos el
mismo subscriber que hemos creado para ejemplificar, pero usted puede crear uno nuevo).
Primero descargamos la librería MQTT de omron desde la página web oficial.
https://www.ia.omron.com/product/tool/sysmac-library/

Tras descargar la licencia descomprima el archivo e inicie el setup para instalar la librería.
Después de la descarga abra un nuevo documento en Sysmac Studio o un programa antiguo y en la
barra superior de herramientas clique en “Proyecto” después en “biblioteca” y en la pestaña
emergente presione en “Mostrar Referencias”.

Tras pulsar en la última pestaña le saldrá la siguiente pestaña.
En la cual tendrá que presionar en el botón más que hay en la esquina inferior izquierda para que le
salga una pestaña en la que tiene que buscar el archivo que contiene la librería anteriormente
instalada. (Si no a elegido un destino personalizado de el archivo lo podrá encontrar con la siguiente
dirección “C:\OMRON\Data\Lib\MQTT_Comm”).
Tras importar y aceptar la librería ya estará dentro del programa y de la caja de herramientas. (Esto
se tendrá que hacer cada vez que se cree un nuevo documento, ya que no se mantendrá guardado).

Tras esto crearemos dos líneas de programa en las cuales pondremos el MQTTClient y el texto
estructural o SCL como se muestra en el ejemplo de siguiente imagen.(Recuerde poner un nombre al
bloque de funciones del MQTT Client, ya que si no tiene un nombre puede dar fallos).
Una vez creadas las dos líneas tendremos que configurar el Bloque de funciones puede configurarlo
igual que en el ejemplo, pero recuerde crear toda la configuración como variable interna

En la siguiente tabla se explica la función de cada comando:
Código Tipo de dato Funcion ¿Es
obligatorio?
ConnectionSettings.TLSUse BOOL Cuando este indicador es TRUE, se utilizan
comunicaciones de socket seguro para
comunicarse con el broker MQTT. Cuando esta
bandera es FALSE. Las comunicaciones por socket
se utilizan para comunicarse con el broker MQTT.
Si
ConnectionSettings.TLSSessionName STRING[17] Este es un nombre de sesión TLS establecido. El
conjunto El nombre de la sesión TLS se especifica
con Secure Comandos de configuración de
sockets. El TLS Los nombres de las sesiones van
desde TLSSession0 a sesión TLS59. Se accede en
el caso de TLSUse=TRUE.
Solo si el TLS
Use se
establece
como
ConnectionSettings.IpAdr STRING[201] Esta es una dirección IP o nombre de host del
broker MQTT. Sí especifica por nombre de host,
necesitas configurar el servidor DNS
Si
ConnectionSettings.PortNo UINT Este es un número de puerto del corredor MQTT.
Cuando se especifica, la conexión con el broker
MQTT está establecido en 8883 para
TLSUse=TRUE o en 1883 para TLSUse=FALSO.
Si
ConnectionSettings.UserName STRING[256] Definir el nombre de usuario para poder iniciar la
conexión con el servidor.
Solo si el
servidor lo
pide
ConnectionSettings.Password STRING[256] Definir la contraseña para poder iniciar la conexión
con el servidor.
Solo si el
servidor lo
pide
ConnectionSettings.WillCfg.WillTopic STRING[256] Estoes el nombre de tópico Will No
ConnectionSettings.WillCfg.WillMsg STRING[256] Crea un mensaje para publicar en el tópico Will No
ConnectionSettings.WillCfg.WillRetein BOOL Cuando está flag es TRUE, después de enviar un
mensaje Will a otro cliente, el MQTT broker
conserva ese mensaje.
No
ConnectionSettings.WillCfg.QoS BYTE Establezca el nivel de QoS cuando el broker MQTT
publica un mensaje Will en esta biblioteca para
otros clientes.
No
ConnectionSettings.WillCfg.WillFlag BOOL Establezca esto en TRUE cuando use la función
will.
No
ConnectionSettings.CleanSession BOOL Cuando este flag es TRUE, en el momento de la
desconexión de esta biblioteca (Habilitación de la
instrucción MQTTClient está establecida en
FALSE), El BrokerMQTT borra el estado de la
suscripción etc. antes de la desconexión; en el
momento de reconexión (la habilitación de la
instrucción MQTTClient está establecida en TRUE),
establece la conexión como una nueva sesión.
No

ClientID STRING[256] Este es un identificador para el Broker MQTT para
identificar el cliente.
Si
KeepAlive UINT Establecer un temporizador de mantenimiento de
vida para el broker MQTT.
No
Timeout UINT Este es un tiempo de espera para una solicitud
para conectarse al broker MQTT.
No
DiscardMsgTime UINT Especifiqué el máximo tiempo pasado esperando el
mensaje recibido para ser descartado.
No
Tras configurar el cliente podemos crear un publisher y un subscribe. Para este ejemplo usaremos un
publisher en string, pero en el pdf del final del documento podrá ver cómo programar un publish en
arybyte subscribe en arybyte y string.
A continuación se enseña un ejemplo de set del publisher y una tabla en la que se explica la función
de cada comando:

Código Tipo de dato Funcion ¿Es
obligatorio?
Topic STRING[512] Especifica un nombre de tópico para publicar. Si
PubSettings OmronLib \MQTT_Co
mm\sPubFlags
Configura la QoS y los ratain settings en la configuración en la
publicación.
Si
Timeout UINT Este es un tieenmpo de espera. Se accede cuando el nivel de
QoS es 1 o 2.
Solo si el
servidor lo pide
ClientReference OmronLib \MQTT_Co
mm\sClientReference
Estos son datos para compartir entre bloques de funciones en
esta biblioteca. No cambies los datos. El contenido de los datos
no se publica.
No
PubMsg STRING[1986] Este es un msaje para ser publicado en el tópico especificado Si

PacketID UINT Esta es un ID de paquete. Si cualquier número que no sea 0 se
especifica al inicio de ejecución, será enviado como mensaje de
reenvío con el mensaje especificado ID del paquete. El ID del
paquete utilizado que se produce en la publicación. Se accede
cuando el nivel de QoS es 1 o 2.
Si
MsgType USINT Enviar tipo de mensaje
0: PUblish
1: PUBREL
Se accede cuando el nivel de QoS es 1 o 2 y el ID del paquete
no es 0
No
Si tienes alguna duda o algún problema con tu servidor MQTT te dejamos un pdf oficial de Omron
donde explican más a detalle el funcionamiento de sus bloques de MQTT para sysmac studio.

https://mega.nz/folder/wmdCxIBa#kgpAYOWfCIUBnUk8OP_rnw
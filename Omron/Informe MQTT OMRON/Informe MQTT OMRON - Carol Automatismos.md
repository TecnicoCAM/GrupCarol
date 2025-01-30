Cómo conectar con un servidor MQTT online con adafruit:
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
igual que en el ejemplo, pero recuerde crear toda la configuración como variable interna.
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
No

no se publica.
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
Ahora usaremos un navegador web en nuestro caso usaremos brave y buscaremos el siguiente
enlace:
https://io.adafruit.com/
Y clicamos en la pestaña que pone Sign in para crearnos una cuenta.

Una vez creada la cuenta saldrá la siguiente ventana en la cual tendremos que pulsar en la opción de
feeds.

Cuando entremos en feeds le daremos a “new feed” para crear una feed nueva y una vez elegido un
nombre le damos a crear.
Cuando creemos la feed nueva le daremos clic en “dashboards” al lado de feeds y crearemos una
nueva dándole a new dashboard y tras introducir el nombre deseado le daremos a crear.

Tras crearlo nos aparecerá abajo en la lista de dashboards, le damos doble clic y lo abrimos. Una vez
abierto le daremos en el engranaje que sale arriba a la derecha y se nos abrirá un menú en el que
picaremos en “create new block”.

Para este ejemplo vamos a crear un stream por lo cual elegiremos la opción de steam.

Elegiremos la feed que hemos creado anteriormente y le pondremos un título a nuestro gusto para
después configurar el steam como nosotros lo queramos o lo podemos dejar como viene de serie
como en este ejemplo. Podemos editar su tamaño y su posición si le clicamos otra vez al engranaje
de arriba a la derecha, pero clicamos esta vez en “Edit Layout” y una vez lo tengamos como
queremos le daremos a “Save Layout” para guardar los cambios.
Ahora nos quedaría poner la IP o el DNS y el tópico del servidor que utilizamos y para el caso de usar adafruit el
usuario y la contraseña. El DNS del servidor es siempre “io.adafruit.com” y el tópico es el nombre de usuario de
nuestra cuenta en el que hemos creado nuestra feed más f más el nombre de nuestra feed, en el ejemplo de
nuestro caso sería “Aitor_Perez/f/ejemplo” y para ver nuestro nombre de usuario y nuestra contraseña le
tenemos que clicar en la llave que sale dentro de un círculo amarillo arriba a la derecha. Tras pulsarlo nos saldrá
un menú en el que nos pondrá nuestro nombre de usuario como “Username” y nuestra contraseña como “Active
Key”
Si tienes alguna duda o algún problema con tu servidor MQTT te dejamos un pdf oficial de Omron
donde explican más a detalle el funcionamiento de sus bloques de MQTT para sysmac studio.
https://mega.nz/folder/wmdCxIBa#kgpAYOWfCIUBnUk8OP_rnw
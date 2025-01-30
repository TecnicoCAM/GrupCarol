Cómo mandar un mensaje JSON a un servidor MQTT con PLC Omron de las
series NX/NJ:
Para esta guía usaremos el broker mosquitto el cual puede descargar buscando “eclipse
mosquitto” en el buscador de google o pulsando este enlace.
https://mosquitto.org/download/
Una vez descargado solo hace falta instalarlo (si no sabe como instalar mosquitto y ponerlo en
funcionamiento mirese la guía de como crear un servidor MQTT con mosquitto que se encuentra en
este enlace: https://mega.nz/file/cqgXxIgZ#J9VXjH-ksK2lY8pZGBSux13ciP3T1x1VDx4ucNbSwq8 ).
Tras instalar y poner en marcha tendremos que descargar una libreria de JSON y de MQTT si no la
tenemos ya instalada, podemos instalarlas directamente desde las fuentes oficiales de Omron
buscándolas desde su página oficial o llamando al número de soporte xxxxxxxxx o descargandola
desde este enlace:
https://mega.nz/folder/pzJTjQiT#SiJNguBb4uXmzAMEfDSL3Q
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
Una vez creado toda la parte de MQTT crearemos una sección nueva para la parte de JSON y
crearemos algo parecido a esto:

(El texto del SCL es el siguiente :
“tu MsgPub” := \\JSON\JSONBuild(EN:=TRUE,Buffer := JSONBuff);)
A continuación se explica más a detalle cada parte del programa.
Código Tipo de dato Funcion ¿Es obligatorio?
Buffer JSON\JSONBuffer Crea un Buffer para el JSON Si
Clear - Limpia el historial del buffer No
Variable Name STRING[32] Nombra la variable Si
Variable Value Depende de lavariable Asigna el valor a la variable No

Nuestro resultado en el cmd tendría que verse algo como esto:
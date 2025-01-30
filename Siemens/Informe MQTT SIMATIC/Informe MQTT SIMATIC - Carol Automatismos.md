Cómo conectar con un servidor MQTT online con adafruit:
(Para este ejemplo estamos usando un TIA Portal 19v y un S71200)
Primero descargamos la librería MQTT de Simatic desde la página web oficial(en nuestro caso
descargamos la versión compatible con TIA Portal 19).
https://support.industry.siemens.com/cs/document/109780503/libraries-for-communication-for-simatic-
controllers?dti=0&lc=en-ES
Una vez descargado y extraído vamos al TIA Portal y le clicamos dentro de “Librería” en donde hay
un símbolo de libro y una flecha verde lo cual abrirá un navegador de archivos en el cual buscaremos
nuestro archivo de la librería:

Tras instalarla buscamos dentro de la carpeta de la libreria la carpeta de “LMQTT” y dentro de la
carpeta “LMQTT_Client” encontraremos el bloque FB de cliente MQTT:
Una vez puesto el bloque solo hay que relacionar las entradas y salidas del bloque con sus
contrapartes del DB como se ve a continuación:

También se tendrán que añadir 2 segmentos las como se muestran a continuación:

También habrá que crear por arriba un segmento como este:
A continuación se deja una tabla que explica la función de cada apartado del bloque:
Nombre Tipo Tipo de Data Comentario
enable Input Bool TRUE: La conexión al MQTT Broker está
establecida y mantenida
FALSE: La conexión está rota.
publish Input Bool Publica “publishMsgPayload” to “mqttTopic” con
“retain” y “qos”.
subscribe Input Bool Subscribe a “mqttTopic” con “qos”.
unsubscribe Input Bool Desubscribe de “mqttTopic”.
retain Input Bool TRUE:La data es enviada con la flag “retain”
FALSE:La data es enviada sin la flag “retain”.
qos Input USInt Calidad del servicio (Quality of Service)
0: El mensaje es enviado o subscrito con QoF 0
1: El mensaje es enviado o subscrito con QoF 1
2: El mensaje es enviado o subscrito con QoF 2
(El FB no soporta QoS 2 para subscripciones).

publishMsgLen Input UDInt Tamaño actual de la tata valida en el parámetro
array de “publishMsgPayload”.
willMsgLen Input UInt Tamaño actual de la tata válida en el parámetro
array de “willMsgPayload”.
timeOut Input Time Parámetro opcional para configurar el tiempo de
monitorización. Después de que el tiempo pase,
el “trabajo” actual será considerado como fallido.
valid Output Bool TRUE: El FB ejecuta sus funciones sin errores.
done Output Bool TRUE: El “trabajo” actual
(publish/subscribe/desubscribe) fue ejecutado
correctamente.
busy Output Bool TRUE: El FB está ocupado.
error Output Bool TRUE: Un error ha ocurrido.
Si “busy” es TRUE al mismo tiempo, el bloque
intenta corregir el error por sí mismo.
status Output Word Status y códigos de error en el pdf del final del
documento (capítulo 5.2.2)
diagnostics Output “typeDiagnost
ics”
Información diagnósticos avanzados en el pdf
del final del documento (capítulo 12.2)
recivedMsgStatus Output USInt Indica por un ciclo al mismo tiempo cuando un
mensaje nuevo a sido recibido (suscripción):
0: No hay mensajes nuevos recibidos.
1:Nuevo mensaje válido recibido.
2:Nuevo mensaje recibido, pero el mensaje es
invalido o la data recibida es más grande que la
área de memoria del tópico o el recibidor de
mensajes.
RecivedMsgDataLen Output UDInt Numero de data valida en el
“recivedMsgPayload”en parámetros de bytes en
array.
connParam InOut “LMQTT_type
ConnParam”
Parámetro al que establecer una conexión al
MQTT Broker.
clientIdentifier InOut WString Identificador de cliente usado cuando estableces
una conexión
username InOut WString Opcional:Nombre de usuario para establecer
conexión
password InOut WString Opcional:Contraseña para establecer conexión
willtopic InOut WString Opcional: Tópico al cual el mensaje “LastWill”
es enviado.
willMsgPayload InOut Array [*] of
bytes
Opcional: Mensaje enviado como “LastWill”.
mqttTopic InOut WString Tópico usado para publicar/suscribir/desuscribir.

publishMsgPayload InOut Array [] of
bytes
Mensaje que es transmitido como data de
usuario al publicar.
recivedTopic InOut WString Tópico suscrito al cual un mensaje se ha
recibido.
recivedMsgPayload InOut Array [] of
bytes
Data de usuario recibida en un mensaje del
tópico suscrito.
Una vez hecho esto solo nos queda definir el largo de los caracteres del mensaje y el mensaje que
queremos enviar.
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
También dejamos aquí abajo un pdf en el que se explica todo con más detalle
https://mega.nz/folder/hygSxYIZ#nCYbpJVOV0Q0RaLuluCMSw


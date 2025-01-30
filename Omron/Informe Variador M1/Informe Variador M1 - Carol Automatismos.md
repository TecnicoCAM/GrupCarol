Cómo conectar correctamente un M1 a un PLC NX102:
Para esta guia usaremos el variador 3G3M1-A4007, el PLC NX102-9020, la tarjeta
PF0730, una CPU de seguridad SL 3300 y una tarjeta SID
En el bastidor colocamos la siguiente disposicion
Y después conectamos via EtherCAT nuestro variador el cual vamos a usar,
nosotros por ejemplo usamos un 3G3M1(Hay que revisar que los nodos esten
puestos correctamente tanto en EtherCAT como en la realidad).
Después iremos a la cpu de safety y en parámetros nos pondremos en la tarjeta de
entradas y pondremos un paro t un reset los cuales nombraremos (Nosotros por
ejemplo los hemos llamado “EStop” y “Reset Button”, cabe recalcar que el botón de
paro pese a ser dos interruptores solo hace falta poner el nombre a uno).

El cableado en la realidad se tiene que ver mas o menos así:
Luego procedemos a modificar el mapa de PDOs del variador para ello iremos al plc
entramos a EtherCAT y buscamos el boton que pone “Configuracion de asignacion”
Tras esto tendremos que poner todas las asignaciones de la siguiente manera

Luego nos iremos al mapa de E/S en la cpu de safety para colocar lo siguiente:
Despues en Programacion del cpu de safety pondremos el siguiente bloque:
Luego en “Parámetros” tendremos que buscar el numero H483 y poner la direccion
FSoE que queremos (en nuestro caso es 3.Tiene que vigilar que no pise la de mada
mas). Una vez puesto tenemos que comprobar que coincida con la que tiene la cpu
de safety.

También tiene esta guía más visual por si no le funciona tras seguir esta:
https://www.youtube.com/watch?v=lT8H641sjLI
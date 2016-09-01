# HTTP (Hyper Text Transfer Protocol) 
________________________________________
________________________________________

Lo esencial
--

**Introducción**
--
_________________
**La web**
--
Internet (o la Web) es un sistema masivo de distribución de información del cliente / servidor, como se muestra en el siguiente diagrama.

![alt text][imagen1]

[imagen1]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/TheWeb.png "The Web"

Muchas aplicaciones se están ejecutando al mismo tiempo a través de Internet, tales como la navegación web / surf, correo electrónico, transferencia de archivos, streaming de audio y video, y así sucesivamente. Para que la comunicación que tendrá lugar entre el cliente y el servidor sea adecuada, estas aplicaciones deben estar de acuerdo con un protocolo específico de nivel de aplicación como HTTP,FTP, SMTP, POP, y etc.

**Protocolo de transferencia de hipertexto (HTTP)**
--
HTTP (Hypertext Transfer Protocol) es quizás el protocolo de aplicación más popular en Internet (o en la web).

- HTTP es un cliente-servidor de petición-respuesta asimétrica de protocolo como se ilustra. Un cliente HTTP envía un mensaje de petición a un servidor HTTP. El servidor, a su vez, devuelve un mensaje de respuesta. En otras palabras, HTTP es un protocolo de extracción , el cliente tira de información desde el servidor (en lugar de que el servidor empuje información hasta el cliente).


![alt text][imagen2]

[imagen2]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png "web programming"

- HTTP es un protocolo sin estado. En otras palabras, la solicitud actual no sabe lo que se ha hecho en las anteriores solicitudes.
- HTTP permite la negociación de tipo de datos y representación, a fin de permitir que los sistemas que se construyan de forma independiente de los datos se transfieran.
- Citando el RFC2616: "El Protocolo de transferencia de hipertexto (HTTP) es un protocolo de nivel de aplicación para sistemas de información distribuidos, de colaboración e hipermedia. Es genérico sin estado, el protocolo se puede utilizar para muchas tareas más allá de su uso para el hipertexto, por ejemplo, como servidores de nombres y sistemas de gestión de objetos distribuidos a través de la extensión de sus métodos de petición, códigos de error y los encabezados".

**Navegador**
--
Cada vez que se emite una dirección URL de su navegador para obtener un recurso web a través de HTTP, por ejemplo http://www.nowhere123.com/index.html, el navegador se convierte en la dirección URL de un _mensaje de solicitud_ y la envía al servidor HTTP. El servidor HTTP interpreta el mensaje de petición, y le devuelve un mensaje de respuesta apropiado, que puede ser el recurso que ha solicitado o un mensaje de error. Este proceso se ilustra a continuación:

![alt text][imagen3]

[imagen3]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_Steps.png "HTTP Steps"

**Localizador Uniforme de Recursos (URL)**
--
Un URL (Uniform Resource Locator) se utiliza para identificar de forma exclusiva un recurso a través de Internet. Un URL tiene la siguiente sintaxis:
```sh 
protocolo://hostname:port/path-and-file-name
```
Hay 4 partes en una dirección URL:

1. *Protocolo* : el protocolo de nivel de aplicación utilizado por el cliente y el servidor, por ejemplo, HTTP, FTP y telnet.
2. *Hostname* : el nombre de dominio DNS (por ejemplo, www.nowhere123.com) o la dirección IP (por ejemplo, 192.128.1.2) del servidor.
3. *Port* : el número de puerto TCP en el que el servidor escucha las peticiones entrantes de los clientes.
4. *Path-and-file-name* : el nombre y la ubicación del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en el URL http://www.nowhere123.com/docs/index.html, el protocolo de comunicación es HTTP; es el nombre de host www.nowhere123.com. El número de puerto no se ha especificado en la URL, y adquiere el número predeterminado, que es el puerto TCP 80 para HTTP. La ruta y el nombre del archivo para el recurso que se encuentra es " /docs/index.html".

Otros ejemplos de URL son:
```
ftp://www.ftp.org/docs/test.txt
mailto: user@test101.com
news: soc.culture.singapore
telnet: //www.nowhere123.com/
```
**Protocolo HTTP**
--
Como se ha mencionado, cada vez que se introduce un URL en el cuadro de dirección del navegador, el navegador traduce la dirección URL en un mensaje de solicitud de acuerdo con el protocolo especificado; y envía el mensaje de petición al servidor.

Por ejemplo, el navegador traduce la dirección URL http://www.nowhere123.com/doc/index.htmlen en el siguiente mensaje de solicitud:
```
GET  /docs/index.html HTTP / 1.1
Host: www.nowhere123.com
Accept: image / gif, image / jpeg, * / *
Accept-Language: en-us
Accept-Encoding: gzip, desinfle
User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
(linea en blanco)
```
Cuando este mensaje de solicitud llega al servidor, el servidor puede tomar cualquiera de estas acciones:

1. El servidor interpreta la petición recibida, mapea la solicitud en un _archivo_ en el directorio de documentos del servidor, y devuelve el archivo solicitado al cliente.
2. El servidor interpreta la petición recibida, mapea la solicitud en un _programa_ guardado en el servidor, ejecuta el programa, y devuelve la salida del programa al cliente.
3. La solicitud no puede ser satisfecha, el servidor devuelve un mensaje de error.

Un ejemplo del mensaje de respuesta HTTP es como se muestra:
```
HTTP / 1.1 200 OK
Date: Sun 18 Oct 2009 08:56:53 GMT
Server: Apache / 2.2.14 (Win32)
Last-Modified: Sáb 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Connection: close
Content-Type: text / html
X-Pad: avoid browser bug
  
<Html> <body> <h1> Así funciona! </ H1> </ body> </ html>
```
El navegador recibe el mensaje de respuesta, interpreta el mensaje y muestra el contenido del mensaje en la ventana del navegador de acuerdo con el tipo de medio de la respuesta (como en la cabecera de respuesta Content-Type). Los tipos de medios comunes incluyen " text/plain", " text/html", " image/gif", " image/jpeg", " audio/mpeg", " video/mpeg", " application/msword" y " application/pdf".
En su estado de reposo, un servidor HTTP no hace más que escuchar la dirección (es) IP y el puerto (s) especificado en la configuración de solicitud entrante. Cuando llega una petición, el servidor analiza el encabezado del mensaje, aplica las reglas especificadas en la configuración, y toma la acción apropiada. El control principal del webmaster sobre la acción del servidor web es a través de la configuración, el cual será tratada en mayor detalle en las secciones posteriores.

**HTTP a través de TCP / IP**
--
HTTP es un protocolo de nivel de aplicación cliente-servidor. Por lo general se ejecuta sobre una conexión TCP / IP, como se ilustra. (HTTP necesita no ser ejecutado en TCP / IP. Sólo se presupone un transporte fiable. Cualquier protocolo de transporte que ofrecen tales garantías pueden ser utilizados.)

![alt text][imagen4]

[imagen4]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_OverTCPIP.png "HTTP OverTCPIP"

TCP / IP (Transmission Control Protocol / Internet Protocol) es un conjunto de protocolos de transporte y capas de red para que las máquinas se comuniquen entre sí a través de la red.
IP (Internet Protocol) es un protocolo de capa de red, se ocupa de direccionamiento de red y enrutamiento. En una red IP, a cada máquina se asigna una dirección IP única (por ejemplo, 165.1.2.3), y el software de IP es responsable de encaminar un mensaje desde la fuente de IP a la dirección IP de destino. En IPv4 (versión 4 de IP), la dirección IP se compone de 4 bytes, cada uno de los rangos es de 0 a 255, separados por puntos, a esta forma se le llama *forma cuádruple de puntos y rayas*. Este esquema de numeración soporta hasta 4G electrónico de la red. La última IPv6 (IP versión 6) soporta más direcciones. Debido a que memorizar el número es difícil para la mayoría de las personas, un nombre de dominio english-like, como www.nowhere123.com se utiliza en su lugar. El DNS (Domain Name Service) traduce el nombre de dominio a la dirección IP (a través de tablas de búsqueda distribuidas). Una dirección IP 127.0.0.1 especial siempre se refiere a su propia máquina. Su nombre es domian " localhost" y puede ser utilizado para *las pruebas de bucle de retorno local*.

TCP (Protocolo de control de transmisión) es un protocolo de capa de transporte, responsable de establecer una conexión entre dos máquinas. TCP consta de 2 protocolos: TCP y UDP (Datagrama de paquete de usuarios). TCP es *fiable*, cada paquete tiene un número de secuencia, y se espera un acuse de recibo. Un paquete será retransmitido si no es recibido por el receptor. La entrega de paquetes está garantizado en TCP. UDP no garantiza la entrega de paquetes, y por lo tanto no es fiable. Sin embargo, UDP tiene menos sobrecarga de la red y se puede utilizar para aplicaciones tales como vídeo y audio streaming, donde la fiabilidad no es crítica.

TCP *multiplexa* aplicaciones dentro de una máquina IP. Para cada máquina de IP, TCP soporta (multiplexa) hasta 65.536 puertos (o enchufes), desde el número puerto entre 0 y 65535. Aplicaciones, tales como HTTP o FTP, se ejecutan (o escuchan) en un número determinado de puerto para las solicitudes entrantes. Del puerto 0 a 1023 son pre-asignados a los protocolos populares, por ejemplo, HTTP a 80, a los 21 FTP, Telnet a 23, a 25 SMTP, NNTP en el 119, y el DNS a los 53, el puerto 1024 y superiores están a disposición de los usuarios.

A pesar de que el puerto TCP 80 es pre-asignado a HTTP como el número de puerto HTTP predeterminado, esto no significa que prohíbe la ejecución de un servidor HTTP en otro número de puerto asignado por el usuario (1024-65535), tales como 8000, 8080, especialmente para servidor de prueba. También puede ejecutar varios servidores HTTP en la misma máquina en diferentes números de puerto. Cuando un cliente envía una URL sin indicar explícitamente el número de puerto, por ejemplo, http://www.nowhere123.com/docs/index.html el navegador se conectará con el número 80 de puerto por defecto de la acogida www.nowhere123.com. Es necesario especificar el número del puerto en la URL, por ejemplo, http://www.nowhere123.com:8000/docs/index.html si el servidor se está ejecutando en el puerto 8000 y no el puerto 80 por defecto.

En resumen, para comunicarse a través de TCP / IP, lo que se necesita saber es (a) la dirección IP o el nombre del host, (b) Número de puerto.

**Especificaciones HTTP**
--

La especificación HTTP se mantiene por el W3C (Consorcio Mundial Web) y disponible en http://www.w3.org/standards/techs/http. Actualmente hay dos versiones de HTTP, es decir, HTTP / 1.0 y HTTP / 1.1. La versión original, HTTP / 0.9 (1991), escrito por Tim Berners-Lee, es un protocolo simple de transferencia de datos en bruto a través de Internet. HTTP / 1.0 (1996) (definido en RFC 1945), ha mejorado el protocolo permitiendo mensajes MIME-like. HTTP / 1.0 no se ocupa de los problemas de servidores proxy, almacenamiento en caché de conexión persistente, hosts virtuales, y el rango de descarga. Estas características se proporcionan en HTTP / 1.1 (1999) (definidos en RFC 2616)

**Apache HTTP Server o Apache Tomcat**
--
______________________________________

Se necesita un servidor HTTP (como Apache HTTP Server o Apache Tomcat) para estudiar el protocolo HTTP.

El servidor HTTP Apache es un servidor de producción industrial-fuerza popular, producida por Apache Software Foundation (ASF) @ www.apache.org . ASF es una base de software de código abierto. Es decir, el servidor Apache HTTP es libre, con el código fuente.

El primer servidor HTTP está escrito por Tim Berners Lee en el CERN (Centro Europeo de Investigación Nuclear) en Ginebra, Suiza, quien también inventó HTML. Apache fue construido en NCSA (National Center for Supercomputing Applications, EE.UU.) "httpd 1.3" servidor, a principios de 1995. Apache probablemente recibe su nombre del hecho de que consiste en un código original (desde un servidor web httpd anterior NCSA) además de algunos parches; o del nombre de una tribu india americana.

Leer "Apache How-to" sobre cómo instalar y configuare servidor Apache HTTP; o "Tomcat How-to" para instalar y empezar a trabajar con Apache Tomcat.

**Solicitud HTTP y Mensajes de respuesta**
--
__________________________________________

El cliente HTTP y el servidor se comunican mediante el envío de mensajes de texto. El cliente envía un *mensaje de petición* al servidor. El servidor, a su vez, devuelve un *mensaje de respuesta*.

Un mensaje HTTP consiste en una *cabecera de mensaje* y un opcional *cuerpo del mensaje*, separados por una *línea en blanco*, como se ilustra a continuación:


![alt text][imagen5]

[imagen5]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_MessageFormat.png "HTTP Message Format"

**HTTP mensaje de solicitud**
--
El formato de un mensaje de solicitud HTTP es como sigue:

![alt text][imagen6]

[imagen6]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png "HTTP Request Message"

**Línea de petición**

La primera línea de la cabecera se llama la *línea de petición*, seguido de *cabeceras de petición* opcionales.

La línea de solicitud tiene la siguiente sintaxis:

*`request-method-name request-URI HTTP-version`*

- *request-method-name* : el protocolo HTTP define un conjunto de métodos de petición, por ejemplo, GET, POST, HEAD y OPCIONES. El cliente puede utilizar uno de estos métodos para enviar una petición al servidor.
- *request-URI* : especifica el recurso solicitado.
- *HTTP-version* : dos versiones están actualmente en uso: HTTP / 1.0 y HTTP / 1.1.

Ejemplos de línea de solicitud son:
```
GET /test.html HTTP / 1.1
HEAD /query.html HTTP / 1.0
POST /index.html HTTP / 1.1
```

**Cabeceras de petición**

Los encabezados de solicitud están en la forma de name:valuepares. Los valores múltiples, separados por comas, se pueden especificar.

*`request-header-name: request-header-value1, request-header-value2, ...`*

Los ejemplos de los encabezados de solicitud son:
```
Host: www.xyz.com
Connection: Keep-Alive
Accept: image / gif, image / jpeg, * / *
Accept-Language: us-es, fr, cn
```

**Ejemplo**

A continuación se muestra un ejemplo de un mensaje de petición HTTP:

![alt text][imagen7]

[imagen7]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessageExample.png "HTTP Request Message Example"

**Mensaje de respuesta HTTP**
--
El formato del mensaje de respuesta HTTP es como se muestra:

![alt text][imagen8]

[imagen8]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessage.png "HTTP Response Message"

**Línea de estado**

La primera línea se llama *línea de estado* , seguida de la cabecera de respuesta opcional (s).

La línea de estado tiene la siguiente sintaxis:

*`HTTP-version status-code reason-phrase`*

- *HTTP-version* : La versión de HTTP utilizada en esta sesión. HTTP / 1.0 y HTTP / 1.1.
- *status-code* : un número de 3 dígitos generado por el servidor para reflejar el resultado de la solicitud.
- *reason-phrase* : da una breve explicación para el código de estado.
- Código de estado común y la razón frase son "200 OK", "404 Not Found", "403 Prohibido", "500 Internal Server Error".

Los ejemplos de línea de estado son:
```
HTTP / 1.1 200 OK
HTTP / 1.0 404 Not Found
HTTP / 1.1 403 Forbidden
```

**Encabezados de respuesta**

Las cabeceras de respuesta se presentan en forma name:valuede pares:

*`response-header-name: response-header-value1, response-header-value2, ...`*

Los ejemplos de cabeceras de respuesta son:
```
Content-Type: text / html
Content-Length: 35
Connection: Keep-Alive
Keep-alive: timeout = 15, max = 100
```
El cuerpo del mensaje de respuesta contiene los datos de los recursos solicitados.

**Ejemplo**

A continuación se muestra un mensaje de respuesta:


![alt text][imagen9]

[imagen9]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessageExample.png "HTTP Response Message Example"

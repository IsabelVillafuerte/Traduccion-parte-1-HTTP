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

Muchas aplicaciones se están ejecutando al mismo tiempo a través de Internet, tales como la navegación web / surf, correo electrónico, transferencia de archivos, streaming de audio y video, y así sucesivamente. Para que la comunicación que tendrá lugar entre el cliente y el servidor sea adecuada, estas aplicaciones deben estar de acuerdo con un protocolo específico de nivel de aplicación como HTTP, FTP, SMTP, POP, y etc.

**Protocolo de transferencia de hipertexto (HTTP)**
--
HTTP (Hypertext Transfer Protocol) es quizás el protocolo de aplicación más popular en Internet (o en la web).

- HTTP es un protocolo de cliente-servidor y petición-respuesta asimétrica como se ilustra. Un cliente HTTP envía un mensaje de petición a un servidor HTTP. El servidor, a su vez, devuelve un mensaje de respuesta. En otras palabras, HTTP es un protocolo de extracción , el cliente tira de información desde el servidor (en lugar de que el servidor empuje información hasta el cliente).


![alt text][imagen2]

[imagen2]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png "web programming"

- HTTP es un protocolo sin estado. En otras palabras, la solicitud actual no sabe lo que se ha hecho en las anteriores solicitudes.
- HTTP permite la negociación de tipo de datos y representación, a fin de permitir que los sistemas que se construyan de forma independiente de los datos se transfieran.
- Citando el RFC2616: "El Protocolo de transferencia de hipertexto (HTTP) es un protocolo de nivel de aplicación para sistemas de información distribuidos, de colaboración e hipermedia. Es genérico sin estado, el protocolo se puede utilizar para muchas tareas más allá de su uso para el hipertexto, por ejemplo, como servidores de nombres y sistemas de gestión de objetos distribuidos a través de la extensión de sus métodos de petición, códigos de error y los encabezados".

**Navegador**
--
Cada vez que se emite una dirección URL de su navegador para obtener un recurso web a través de HTTP, por ejemplo http://www.nowhere123.com/index.html, el navegador convierte la dirección URL en un _mensaje de solicitud_ y la envía al servidor HTTP. El servidor HTTP interpreta el mensaje de petición, y devuelve un mensaje de respuesta apropiado, que puede ser el recurso que ha solicitado o un mensaje de error. Este proceso se ilustra a continuación:

![alt text][imagen3]

[imagen3]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_Steps.png "HTTP Steps"

**Localizador Uniforme de Recursos (URL)**
--
Un URL (Uniform Resource Locator) se utiliza para identificar de forma exclusiva un recurso a través de Internet. Un URL tiene la siguiente sintaxis:

```sh
protocol://hostname:port/path-and-file-name
```

Hay 4 partes en una dirección URL:

1. *Protocol* : el protocolo de nivel de aplicación utilizado por el cliente y el servidor, por ejemplo, HTTP, FTP y telnet.
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

Por ejemplo, el navegador traduce la dirección URL http://www.nowhere123.com/doc/index.html en el siguiente mensaje de solicitud:

```
GET  /docs/index.html HTTP / 1.1
Host: www.nowhere123.com
Accept: image / gif, image / jpeg, * / *
Accept-Language: en-us
Accept-Encoding: gzip, desinfle
User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
(linea en blanco)
```

Cuando este mensaje de solicitud llega al servidor, el servidor puede realizar cualquiera de estas acciones:

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
En su estado de reposo, un servidor HTTP no hace más que escuchar la dirección (es) IP y el puerto (s) especificado en la configuración de solicitud entrante. Cuando llega una petición, el servidor analiza el encabezado del mensaje, aplica las reglas especificadas en la configuración, y toma la acción apropiada. El control principal del webmaster sobre la acción del servidor web es a través de la configuración, la cual será tratada con mayor detalle en las secciones posteriores.

**HTTP a través de TCP / IP**
--
HTTP es un protocolo de nivel de aplicación cliente-servidor. Por lo general se ejecuta sobre una conexión TCP / IP, como se ilustra. (HTTP necesita no ser ejecutado en TCP / IP. Sólo se presupone un transporte fiable. Cualquier protocolo de transporte que ofrecen tales garantías pueden ser utilizados.)

![alt text][imagen4]

[imagen4]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_OverTCPIP.png "HTTP OverTCPIP"

TCP / IP (Transmission Control Protocol / Internet Protocol) es un conjunto de protocolos de transporte y capas de red para que las máquinas se comuniquen entre sí a través de la red.

IP (Internet Protocol) es un protocolo de capa de red, se ocupa de direccionamiento de red y enrutamiento. En una red IP, a cada máquina se asigna una dirección IP única (por ejemplo, 165.1.2.3), y el software de IP es responsable de encaminar un mensaje desde la fuente de IP a la dirección IP de destino. En IPv4 (versión 4 de IP), la dirección IP se compone de 4 bytes, cada uno de los rangos es de 0 a 255, separados por puntos, a esta forma se le llama *forma cuádruple de puntos y rayas*. Este esquema de numeración soporta hasta 4G electrónico de la red. La última IPv6 (IP versión 6) soporta más direcciones. Debido a que memorizar el número es difícil para la mayoría de las personas, un nombre de dominio english-like, como www.nowhere123.com se utiliza en su lugar. El DNS (Domain Name Service) traduce el nombre de dominio a la dirección IP (a través de tablas de búsqueda distribuidas). Una dirección especial IP 127.0.0.1 siempre se refiere a su propia máquina. Su nombre es domian " localhost" y puede ser utilizada para *las pruebas de bucle de retorno local*.

TCP (Protocolo de control de transmisión) es un protocolo de capa de transporte, responsable de establecer una conexión entre dos máquinas. TCP consta de 2 protocolos: TCP y UDP (Datagrama de paquete de usuarios). TCP es *fiable*, cada paquete tiene un número de secuencia, y se espera un acuse de recibo. Un paquete será retransmitido si no es recibido por el receptor. La entrega de paquetes está garantizado en TCP. UDP no garantiza la entrega de paquetes, y por lo tanto no es fiable. Sin embargo, UDP tiene menos sobrecarga de la red y se puede utilizar para aplicaciones tales como vídeo y audio streaming, donde la fiabilidad no es crítica.

TCP *multiplexa* aplicaciones dentro de una máquina IP. Para cada máquina de IP, TCP soporta (multiplexa) hasta 65.536 puertos (o enchufes), desde el número puerto entre 0 y 65535. Aplicaciones, tales como HTTP o FTP, se ejecutan (o escuchan) en un número determinado de puerto para las solicitudes entrantes. Del puerto 0 a 1023 son pre-asignados a los protocolos populares, por ejemplo, HTTP a 80, a los 21 FTP, Telnet a 23, a 25 SMTP, NNTP en el 119, y el DNS a los 53, el puerto 1024 y superiores están a disposición de los usuarios.

A pesar de que el puerto TCP 80 es pre-asignado a HTTP como el número de puerto HTTP predeterminado, esto no significa que prohíbe la ejecución de un servidor HTTP en otro número de puerto asignado por el usuario (1024-65535), tales como 8000, 8080, especialmente para servidor de prueba. También puede ejecutar varios servidores HTTP en la misma máquina en diferentes números de puerto. Cuando un cliente envía una URL sin indicar explícitamente el número de puerto, por ejemplo, http://www.nowhere123.com/docs/index.html el navegador se conectará con el puerto 80 por defecto a partir del host www.nowhere123.com. Es necesario especificar el número del puerto en la URL, por ejemplo, http://www.nowhere123.com:8000/docs/index.html si el servidor se está ejecutando en el puerto 8000 y no el puerto 80 por defecto.

En resumen, para comunicarse a través de TCP / IP, lo que se necesita saber es (a) la dirección IP o el nombre del host, (b) Número de puerto.

**Especificaciones HTTP**
--

La especificación HTTP se mantiene por el W3C (Consorcio Mundial Web) y disponible en http://www.w3.org/standards/techs/http. Actualmente hay dos versiones de HTTP, es decir, HTTP / 1.0 y HTTP / 1.1. La versión original, HTTP / 0.9 (1991), escrito por Tim Berners-Lee, es un protocolo simple de transferencia de datos en bruto a través de Internet. HTTP / 1.0 (1996) (definido en RFC 1945), ha mejorado el protocolo permitiendo mensajes MIME-like. HTTP / 1.0 no se ocupa de los problemas de servidores proxy, almacenamiento en caché de conexión persistente, hosts virtuales, y el rango de descarga. Estas características se proporcionan en HTTP / 1.1 (1999) (definidos en RFC 2616)

**Servidor HTTP Apache ó Apache Tomcat**
--
______________________________________

Se necesita un servidor HTTP (como Apache HTTP Server o Apache Tomcat) para estudiar el protocolo HTTP.

El servidor HTTP Apache es un servidor de producción industrial-fuerza popular, producida por Apache Software Foundation (ASF) @ www.apache.org . ASF es una base de software de código abierto. Es decir, el servidor Apache HTTP es libre, con el código fuente.

El primer servidor HTTP fué escrito por Tim Berners Lee en el CERN (Centro Europeo de Investigación Nuclear) en Ginebra, Suiza, quien también inventó HTML. Apache fue construido en NCSA (National Center for Supercomputing Applications, EE.UU.) en el servidor "httpd 1.3", a principios de 1995. Apache probablemente recibe su nombre debido a que consiste en un código original (desde un servidor web httpd anterior NCSA) además de algunos parches; o del nombre de una tribu india americana.

Leer "Apache How-to" sobre cómo instalar y configuare servidor Apache HTTP; o "Tomcat How-to" para instalar y empezar a trabajar con Apache Tomcat.

**Solicitud HTTP y Mensajes de respuesta**
--
__________________________________________

El cliente HTTP y el servidor se comunican mediante el envío de mensajes de texto. El cliente envía un *mensaje de petición* al servidor. El servidor, a su vez, devuelve un *mensaje de respuesta*.

Un mensaje HTTP consiste en una *cabecera de mensaje* y un opcional *cuerpo del mensaje*, separados por una *línea en blanco*, como se ilustra a continuación:


![alt text][imagen5]

[imagen5]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_MessageFormat.png "HTTP Message Format"

**Mensaje de solicitud HTTP**
--
El formato de un mensaje de solicitud HTTP es como sigue:

![alt text][imagen6]

[imagen6]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png "HTTP Request Message"

**Línea de petición**

La primera línea de la cabecera se llama la *línea de petición*, seguido de *cabeceras de petición* opcionales.

La línea de solicitud tiene la siguiente sintaxis:

*`request-method-name request-URI HTTP-version`*

- *request-method-name* : el protocolo HTTP define un conjunto de métodos de petición, por ejemplo, GET, POST, HEAD y OPTIONS. El cliente puede utilizar uno de estos métodos para enviar una petición al servidor.
- *request-URI* : especifica el recurso solicitado.
- *HTTP-version* : dos versiones están actualmente en uso: HTTP / 1.0 y HTTP / 1.1.

Ejemplos de línea de solicitud:
```
GET /test.html HTTP / 1.1
HEAD /query.html HTTP / 1.0
POST /index.html HTTP / 1.1
```

**Cabeceras de petición**

Los encabezados de solicitud están en la forma de nombre:valores pares. Los valores múltiples, separados por comas, se pueden especificar.

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

La primera línea se llama *línea de estado*, seguida de la cabecera de respuesta opcional (s).

La línea de estado tiene la siguiente sintaxis:

*`HTTP-version status-code reason-phrase`*

- *HTTP-version* : La versión de HTTP utilizada en esta sesión. HTTP / 1.0 y HTTP / 1.1.
- *status-code* : un número de 3 dígitos generado por el servidor para reflejar el resultado de la solicitud.
- *reason-phrase* : da una breve explicación para el código de estado.
- El código de estado común es "200 OK", "404 Not Found", "403 Forbidden", "500 Internal Server Error".

Los ejemplos de línea de estado son:

```
HTTP / 1.1 200 OK
HTTP / 1.0 404 Not Found
HTTP / 1.1 403 Forbidden
```

**Encabezados de respuesta**

Las cabeceras de respuesta se presentan en forma nombre:valores pares:

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

**Métodos de Petición HTTP**
--
---------------------------
El protocolo HTTP define un conjunto de métodos de petición. Un cliente puede utilizar uno de estos métodos de petición para enviar un mensaje de petición a un servidor HTTP. Los métodos son:

- GET: Un cliente puede utilizar la solicitud GET para obtener un recurso web desde el servidor.
- HEAD: Un cliente puede utilizar la petición HEAD para obtener el encabezado que una petición GET habría obtenido. Desde el encabezado se incluye la fecha de la última modificación de los datos, esto se puede utilizar para comprobarla con la copia caché local.
- POST: Se utiliza para enviar los datos al servidor web.
- PUT: Pregunta el servidor para almacenar los datos.
- DELETE: Pregunta el servidor para eliminar los datos.
- TRACE: Pregunta el servidor para devolver un rastreo de diagnóstico de las medidas que adopta.
- OPTIONS: Pregunta al servidor para devolver la lista de métodos de petición que apoya.
- CONNECT: Se utiliza para decirle a un proxy que establezca una conexión con otro host y sólo debe responder al contenido, sin intentar analizar o almacenar en caché. Esto a menudo se utiliza para hacer la conexión SSL a través del proxy.
- Otros métodos de extensión.

**"GET" Método de solicitud**
--
-----------------------------
GET es el método más común de solicitud HTTP. Un cliente puede utilizar el método GET para solicitar (o "get") una pieza de recursos desde un servidor HTTP. Un mensaje de petición GET toma la siguiente sintaxis:

```
GET request-URI HTTP-version
( cabeceras de petición opcional )
 (línea en blanco) 
( cuerpo de la petición opcional )
```

- La palabra clave GET es sencible en su escritura, debe estar en mayúsculas.
- request-URI : especifica la ruta del recurso solicitado, la cual debe empezar desde la raíz " /" del directorio de la base de documentos.
- HTTP-version : HTTP / 1.0 o HTTP / 1.1. Este cliente negocia el protocolo a utilizar para la sesión actual. Por ejemplo, el cliente puede solicitar el uso de HTTP / 1.1. Si el servidor no soporta el protocolo HTTP / 1.1, puede informar al cliente mediante la respuesta utilizada de HTTP / 1.0.
- El cliente utiliza los encabezados opcionales de solicitud (tales como Accept, Accept-Language, y etc) para negociar con el servidor y pedir al servidor entregar los contenidos preferidos (por ejemplo, en el idioma que el cliente prefiere).
- El mensaje de solicitud GET tiene un cuerpo de solicitud opcional que contiene la cadena de consulta (que se explica más adelante).

Las solicitudes HTTP de pruebas
--

Hay muchas maneras de poner a prueba las peticiones HTTP. Su pueden utilizar programas de utilidad como " telnet" o " hyperterm" (búsqueda de " telnet.exe" o " hypertrm.exe" bajo c:\windows), o escribir en el mismo programa de la red para enviar un mensaje de petición puro a un servidor HTTP para poner a prueba las diversas peticiones HTTP.

**Telnet**

"Telnet" es muy útil en la creación de redes. Puede utilizar telnet para establecer una conexión TCP con un servidor; y emitir solicitudes HTTP primas. Por ejemplo, suponga que ha comenzado su servidor HTTP en la máquina local (la dirección IP 127.0.0.1) en el puerto 8000:

```
> telnet
telnet> help
... telnet help menu ...
telnet> open 127.0.0.1 8000
Connecting To 127.0.0.1...
GET /index.html HTTP/1.0
( Pulsa INTRO dos veces para enviar la línea en blanco que termina ...)
... Mensaje de respuesta HTTP ...
```

Telnet es un protocolo basado en caracteres. Cada caracter que se introduce en el cliente telnet se enviará inmediatamente al servidor. Por lo tanto, no se puede hacer un error tipográfico al ingresar comandos puros, como borrar y la tecla de retroceso que se envían al servidor. Puede que tenga que activar la opción de "eco local" para ver los caracteres que ingresa. Consulte el manual de telnet (ayuda de búsqueda de Windows ') para obtener más información sobre el uso de telnet.

Programa de red
--

También puede escribir su propio programa de red para emitir peticiones puras de HTTP a un servidor HTTP. El programa de red deberá establecer primero una conexión TCP / IP con el servidor. Una vez establecida la conexión TCP, puede emitir la solicitud.
Un ejemplo de un programa de red escrito en Java, se muestra a continuación (suponiendo que el servidor HTTP se ejecuta en el localhost 127.0.0.1 dirección (IP) en el puerto 8000):

```
import java.net. *;
import java.io. *;
   
public class HttpClient {
   public static void main(String[] args) throws IOException {
      // El host y el puerto que va a conectar.
      String host = "127.0.0.1";
      int port = 8000;
      // Crear un socket TCP y conectar con el host: puerto.
      Socket socket = new Socket(host, port);
      // Crear los flujos de entrada y de salida para la toma de red.
      BufferedReader in
         = new BufferedReader(
              new InputStreamReader(socket.getInputStream()));
      PrintWriter out
         = new PrintWriter(socket.getOutputStream(), true);
      // Enviar solicitud al servidor HTTP. 
      out.println("GET /index.html HTTP/1.0");
      out.println();   // línea en blanco de cabeza y cuerpo separador
      out.flush();
      // Leer la respuesta y la pantalla en la consola.
      String line;
      // readLine () devuelve un valor nulo si el servidor cierra el socket de red.
      while((line = in.readLine()) != null) {
         System.out.println(line);
      }
      // Cerrar el I/O streams.
      in.close();
      out.close();
   }
}
```

Solicitud HTTP / 1.0 GET
--

A continuación se muestra la respuesta de una petición HTTP / 1.0 GET (tema a través de telnet o en su propio programa de red - suponiendo que haya comenzado su servidor HTTP):

```
GET /index.html HTTP / 1.0 
(introducir dos veces para crear una línea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Sun 18 Oct 2009 08:56:53 GMT
Servidor: Apache / 2.2.14 (Win32)
Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Conexión: cerrar
Content-Type: text / html
X-Pad: evitar el fallo del navegador
   
<Html> <body> <h1> Así funciona! </ H1> </ body> </ html>
   
Conexión al host perdido.
```

En este ejemplo, el cliente envía una solicitud GET para pedir un documento denominado " /index.html"; y negocia utilizar el protocolo HTTP / 1.0. Se necesita una línea en blanco después de la cabecera de la solicitud. Este mensaje de petición no contiene un cuerpo.

El servidor recibe el mensaje de petición, interpreta y asigna el URI de solicitud de un documento bajo su documentación de directorio. Si el documento solicitado está disponible, el servidor devuelve el documento con un código de estado de respuesta "200 OK". Las cabeceras de respuesta proporcionan la descripción necesaria del documento devuelto, tal como la última fecha de modificación ( Last-Modified), el tipo MIME ( Content-Type), y la longitud del documento ( Content-Length). El cuerpo de la respuesta contiene el documento solicitado. El navegador formateará y mostrará el documento de acuerdo con su tipo de medio (por ejemplo, texto plano, HTML, JPEG, GIF, etc) y diversa información obtenida de las cabeceras de respuesta.

Notas:

- El nombre del método de petición "GET" es sencible en su escritura, y debe estar en mayúsculas.
- Si el nombre del método de solicitud fue escrito incorrectamente, el servidor devolverá un mensaje de error "501 Method Not Implemented".
- Si no se permite el nombre del método de la petición, el servidor devolverá un mensaje de error "405 Method Not Allowed". Por ejemplo, DELETE es un nombre de método válido, pero no se puede permitir (o implementar) por el servidor.
- Si el URI de solicitud no existe, el servidor devolverá un mensaje de error "404 Not Found". Usted tiene que emitir una URI de solicitud adecuada, a partir de la raíz del documento " /". De lo contrario, el servidor devolverá un mensaje de error "400 Bad Request".
- Si la versión HTTP es incorrecta, el servidor devolverá un mensaje de error "400 Bad Request".
- En HTTP / 1.0, de forma predeterminada, el servidor cierra la conexión TCP después de que se entregó la respuesta. Si utiliza telnet para conectarse al servidor, el mensaje "Connection to host lost" aparece inmediatamente después que se recibe el cuerpo de la respuesta. Se podría utilizar un encabezado de solicitud opcional " Connection: Keep-Alive" para solicitar una persistencia de conexión (o keep-alive), de modo que otra petición puede ser enviada a través de la misma conexión TCP para lograr una mejor eficiencia de la red. Por otro lado, utiliza HTTP / 1.1 keep-alive como conexión predeterminada.

Respuesta Código de estado
--

La primera línea del mensaje de respuesta (es decir, la línea de estado) contiene el código de estado de respuesta, que se genera por el servidor para indicar el resultado de la solicitud.

El código de estado es un número de 3 dígitos:

- 1xx (Informativo): Solicitud recibida, el servidor continúa el proceso.
- 2xx (Éxito): La petición fue recibida con éxito, entendido, aceptado y mantenido.
- 3xx (redirección): La acción será tomada en orden con el fin de completar la solicitud.
- 4xx (Error de cliente): La solicitud contiene sintaxis incorrecta o no se puede entender.
- 5xx (Error del servidor): El servidor no pudo cumplir con una solicitud aparentemente válida.

Algunos códigos de estado que se encuentran comúnmente son:

- 100 Continue: El servidor ha recibido la solicitud y está en proceso de dar la respuesta.
- 200 OK: La solicitud se ha cumplido.
- 301 Move Permanently: el recurso solicitado se ha movido permanentemente a una nueva ubicación. La URL de la nueva ubicación se da en la cabecera de respuesta llamada Location. El cliente debe emitir una nueva petición a la nueva ubicación. La aplicación debe actualizar todas las referencias a esta nueva ubicación.
- 302 Found & Redirect (or Move Temporarily): Igual que el 301, pero la nueva ubicación está temporalmente redireccionada. El cliente debe emitir una nueva solicitud, para las aplicaciones no es necesario actualizar las referencias.
- 304 Not Modified: En respuesta a la If-Modified-Sincepetición de GET condicional, el servidor notifica que el recurso solicitado no se ha modificado.
- 400 Bad Request: el servidor no puede interpretar o comprender la solicitud, probablemente hay un error de sintaxis en el mensaje de petición.
- 401 Authentication Required: El recurso solicitado está protegido, y requieren credenciales de cliente (usuario / contraseña). El cliente debe volver a presentar la solicitud con su credencial (usuario / contraseña).
- 403 Forbidden: El servidor se niega a suministrar el recurso, independientemente de la identidad del cliente.
- 404 Not Found: El recurso solicitado no se encuentra en el servidor.
- 405 Method Not Allowed: El método de solicitud utilizado, por ejemplo, POST, PUT, DELETE, es un método válido. Sin embargo, el servidor no permite el método para el recurso solicitado.
- 408 Request Timeout:
- 414 Request URI too Large:
- 500  Internal Server Error: El servidor se confunde, a menudo causado por un error en el programa del servidor al responder a la solicitud.
- 501 Method Not Implemented: El método de solicitud utilizado no es válido (podría ser causado por un error de escritura, por ejemplo, "GET" mal escrito como "Get").
- 502 Bad Gateway: proxy o el puerto de enlace indica que se recibió una mala respuesta del servidor en sentido ascendente.
- 503 Service Unavailable: El servidor no puede responder debido a una sobrecarga o mantenimiento. El cliente puede volver a intentarlo más tarde.
- 504 Gateway Timeout: proxy o el puerto de enlace indican que se recibió un tiempo de espera de un servidor ascendente.

Más HTTP / 1.0. Ejemplos de petición GET
--

**Ejemplo: Método de solicitud misspelt**

En la solicitud, "GET" está mal escrito como "get". El servidor devuelve un error "501 Method Not Implemented". El encabezado de respuesta " Allow" le dice al cliente los métodos permitidos.

```
get /test.html HTTP / 1.0
(Introduzca dos veces para crear una línea en blanco)
```

```
HTTP / 1.1 501 Método no implementado
Fecha: Sun 18 Oct 2009 10:32:05 GMT
Servidor: Apache / 2.2.14 (Win32)
Permitir: GET, HEAD, POST, OPCIONES, TRACE
Content-Length: 215
Conexión: cerrar
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 501 Método no implementado </ title>
</ Head> <body>
<H1> Método no implementado </ h1>
<P> llegar a /index.html no es compatible. <br />
</ P>
</ Body> </ html>
```

**Ejemplo: 404 Archivo no encontrado**

En esta solicitud GET, la solicitud de URL " /t.html" no se puede encontrar en el directorio de documentos del servidor. El servidor devuelve un error "404 Not Found".

```
GET /t.html HTTP / 1.0
(Introduzca dos veces para crear una línea en blanco)
```

```
HTTP / 1.1 404 Not Found
Fecha: Sun 18 Oct 2009 10:36:20 GMT
Servidor: Apache / 2.2.14 (Win32)
Content-Length: 204
Conexión: cerrar
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 404 no encontrado </ title>
</ Head> <body>
<H1> No se ha encontrado </ h1>
<P> El /t.html URL solicitada no se encuentra en este servidor. </ P>
</ Body> </ html>
```

**Ejemplo: HTTP número incorrecto de versión**

En esta solicitud GET, la versión HTTP está mal escrita, con un error en la sintaxis. El servidor devuelve un error "404 Bad Request". La versión HTTP debe ser HTTP / 1.0 o HTTP / 1.1.

```
GET /index.html HTTTTTP / 1.0 
(introducir dos veces para crear una línea en blanco)
```

```
HTTP / 1.1 400 Bad Request
Fecha: 08 de Feb de 2004 01:29:40 GMT
Servidor: Apache / 1.3.29 (Win32)
Conexión: cerrar
Content-Type: text / html; charset = iso-8859-1

<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<HTML> <HEAD>
<TITLE> 400 Bad Request </ TITLE>
</ HEAD> <BODY>
<H1> Solicitud incorrecta </ h1>
Su navegador envía una petición que este servidor no podía comprender. <P>
La línea de solicitud contenía caracteres no válidos a partir de la cadena de protocolo. <P> <P>
</ BODY> </ HTML>
```

Nota: La última versión de Apache 2.2.14 ignora este error y devuelve el documento con código de estado "200 OK".


**Ejemplo: URI de solicitud incorrecto**

En la solicitud GET siguiente, el URI de solicitud no comenzó de la raíz " /", lo que dio lugar a una "solicitud incorrecta".

```
GET test.html HTTP / 1.0
(linea en blanco)
```

```
HTTP / 1.1 400 Bad Request
Fecha: Sun 18 Oct 2009 10:42:27 GMT
Servidor: Apache / 2.2.14 (Win32)
Content-Length: 226
Conexión: cerrar
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 400 Bad Request </ title>
</ Head> <body>
<H1> Solicitud incorrecta </ h1>
<P> El navegador envía una petición que este servidor no podía entender. <br />
</ P>
</ Body> </ html>
```

**Ejemplo: conexión Keep-Alive**

Por defecto, a petición de HTTP / 1.0 GET, el servidor cierra la conexión TCP una vez que la respuesta se entrega. Se podría solicitar que se mantenga la conexión TCP, (a fin de enviar otra solicitud a través de la misma conexión TCP, para mejorar la eficiencia de la red), a través de un encabezado de solicitud opcional "Connection: Keep-Alive". El servidor incluye una " Connection: Keep-Alive con cabecera de respuesta" para informar al cliente que puede enviar otra solicitud a través de esta conexión, antes de la conexión de tiempo de espera. Otra cabecera de respuesta " Keep-Alive: timeout=x, max=x" indica al cliente el tiempo de espera (en segundos) y el número máximo de solicitudes que se pueden enviar a través de esta conexión persistente.

```
GET /test.html HTTP / 1.0
 Conexión: Keep-Alive 
(línea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Sun 18 Oct 2009 10:47:06 GMT
Servidor: Apache / 2.2.14 (Win32)
Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Mantenimiento de conexión: tiempo de espera = 5, max = 100 
Conexión: keep-alive
Content-Type: text / html
   
<Html> <body> <h1> Así funciona! </ H1> </ body> </ html>
```

Notas:
- El mensaje "Connection to host lost" (para telnet) aparece después de " keep-alive" en tiempo de espera.
- Antes de que el mensaje "Connection to host lost" aparezca (es decir, mantenimiento de conexión de tiempo de espera), se puede enviar una nueva solicitud a través de la misma conexión TCP.
- El encabezado " Connection: Keep-alive" no distingue entre mayúsculas y minúsculas. El espacio es opcional.
- Si una cabecera opcional está mal escrita o no es válida, se omite en el servidor.

**Ejemplo: Cómo acceder a un recurso protegido**

La siguiente petición GET ha intentado acceder a un recurso protegido. El servidor devuelve un error "403 Forbidden". En este ejemplo, el directorio " htdocs\forbidden" está configurado para denegar el acceso completo con el archivo de configuración del servidor Apache HTTP " httpd.conf" de la siguiente manera:

```
<Directorio "C: / apache / htdocs / prohibido">
   Orden negar, permitir
   negar todo
</ Directory>
```

```
GET /forbidden/index.html HTTP / 1.0
(linea en blanco)
```

```
HTTP / 1.1 403 Forbidden
Fecha: Sun 18 Oct 2009 11:58:41 GMT
Servidor: Apache / 2.2.14 (Win32)
Content-Length: 222
Mantenimiento de conexión: tiempo de espera = 5, max = 100
Conexión: Keep-Alive
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 403 Prohibido </ title>
</ Head> <body>
<H1> Prohibida </ h1>
<P> Usted no tiene permiso para acceder a /forbidden/index.html
en este servidor. </ p>
</ Body> </ html>
```

**Solicitud GET HTTP / 1.1**

El servidor HTTP / 1.1 es compatible con las llamadas máquinas virtuales. Es decir, el mismo servidor físico podría albergar varios hosts virtuales, con diferentes nombres de host (por ejemplo, www.nowhere123.comy www.test909.com) y sus propios directorios dedicados a documentos de raíz. Por lo tanto, en una petición HTTP / 1.1 GET, es obligatorio incluir un encabezado de solicitud llamado " Host", para seleccionar uno de los hosts virtuales.

**Ejemplo: Solicitud HTTP / 1.1**

HTTP / 1.1 mantiene persistencia (o keep-alive) de conexión por defecto para mejorar la eficiencia de la red. Puede utilizar un encabezado de solicitud " Connection: Close" para pedir al servidor cerrar la conexión TCP una vez que se entrega la respuesta.

```
GET /index.html HTTP / 1.1
 Host: 127.0.0.1 
(línea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Sun 18 Oct 2009 12:10:12 GMT
Servidor: Apache / 2.2.14 (Win32)
Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Content-Type: text / html
   
<Html> <body> <h1> Así funciona! </ H1> </ body> </ html>
```

**Ejemplo: HTTP / 1.1. Ausencia del encabezado de host**

El siguiente ejemplo muestra que la cabecera " Host" es obligatoria en una petición HTTP / 1.1. Si la cabecera " Host" no se encuentra, el servidor devuelve un error "400 Bad Request".

```
GET /index.html HTTP / 1.1
(linea en blanco)
```

```
HTTP / 1.1 400 Bad Request
Fecha: Sun 18 Oct 2009 12:13:46 GMT
Servidor: Apache / 2.2.14 (Win32)
Content-Length: 226
Conexión: cerrar
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 400 Bad Request </ title>
</ Head> <body>
<H1> Solicitud incorrecta </ h1>
<P> El navegador envía una petición que este servidor no podía entender. <br />
</ P>
</ Body> </ html>
```

Las peticiones GET condicionales
--
En todos los ejemplos anteriores, el servidor devuelve todo el documento si la petición puede ser satisfecha (es decir incondicional). Es posible utilizar el encabezado de la solicitud adicional para emitir una "solicitud condicional". Por ejemplo, para que se solicite un documento basado en la fecha de la última modificación (a fin de decidir si utilizar la copia caché local), o para pedir una parte del documento (o rango) en lugar de todo el documento (útil para la descarga de documentos de gran tamaño).

Los encabezados de solicitud condicional incluyen:

-If-Modified-Since (Verificar el código de estado de respuesta "304 Not Modified").
-If-Unmodified-Since
-If-Match
-If-None-Match
-If-Range

Cabeceras de petición
--
En esta sección se describen algunas de las cabeceras de petición de uso común. Consulte la especificación HTTP para más detalles. La sintaxis del nombre de la cabecera, es decir, con inicial-cap se unen utilizando guión ( -), por ejemplo, Content-Length, If-Modified-Since.

**Host: domain-name** - HTTP / 1.1 soporta máquinas virtuales. Múltiples nombres DNS (por ejemplo, www.nowhere123.com y www.nowhere456.com) pueden residir en el mismo servidor físico, con sus propios directorios para documentos de raíz. La cabecera Host es obligatoria en HTTP / 1.1 para seleccionar uno de los anfitriones.

Los siguientes encabezados pueden ser utilizados para la negociación del contenido por el cliente para pedir al servidor entregar el tipo preferido del documento (en términos del tipo de medio, por ejemplo, JPEG vs GIF, o el lenguaje usado por ejemplo Inglés vs francés) si el servidor mantiene múltiples versiones de un mismo documento.

**Accept: mime-type-1, mime-type-2, ...**- El cliente puede utilizar el encabezado Accept para indicar al servidor los tipos MIME que prefiere y puede manejar. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, una imagen en formato GIF y PNG, o un documento en formato TXT y PDF), se puede comprobar esta cabecera para decidir qué versión entregar al cliente. (Por ejemplo, PNG es más avanzado más GIF, pero no todas navegador soporta PNG.) Este proceso se denomina tipo de contenido de negociación .

**Accept-Language: language-1, language-2, ...**- El cliente puede utilizar el encabezado Accept-Language para indicar al servidor qué idiomas puede manejar o cuáles prefiere. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, en Inglés, chino, francés), se puede comprobar esta cabecera para decidir cuál es la versión que regresa. Este proceso se llama negociación de idioma .

**Accept-Charset: Charset-1, Charset-2, ...**- Para el conjunto de caracteres de negociación, el cliente puede utilizar esta cabecera para indicar al servidor qué conjuntos de caracteres puede manejar o cuáles prefiere. Ejemplos de conjuntos de caracteres ISO-8859-1, ISO-8859-2, ISO-8859-5, Big5, UCS2, UCS4, UTF8.

**Accept-Encoding: encoding-method-1, encoding-method-2, ...**- El cliente puede utilizar esta cabecera para indicar al servidor el tipo de codificación que soporta. Si el servidor ha codificado (o comprimido) la versión del documento solicitado, puede devolver una versión codificada soportada por el cliente. El servidor también puede elegir codificar el documento antes de devolverlo al cliente para reducir el tiempo de transmisión. El servidor debe establecer la cabecera de respuesta " Content-Encoding" para informar al cliente que se codificó el documento devuelto. Los métodos de codificación comunes son " x-gzip( .gz, .tgz)" y " x-compress( .Z)".

**Connection: Close|Keep-Alive**- El cliente puede utilizar esta cabecera para indicar al servidor la posibilidad de cerrar la conexión después de la solicitud, o para mantener la conexión activa durante otra solicitud. HTTP / 1.1 usa conexión persistente (keep-alive) de forma predeterminada. HTTP / 1.0 se cierra la conexión por defecto.

**Referer: referer-URL**- El cliente puede utilizar esta cabecera para indicar la referencia de esta solicitud. Si hace clic en un enlace para visitar la página web 2 desde la página web 1, la página web 1 es la referencia para la solicitud de la página web 2. Todos los navegadores más importantes establecen esta cabecera, que puede ser utilizada para hacer un seguimiento de la solicitud proveniente (por publicidad en la web o la personalización del contenido). No obstante, esta cabecera no es fiable y se puede suplantar fácilmente. Tenga en cuenta que Referencia está mal escrito como "Referer" (por desgracia, usted tiene que seguirla también).

**User-Agent: browser-type**- Identifica el tipo de navegador que se utiliza para realizar la solicitud. El servidor puede utilizar esta información para devolver un documento diferente dependiendo del tipo de navegador.

**Content-Length: number-of-bytes** - Utilizado por solicitud POST, para informar al servidor de la longitud del cuerpo de la petición.

**Content-Type: mime-type** - Utilizado por solicitud POST, para informar al servidor el tipo de medio del cuerpo de la petición.

**Cache-Control: no-cache|...**- El cliente puede utilizar esta cabecera para especificar cómo las páginas se van a almacenar en caché por el servidor proxy. " no-cache" Requiere proxy para obtener una nueva copia del servidor original, a pesar de que una copia en caché local este disponible. (HTTP / 1.0 servidor no reconoce " Cache-Control: no-cache". En su lugar, utiliza " Pragma: no-cache". Incluye dos cabeceras de la petición si no está seguro acerca de la versión del servidor.)

**Authorization**: Usado por el cliente para suministrar su credencial (usuario / contraseña) para tener acceso a los recursos protegidos. (Esta cabecera se describirá en el capítulo después de la autenticación.)

**Cookie: cookie-name-1=cookie-value-1, cookie-name-2=cookie-value-2, ...**- El cliente utiliza esta cabecera para devolver la cookie (s) de vuelta al servidor, que fue creada por este servidor antes de la administración del estado. (Esta cabecera se discutirá en el capítulo más adelante en la administración del estado.)

**If-Modified-Since: date** - Dice al servidor la página para enviar sólo si ha sido modificado después de la fecha específica.

GET Solicitud de Directorio
--
Supongamos que un directorio llamado " testdir" está presente en el directorio raíz de documentos " htdocs".

Si un cliente emite una solicitud GET a " /testdir/" (es decir, en el directorio).
1. El servidor devolverá " /testdir/index.html" si el directorio contiene un " index.htmlarchivo".
2. De lo contrario, el servidor devuelve el listado de directorios, si el listado de directorios está habilitado en la configuración del servidor.
3. De lo contrario, el servidor devuelve "404 Page Not Found".

Es interesante tomar nota de que si surge un problema del cliente en una solicitud GET " /testdir" (sin especificar la ruta del directorio "/"), el servidor devuelve un" 301 Move Permanently" con un nuevo "Location" del " /testdir/", de la siguiente manera.

```
GET / testdir HTTP / 1.1
Anfitrión: 127.0.0.1
(linea en blanco)
```

```
HTTP / 1.1 301 Movido permanentemente
Fecha: Sun 18 Oct 2009 13:19:15 GMT
Servidor: Apache / 2.2.14 (Win32)
Ubicación: http://127.0.0.1:8000/testdir/
Content-Length: 238
Content-Type: text / html; charset = iso-8859-1
   
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<Html> <head>
<Title> 301 Movido permanentemente </ title>
</ Head> <body>
<H1> trasladado de manera permanente </ h1>
<P> El documento se ha movido <a href="http://127.0.0.1:8000/testdir/"> aquí </a>. </ P>

</ Body> </ html>
```

La mayor parte del navegador seguirá con otra petición de " /testdir/". Por ejemplo, si emite http://127.0.0.1:8000/testdir sin el arrastre " /" desde un navegador, se puede notar que un arrastre " /" se añadió a la dirección después se le dio la respuesta. La moraleja de la historia es: usted debe incluir el " /" en una solicitud GET para la petición de directorio para un ahorro adicional.

Una petición GET a través de un servidor proxy
--

Para enviar una petición GET a través de un servidor proxy, (a) establecer una conexión TCP con el servidor proxy; (b) utilizar un URI de solicitud absoluto al servidor de destino. http://hostname:port/path/fileName.

El siguiente seguimiento fue capturado por medio de telnet. Se establece una conexión con el servidor proxy, y emitió una petición GET. Una solicitud absoluta URI se utiliza en la línea de petición.

```
GET http://www.amazon.com/index.html HTTP / 1.1
Anfitrión: www.amazon.com
Conexión: Cerrar
(linea en blanco)
```

```
HTTP / 1.1 302 Found
Transfer-Encoding: fragmentada
Fecha: Fri 27 Feb 2004 09:27:35 GMT
Content-Type: text / html; charset = iso-8859-1
Conexión: cerrar
Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
Set-Cookie: = piel; domain = .amazon.com; path = /; expira = Mie, 01-Ago-01 12:00:00 GMT
Conexión: cerrar
Ubicación: http://www.amazon.com:80/exec/obidos/subst/home/home.html
Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
   
ed
<! DOCTYPE HTML PUBLIC "- // IETF // DTD HTML 2.0 // EN">
<HTML> <HEAD>
<TITLE> 302 encontrados </ TITLE>
</ HEAD> <BODY>
<H1> Encontrados </ h1>
El documento se ha movido
<A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
</A> aquí. <P>
</ BODY> </ HTML>
   
0
```

Tome en cuenta que la respuesta se devuelve en "trozos".

**"HEAD" método de petición**
--
--------------------------------------------------------
La petición HEAD es similar a la petición GET. Sin embargo, el servidor devuelve sólo el encabezado de respuesta sin el cuerpo de la respuesta, que contiene el documento actual. La petición HEAD es útil para comprobar las cabeceras, tales como Last-Modified, Content-Type, Content-Length, antes de enviar una solicitud GET adecuada para recuperar el documento.

La sintaxis de la petición HEAD es la siguiente:

```
CABEZA URI de solicitud  HTTP-versión
 (otras cabeceras de solicitud opcionales)
(linea en blanco)
(Cuerpo de la petición opcional)
```

**Ejemplo**

```
CABEZA /index.html HTTP / 1.0
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Sun 18 Oct 2009 14:09:16 GMT
Servidor: Apache / 2.2.14 (Win32)
Última modificación: Sáb 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Conexión: cerrar
Content-Type: text / html
X-Pad: evitar el fallo del navegador
```

Observe que la respuesta consiste sólo en la cabecera sin el cuerpo, que contiene el documento real.

**"OPTIONS" método de petición**
--
-------------------------------------

Un cliente puede utilizar un método de petición OPTIONS para consultar al servidor en el que se apoyan los métodos de petición. La sintaxis de mensaje de solicitud de OPTIONS es:

```
OPTIONS request-URI|* HTTP-version
 (otros títulos opcionales)
(linea en blanco)
```

" *" Se puede utilizar en lugar de una solicitud-URI para indicar que la solicitud no se aplica a un recurso en particular.

**Ejemplo**

Por ejemplo, la siguiente petición OPTIONS se envía a través de un servidor proxy:

```
OPCIONES http://www.amazon.com/~~V~~plural~~3rd HTTP / 1.1
Anfitrión: www.amazon.com
Conexión: Cerrar
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Fri 27 Feb 2004 09:42:46 GMT
Content-Length: 0
Conexión: cerrar
Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
Permitir: GET, HEAD, POST, OPCIONES, TRACE
Conexión: cerrar
Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
(linea en blanco)
```

Todos los servidores que permiten la petición GET permitirán la petición HEAD. A veces, la cabeza no está en la lista.

**"TRACE" método de petición**
--
---------------------------------

Un cliente puede enviar una solicitud de rastreo pidiendo al servidor devolver un diagnóstico de rastreo.

La solicitud de rastreo toma la siguiente sintaxis:

```
TRACE / HTTP-versión
 (línea en blanco)
```
 
**Ejemplo**

El siguiente ejemplo muestra una petición TRACE emitida a través de un servidor proxy.

```
TRACE http://www.amazon.com/ HTTP / 1.1
Anfitrión: www.amazon.com
Conexión: Cerrar
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Transfer-Encoding: fragmentada
Fecha: Fri 27 Feb 2004 09:44:21 GMT
Content-Type: mensaje / http
Conexión: cerrar
Servidor: Fortaleza / 2.4.2 Apache / 1.3.6 C2NetEU / 2412 (Unix)
Conexión: cerrar
Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
   
9d
TRACE / HTTP / 1.1
Conexión: keep-alive
Anfitrión: www.amazon.com
Vía: 1.1 xproxy (NetCache NetApp / 5.3.1R4D5)
X-reenvía a: 155.69.185.59, 155.69.5.234
   
0
```

(Para comparar la solicitud de rastreo con el trazado de ruta)

**La presentación de los formularios HTML y datos de cadena de consulta**
--
-----------------------------------

En muchas aplicaciones de Internet, tales como el comercio electrónico y el motor de búsqueda, se requiere de los clientes presenten información adicional al servidor (por ejemplo, el nombre, la dirección, las palabras clave de búsqueda). Sobre la base de los datos presentados, el servidor toma una acción apropiada y produce una respuesta personalizada.

Los clientes suelen presentarse con una forma (producidos utilizando HTML <form>etiqueta). Una vez que se llenan los datos solicitados y pulsa el botón de enviar, el navegador empaqueta los datos del formulario y las somete al servidor, usando una petición GET o una solicitud POST.

La siguiente es una forma HTML de la muestra que se produce por la siguiente secuencia de comandos HTML:

```
<Html>
<Head> <title> Un formulario HTML de ejemplo </ title> </ head>
<Body>
  <H2 align = "left"> un formulario de entrada de datos de ejemplo HTML </ h2>
  <Form method = "get" action = "/ bin / proceso">
    Introduzca su nombre: <input type = "text" name = "nombre de usuario"> <br />
    Introduzca su contraseña: <input type = nombre de "contraseña" = "contraseña"> <br />
    ¿Cuál año?
    <Input type = "radio" nombre = valor "año" = "2" /> Año 1
    <Input type = "radio" nombre = valor "año" = "2" /> Año 2
    <Input type = "radio" nombre = valor "año" = "3" /> <br /> Año 3
    Asunto registrado:
    <Input type = "checkbox" name = "sujeto" value = "e101" /> E101
    <Input type = "checkbox" name = "sujeto" value = "E102" /> E102
    <Input type = "checkbox" name = "sujeto" value = "e103" /> <br /> E103
    Elija un día:
    <Select name = "día">
      <Option value = "mon"> Lunes </ option>
      <Option value = "casarse"> Miércoles </ option>
      <Option value = "fri"> Viernes </ option>
    </ Select> <br />
    <Filas de área de texto = "3" cols = "30"> Introduzca su petición especial aquí </ textarea> <br />
    <Input type = "submit" value = "ENVIAR" />
    <Input type = "reset" value = "CLEAR" />
    <Input type = "hidden" name = "acción" value = "registro" />
  </ Form>
</ Body>
</ Html>
```

![alt text][imagen10]

[imagen10]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_SampleForm.png "HTML Data"

Un formulario contiene campos. Los tipos de campo incluyen:

- Text box: producida por <input type="text">.
- Password box: producida por <input type="password">.
- Radio Button: producida por <input type="radio">.
- Checkbox: producida por <input type="checkbox">.
- Selection: producida por <select> y <option>.
- Text area: producida por <textarea>.
- Submit Button: producida por <input type="submit">.
- Reset Button: producida por <input type="reset">.
- Hidden Field: producida por <input type="hidden">.
- Button: producida por <input type="button">.

Cada campo tiene un nombre y puede tomar un determinado valor. Una vez que el cliente rellena los campos y pulsa el botón de enviar, el navegador recoge cada uno de los nombres y valores de los campos, ellos empaquetan en "name=valores pares", y concatena todos los campos juntos usando " &" como separador de campo. Esto se conoce como una cadena de consulta. Se enviará la cadena de consulta al servidor como parte de la solicitud.

*`nombre1 = valor1 y nombre2 = valor2 y nombre3 = valor3 y ...`*

Los caracteres especiales no están permitidos dentro de la cadena de consulta. Ellos deben ser reemplazados por un " %" seguido de código ASCII en hexadecimal. Por ejemplo, " ~" se sustituye por " %7E", " #" por " %23" y así sucesivamente. Debido a que el espacio blanco es bastante común, éste puede ser sustituido por cualquiera " %20" o " +" (el " +" carácter debe ser sustituido por " %2B"). Este proceso de sustitución se llama codificación URL , y el resultado es una cadena de consulta con codificación URL. Por ejemplo, supongamos que hay 3 campos dentro de un formulario, con el nombre / valor del "name = Peter Lee", "address = # 123 Happy Ave" y "language = C++", la cadena de consulta con codificación URL es:

*`name=Peter+Lee&address=%23123+Happy+Ave&Language=C%2B%2B`*

La cadena de consulta se puede enviar al servidor por medio de HTTP GET o el método de solicitud POST, que se especifica en el atributo <form>  "method".

```
<form method="get|post" action="url">
```

Si se utiliza el método GET, la cadena de consulta con codificación URL se añade detrás de la URI de solicitud después de un carácter "?", es decir,

```
GET request-URI?query-string HTTP-version
(otras cabeceras de petición opcional)
(linea en blanco)
(Cuerpo de la petición opcional)
```

Usar la solicitud GET para enviar la cadena de consulta tiene los siguientes inconvenientes:

- La cantidad de datos que se pueden agregar detrás de una solicitud URI es limitado. Si esta cantidad excede un umbral específico del servidor, el servidor devolverá un error "414 Request URI too Large".
- La cadena de consulta con codificación URL aparecería en el cuadro de dirección del navegador.

El método POST supera estos inconvenientes. Si se utiliza el método de solicitud POST, la cadena de consulta se enviará en el cuerpo del mensaje de solicitud, donde la cantidad no está limitada. Las cabeceras de petición Content-Typey Content-Length se utilizan para notificar al servidor el tipo y la longitud de la cadena de consulta. La cadena de consulta no aparecerá en el cuadro de dirección del navegador. El método POST se discutirá más adelante.

**Ejemplo**

El siguiente formulario HTML se utiliza para recopilar el nombre de usuario y contraseña en un menú de inicio de sesión.

```
<Html>
<Head> <title> Iniciar sesión </ title> </ head>
<Body>
  <H2> LOGIN </ h2>
  <Form method = "get" action = "/ bin / login">
    Nombre de usuario: <input type = "text" name = "usuario" size = "25" /> <br />
    Contraseña: <input type = nombre de "contraseña" = tamaño "PW" = "10" /> <br /> <br />
    <Input type = "hidden" name = "acción" value = "entrada" />
    <Input type = "submit" value = "ENVIAR" />
  </ Form>
</ Body>
</ Html>
```

![alt text][imagen11]

[imagen11]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_LoginForm.png "Login Form"

El método de la petición HTTP GET se utiliza para enviar la cadena de consulta. Supongamos que el usuario introduce "Peter Lee" como nombre de usuario, "123456" como contraseña; y pulsa el botón Enviar. La siguiente es la petición GET:

```
GET /bin/login?user=Peter+Lee&pw=123456&action=login HTTP/1.1
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 127.0.0.1:8000
Connection: Keep-Alive
```
 
Tenga en cuenta que aunque la contraseña que introduzca, no se muestra en la pantalla, se muestra claramente en el cuadro de dirección del navegador. Nunca se debe enviar la contraseña sin el cifrado adecuado.

```
http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login
```

URL y URI
--
--------

**URL (Uniform Resource Locator)**

Un URL que se define en el RFC 2396, se utiliza para identificar de forma exclusiva un recurso a través de Internet. El URL tiene la siguiente sintaxis:

``` protocol://hostname:port/path-and-file-name ```

Hay 4 partes en una dirección URL:

- 1.- Protocol: El protocolo de capa de aplicación utilizado por el cliente y el servidor, por ejemplo, HTTP, FTP y telnet.
- 2.- Hostname: El nombre de dominio DNS (por ejemplo, www.nowhere123.com) o la dirección IP (por ejemplo, 192.128.1.2) del servidor.
- 3.- Port: El número de puerto TCP que el servidor usa para escuchar peticiones entrantes de los clientes.
- 4.- Path-and-file-name: El nombre y la ubicación del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en el URL http://www.nowhere123.com/docs/index.html, el protocolo de comunicación es HTTP; el nombre de host es www.nowhere123.com. El número de puerto no se ha especificado en la URL, y adquiere el número predeterminado, que es el puerto TCP 80 para HTTP [STD 2]. La ruta y el nombre del archivo para el recurso que se encuentra es " /docs/index.html".

Otros ejemplos de URL son:

```
ftp://www.ftp.org/docs/test.txt
mailto:user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```

**URL codificado**

Un URL no puede contener caracteres especiales, como blanco o '~'. Los caracteres especiales se codifican, en forma de %xx, donde xx es código ASCII en hexadecimal. Por ejemplo, '~'se codifica como %7e; '+'se codifica como %2b. Un espacio en blanco puede ser codificado como %20o '+'. La dirección URL después de la codificación se llama URL codificada.

**URI (Uniform Resource Identifier)**

 El URI definido en RFC3986, es más general que el URL, que puede incluso localizar un fragmento dentro de un recurso. La sintaxis URI para el protocolo HTTP es:

``` http://host:port/path?request-parameters#nameAnchor ```

- Los parámetros de la petición, en forma de nombre = valores pares, se separan de la URL por un '?'. Los name=value pairs están separados por una '&'.
- Los #nameAnchor identifican un fragmento dentro del documento HTML, que se define a través de la etiqueta de anclaje .<a name="anchorName">...</a>.
- Reescritura de URL para la gestión de la sesión, por ejemplo, " ...;sessionID=xxxxxx".

"POST" método de petición
--
----------------------------

El método de solicitud POST se utiliza para datos adicionales "post" hasta el servidor (por ejemplo, la presentación de los datos del formulario HTML o la carga un archivo). La emisión de un URL HTTP desde el navegador siempre activa una solicitud GET. Para desencadenar una solicitud POST, se puede utilizar un formulario HTML con el atributo method="post"o escribir su propio programa de la red. Para la presentación de los formularios HTML, la solicitud POST es la misma que la solicitud GET, excepto que la cadena de consulta con codificación URL se envía en el cuerpo de la solicitud, en lugar de adjuntarse detrás de la *URI de solicitud*.

La solicitud POST toma la siguiente sintaxis:

```
POST request-URI HTTP-version
Content-Type: mime-type
Content-Length: number-of-bytes
(otras cabeceras de petición opcional)
  
(Cadena de consulta con codificación URL)
```

Las cabeceras de petición Content-Typey Content-Length son necesarias en la solicitud POST para informar al servidor el tipo y la longitud del cuerpo de la petición.

**Ejemplo: El envío de formularios de datos mediante el método de solicitud POST**

Se utiliza el mismo guión HTML como el anterior, pero se cambia el método de la petición POST.

```
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="post" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

Supongamos que el usuario introduce "Peter Lee" como nombre de usuario y "123456" como contraseña, y pulsa el botón de enviar, la siguiente petición POST sería generada por el navegador:

```
POST /bin/login HTTP/1.1
Host: 127.0.0.1:8000
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 37
Connection: Keep-Alive
Cache-Control: no-cache
   
User=Peter+Lee&pw=123456&action=login
```

Tenga en cuenta que la cabecera Content-Type informa al servidor los datos que se codifican en URL (con un tipo MIME especial application/x-www-form-urlencoded), y el encabezado Content-Length indica al servidor el número de bytes a leer desde el cuerpo del mensaje.

**POSTAL vs GET para la presentación de formularios de datos**

Como se mencionó en la sección anterior, la solicitud POST tiene las siguientes ventajas en comparación con la solicitud GET en el envío de una cadena de consulta:

- La cantidad de datos que pueden ser publicados es ilimitada, y cuando se mantengan en el cuerpo de la petición, generalmente se envía al servidor en un flujo de datos independiente.
- La cadena de consulta no se muestra en el cuadro de dirección del navegador.

Tenga en cuenta que aunque la contraseña no se muestra en el cuadro de dirección del navegador, se transmite al servidor en texto claro, y se somete a la red sniffing. Por lo tanto, el envío de la contraseña mediante una solicitud POST no es seguro.

Subir archivo usando la solicitud POST multipart/form-data 
--
-----

"RFC 1867 basado en la forma de cargar archivos en HTML" se especifica un archivo que se puede cargar en el servidor mediante una petición POST de un formulario HTML. Un nuevo atributo type="file" se añadió a la etiqueta <input> del código HTML <form> para soportar la carga de archivos. Los datos de la solicitud POST de carga de archivos no es una URL codificada (en la norma application/x-www-form-urlencoded), sino que utiliza un nuevo tipo MIME multipart/form-data.

**Ejemplo**

El siguiente formulario HTML puede ser utilizado para la carga de archivos:

```
<html>
<head><title>File Upload</title></head>
<body>
  <h2>Upload File</h2>
  <form method="post" enctype="multipart/form-data" action="servlet/UploadServlet">
    Who are you: <input type="text" name="username" /><br />
    Choose the file to upload:
    <input type="file" name="fileID" /><br />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

![alt text][imagen12]

[imagen12]: https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_FileUploadForm.png "File Upload Form"

Cuando el navegador encuentra una <input>etiqueta con el atributo type="file", se muestra un cuadro de texto y un botón "Examinar ...", para permitir al usuario elegir el archivo para ser cargado.

Cuando el usuario hace clic en el botón de enviar, el navegador envía los datos del formulario y el contenido del archivo (s) seleccionado. El anterior tipo de codificación " application/x-www-form-urlencoded" es ineficiente para el envío de datos binarios y caracteres que no son ASCII. En su lugar se utiliza un nuevo tipo de medio " multipart/form-data".

Cada parte identifica el nombre de entrada en el formulario HTML original, y el tipo de contenido si el medio es conocido, o de otra manera como application/octet-stream.

El nombre de archivo local original podría ser suministrado como un " filenameparámetro" o en el " Content-Disposition: form-data" de cabecera.

Un ejemplo del mensaje POST de carga de archivos es el siguiente:

```
POST /bin/upload HTTP/1.1
Host: test101
Accept: image/gif, image/jpeg, */*
Accept-Language: en-us
Content-Type: multipart/form-data; boundary=---------------------------7d41b838504d8
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 342
Connection: Keep-Alive
Cache-Control: no-cache
   
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="username" 
Peter Lee
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="fileID"; filename="C:\temp.html" Content-Type: text/plain 
<h1>Home page on main server</h1> 
-----------------------------7d41b838504d8--
```

Servlet 3.0 proporciona soporte integrado para la carga de archivos de procesamiento. Leer " Carga de archivos en Servlet 3.0 ".

"CONNECT" método de la petición
--
-------------------------------

La solicitud de conexión HTTP se utiliza para pedir un proxy para establecer una conexión con otro host y simplemente se retransmite el contenido, en lugar de intentar analizar o almacenar en caché el mensaje. Esto a menudo se utiliza para realizar una conexión a través de un proxy.
(En construcción)

Otros Métodos de petición
--
-------------------------

PUT: Pregunta el servidor para almacenar los datos.

DELETE: Pregunta el servidor para eliminar los datos.

Por consideraciones de seguridad, PUT y DELETE no son compatibles con la mayor parte del servidor de producción.

Los métodos de extensión (también códigos de error y cabeceras) se pueden definir para extender la funcionalidad del protocolo HTTP.

(En construcción)

Negociación de contenido
--
------------------------

Como se mencionó anteriormente, la negociación de contenido HTTP es apoyo entre el cliente y el servidor. Un cliente puede utilizar los encabezados de solicitudes adicionales (como Accept, Accept-Language, Accept-Charset, Accept-Encoding) para indicar al servidor el contenido que puede manejar o que se prefiere. Si el servidor posee varias versiones de un mismo documento en un formato diferente, devolverá el formato que el cliente prefiera. Este proceso se llama *negociación de contenido*.

Content-Type Negociación
--

El servidor utiliza un archivo de configuración MIME (llamado " conf\mime.types") para mapear la extensión de archivo a un tipo de soporte, de modo que se pueda determinar el tipo de medio del archivo mirando su extensión de archivo. Por ejemplo, las extensiones de archivo " .htm", " .html" están asociados con el tipo de medio MIME " text/html", la extensión de archivo " .jpg", " .jpeg" está asociada con " image/jpeg". Cuando un archivo se devuelve al cliente, el servidor tiene que poner un encabezado de resuesta Content-Type para informar al cliente el tipo de soporte de los datos.

Para la negociación de tipo de contenido, supongamos que las solicitudes de los clientes para una llamada de archivos es "logo", sin especificar su tipo, se envía una cabecera " Accept: image/gif, image/jpeg,...". Si el servidor tiene 2 formatos de " logo": " logo.gif" y " logo.jpg" el archivo de configuración MIME tiene las siguientes entradas:

```
image / gif gif
image / jpeg jpeg jpg jpe
```
El servidor devolverá " logo.gif" al cliente, basado en el cliente de cabecera Accept, y la asignación de tipo de archivo MIME /. El servidor incluirá un encabezado de respuesta " Content-type: image/gif".

A continuación se muestra la traza del mensaje:

```
GET / logotipo de HTTP / 1.1
Accept: image / gif, image / x-xbitmap, image / jpeg, imagen / pjpeg,
  application / x-shockwave-flash, application / vnd.ms-excel, 
  application / vnd.ms-powerpoint, la aplicación / pdf, * / *
Accept-Language: en-us
Accept-Encoding: gzip, desinfle
User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Anfitrión: test101: 8080
Conexión: Keep-Alive
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Dom 29 Feb 2004 01:42:22 GMT
Servidor: Apache / 1.3.29 (Win32)
Content-Location: logo.gif
Variar: negociar, aceptar
TCN: elección
Última modificación: Mie 21 Feb de 1996 19:45:52 GMT
ETag: "0-916-312b7670; 404142de"
Accept-Ranges: bytes
Content-Length: 2326
Keep-alive: timeout = 15, max = 100
Conexión: Keep-Alive
Content-Type: image / gif
(linea en blanco)
(Cuerpo omitida)
```

Sin embargo, si el servidor tiene 3 archivos "logo.": " logo.gif", "logo.html" y "logo.jpg". Se utilizó Accept: */*:

```
GET / logotipo de HTTP / 1.1
Aceptar: * / *
Accept-Language: en-us
Accept-Encoding: gzip, desinfle
User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Anfitrión: test101: 8080
Conexión: Keep-Alive
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Dom 29 Feb 2004 01:48:16 GMT
Servidor: Apache / 1.3.29 (Win32)
Content-Location: logo.html
Variar: negociar, aceptar
TCN: elección
Última modificación: Vie 20 Feb de 2004 04:31:17 GMT
ETag: "0-10-40358d95; 404144c1"
Accept-Ranges: bytes
Content-Length: 16
Keep-alive: timeout = 15, max = 100
Conexión: Keep-Alive
Content-Type: text / html
(linea en blanco)
(Cuerpo omitida)
```

```Acept: * / *```

Las siguientes directivas de configuración de Apache son relevantes para la negociación del tipo de contenido:

- La directiva TypeConfig se puede utilizar para especificar la ubicación del archivo de asignación MIME:

```TypeConfig conf / mime.types```

- La directiva AddType se puede utilizar para incluir la asignación de tipos MIME adicional en el archivo de configuración:

```AddType tipo MIME  extensión1 [ extensión2 ]```

- La directiva DefaultType da el tipo MIME de una extensión de archivo desconocido (en la Content-Typecabecera de la respuesta).

```texto DefaultType / plain```

Negociación de lenguaje y "Opciones MultiView"
--

La directiva "Options MultiView" es la forma más simple de implementar la negociación de idioma. Por ejemplo:

```
AddLanguage en .en
<Directorio "C: / _ JAVABIN / Apache1.3.29 / htdocs">
    Índices de opciones MultiView
</ Directory>
```

Supongamos que el cliente solicita para "index.html" y envía un "Accept-Language: en-us". Si el servidor tiene "test.html", "test.html.en" y "test.html.cn", se devolverá basado en la preferencia del cliente ", test.html.en". ( " en" Incluye " en-us".)

Una traza de mensaje es el siguiente:

```
GET /index.html HTTP / 1.1
Aceptar: * / *
Accept-Language: en-us
Accept-Encoding: gzip, desinfle
User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Anfitrión: test101: 8080
Conexión: Keep-Alive
(linea en blanco)
```

```
HTTP / 1.1 200 OK
Fecha: Dom 29 Feb 2004 02:08:29 GMT
Servidor: Apache / 1.3.29 (Win32)
Content-Location: index.html.en
Variar: negociar
TCN: elección
Última modificación: Dom 29 Feb 2004 02:07:45 GMT
ETag: "0-13-40414971; 40414964"
Accept-Ranges: bytes
Content-Length: 19
Keep-alive: timeout = 15, max = 100
Conexión: Keep-Alive
Content-Type: text / html
Content-Language: en
(linea en blanco)
(Cuerpo omitida)
```

El AddLanguage necesita una directiva para asociar un código de idioma con una extensión de archivo, similar a la asignación de archivo tipo MIME /.

Tenga en cuenta que la directiva "Options All" no incluye la opción " MultiViews". Es decir, hay que girar de forma explícita en MultiViews.

La directiva LanguagePriority se puede utilizar para especificar la preferencia del idioma en caso de empate durante la negociación de contenido o si el cliente no expresa una preferencia. Por ejemplo:

```
<IfModule mod_negotiation.c>
   LanguagePriority es da nl et fr el it ja KR no pl pt pt-br
</ IfModule>
```

Conjunto de caracteres de negociación
--

Un cliente puede utilizar el encabezado de la solicitud Accept-Charset para negociar con el servidor el conjunto de caracteres que prefiere.

```Accept-Charset: charset-1 , charset-2 , ...```

Los conjuntos de caracteres comúnmente encontrados incluyen: ISO-8859-1 (Latin-I), ISO-8859-2, ISO-8859-5, Big5 (chino tradicional), GB2312 (chino simplificado), UCS2 (2 bytes Unicode), UCS4 (4 bytes Unicode), UTF-8 (Unicode codificada), y etc.

Del mismo modo, la directiva AddCharset se utiliza para asociar la extensión de archivo con el conjunto de caracteres. Por ejemplo:

```
AddCharset ISO-8859-8 .iso8859-8
AddCharset ISO-2022-JP .jis
.big5 AddCharset Big5 .Big5
AddCharset de WINDOWS-1251 .cp-1251
AddCharset CP866 .cp866
AddCharset ISO-8859-5 Iso-ru
AddCharset KOI8-R .koi8-r
AddCharset UCS-2 .ucs2
AddCharset UCS-4 .ucs4
AddCharset UTF-8 .utf8
```

La negociación de codificación
--

Un cliente puede utilizar la cabecera Accept-Encoding para indicar al servidor el tipo de codificación que soporta. Los esquemas de codificación comunes son: " x-gzip (.gz, .tgz)" y " x-compress (.Z)".

```Accept-Encoding: Codificación-método-1 , que codifica-método-2 , ...```

Del mismo modo, la directiva AddEncoding se utiliza para asociar la extensión de archivo con el esquema de una codificación. Por ejemplo:

```
AddEncoding x-compress .Z
AddEncoding x-gzip .gz .tgz
```

Conexiones persistentes (keep-alive)
--
-------------------------------------

En HTTP / 1.0, el servidor cierra la conexión TCP después de entregar la respuesta por defecto ( Connection: Close). Es decir, cada uno de los servicios de conexión TCP sólo hacen una petición. Esto no es eficiente en páginas HTML que contienen hipervínculos (a través de < a href="url" > la etiqueta) y otros recursos (como imágenes, scripts - ya sea local o desde un servidor remoto). Si descarga una página que contiene 5 imágenes en línea, el navegador tiene que establecer una conexión TCP 6 veces en el mismo servidor.

El cliente puede negociar con el servidor y pedir al servidor no cerrar la conexión después de la entrega de la respuesta, de modo que otra petición pueda ser enviada a través de la misma conexión. Esto se conoce como conexión persistente (o conexión keep-alive). Las conexiones persistentes mejoran en gran medida la eficiencia de la red. Para HTTP / 1.0, la conexión por defecto no es persistente. Para solicitar una conexión persistente, el cliente debe incluir un encabezado de solicitud "Connection: Keep-alive" en el mensaje de petición de negociación con el servidor.

Para HTTP / 1.1, la conexión por defecto es persistente. El cliente no tiene que enviar la cabecera "Connection: Keep-alive". En su lugar, el cliente puede desear enviar el encabezado "Connection: Close" para pedir al servidor cerrar la conexión después de la entrega de la respuesta.

La conexión persistente es extremadamente útil para páginas web con muchas imágenes pequeñas en línea y otros datos asociados, ya que todos estos pueden ser descargados a través de la misma conexión. Los beneficios para la conexión persistente son:

- Ahorro de tiempo de CPU y de recursos en la apertura y cierre de conexión TCP en el cliente, proxy, puertas de enlace, y el servidor de origen.
- La solicitud se puede "pipeline". Es decir, un cliente puede hacer varias solicitudes sin esperar a cada respuesta, con el fin de utilizar la red de manera más eficiente.
- Una respuesta más rápida ya que ningún tiempo es necesario para realizar la conexión del protocolo de enlace de apertura TCP.

En servidor HTTP Apache, varias directivas de configuración están relacionadas con las conexiones persistentes:

La directiva KeepAlive decide si admite conexiones persistentes. Esto toma valor de encendido o apagado.

```KeepAlive On | Off```

La directiva MaxKeepAliveRequests establece el número máximo de solicitudes que se pueden enviar a través de una conexión persistente. Se puede establecer en 0 para permitir un número ilimitado de solicitudes. Se recomienda establecer en un número alto para un mejor rendimiento y eficiencia de la red.

```MaxKeepAliveRequests 200```

La directiva KeepAliveTimeOut establece el tiempo de espera en segundos para una conexión persistente que espera a la siguiente solicitud.

```KeepAliveTimeout 10```

Rango de descarga
--
--------------
Accept-Ranges: bytes

Transfer-Encoding: fragmentada

(En construcción)

Control de caché
--
---------------

El cliente puede enviar un encabezado de solicitud "Cache-control: no-cache" para indicar al proxy que se requiere obtener una nueva copia del servidor original, incluso una copia en caché local. Por desgracia, el servidor HTTP / 1.0 no entiende esta cabecera, pero utiliza un encabezado de la solicitud más antigua " Pragma: no-cache". Usted podría incluirla a la cabecera de su solicitud.

```
Pragma: no-cache
Cache-Control: no-cache
```

(Más en construcción)
 
REFERENCIAS Y RECURSOS
--

- Especificaciones HTTP W3C en http://www.w3.org/standards/techs/http.
- RFC 2616 "Protocolo de transferencia de hipertexto HTTP / 1.1" de 1999 @ http://www.ietf.org/rfc/rfc2616.txt .
- RFC 1945 "Protocolo de transferencia de hipertexto HTTP / 1.0", 1996 @ http://www.ietf.org/rfc/rfc1945.txt .
- ETS 2: "Assigned Numbers", de 1994.
- STD 5: "Protocolo de Internet (IP)" de 1981.
- STD 6: "User Datagram Protocol (UDP)", 1980.
- STD 7: "Protocolo de Control de Transmisión (TCP)", de 1983.
- RFC 2396: "Identificadores uniformes de recursos (URI): Sintaxis Genérica", de 1998.
- RFC 2045: "Multipurpose Internet Mail Extension (MIME) Parte 1: Formato de los mensajes de Internet cuerpos", de 1996.
- RFC 1867: "carga basado en el Formulario de HTML", 1995 (desfasadas por el RFC2854).
- RFC 2854: "El text / html tipo de medio", de 2000.
- Mutlipart servlet para la carga de archivos @ www.servlets.com


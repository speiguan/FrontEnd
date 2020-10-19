# FrontEnd  Tarea Métodos HTTPs

### Un HTTP request se compone de:

* **Método:** GET, POST, PUT, etc. Indica que tipo de request es.
* **Path:** la URL que se solicita, donde se encuentra el resource.
* **Protocolo:** contiene HTTP y su versión.

### Un HTTP response se compone de:

Una vez que el navegador envía el HTTP request, el servidor responde con un HTTP response, compuesto por:

* **Protocolo**: Contiene HTTP y su versión.
* **Status code**: El código de respuesta, por ejemplo: 200 OK, que significa que el GET request ha sido satisfactorio y el servidor devolverá los contenidos del documento solicitado. Otro ejemplo es 404 Not Found, el servidor no ha encontrado el resource solicitado.
* **Headers**: Contienen información sobre el software del servidor, cuando se modificó por última vez el resource solicitado, el mime type, etc. De nuevo la mayoría son opcionales.
* **Body:** Si el servidor devuelve información que no sean headers ésta va en el body.


## Método GET

_[GET](https://diego.com.es/metodos-http): El método [GET](https://diego.com.es/metodos-http) se emplea para leer una representación de un resource.  [GET](https://diego.com.es/metodos-http) devuelve la representación en un formato concreto: [HTML](https://www.significados.com/http/), XML, JSON o imágenes, JavaScript, CSS, etc._

**header GET ejemplo:** 
```
GET php.net HTTP/1.1 **Accept**: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
**Accept-Encoding**: gzip, deflate, sdch
**Accept-Language**: es-ES,es;q=0.8,en;q=0.6
**Cache-Control**: max-age=0
**Connection**: keep-alive
**Cookie**: COUNTRY=NA%2C122.16.430.651; LAST_LANG=es; LAST_NEWS=3847110839
**Host**: php.net
**If-Modified-Since**: Mon, 09 Nov 2015 11:50:11 GMT
**Upgrade-Insecure-Requests**: 1
**User-Agent**: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.80 Safari/537.36
```
## Método HEAD
_Es idéntido a [GET](https://diego.com.es/metodos-http), pero el servidor no devuelve el contenido en el [HTTP](https://www.significados.com/http/) response. Cuando se envía un [HEAD](https://diego.com.es/metodos-http) request, significa que sólo se está interesado en el código de respuesta y los headers [HTTP](https://www.significados.com/http/), no en el propio documento. Con este método el navegador puede comprobar si un documento se ha modificado, por razones de caching. Puede comprobar también directamente si el archivo existe._

**header HEAD ejemplo:** 
```

```

## POST

_Aunque se puedan enviar datos a través del método GET, en muchos casos se utiliza POST por las limitaciones de GET. En caso de respuesta positiva devuelve 201 (created). Los POST requests se envían normalmente con formularios._

```
<form action="formpost.php" method="post">
    Nombre: <input type="text" name="nombre"><br>
    Email: <input type="text" name="email"><br>
    <input type="submit" value="Enviar">
</form>
```

## PATCH

_El método [PATCH](https://sites.google.com/site/httpsprotocolo/versiones-de-http)  es utilizado para aplicar modificaciones parciales a un recurso._
```
PATCH /file.txt HTTP/1.1 
Host: www.example.com
Content-Type: application/example
If-Match: "e0023aa4e"
Content-Length: 100

[description of changes]
```

## PUT
_El modo [PUT](https://sites.google.com/site/httpsprotocolo/versiones-de-http) reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición. Sube, carga o realiza un upload de un recurso especificado (archivo), es el camino más eficiente para subir archivos a un servidor._
```
PUT /nuevo.html HTTP/1.1
Host: ejemplo.com
Content-type: text/html
Content-length: 16

<p>Nuevo Archivo</p>
```

## DELETE

_El método [DELETE](https://sites.google.com/site/httpsprotocolo/versiones-de-http) borra un recurso en específico._

###Ejemplo de petición HTTP DELETE enviando datos JSON en Golang
```
func main() {
	clienteHttp := &http.Client{}
	// Si quieres agregar parámetros a la URL simplemente haz una
	// concatenación :)
	url := "https://httpbin.org/delete"
	type Usuario struct {
		Nombre string
		Edad   int
	}
	usuario := Usuario{
		Nombre: "Luis",
		Edad:   22,
	}
	usuarioComoJson, err := json.Marshal(usuario)
	if err != nil {
		// Maneja el error de acuerdo a tu situación
		log.Fatalf("Error codificando usuario como JSON: %v", err)
	}

	peticion, err := http.NewRequest("DELETE", url, bytes.NewBuffer(usuarioComoJson))
	if err != nil {
		// Maneja el error de acuerdo a tu situación
		log.Fatalf("Error creando petición: %v", err)
	}
```
## OPTIONS

El método [OPTIONS](https://sites.google.com/site/httpsprotocolo/versiones-de-http) es utilizado para describir las opciones de comunicación para el recurso de destino.
Devuelve los métodos [HTTP](https://www.significados.com/http/) que el servidor soporta para un URL específico.Esto puede ser utilizado para comprobar la funcionalidad de un servidor web mediante petición en lugar de un recurso específico.
```
```

#Tipos de mensajes de las peticiones HTTPs 
* **100-199 (Respuestas informativas)**:


100 Continue: Esta respuesta provisional indica que todo hasta ahora está bien y que el cliente debe continuar con la solicitud o ignorarla si ya está terminada.
```
```

101 Switching Protocol:Este código se envía en respuesta a un encabezado de solicitud Upgrade por el cliente e indica que el servidor acepta el cambio de protocolo propuesto por el agente de usuario.

``` http://mirror.upb.edu.co/ubuntu bionic/universe amd64 libatinject-jsr330-api-java all 1.0+ds1-5 No se puede iniciar la conexión a mirror.upb.edu.co:80 (2801:190:0:a010:0:200:50c8:7b09). - connect (101: La red es inaccesible)```

102 Processing (WebDAV):Este código indica que el servidor ha recibido la solicitud y aún se encuentra procesandola, por lo que no hay respuesta disponible.
103 Early Hints: Este código de estado está pensado principalmente para ser usado con el encabezado Link, permitiendo que el agente de usuario empiece a pre-cargar recursos mientras el servidor prepara una respuesta. 


* **200-299(Respuestas satisfactorias)**:

200 OK: este código de estado es enviado en respuesta a una solicitud exitosa.

201 Createds: La petición ha sido completada y ha resultado en la creación de un nuevo recurso.

202 Accepted: La petición ha sido aceptada para procesamiento, pero este no ha sido completado. La petición eventualmente pudiere no ser satisfecha, ya que podría ser no permitida o prohibida cuando el procesamiento tenga lugar.

204 No Content: La petición se ha completado con éxito pero su respuesta no tiene ningún contenido (la respuesta puede incluir información en sus cabeceras HTTP).

206 Contenido Parcial: Si una aplicación solicita solo un rango del archivo solicitado, el código 206 es devuelto.


* **300-399(Redirecciones)**:

304 Not Modified: Indica que la petición a la URL no ha sido modificada desde que fue requerida por última vez. Típicamente, el cliente HTTP provee un encabezado como If-Modified-Since para indicar una fecha y hora contra la cual el servidor pueda comparar. 

305 Use Proxy (desde HTTP/1.1): Muchos clientes HTTP (como Mozilla3 e Internet Explorer) no se apegan al estándar al procesar respuestas con este código, principalmente por motivos de seguridad.

306 Switch Proxy:Este código se utilizaba en las versiones antiguas de HTTP pero ya no se usa (aunque está reservado para usos futuros).

307 Temporary Redirect (desde HTTP/1.1):Se trata de una redirección que debería haber sido hecha con otra URI, sin embargo aún puede ser procesada con la URI proporcionada. 

308 Permanent Redirect:  El recurso solicitado por el navegador se encuentra en otro lugar y este cambio es permanente. 

* **400-499(Errores de los clientes)**:

404 No Encontrado:Cuando la página solicitada o archivo no fue encontrado. 

401 No Autorizado: Páginas web protegidas por contraseña envían este código. 

403 Prohibido: Si no estás permitido para acceder a la página, este código puede ser enviado a tu navegador. 

* **500-599(Errores de los servidores)**:

500 Error de Servidor Interno:Este código es usualmente visto cuando un script web se rompe.

501 Not Implemented: El servidor no soporta alguna funcionalidad necesaria para responder a la solicitud del navegador (como por ejemplo el método utilizado para la petición).
​
502 Bad Gateway: El servidor está actuando de proxy o gateway y ha recibido una respuesta inválida del otro servidor, por lo que no puede responder adecuadamente a la petición del navegador.

503 Service Unavailable: El servidor no puede responder a la petición del navegador porque está congestionado o está realizando tareas de mantenimiento.

504 Gateway Timeout:El servidor está actuando de proxy o gateway y no ha recibido a tiempo una respuesta del otro servidor, por lo que no puede responder adecuadamente a la petición del navegador.

505 HTTP Version Not Supported: El servidor no soporta o no quiere soportar la versión del protocolo HTTP utilizada en la petición del navegador.
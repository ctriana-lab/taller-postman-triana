# taller-postman-Triana

##### Angie Camila Triana - Ingeniería de Software II

#### TAREA 1

#### Taller de APIs y Postman

###### Marco conceptual

###### ¿Qué es una API REST?

Una API REST es una interfaz que permite que diferentes aplicaciones se comuniquen entre sí mediante solicitudes HTTP. REST significa Transferencia de estado representacional y es un estilo de arquitectura que organiza la información en recursos.

Un recurso es un elemento o datos que una aplicación puede consultar o administrar, como un usuario, una publicación o un producto. Un endpoint es la dirección específica de una API a la que se envía una solicitud para acceder a un recurso.

Por ejemplo, una aplicación cotidiana que puede utilizar APIs es una aplicación de compras en línea, que puede comunicarse con otros servicios para consultar productos, procesar pagos o verificar información de envíos.

Fuente consultada: https://restfulapi.net/

## TAREA 2

### Métodos HTTP

los métodos HTTP indican que acción queremos realizar sobre un recurso de una API. se relacionan con las operaciones CRUD, que permiten crear, consultar, actualizar y eliminar información.

|Método HTTP|Operación CRUD|Qué hace?|
|-|-|-|
|GET|Read, Leer|Consulta información de un recurso sin modificarlo|
|POST|Create, Crear|Envía información para crear un recurso nuevo|
|PUT|Update, Actualizar|Reemplaza o actualiza la representación completa de un recurso, según el comportamiento de la API|
|PATCH|Update, Actualizar parcialmente|Modifica uno o varios campos específicos de un recurso|
|DELETE|Delete, Eliminar|Solicita eliminar un recurso|

Fuente consultada: https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Methods

## Tarea 3

### Código de estado HTTP

Son números que indican el resultado de una solicitud realizada a un servidor. se clasifican en cinco familias principales.

|Familia|Significado|Ejemplos|
|-|-|-|
|1xx|Respuestas informativas indicando que la solicitud continúa en proceso|100 Continue|
|2xx|Respuestas satisfactoria que indican que la solicitud fue recibida y procesada correctamente|200 OK, 201 Created, 204 No Content|
|3xx|Redirecciones que indican que se requieren acciones adicionales para completar la solicitud|301 Moved Permanently, 302 Found|
|4xx|Errores del cliente que indican que la solicitud presenta un problema|400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found|
|5xx|Errores del servidor que indican que el servidor no pudo completar una solicitud aparentemente válida|500 Internal Server Error, 503 Service Unavailable|

¿por qué se separan los errores 4xx de los 5xx?

Los errores 4xx generalmente indican un problema relacionado con la solicitud del cliente, como una dirección incorrecta, falta de autenticación o ausencia del recurso solicitado. Por ejemplo, el código 404 Not Found indica que el recurso solicitado no fue encontrado.

Los errores 5xx indican que el servidor encontró una dificultad al intentar procesar la solicitud. por ejemplo, 500 Internal Server Error señala un error interno del servidor.

¿Qué cambia entre unos y otros desde el punto de vista de quién tiene la culpa?

Por eso durante las pruebas con Postman, los códigos de estado permiten comprobar si la API responde de acuerdo con lo esperado. comprar el código esperado con el obtenido ayuda a identificar comportamientos incorrectos y documentar posibles hallazgos.

|Método|Recurso|Código HTTP esperado|Resultado esperado|Evidencia|
|-|-|-|-|-|
|GET|/posts/1|200 OK|Una publicación en formato JSON, con campos como userId, id, title y body.|evidencias/01-get-recurso.png|
|GET|/posts|200 OK|Una lista de publicaciones en formato JSON|evidencias/02-get-coleccion.png|
|GET|/posts/9999|404 Not Found|{} Una respuesta que indique que el recurso no fue encontrado.|evidencias/03-error-404.png|
|POST|/posts/|201 Created|Una respuesta que simula la creación de una publicación. En las ejecuciones realizadas se obtuvo el identificador 101.|evidencias/04-post-creacion.png|



## Prueba de creación con POST

Se ejecutó cinco veces consecutivas la petición POST a la dirección `https://jsonplaceholder.typicode.com/posts`, utilizando el mismo cuerpo JSON con los campos title, body y userId.

##### Resultados observados

En las ejecuciones realizadas se obtuvo la respuesta 201 Created y el identificador devuelto se mantuvo en 101.

###### 1\. ¿Qué observaste al ejecutar la petición cinco veces seguidas?

Observé que, al ejecutar varias veces la misma petición POST, la API respondió con el estado 201 Created y devolvió el mismo identificador, `101`. Esto indica que el servicio respondió de la misma manera en las pruebas realizadas.

###### 2\. ¿Por qué ocurre esto?

Ocurre porque JSONPlaceholder es una API de prueba que simula la creación de recursos. Las respuestas de las peticiones POST no se guardan de manera persistente, por lo que repetir la solicitud no significa que se estén creando publicaciones reales y permanentes en un servidor.

###### 3\. ¿Cómo comprobarías que un recurso realmente se creó en una API real?

Primero, enviaría la petición POST y guardaría el identificador devuelto por el servidor. Después, realizaría una petición GET utilizando ese identificador para verificar que el recurso existe y que sus datos coinciden con los enviados. También comprobaría que el recurso continúa disponible después de un tiempo o de una nueva sesión, según el funcionamiento de la API.

Evidencia

La captura de pantalla de esta prueba se encuentra en evidencias/04-post-creacion.png.



##### Instrucciones para reproducir las pruebas

Para ejecutar las pruebas de este taller se requiere tener instalado Postman y acceso a internet.

1\. Descargar o clonar el repositorio de GitHub.

2\. Abrir Postman.

3\. Importar el archivo `coleccion.json` desde la opción \*\*Import\*\*.

4\. Abrir la colección `Taller-API`.

5\. Seleccionar la solicitud que se desea ejecutar y verificar la URL, el método HTTP y, cuando corresponda, el cuerpo de la solicitud.

6\. Pulsar \*\*Send\*\* para ejecutar cada petición.

7\. Revisar el código de estado HTTP y el contenido de la respuesta.

8\. Para consultar los resultados de las pruebas automáticas, abrir la solicitud GET `/posts/1` y revisar la sección \*\*Test Results\*\*.

Las solicitudes se ejecutan contra JSONPlaceholder, un servicio de prueba disponible en `https://jsonplaceholder.typicode.com`. Las operaciones de escritura son simuladas y sus respuestas no garantizan que los cambios se almacenen permanentemente.



###### Archivos del repositorio

\- `README.md`: marco conceptual, métodos HTTP, códigos de estado e instrucciones para reproducir las pruebas.

\- `hallazgos.md`: resultados y análisis de las solicitudes realizadas, comparación entre PUT y PATCH, prueba de límites y exploración de otros recursos.

\- `conclusiones.md`: análisis de idempotencia, cabeceras HTTP y conclusiones generales del taller.

\- `coleccion.json`: colección exportada de Postman en formato Collection v2.1.

\- `evidencias/`: capturas de pantalla de las solicitudes y de las pruebas automáticas.


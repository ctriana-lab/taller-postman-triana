# taller-postman-Triana

##### Angie Camila Triana - Ingeniería de Software II

## TAREA 1

### Taller de APIs y Postman

###### Marco conceptual

###### ¿Qué es una API REST?

Una API REST es una interfaz que permite que diferentes aplicaciones se comuniquen entre si mediante solicitudes HTTP. REST significa Transferencia de estado representacional y es un estilo de arquitectura que organiza la información en recursos.

Un recurso es un elemento o datos que una aplicación puede consultar o administrar, como un usuario, una publicaciones o un producto. Un endpoint es la dirección especifica de una API a la que se envía una solicitud para acceder a un recurso.

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
|GET|/posts/1|200 OK|Una publicación en formato JSON, con campos como userId, id, title y body.|evidencia\_01\_get\_posts\_1.png|
|GET|/posts|200 OK|Una lista de publicaciones en formato JSON|evidencia\_02\_get\_posts.png|
|GET|/posts/9999|404 Not Found|{}|evidencia\_03\_get\_posts\_9999.png|
||||||
||||||




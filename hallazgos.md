#### Hallazgos de las pruebas de API Tarea 4

##### 1\. Pruebas de creación con POST

Se realizaron varias solicitudes consecutivas con el método POST al endpoint `https://jsonplaceholder.typicode.com/posts`, enviando un título, un cuerpo de texto y el identificador del usuario.

En las ejecuciones realizadas, la API respondió con el estado \*\*201 Created\*\* y devolvió el identificador `101` en todas las respuestas observadas.

###### Observación

Aunque se enviaron varias solicitudes consecutivas, el estado HTTP y el identificador devuelto permanecieron iguales: `201 Created` e ID `101`.

###### ¿Por qué ocurre?

JSONPlaceholder es una API de prueba que simula operaciones de creación. La respuesta permite comprobar cómo se comporta una solicitud POST, pero no demuestra que el recurso se haya guardado permanentemente en una base de datos.

###### ¿Cómo verificar la creación en una API real?

Se puede consultar el recurso mediante una solicitud GET utilizando el identificador devuelto por POST y comparar los datos recibidos con los enviados. También se debe comprobar si el recurso continúa disponible en consultas posteriores, según el funcionamiento de la API real.

###### Evidencia

La captura de pantalla de esta prueba se encuentra en evidencias/04-post-creacion.png.



#### Tarea 5 y 6

##### Comparación entre PUT y PATCH

Se realizaron pruebas con los métodos PUT y PATCH sobre el endpoint `https://jsonplaceholder.typicode.com/posts/1`.

###### Prueba con PUT

Se envió una solicitud PUT con los campos `id`, `title`, `body` y `userId`. La API respondió con el estado \*\*200 OK\*\* y devolvió los campos enviados, incluyendo el título y el cuerpo del texto actualizados.

###### Prueba con PATCH

Se envió una solicitud PATCH con únicamente el campo `title`. La API respondió con el estado \*\*200 OK\*\*. La respuesta mostró el nuevo título, pero también devolvió el `body` original de la publicación.

###### Análisis de los resultados

PUT se utilizó enviando el objeto completo, mientras que PATCH se utilizó enviando solamente el campo que se quería modificar. En esta prueba, ambos métodos devolvieron el estado 200 OK. Sin embargo, las respuestas de JSONPlaceholder no demuestran que las modificaciones se hayan guardado de manera permanente.

La diferencia principal es que PUT se emplea normalmente para reemplazar la representación de un recurso, mientras que PATCH se utiliza para aplicar modificaciones parciales.

###### Conclusión

Los resultados permiten observar la diferencia entre enviar un objeto completo y enviar únicamente el campo que se desea cambiar. Para comprobar la persistencia de las modificaciones en una API real, sería necesario consultar nuevamente el recurso y verificar sus datos.



#### 7 Prueba de eliminación con DELETE

Se realizó una solicitud con el método DELETE al endpoint `https://jsonplaceholder.typicode.com/posts/1`.

###### Resultado obtenido

La API respondió con el código de estado \*\*200 OK\*\*, lo que indica que la solicitud fue procesada correctamente. En esta prueba, el resultado observado fue el código de estado 200 OK.

###### Análisis

El método DELETE se utiliza para solicitar la eliminación de un recurso. Sin embargo, JSONPlaceholder es una API de prueba que simula operaciones, por lo que recibir una respuesta satisfactoria no garantiza que el recurso haya sido eliminado permanentemente.

###### Conclusión

La prueba permitió comprobar que la API acepta la solicitud DELETE y responde con un estado satisfactorio. En una API real, sería necesario realizar una consulta posterior para verificar si el recurso dejó de estar disponible.



#### Prueba de límites de los identificadores Fase 3 tarea 10

Se realizaron solicitudes GET para comprobar el límite de los identificadores de las publicaciones disponibles en JSONPlaceholder.

###### Resultados obtenidos

| Solicitud | Código de estado | Resultado |

|---|---|---|

| GET `/posts/100` | 200 OK | Se recibió la publicación con ID 100. |

| GET `/posts/101` | 404 Not Found | No se encontró la publicación solicitada. |

| GET `/posts/9999` | 404 Not Found | No se encontró la publicación solicitada. |

###### Análisis

El identificador 100 fue el último que se comprobó con una respuesta satisfactoria, mientras que el identificador 101 fue el primero que se comprobó con una respuesta 404 Not Found. Por tanto, se identificó el límite entre ambos resultados para las solicitudes realizadas.

###### ¿Qué tipo de prueba es?

Es una prueba de límites, porque se verifican valores cercanos al límite de los recursos disponibles. Estas pruebas ayudan a detectar errores que pueden presentarse cuando un sistema procesa identificadores, cantidades o rangos.

###### ¿Por qué pueden aparecer defectos en los límites?

Los errores pueden ocurrir cuando se utilizan condiciones incorrectas para determinar si un valor está dentro o fuera de un rango. Por eso es importante probar el último valor válido y el primer valor no válido.



#### Exploración de otros recursos de la API

Para conocer otros recursos disponibles en JSONPlaceholder, se realizaron dos solicitudes GET adicionales.

###### Consulta de usuarios

\- Endpoint: `https://jsonplaceholder.typicode.com/users`

\- Método HTTP: GET

\- Código de estado obtenido: 200 OK

\- Hallazgo: la API respondió satisfactoriamente a la solicitud de usuarios.

Esta consulta permite explorar el recurso `users`, independiente del recurso `posts` utilizado en las primeras pruebas.

###### Consulta de comentarios de una publicación

\- Endpoint: `https://jsonplaceholder.typicode.com/posts/1/comments`

\- Método HTTP: GET

\- Código de estado obtenido: 200 OK

\- Hallazgo: la API respondió satisfactoriamente a la solicitud de comentarios de la publicación con identificador 1.

###### ¿Cómo se puede inferir la estructura de las URL?

La estructura `/posts/1/comments` permite interpretar que se solicitan los comentarios relacionados con la publicación identificada con el número 1. Por su parte, `/users` permite consultar el recurso de usuarios.

###### Conclusión

La exploración permitió comprobar que JSONPlaceholder ofrece diferentes recursos y rutas relacionadas. Las respuestas 200 OK indican que las solicitudes se procesaron satisfactoriamente, aunque por sí solas no demuestran la persistencia de los datos.



##### Fase 4. Tarea 12 y 13: Pruebas automáticas en Postman

Se configuraron cuatro pruebas automáticas en la solicitud GET `https://jsonplaceholder.typicode.com/posts/1`, utilizando la sección \*\*Scripts → Post-response\*\* de Postman.



###### Código de las pruebas automáticas

```javascript

pm.test("El estado es 200", function () {

&#x20;   pm.response.to.have.status(200);

});



pm.test("La respuesta tiene formato JSON", function () {

&#x20;   pm.response.to.be.json;

});



pm.test("La publicación tiene el ID 1", function () {

&#x20;   const datos = pm.response.json();

&#x20;   pm.expect(datos.id).to.eql(1);

});



pm.test("La publicación contiene un título", function () {

&#x20;   const datos = pm.response.json();

&#x20;   pm.expect(datos.title).to.be.a("string").and.not.empty;

});

```

###### ¿Qué verifica cada prueba?

1\. El estado es 200: comprueba que la solicitud responda con el código HTTP 200 OK.

2\. La respuesta tiene formato JSON: verifica que la respuesta tenga formato JSON.

3\. La publicación tiene el ID 1: comprueba que el identificador recibido sea exactamente 1.

4\. La publicación contiene un título:\*\* verifica que el campo `title` sea una cadena de texto y que no esté vacío.



###### Resultados obtenidos

Al ejecutar la solicitud GET `/posts/1` con el código esperado, las cuatro pruebas finalizaron satisfactoriamente (\*\*PASS\*\*). Esto permitió comprobar automáticamente el estado de la respuesta, su formato y dos características de los datos recibidos.

Posteriormente, se modificó temporalmente la primera prueba para esperar el código 201 en lugar de 200. Como la respuesta real fue 200 OK, esa prueba falló (\*\*FAIL\*\*), mientras que las otras tres continuaron aprobadas. Después, se restauró el código esperado a 200 y las cuatro pruebas volvieron a aprobarse.

###### 

###### Importancia de las pruebas automáticas

Las pruebas automáticas permiten verificar de forma repetible si una respuesta cumple las condiciones definidas. Un resultado \*\*FAIL\*\* ayuda a identificar una diferencia entre el resultado esperado y el obtenido. Sin embargo, un fallo también puede deberse a una condición de prueba incorrecta, por lo que es necesario revisar el código y la respuesta antes de concluir que existe un defecto en la API.



###### Evidencias

\- `evidencias/05-test-automatico.png`: muestra las cuatro pruebas aprobadas.

\- `evidencias/06-test-fallido.png`: muestra la prueba del estado fallida al esperar 201, mientras las otras tres permanecieron aprobadas.


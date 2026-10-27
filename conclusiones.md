### Conclusiones del taller de investigación: APIs y pruebas con Postman



#### 1\. Idempotencia de los métodos HTTP

La idempotencia es una propiedad según la cual realizar varias veces una misma solicitud produce el mismo efecto previsto sobre el estado del recurso que realizarla una sola vez.

De los cinco métodos estudiados, GET, PUT y DELETE son idempotentes según su semántica HTTP. POST no es idempotente por defecto y PATCH puede ser idempotente o no, dependiendo de la operación de modificación definida.

En las pruebas realizadas con JSONPlaceholder, PUT devolvió el estado 200 OK y los campos enviados. PATCH también devolvió 200 OK, pero mostró el título modificado junto con el cuerpo original de la publicación. DELETE respondió 200 OK.

Es importante distinguir entre el resultado de las solicitudes y el efecto que producen sobre el recurso. La idempotencia significa que repetir una misma solicitud tiene el mismo efecto previsto que ejecutarla una sola vez, aunque las respuestas HTTP puedan variar. En JSONPlaceholder, las respuestas observadas no demuestran que los cambios se hayan guardado permanentemente.

##### 2\. Pruebas repetidas con PUT y POST

Al repetir solicitudes POST para crear una publicación, se observó que las respuestas devolvían el estado 201 Created y el identificador 101 en las ejecuciones realizadas.

Este comportamiento es consistente con la simulación de JSONPlaceholder, que permite probar solicitudes sin garantizar la persistencia permanente de los recursos creados.

En una API real, se puede verificar una creación mediante una solicitud GET al identificador devuelto por POST, comparando los campos recibidos con los datos enviados y comprobando su disponibilidad posterior.

En el caso de PUT, se envió varias veces la solicitud de actualización con el mismo contenido. La respuesta observada fue 200 OK con los campos enviados. Para evaluar la idempotencia, es importante comparar el efecto de repetir la solicitud, no solamente el código de estado.



##### 3\. Cabeceras de respuesta HTTP

Al consultar la publicación con el endpoint `GET /posts/1`, se revisaron las cabeceras de respuesta en Postman. Entre las cabeceras observadas se encuentran las siguientes:



* Content-Type: su valor fue `application/json; charset=utf-8`. Indica que la respuesta contiene datos en formato JSON y utiliza la codificación UTF-8. Es importante porque permite interpretar correctamente la información recibida.
* Cache-Control: su valor fue `max-age=43200`. Esta directiva establece un tiempo máximo de 43.200 segundos (12 horas) para considerar válida una respuesta almacenada en caché, sujeto a las demás reglas aplicables.
* Pragma: su valor fue `no-cache`. Es una directiva relacionada con el comportamiento de la caché y se conserva principalmente por compatibilidad con sistemas HTTP antiguos.



También se observó la cabecera `X-Content-Type-Options`, con el valor `nosniff`, que contribuye a evitar la interpretación del contenido como un tipo diferente del declarado.

La revisión de las cabeceras permite comprender que una respuesta HTTP no contiene únicamente el cuerpo de los datos y el código de estado, sino también información sobre el formato, la caché y otros aspectos del intercambio.



##### 4\. Importancia de las pruebas de límites

Las pruebas de límites permiten comprobar el comportamiento de una API cerca de los valores extremos de un rango. En este taller, la consulta a `/posts/100` respondió 200 OK, mientras que `/posts/101` y `/posts/9999` respondieron 404 Not Found.

Estos resultados permiten identificar el límite observado entre las publicaciones disponibles y los identificadores que no se encontraron. Probar valores cercanos a ese límite ayuda a detectar errores en las condiciones de validación y en el manejo de rangos.



##### 5\. Importancia de las pruebas automáticas

Se configuraron cuatro pruebas automáticas para la solicitud GET `/posts/1`:

1\. Verificar que el estado HTTP sea 200.

2\. Comprobar que la respuesta tenga formato JSON.

3\. Validar que el identificador de la publicación sea 1.

4\. Comprobar que la publicación contenga un título de texto no vacío.

Las cuatro pruebas terminaron aprobadas. Además, se cambió temporalmente el estado esperado de 200 a 201 para provocar un fallo controlado. Postman detectó la diferencia entre el estado esperado y el recibido, demostrando la utilidad de las pruebas automáticas para identificar discrepancias.

La evidencia `evidencias/05-test-automatico.png` muestra las cuatro pruebas aprobadas, mientras que `evidencias/06-test-fallido.png` registra el fallo controlado de la primera prueba al esperar el código 201 en lugar del 200 recibido. Después de restaurar el estado esperado a 200, las cuatro pruebas volvieron a aprobarse.



##### 6\. ¿Qué se necesita para elaborar un plan de pruebas formal?

La tabla de solicitudes y resultados constituye un conjunto de casos de prueba, pero un plan de pruebas formal necesita más elementos: objetivos, alcance, requisitos, riesgos, recursos, responsables, ambiente de pruebas, datos de entrada, criterios de entrada y salida, resultados esperados, criterios de aceptación y un procedimiento para registrar y dar seguimiento a los defectos encontrados.



##### 7\. ¿Por qué un 404 puede ser una buena noticia y un 200 puede ser un defecto?

Un código 404 puede ser un resultado correcto cuando se solicita intencionalmente un recurso inexistente, porque demuestra que la API identifica que no lo encuentra. En cambio, un 200 OK puede representar un defecto si la prueba esperaba un rechazo o si la respuesta no cumple los requisitos funcionales. Por eso, los códigos de estado deben evaluarse de acuerdo con el resultado esperado para cada caso de prueba.



##### Conclusión general

El desarrollo del taller permitió practicar solicitudes HTTP con Postman, interpretar códigos de estado, comparar métodos de actualización, explorar diferentes recursos y construir pruebas automáticas. También permitió reconocer la importancia de documentar los resultados reales y de distinguir entre una respuesta satisfactoria y la persistencia efectiva de los datos.


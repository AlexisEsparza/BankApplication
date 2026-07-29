# BankApplication
BankApplication project with 2 microservices for store and retrieve information about clients, accounts and transactions.

# Consideraciones importantes

### Error en extensión EchoAPI
No fue posible utilizar la extensión EchoAPI para generar la colección de postman como se indica en las instrucciones debido al siguiente error:

![Error al abrir EchoAPI](<Error EchoAPI.png>)

### Error al ejecutar pruebas con submit
Se presentan múltiples errores en las pruebas que ejecutan obtener por id, actualización y eliminación de las entidades debido a que se esperaba un error 404, pero el resultado fue un código 200.


![Error obtener por id](<Obtener por id.png>)
![Error actualizar cuenta parcial](<Actualizar cuenta parcial.png>)

Los métodos y las consultas a la base sí contemplan correctamente los casos en los que una entidad no exista antes de ejecutar una consulta por id, actualización o eliminación de la entidad. Adicionalmente, también se tiene implementado una clase GlobalExceptionHandler que captura las excepciones generadas cuando no se encuentra el registro solicitado y construye el objeto de respuesta con el código 404 correspondiente. Sin embargo, la prueba unitaria falla de igual manera.

![Método para obtener registro por id](<Método obtener registro por id.png>)
![GlobalExceptionHandler](<Exception handler.png>)

Esto podría estar relacionado a que las pruebas unitarias crean registros antes de ejecutar las pruebas para validar obtenciones, actualizaciones o eliminaciones de registros que no existen y por lo tanto los id's sí terminan existiendo al momento de ejecutar, pero es debido a que estos registros son creados por pruebas ejecutadas en un orden distinto al esperado.
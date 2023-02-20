# Protobuffers y gRPC

Ayudan a crear MS los cuales tienen que cumplir con un alto rendimiento. Aplicaremos métodos de gRPC.

# Protobuffers

**¿Que son?**

Protocol buffers, son una forma de serializar datos y definir estructuras de datos. La estructura tiene que tener un
identificador único que va a permitir la serialización de manera correcta.

**Ventajas:**

* Serializa <-> deserializa y la estructura lo permite hacer de una manera más rápida.
* Se pueden importar las serializaciones. Por ejemplo: `student.proto` a otro archivo por ejemplo: `test.proto`
* Existe compilación a través de `protoc`.

[Página de referencia.](https://developers.google.com/protocol-buffers/docs/reference/go-generated?hl=es-419)

## Comando de protobuffer

```
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative proto/student.proto
```

## Servicios

* Los proto buffer permiten definir servicios
* gRPC simplifica el tiempo de comunicación entre diferentes microservicios

## RPC (Remote Procedure Call)

* Protocolo en el cual siempre tenemos un cliente y un servidor. Este cliente siempre le dice que tiene una rutina al
  servidor para obtener una respuesta.
* Permite mantener una comunicación entre el cliente y el servidor y la invoca como si fuese desde el cliente.
* Oculta la implementación en el backend de la petición que hizo un cliente, aunque el cliente sepa como hacer la
  petición y pueda invocarla como si fuese suya.

## gRPC (por google)

* Decidieron utilizar HTTP2 y ProtoBuffers como método de intercambio de datos.
* Framework creado por Google para trabajar RPC con más eficiencia y alto rendimiento.
* El transporte de datos funciona con HTTP2.
* Permite crear multiplexación a la hora de enviar mensajes: más mensajes en la conexión TCP de manera simultánea.
* Permite serializar datos.
* Usa los ProtoBuffers como estructura para intercambio de datos.
* Permite serializar y deserializar datos más rápido.
* Métodos de gRPC
    * Unary: similar a como funciona REST. Envía una petición al servidor, y el servidor la responde.
    * Streaming: permite constante envío de data en un canal.
        * Del lado del cliente: el cliente envía muchas peticiones, y el servidor responde una sola vez.
        * Del lado del servidor: el cliente realiza una sola petición, y el servidor responde enviando la data en
          partes.
        * Bidireccional: cliente y servidor deciden ambos comunicarse por streaming de data.

## ProtoBuffers vs. JSON
La serialización y deserialización de ambos formatos siempre ocurre. Los ProtoBuffers tienen mucha menor latencia que los JSON al hacerlo.

### JSON: formato de mensajes eficiente para JavaScript.
* Pares de llave y valor.
* Es más fácil de leer al ojo humano.
* Es costoso en rendimiento si se quiere trabajar con otro lenguaje distinto de JavaScript.

### Protobuffers: formato de mensaje agnóstico a cualquier lenguaje de programación.
* Un compilador se encarga de convertir la sintaxis de ProtoBuffer al lenguaje correspondiente.
Esta compilación solo ocurre en tiempo de creación o modificación, no en tiempo de ejecución.
Se puede llamar archivos `.proto` desde otros archivos `.proto`.

 ### ¿Cuándo usar?
* JSON: cuando la aplicación requiere que la data sea más flexible.
* ProtoBuffers: Cuando la aplicación necesita correr muy rápido; cuando los procesos de serialización y deserialización deben ocurrir rápido.

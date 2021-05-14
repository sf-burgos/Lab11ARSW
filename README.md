### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/en-us/free/search/?&ef_id=Cj0KCQiA2ITuBRDkARIsAMK9Q7MuvuTqIfK15LWfaM7bLL_QsBbC5XhJJezUbcfx-qAnfPjH568chTMaAkAsEALw_wcB:G:s&OCID=AID2000068_SEM_alOkB9ZE&MarinID=alOkB9ZE_368060503322_%2Bazure_b_c__79187603991_kwd-23159435208&lnkd=Google_Azure_Brand&dclid=CjgKEAiA2ITuBRDchty8lqPlzS4SJAC3x4k1mAxU7XNhWdOSESfffUnMNjLWcAIuikQnj3C4U8xRG_D_BwE). Al hacerlo usted contará con $200 USD para gastar durante 1 mes.

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?

Azure Function es una solución para ejecutar fácilmente pequeños fragmentos de código o “funciones” en la nube. Toma los conceptos básicos de los ya conocidos WebJobs y los amplía de forma interesante, Azure Function nos presenta una multitud de nuevos triggers para poder ejecutarlo. Entre todos estos triggers podemos encontrar: Cosmos DB, Event Hub y WebHooks.

Entre las características más importantes que podemos encontrar en Azure Function se encuentran:

Codificar en distintos lenguajes de programación: C#, F#, JavaScript…
Pagar solo el tiempo en el que el Azure Function este en ejecución.
Admite tanto Nuget como NPM.
Permite codificar tanto en el portal de Azure como en nuestra aplicación y luego integrarla configurando la integración continua en Azure.


* ¿Qué es serverless?

RTA: Serverless es un tipo de arquitectura donde los servidores (físicos o en la nube) dejan de existir para el desarrollador y en cambio el código corre en “ambientes de ejecución” que administran proveedores como Amazon, Google, IBM, etc. Cuando su función es invocada, ya sea por un request HTTP u otro evento, el ambiente de ejecución es iniciado, el código se ejecuta e inmediatamente el ambiente desaparece. Si la función es invocada mil veces, el proveedor se encarga de escalar y generar el número de ambientes necesarios para responder a las mil invocaciones.

* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?

RTA: Runtime es el intervalo de tiempo en el que un programa de computadora se ejecuta en un sistema operativo. Este tiempo se inicia con la puesta en memoria principal del programa, por lo que el sistema operativo comienza a ejecutar sus instrucciones, al seleccionarlo al crear el function app basicamente se va a decidir el tiempo en el que se va a ejecutar un programa dependiendo del entorno elegido (.NET core, python, java, etc).

* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?

RTA: Azure Storage account nos proporciona un espacio de nombres unico para el almacenamiento lo cual es necesario para operaciones de almacenamiento y administración como son Manejo de triggers y logs.

* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.

Son 3 tipos de planes.

Plan de consumo: Tiene 2 ventajas muy grandes y son que escala horizontalmente de manera automatica y por otro lado solo se pga por los servicios utilizados

Plan Premium: Algunas de sus ventajas son aplicaciones de funciones, Conectividad de red virtual, Tamaños de la instancia Prémium , Asignación de aplicaciones de alta densidad para planes con varias, Duración de la ejecución ilimitada.

Plan de Servicio de Aplicaciones: Algunas de sus ventajas son que puede tener timeouts ilimitados, memoría por instancia de 1.7 GB y una capacidad de almacenamiento hasta de 1000 GB y el numero de instancias es máximo 20.




* ¿Por qué la memoization falla o no funciona de forma correcta?

RTA: La memorización falla ya que para realizar el calculo de numeros muy grandes ya que el stack de memoria se llena y la capacidad por instancia es de 1.5GB, se necesitan peticiones de numeros más pequeños hasta lograr calcular el numero grande.

* ¿Cómo funciona el sistema de facturación de las Function App?

RTA: Azure Functions se factura según el consumo de recursos y las ejecuciones por segundo, tambien se tiene en cuenta el consumo de recursos, la duración de uso de VCPU y la duración de uso de la memoria.

* Informe

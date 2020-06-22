# Service Factory 

## Пользовательские сервисы, предоставляемые Scalecube узлом

Основное назначение любого Scalecube узла заключается в выполнении некоторой логики. 
За реализацию этой логики выступают Scalecube сервисы – объекты, которые реактивно обрабатывают поступающие данные и соответствуют определенным требованиям. 

### Ограничения 

Требования к Scalecube сервисам:
- Реализовывать интерфейс, который:
	- помечен аннотацией `io.scalecube.services.annotations.Service` 
	- имеет хотя бы один метод, который:
		- помечен аннотацией `io.scalecube.services.annotations.ServiceMethod`	
		- имеет 0...1 аргументов
		- соответствует одному из способу коммуникации

Коммуникационные способы:
- `Request Channel` – на поток событий получаем ответный поток событий.

	__Тип аргумента__:  `org.reactivestreams.Publisher<T>`, где тип `T`:
	- должен быть сериализуем через 
	указанный `io.scalecube.services.transport.api.DataCodec`
	- являться `ServiceMessage`. В этом случае необходимо использовать аннотацию `RequestType`.
	
	__Тип возвращаемого значения__:  `org.reactivestreams.Publisher<T>`, где тип `T`:
	- должен быть сериализуем через 
	указанный `io.scalecube.services.transport.api.DataCodec`
	- являться `ServiceMessage`. В этом случае необходимо использовать аннотацию `ResponseType`  для явного указания типа полезной нагрузки.

	Примеры:
	
	```java
	@ServiceMethod
	Flux<String> toUpperCase(Flux<String> input);
	```
	```java
	@ServiceMethod
	@ResponseType(String.class)
	Flux<ServiceMessage> toUpperCase(Flux<String> input);
	```
	```java
	@ServiceMethod
	@ResponseType(String.class)
	@RequestType(String.class)
	Flux<ServiceMessage> toUpperCase(Flux<ServiceMessage> input);
	```
	
- `Request Stream` – запрашиваем поток событий. 

	__Тип аргумента__:  Любой тип, удолетворяющий следующим условиям:
	- сериализуем через 
	указанный `io.scalecube.services.transport.api.DataCodec`
	- являющийся `ServiceMessage`. В этом случае необходимо использовать аннотацию `RequestType` для явного указания типа полезной нагрузки.
	
	__Тип возвращаемого значения__:  `org.reactivestreams.Publisher<T>`, где тип `T`:
	- должен быть сериализуем через 
	указанный `io.scalecube.services.transport.api.DataCodec`
	- являться `ServiceMessage`. В этом случае необходимо использовать аннотацию `ResponseType` для явного указания типа полезной нагрузки.

	Примеры:

	```java
	@ServiceMethod
	Flux<String> findById(String id);
	```
	```java
	@ServiceMethod
	@ResponseType(String.class)
	@RequestType(String.class)
	Flux<ServiceMessage> findById(ServiceMessage input);
	```

	




## Алгоритм инициализации Scalecube узла

```mermaid
graph TD;
Z(Basic Initialization) --> A(run Server Transport)
Z --> A1
A -- server network address --> B(Service Endpoint)
A1(Service Factory) -- service definitions --> B
B -- service endpoint --> C(create Service Discovery)
C -- nothing --> D(create MicroservicesContext)
D -- microservices context --> E(Service Factory initializes user's services)
E -- service info set --> F(register services in Method Registry)
F --> H(start Gateways)
F --> J(run Service Discovery)
```





<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyOTI1NTI0MiwyMTI1MTIxNDU1XX0=
-->
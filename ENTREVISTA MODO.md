# 🧠 Bloque 1: Preguntas Teóricas

### ✅ Node.js / NestJS / Express

- **¿Cómo funciona el event loop de Node.js y por qué es single-threaded?**

*El event loop en Node.js es un bucle que corre en un solo hilo y procesa callbacks en distintas fases, manejando la concurrencia de manera no bloqueante. Por eso se dice que es single-threaded: solo hay un hilo que ejecuta JS. Sin embargo, debajo usa un thread pool para operaciones I/O y, si necesito paralelismo real en tareas pesadas, puedo usar worker threads o cluster.*

- **Diferencia entre usar Express y NestJS**: ¿cuándo elegirías uno sobre otro?   

*Express: minimalista, flexible, rápido de prototipar.*      
*NestJS: opinionado, arquitectura modular (controllers, services, DI).*
*Elegir NestJS en proyectos grandes → mejor escalabilidad y mantenibilidad*.

- **¿Qué son los middlewares en Express y los interceptors/guards en NestJS?**

Middleware (Express): lógica previa al handler (auth, logs, parsers).      
Guards (NestJS): control de acceso antes de ejecutar un handler.
Interceptors (NestJS): modificar request/response, logging, transformar datos.

- **¿Cómo manejarías validaciones en NestJS? (class-validator, pipes)**

*`class-validator` + `class-transformer`.*
*Pipes (`ValidationPipe`) para validar DTOs automáticamente.*
Un pipe en NestJS es un mecanismo para transformar y validar datos de entrada antes de que lleguen al handler. Se usan, por ejemplo, para asegurar que un parámetro es un número o que un DTO cumple con las reglas de validación


---

### ✅ Microservicios y Arquitectura

- **¿Qué patrones usarías para comunicar microservicios?** (REST, pub/sub, colas).
    
- **¿Qué es un API Gateway y cómo lo usarías en una arquitectura de microservicios?**
    
- **Explicá el patrón Circuit Breaker y por qué lo usarías.**
    
- **¿Cómo versionarías APIs expuestas a clientes externos?**
    

---

### ✅ Bases de datos

- **SQL**:
    
    - Diferencia entre `INNER JOIN`, `LEFT JOIN` y `RIGHT JOIN`.
        
    - ¿Cómo usarías índices y qué trade-offs tienen?
        
- **DynamoDB**:
    
    - Explicá Primary Key + Sort Key.
        
    - ¿Cuándo usarías un GSI vs un LSI?
        
    - Estrategia para modelar un **one-to-many** en DynamoDB.
        

---

### ✅ Seguridad

- **¿Qué diferencia hay entre TLS y mTLS? ¿En qué caso usarías mTLS?**
    
- **Buenas prácticas para almacenar secretos en AWS.**
    
- **¿Qué es el principio de mínimo privilegio y cómo lo aplicás en IAM?**
    
- **Explícame cómo protegerías un microservicio expuesto a internet.**
    

---

### ✅ Cloud / AWS

- **¿Qué diferencia hay entre SQS y SNS? ¿Cuándo usar cada uno?**
    
- **¿Cómo usarías EventBridge en una arquitectura event-driven?**
    
- **¿Cómo manejarías la observabilidad en microservicios distribuidos?** (logs, traces, métricas).
    
- **¿Qué estrategia de despliegue preferís en producción: blue/green, canary o rolling? ¿Por qué?**
    

---

### ✅ Trabajo en equipo / Cultura

- **Contame una vez que te encontraste con un problema técnico que no sabías resolver. ¿Cómo lo abordaste con tu equipo?**
    
- **Si tuvieras que enseñar NestJS a un compañero que nunca lo usó, cómo lo harías?**
    

---

# 💻 Bloque 2: Ejercicios Prácticos

### 1. **Código Express/NestJS**

👉 Te piden: _“Creá un endpoint en NestJS que reciba un pedido (order), lo guarde en una base MySQL y publique un evento `OrderCreated` en SQS.”_

- Evaluarán:
    
    - Conocimiento de **TypeORM/Prisma** o queries SQL.
        
    - Uso de **service + controller** en NestJS.
        
    - Buenas prácticas (DTOs, validación con `class-validator`).
        
    - Envío de mensaje asíncrono (SDK de AWS).
        

---

### 2. **Query SQL**

👉 Ejemplo: _“Tenés una tabla Orders con columnas (id, user_id, amount, created_at).  
Devolveme el total gastado por cada usuario en el último mes, ordenado por monto.”_

Respuesta esperada:

`SELECT user_id, SUM(amount) as total FROM Orders WHERE created_at >= DATE_SUB(CURDATE(), INTERVAL 1 MONTH) GROUP BY user_id ORDER BY total DESC;`

---

### 3. **Modelado en DynamoDB**

👉 Pregunta: _“Queremos guardar transacciones de usuarios. Cada usuario puede tener miles de transacciones. ¿Cómo modelarías la tabla en DynamoDB para obtener todas las transacciones de un usuario de forma eficiente?”_

Respuesta esperada:

- PK: `userId`
    
- SK: `transactionId` o `timestamp`
    
- Posible GSI: `transactionType` si se quieren filtrar por tipo.
    

---

### 4. **Arquitectura Event-Driven**

👉 Ejercicio: _“Diseñá un diagrama simple para el flujo de un pago: un servicio de Orders recibe la request, publica el evento, un servicio de Payments lo procesa, y un servicio de Notifications avisa al usuario.”_

Evaluarán que:

- Uses **SNS + SQS** o **EventBridge**.
    
- Incluyas **DLQ** para errores.
    
- Pienses en **idempotencia** en Payments.
    
- Consideres **métricas/observabilidad**.
    

---

### 5. **Debugging**

👉 Te muestran un error:

> _“Express app con endpoint `/orders` tarda mucho en responder cuando se procesan PDFs grandes.”_  
> Te piden:

- Identificar el problema (**bloqueo en CPU por procesar PDF en el event loop**).
    
- Proponer solución (**usar worker threads o delegar a un microservicio especializado en procesamiento de archivos**).
    

---

# 🎯 Estrategia para la entrevista

- **En teórico**: ser claro, dar ejemplos simples de uso real (ej: “en Bonvivir usamos EventBridge para orquestar pedidos”).
    
- **En práctico**: escribir código limpio pero no necesariamente perfecto; explicar en voz alta tus decisiones.
    
- **En cultura**: mostrar que sos capaz de **aprender rápido y trabajar en equipo**, algo que MODO valora mucho.



# 🧠 Respuestas Modelo – Preguntas Teóricas

## 🔹 Node.js / NestJS / Express

- **Event loop / single-threaded**
    

        
- **Express vs NestJS**
    
    - Express: minimalista, flexible, rápido de prototipar.
        
    - NestJS: opinionado, arquitectura modular (controllers, services, DI).
        
    - Elegir NestJS en proyectos grandes → mejor escalabilidad y mantenibilidad.
        
- **Middlewares / Interceptors / Guards**
    
    - Middleware (Express): lógica previa al handler (auth, logs, parsers).
        
    - Guards (NestJS): control de acceso antes de ejecutar un handler.
        
    - Interceptors (NestJS): modificar request/response, logging, transformar datos.
        
- **Validaciones (NestJS)**
    
    - `class-validator` + `class-transformer`.
        
    - Pipes (`ValidationPipe`) para validar DTOs automáticamente.
        

---

## 🔹 Microservicios y Arquitectura

- **Comunicación**
    
    - Sincrónica: REST/GraphQL.
        
    - Asincrónica: colas (SQS, Rabbit), pub/sub (SNS, Kafka).
        
    - Elección depende de latencia, resiliencia y acoplamiento.
        
- **API Gateway**
    
    - Punto único de entrada.
        
    - Maneja routing, auth, rate limiting, versionado.
        
    - En AWS: API Gateway o ALB.
        
- **Circuit Breaker**
    
    - Evita llamadas repetidas a un servicio caído.
        
    - Responde rápido con fallback o error controlado.
        
    - Implementable con librerías como Resilience4j o en API Gateway.
        
- **Versionado de APIs**
    
    - URI (`/v1/orders`), header (`Accept-Version`), o query param.
        
    - Mantener backward compatibility siempre que sea posible.
        

---

## 🔹 Bases de Datos

- **SQL**
    
    - `INNER JOIN`: solo coincidencias en ambas tablas.
        
    - `LEFT JOIN`: todos los registros de la izquierda + coincidencias de la derecha.
        
    - `RIGHT JOIN`: opuesto al LEFT.
        
    - Índices: aceleran lecturas, pero consumen más espacio y ralentizan escrituras.
        
- **DynamoDB**
    
    - PK = partición, SK = ordenación.
        
    - GSI: nuevo índice con otra PK/SK, útil para nuevas queries.
        
    - LSI: mismo PK, distinto SK.
        
    - Modelado one-to-many: PK = `userId`, SK = `timestamp#transactionId`.
        

---

## 🔹 Seguridad

- **TLS vs mTLS**
    
    - TLS: cliente verifica al servidor.
        
    - mTLS: verificación mutua, servidor y cliente presentan certificados.
        
    - Usar mTLS en microservicios internos (ej. fintech).
        
- **Gestión de secretos en AWS**
    
    - AWS Secrets Manager o Parameter Store.
        
    - Nunca en código o repositorios.
        
    - Rotación automática de credenciales.
        
- **Principio de mínimo privilegio (IAM)**
    
    - Dar solo los permisos estrictamente necesarios.
        
    - Roles por servicio, no por usuario genérico.
        
    - Revisiones periódicas de políticas.
        
- **Proteger microservicios expuestos**
    
    - TLS obligatorio.
        
    - Autenticación (JWT, OAuth2).
        
    - Rate limiting + WAF.
        
    - Logs y monitoreo de intentos fallidos.
        

---

## 🔹 Cloud / AWS

- **SQS vs SNS**
    
    - SNS: pub/sub, fan-out a múltiples subscriptores.
        
    - SQS: cola, procesamiento asíncrono, 1 consumidor por mensaje.
        
    - SNS + SQS: fan-out → cada microservicio tiene su cola.
        
- **EventBridge**
    
    - Router de eventos serverless.
        
    - Filtro de eventos → reduce acoplamiento.
        
    - Útil para arquitecturas event-driven escalables.
        
- **Observabilidad en microservicios**
    
    - Logs estructurados (JSON).
        
    - Métricas (Prometheus, Datadog).
        
    - Tracing distribuido (OpenTelemetry, X-Ray).
        
    - Correlation ID en cada request/evento.
        
- **Estrategias de despliegue**
    
    - Blue/Green: 2 entornos, switch instantáneo → cero downtime.
        
    - Canary: liberar poco tráfico a la nueva versión → seguro pero gradual.
        
    - Rolling: reemplazar instancias progresivamente → balance costo/seguridad.
        

---

## 🔹 Trabajo en equipo / Cultura

- **Problema técnico desconocido**
    
    - Investigo (docs, logs, PoC).
        
    - Si no alcanza, lo llevo al equipo → brainstorming.
        
    - Documentar la solución para que otros la aprovechen.
        
- **Enseñar NestJS a un compañero**
    
    - Empezar con similitudes con Express (routes → controllers).
        
    - Mostrar estructura básica (módulos, servicios, inyección).
        
    - Hacer un pequeño API demo juntos.




- - -
### Principios de diseño de software: SOLID

- **S — Single Responsibility Principle (SRP)**  
    Cada clase/módulo debe tener **una sola razón para cambiar**.
    
    > Ej: una clase que gestiona usuarios no debería también enviar emails.
    
- **O — Open/Closed Principle (OCP)**  
    El código debe estar **abierto a extensión** pero **cerrado a modificación**.
    
    > Ej: usar interfaces/estrategias para agregar nuevos métodos de pago sin tocar el código existente.
    
- **L — Liskov Substitution Principle (LSP)**  
    Las clases hijas deben poder **reemplazar** a las clases padres sin romper el programa.
    
    > Ej: si `Ave` tiene un método `volar()`, un `Pingüino` no debería heredarla si no puede volar.
    
- **I — Interface Segregation Principle (ISP)**  
    Es mejor tener **interfaces pequeñas y específicas**, que una grande y genérica.
    
    > Ej: no obligar a una clase a implementar métodos que no necesita.
    
- **D — Dependency Inversion Principle (DIP)**  
    Las clases deben depender de **abstracciones**, no de implementaciones concretas.
    
    > Ej: inyectar un `RepositorioDeUsuarios` en lugar de instanciarlo dentro de la clase.



### Principio de diseño de responsabilidad: GRASP 

1. **Information Expert**  
    La responsabilidad debe asignarse al objeto que tiene la **información necesaria** para cumplirla.
    
    > Ej: si una factura debe calcular su total, la clase `Factura` (que tiene los ítems) debería hacerlo.
    
2. **Creator**  
    Una clase debe crear instancias de otra si las **usa, agrega o contiene**.
    
    > Ej: `Pedido` crea sus `ItemPedido`.
    
3. **Controller**  
    Define un objeto intermediario que maneja eventos del sistema y delega trabajo a las entidades.
    
    > Ej: un `PaymentController` recibe la request y delega a `ServicioDePagos`.
    
4. **Low Coupling**  
    Se busca minimizar las dependencias entre clases.
    
    > Ej: usar interfaces o inyección de dependencias en lugar de acoplarse a una implementación concreta.
    
5. **High Cohesion**  
    Una clase debe tener responsabilidades **relacionadas entre sí** (que tengan sentido juntas).
    
    > Ej: no mezclar lógica de negocio y lógica de persistencia en la misma clase.
    
6. **Polymorphism**  
    Usar polimorfismo para manejar variaciones en el comportamiento.
    
    > Ej: distintos tipos de `MedioDePago` (tarjeta, transferencia) implementan la misma interfaz.
    
7. **Pure Fabrication**  
    Crear clases que no representan algo del dominio pero ayudan a **reducir acoplamiento o aumentar cohesión**.
    
    > Ej: un `RepositorioDeUsuarios` para encapsular acceso a la base de datos.
    
8. **Indirection**  
    Usar un intermediario para desacoplar componentes.
    
    > Ej: un `MessageBroker` entre servicios en lugar de comunicarse directamente.
    
9. **Protected Variations**  
    Proteger partes del sistema de cambios en otras usando interfaces, capas o adaptadores.
    
    > Ej: usar un `PaymentGateway` para abstraer MercadoPago o Stripe.



### Formas de organizar el código 

 🔷 Arquitectura Hexagonal (Ports & Adapters)

- También llamada **Ports and Adapters**.
    
- La idea es que la **lógica de negocio (dominio)** quede en el centro, totalmente independiente de frameworks, bases de datos o APIs externas.
    
- Los **Ports** son interfaces que definen cómo el dominio se comunica con el exterior.
    
- Los **Adapters** son implementaciones concretas (ej: repositorio en DynamoDB, controlador HTTP, cliente de Kafka).
    

➡️ Ejemplo en un sistema de pagos:

- El **dominio** define un `ServicioDePagos`.
    
- Un **port** es `RepositorioDePagos`.
    
- Un **adapter** puede ser `RepositorioPagosDynamoDB`.
    

👉 Ventaja: podés cambiar la base de datos o el framework sin tocar el dominio.

---

🔷 Clean Architecture (Robert C. Martin – Uncle Bob)

- Es una evolución que engloba varias (incluida la hexagonal).
    
- Se organiza en **capas concéntricas**, donde las **dependencias solo apuntan hacia adentro**:
    
    1. **Entities (Domino)** → reglas de negocio más puras.
        
    2. **Use Cases (Aplicación)** → coordinan lógica de negocio en escenarios específicos.
        
    3. **Interface Adapters** → adaptan datos/formatos (repositorios, presenters).
        
    4. **Frameworks & Drivers** → base de datos, UI, APIs externas.
        

➡️ Ejemplo en transferencias:

- **Entities**: `Cuenta`, `Transferencia`.
    
- **Use case**: `EjecutarTransferencia`.
    
- **Adapter**: `RepositorioCuentaPostgres`.
    
- **Framework**: NestJS + Express.
    

👉 Ventaja: muy claro qué cambia poco (dominio) y qué cambia mucho (frameworks).

---

 🔷 Onion Architecture

- Muy parecida a Clean, pero más simple visualmente.
    
- Se estructura en **anillos concéntricos**:
    
    - **Core** (dominio puro).
        
    - **Application Services** (coordinan casos de uso).
        
    - **Infrastructure** (acceso a DB, APIs).
        
- La regla es la misma: **las dependencias solo van hacia adentro**.
    

➡️ La diferencia con Clean: Onion es más ligera, menos estricta en formalismos.

---

 🔷 En qué coinciden todas

- Separan la **lógica de negocio** de los **detalles técnicos**.
    
- Usan **inversión de dependencias** (principio D de SOLID).
    
- Facilitan **test unitarios del dominio** sin depender de DB o frameworks.
    

---

 🔷 Diferencias rápidas

| Arquitectura  | Enfoque               | Diferencia clave                                 |
| ------------- | --------------------- | ------------------------------------------------ |
| **Hexagonal** | Puertos y adaptadores | Comunicación clara entre dominio y mundo externo |
| **Clean**     | Capas concéntricas    | Más formal y extensa, propuesta por Uncle Bob    |
| **Onion**     | Anillos concéntricos  | Versión más simple y pragmática de Clean         |


👉 En una entrevista como la de **MODO**, podés esperar que te pregunten:

- ¿Por qué elegirías hexagonal en un sistema financiero?
    
- ¿Cómo aplicarías Clean Architecture en un microservicio de pagos?
    
- ¿Qué diferencia hay con un **monolito modular** tradicional?





### Patrones de diseño

 🔷 1. Patrones Creacionales (cómo crear objetos)

- **Singleton** → una sola instancia global (ej: conexión a DB).
    
- **Factory Method** → delega la creación de objetos a subclases o fábricas.
    
- **Abstract Factory** → fabrica familias de objetos relacionados (ej: crear repositorios para distintas DB).
    
- **Builder** → construye objetos paso a paso (útil para objetos complejos como queries).
    
- **Prototype** → clonar objetos sin acoplarse a su clase concreta.
    

👉 En backend: Factory + Builder son los más comunes.

---

 🔷 2. Patrones Estructurales (cómo organizar clases/objetos)

- **Adapter** → traduce interfaces incompatibles (ej: adaptar SDK de un banco a tu interfaz interna).
    
- **Facade** → provee una interfaz simple sobre un sistema complejo (ej: clase que centraliza llamadas a varios microservicios).
    
- **Decorator** → agrega responsabilidades dinámicamente (ej: logging o retries sobre un cliente HTTP).
    
- **Proxy** → un intermediario que controla acceso (ej: proxy de cache, proxy de seguridad).
    
- **Composite** → estructura jerárquica (ej: menú con ítems que pueden contener submenús).
    

👉 En backend: Adapter, Facade, Decorator y Proxy son súper preguntados.

---

 🔷 3. Patrones de Comportamiento (cómo interactúan objetos)

- **Strategy** → elegir algoritmo en tiempo de ejecución (ej: distintas formas de calcular comisión).
    
- **Observer** → notificación reactiva (ej: eventos en EventBus).
    
- **Command** → encapsula una acción como objeto (ej: ejecutar pagos encolados).
    
- **Chain of Responsibility** → una cadena de handlers que procesan una request (ej: middlewares en NestJS/Express).
    
- **Template Method** → define un esqueleto y deja pasos a subclases (ej: flujo de validación).
    
- **State** → cambia comportamiento según estado interno (ej: orden en estado `pending`, `paid`, `failed`).
    
- **Mediator** → coordina comunicación entre objetos sin que se conozcan entre sí.
    
- **Memento** → guardar/restaurar estado (ej: snapshots de entidades).
    
- **Iterator** → recorrer colecciones sin exponer su representación interna.
    

👉 En backend: Strategy, Observer, Chain of Responsibility y Command son los top.

---

 🔷 4. Patrones de Arquitectura (nivel más alto)

No son GoF, pero sí muy preguntados en entrevistas:

- **MVC / MVVM** → separación de modelo, vista, controlador.
    
- **Repository** → abstraer acceso a datos.
    
- **Service Layer** → separar lógica de negocio de controladores.
    
- **CQRS** → separar comandos (write) de queries (read).
    
- **Event Sourcing** → reconstruir estado a partir de eventos.
    
- **Saga** → coordinar transacciones distribuidas.
    
- **Circuit Breaker** → resiliencia ante fallas de servicios externos.
    
- **BFF (Backend For Frontend)** → backend especializado para cada frontend.
    

👉 Estos son ultra relevantes en un **contexto fintech** como MODO.

---

✅ **Resumen de los que más te pueden preguntar en entrevista**:

- **Creacionales**: Singleton, Factory, Builder.
    
- **Estructurales**: Adapter, Facade, Decorator, Proxy.
    
- **Comportamiento**: Strategy, Observer, Chain of Responsibility, Command.
    
- **Arquitectura**: Repository, Service Layer, CQRS, Saga, Circuit Breaker.















## 🧩 **Principios de diseño**

- SOLID
    
- KISS (Keep It Simple, Stupid)
    
- DRY (Don’t Repeat Yourself)
    
- YAGNI (You Aren’t Gonna Need It)
    
- SoC (Separation of Concerns)
    

---

## 🧭 **Patrones de responsabilidad (GRASP)**

- Information Expert
    
- Creator
    
- Controller
    
- Low Coupling
    
- High Cohesion
    
- Polymorphism
    
- Pure Fabrication
    
- Indirection
    
- Protected Variations
    

---

## 🏗️ **Formas de organizar el código / Arquitecturas**

- MVC / MVVM
    
- Layered Architecture (Presentation, Application, Domain, Infra)
    
- Hexagonal (Ports & Adapters)
    
- Clean Architecture (Uncle Bob)
    
- Onion Architecture
    
- Microservicios / Event-driven
    
- DDD (Domain-Driven Design)
    

---

## 🔨 **Patrones de diseño más importantes**

### Creacionales

- Singleton
    
- Factory Method / Abstract Factory
    
- Builder
    
- Prototype
    

### Estructurales

- Adapter
    
- Facade
    
- Decorator
    
- Proxy
    
- Composite
    

### Comportamiento

- Strategy
    
- Observer
    
- Command
    
- Chain of Responsibility
    
- Template Method
    
- State
    
- Mediator
    
- Iterator
    

### Arquitectura (prácticos en backend)

- Repository
    
- Service Layer
    
- CQRS
    
- Event Sourcing
    
- Saga
    
- Circuit Breaker
    
- BFF
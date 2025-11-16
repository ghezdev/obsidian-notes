# GRASP

- General Responsibility Assignament Software Patterns​
- Son una serie de principios generales para la asignación de responabilidades​
- NO son patrones de diseño, si no prinicipios guia que nos ayudan a tomar mejores desiciones.


> [!NOTE] Tip
> Nos ayuda a responder la pregunte: **¿Qué clase debe hacer esta tarea?​**



## 1. Information Expert 

- **Definición Sencilla:** ¿Quién tiene la información necesaria para hacer una tarea? Esa clase es el **experto** y, por lo tanto, debería tener la **responsabilidad** de hacer esa tarea.
    
- **Explicación:** Este es el patrón más fundamental. Las operaciones deben ir junto a los datos que operan. Si una clase contiene la mayoría o la totalidad de los datos necesarios para realizar una operación, esa operación debería ser un método de esa clase. Esto aumenta la **cohesión** y la **encapsulación**.
    
- **Ejemplo Claro:**
    
    - **Problema:** Calcular el total de un carrito de compras.
        
    - **¿Quién es el Experto?:** La clase `CarritoDeCompras` (o `Order` si estamos hablando de un pedido ya confirmado) tiene la lista de `Productos` y sus `cantidades`. Cada `Producto` tiene su `precio`.
        
    - **Aplicación GRASP:** El método `calcularTotal()` debería estar en la clase `CarritoDeCompras`, porque es esta clase la que tiene la información (la lista de ítems) para realizar el cálculo, y puede acceder al precio de cada producto.

```java 
// Clase Producto (tiene el precio)
public class Producto {
    private String nombre;
    private double precio;
    // ... constructor, getters
    public double getPrecio() { return precio; }
}

// Clase CarritoDeCompras (tiene la lista de productos)
public class CarritoDeCompras {
    private List<Producto> items;
    // ... constructor, métodos para agregar/quitar
    public double calcularTotal() { // <-- El Experto en Información
        double total = 0;
        for (Producto item : items) {
            total += item.getPrecio();
        }
        return total;
    }
}
```


## 2. Creator

- **Definición Sencilla:** ¿Quién debería ser responsable de **crear** un objeto de otra clase? Quien use, contenga o esté estrechamente relacionado con el objeto que se va a crear.
    
- **Explicación:** Asignar la responsabilidad de crear una instancia a la clase que:
    
    - Contiene o agrega instancias de la clase a crear.
        
    - Registra instancias de la clase a crear.
        
    - Usa intensivamente instancias de la clase a crear.
        
    - Tiene los datos de inicialización para la clase a crear.
        
- **Ejemplo Claro:**
    
    - **Problema:** ¿Quién debería crear un objeto `LineaDePedido`?
        
    - **¿Quién es el Creador?:** La clase `Pedido` contiene objetos `LineaDePedido` y tiene los datos necesarios (el `Producto` y la `cantidad`) para crearlas.
        
    - **Aplicación GRASP:** El método `agregarLinea(Producto p, int cantidad)` debería estar en la clase `Pedido`, y este método se encargaría de instanciar `LineaDePedido`.


```java
// Clase LineaDePedido (lo que se va a crear)
public class LineaDePedido {
	private Producto producto;
	private int cantidad;
	// ... constructor, getters
}

// Clase Pedido (el Creador)
public class Pedido {
	private List<LineaDePedido> lineas;
	// ... constructor
	public void agregarLinea(Producto p, int cantidad) { // <-- El Creador
		LineaDePedido nuevaLinea = new LineaDePedido(p, cantidad);
		lineas.add(nuevaLinea);
	}
}
```


## 3. Controller 

- **Definición Sencilla:** ¿Quién es responsable de recibir y coordinar las peticiones del sistema (eventos de la interfaz de usuario o llamadas a la API)? Una clase que representa el sistema en general o un caso de uso específico.
    
- **Explicación:** Los objetos Controlador son los primeros en recibir y manejar los eventos del sistema (interacciones del usuario). No hacen el trabajo directamente, sino que **delegaran la tarea a otras clases** que sean expertas en esa información o lógica de negocio.
    
- **Ejemplo Claro:**
    
    - **Problema:** El usuario hace clic en un botón "Comprar" en la interfaz.
        
    - **¿Quién es el Controlador?:**
        
        - Un `PedidoController` si tienes una API web.
            
        - En el contexto de Swing: un método en `MainFrame` (como `actionPerformed`) o una clase `GestorDeAnimes` (que recibe la acción del botón de la UI y coordina con el repositorio).
            
    - **Aplicación GRASP (en nuestro ejemplo de examen):**
        
        - `MainFrame` recibe el clic del botón (es el controlador de la interfaz).
            
        - `MainFrame` luego **delega** la acción real al `GestorAnimes`.
            
        - `GestorAnimes` es el **Controlador de Dominio/Lógica de Negocio**. Recibe la petición (`agregarAnime`), valida (`if (gestorAnimes.agregarAnime(nuevoAnime))`) y delega la persistencia al `RepositorioAnimes`.
            

```java
// Desde la Vista (MainFrame):
// El usuario hace clic en "Agregar Anime"
public void actionPerformed(ActionEvent e) {
	if (e.getSource() == addButton) {
		// MainFrame (Controlador de UI) recibe el evento y delega
		gestorAnimes.agregarAnime(new Anime(...));
	}
}

// Clase GestorAnimes (Controlador de Dominio)
public class GestorAnimes {
	private RepositorioAnimes repositorioAnimes;
	public GestorAnimes(RepositorioAnimes repo) { this.repositorioAnimes = repo; }

	public boolean agregarAnime(Anime anime) { // <-- El Controlador de Dominio
		// ... lógica de negocio (validaciones) ...
		return repositorioAnimes.agregar(anime); // Delega la persistencia
	}
}
```



## 4. Low Coupling

- **Definición Sencilla:** Minimiza las dependencias entre las clases. Si cambias una clase, que no afecte a muchas otras.
    
- **Explicación:** El acoplamiento mide qué tan interdependientes son dos clases. Un bajo acoplamiento significa que los cambios en una clase tienen un impacto mínimo en otras clases. Esto se logra haciendo que las clases dependan de **abstracciones** (interfaces) en lugar de implementaciones concretas, y limitando el conocimiento que una clase tiene de los internos de otra.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **Problema:** Si decidimos cambiar de un repositorio en memoria a una base de datos.
        
    - **Aplicación GRASP:** La clase `GestorAnimes` no está acoplada directamente a `RepositorioAnimesEnMemoria`. En su lugar, está acoplada a la interfaz `RepositorioAnimes`.

```java
// GestorAnimes depende de la INTERFAZ (abstracción)
public class GestorAnimes {
	private final RepositorioAnimes repositorioAnimes; // <-- Depende de la interfaz

	public GestorAnimes(RepositorioAnimes repositorioAnimes) { // Inyección de Dependencia
		this.repositorioAnimes = repositorioAnimes;
	}
	// ...
}

// En el main o en la configuración, es donde se decide la implementación concreta:
// gestorAnimes = new GestorAnimes(new RepositorioAnimesEnMemoria());
// O si cambias:
// gestorAnimes = new GestorAnimes(new RepositorioAnimesEnBaseDeDatos());
```

Si el `GestorAnimes` hubiera creado `new RepositorioAnimesEnMemoria()` directamente, estaría **fuertemente acoplado** a esa implementación específica, y cualquier cambio en el repositorio de persistencia obligaría a modificar el `GestorAnimes`.


## 5. High Cohesion

- **Definición Sencilla:** Cada clase debe tener una única y clara responsabilidad. Una clase debe hacer "una cosa y hacerla bien".
    
- **Explicación:** La cohesión mide qué tan relacionadas y enfocadas están las responsabilidades de una clase. Una alta cohesión significa que las responsabilidades de una clase están fuertemente relacionadas y colaboran para lograr un objetivo bien definido. Esto mejora la comprensibilidad, la reusabilidad y la facilidad de mantenimiento.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **`Anime.java`**: Solo se encarga de representar un anime. No se preocupa por cómo se guarda, cómo se muestra en la UI, o cómo se gestiona el catálogo.
        
    - **`RepositorioAnimesEnMemoria.java`**: Solo se encarga de las operaciones de persistencia (agregar, eliminar, obtener) para los animes en memoria. No tiene lógica de negocio.
        
    - **`GestorAnimes.java`**: Solo se encarga de la lógica de negocio de los animes (promedio, ordenamiento, coordinación de agregar/eliminar). No interactúa directamente con la UI ni con los detalles de la base de datos.
        
    - **`MainFrame.java`**: Solo se encarga de la interfaz de usuario (mostrar, capturar entrada) y delegar eventos.
        
    - **Problema sin Cohesión:** Imagina una clase `GestorDeTodo` que tenga métodos para la UI, para guardar en BD, para calcular promedios, etc. Sería una clase gigante, difícil de entender y modificar (tendría "baja cohesión").


## 6. Polymorphism

- **Definición Sencilla:** Usa interfaces o herencia para manejar diferentes tipos de objetos que comparten un comportamiento común de una manera uniforme.
    
- **Explicación:** Este principio se utiliza cuando existen alternativas de comportamiento basadas en el tipo de objeto. En lugar de usar múltiples `if-else if` o `switch` statements para determinar el tipo de objeto y su comportamiento, se define una interfaz o una clase base, y las subclases o implementaciones proporcionan su propio comportamiento especializado.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **Problema:** Necesitamos que `GestorAnimes` pueda interactuar con diferentes formas de almacenar animes (en memoria, en BD, en archivo).
        
    - **Aplicación GRASP:** La interfaz `RepositorioAnimes` define el comportamiento `agregar()`, `eliminar()`, etc. `GestorAnimes` interactúa con esta interfaz. Luego, podemos tener `RepositorioAnimesEnMemoria` y, hipotéticamente, `RepositorioAnimesEnBaseDeDatos`, ambos implementando la misma interfaz. `GestorAnimes` solo sabe cómo "hablar" con un `RepositorioAnimes` genérico.

```java
// Interfaz
public interface RepositorioAnimes {
	boolean agregar(Anime anime);
	// ... otros métodos
}

// Implementación 1
public class RepositorioAnimesEnMemoria implements RepositorioAnimes {
	@Override
	public boolean agregar(Anime anime) { /* lógica en memoria */ return true; }
	// ...
}

// Implementación 2 (futura)
public class RepositorioAnimesEnBaseDeDatos implements RepositorioAnimes {
	@Override
	public boolean agregar(Anime anime) { /* lógica de BD */ return true; }
	// ...
}

// GestorAnimes usa el polimorfismo:
public class GestorAnimes {
	private RepositorioAnimes repositorioAnimes; // Tipo de interfaz, no concreto
	public GestorAnimes(RepositorioAnimes repositorioAnimes) { this.repositorioAnimes = repositorioAnimes; }

	public boolean agregarAnime(Anime anime) {
		return repositorioAnimes.agregar(anime); // Llama al método polimórfico
	}
}
```

`GestorAnimes` no necesita saber si está llamando al método `agregar` de la versión en memoria o en base de datos; simplemente llama al método de la interfaz.


## 7. Pure Fabrication 

- **Definición Sencilla:** Cuando ninguna clase existente es un "experto en información" natural para una responsabilidad, crea una nueva clase que no representa un concepto del mundo real, pero que existe solo para mantener un buen diseño (alta cohesión, bajo acoplamiento).
    
- **Explicación:** A veces, una responsabilidad no encaja naturalmente en ninguna clase de dominio (modelo). Si tratamos de forzarla en una clase existente, podríamos romper la cohesión o aumentar el acoplamiento de esa clase. Una "Fabricación Pura" es una clase de servicio o utilidad artificialmente creada para delegar esa responsabilidad y mantener la limpieza del diseño.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **Problema:** ¿Quién es responsable de la lógica de negocio de animes (promedio, ordenamiento, coordinación entre la UI y el repositorio)?
        
    - **¿Ningún Experto Natural?:** No es el `Anime` (es un modelo). No es el `RepositorioAnimes` (es solo persistencia). No es el `MainFrame` (es solo UI).
        
    - **Aplicación GRASP:** Creamos la clase `GestorAnimes`. `GestorAnimes` no es un concepto del mundo real como un "Anime" o un "Usuario". Es una clase de "servicio" que existe puramente para agrupar la lógica de negocio y coordinar las operaciones, manteniendo así alta cohesión y bajo acoplamiento en las otras clases.
    
```java
// GestorAnimes es una Pure Fabrication
public class GestorAnimes {
	private RepositorioAnimes repositorioAnimes; // Se inyecta la dependencia

	public GestorAnimes(RepositorioAnimes repositorioAnimes) {
		this.repositorioAnimes = repositorioAnimes;
	}

	public double calcularPromedioCalificaciones() { /* lógica */ }
	public List<Anime> obtenerAnimesOrdenadosPorCalificacionDescendente() { /* lógica */ }
	public boolean agregarAnime(Anime anime) { /* lógica */ }
	// ...
}
```
   
La existencia de `GestorAnimes` permite que `Anime` siga siendo solo un modelo, `RepositorioAnimes` solo persistencia, y `MainFrame` solo UI, manteniendo el diseño limpio.


## 8. Indirection

- **Definición Sencilla:** Introduce un intermediario entre dos componentes para evitar que se comuniquen directamente y reducir su acoplamiento.
    
- **Explicación:** Este patrón es una extensión del bajo acoplamiento. Implica crear un objeto intermedio (un "intermediario" o "proxy") que retransmite las peticiones entre dos componentes que, de otro modo, estarían fuertemente acoplados. Esto es a menudo logrado mediante el uso de interfaces y el patrón `Observer` o `Strategy`.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **Problema:** `MainFrame` (la Vista) necesita acceder a los datos y la lógica de negocio, pero no queremos que se acople directamente a la implementación específica del repositorio.
        
    - **Aplicación GRASP:**
        
        - `MainFrame` no habla directamente con `RepositorioAnimesEnMemoria`.
            
        - En su lugar, `MainFrame` habla con `GestorAnimes`.
            
        - `GestorAnimes` a su vez habla con la **interfaz** `RepositorioAnimes`, que es un nivel de **indirección**.

```java
// MainFrame (Vista) -- (directamente, pero por abstracción) --> GestorAnimes (Indirección)
// GestorAnimes (Indirección) -- (a través de interfaz) --> RepositorioAnimesEnMemoria (Implementación)
```
   
Este `GestorAnimes` y la interfaz `RepositorioAnimes` actúan como la capa de indirección, protegiendo a la `MainFrame` de los detalles de cómo se gestiona la persistencia.


## 10. Protected Variations 

- **Definición Sencilla:** Identifica los puntos donde el sistema podría cambiar en el futuro y diseña tus clases para que esos cambios tengan un impacto mínimo.
    
- **Explicación:** Este patrón se logra encapsulando los puntos de variación detrás de una interfaz o una clase abstracta. Así, los clientes que usan esa interfaz o clase abstracta no se ven afectados cuando se introduce una nueva implementación o se modifica una existente. Es el "escudo" contra el cambio.
    
- **Ejemplo Claro (en nuestro examen):**
    
    - **Problema:** La forma en que se almacenan los animes (en memoria, en base de datos, en un archivo JSON) podría cambiar en el futuro.
        
    - **Aplicación GRASP:** La **interfaz `RepositorioAnimes`** es el mecanismo principal de **variaciones protegidas**. Cualquier clase que use un `RepositorioAnimes` (como `GestorAnimes`) está protegida de los detalles de cómo se implementa la persistencia. Si cambiamos de `RepositorioAnimesEnMemoria` a `RepositorioAnimesEnBaseDeDatos`, `GestorAnimes` no necesita modificarse

```java
// La interfaz RepositorioAnimes protege al GestorAnimes del cambio en la persistencia.
public interface RepositorioAnimes {
	boolean agregar(Anime anime);
	// ...
}

// GestorAnimes solo depende de la interfaz.
public class GestorAnimes {
	private final RepositorioAnimes repositorioAnimes;
	// ...
}
```

Otros ejemplos podrían ser un "Motor de Pago" (interfaz con diferentes implementaciones para tarjetas de crédito, PayPal, etc.) o un "Formateador de Reportes" (interfaz para PDF, CSV, HTML).


## Resumen 

**Information Expert**: Asignar responsabilidades a quien tiene la información​

**Creator**: Decidir quién debe crear instancias de otras clases​

**Controller**: Coordinar operaciones y manejar eventos del sistema​

**Low Coupling**: Minimizar dependencias entre clases​

**High Cohesion**: Agrupar responsabilidades relacionadas​

**Polymorphism**: Manejar variaciones usando polimorfismo​

**Pure Fabrication**: Crear clases artificiales para mantener buen diseño​

**Indirection**: Usar intermediarios para desacoplar componentes​

**Protected Variations**: Proteger contra cambios futuros

- Los patrones trabajan juntos. No son reglas rígidas ni obligatorias.​
- Son principios que nos guían para desarrollar mejor software utilizando el paradigma de objetos.​
- El código es más mantenible​
- Facilita pruebas unitarias (Utest)​
- Baja la complejidad (BA y AC)​
- Mejora la reutilización de código​


- SOLID nos valida el diseño​
	- Es un checklist de Calidad de Código​
	- Me ayuda a responder: “¿Diseñé bien esto?”​
	
- POO: Nos ayuda a implementar GRASP​
	- Herencia, Polimorfimos y Encapsulación son las bases.​



> [!NOTE] Tip
> Usa GRASP para pensar. SOLID para validar. POO para implementer.




# SOLID

## Principios SOLID: Diseño para Software Robusto

---

## 1. Single Responsibility Principle (SRP) - Principio de Responsabilidad Única

---

- **Definición Sencilla:** Una clase debería tener **una y solo una razón para cambiar**.
    
- **Explicación:** Este principio significa que una clase debe ser responsable de una única parte de la funcionalidad del programa. Si una clase tiene más de una responsabilidad, significa que podría cambiar por múltiples razones, aumentando la probabilidad de errores y dificultando su mantenimiento. Es una de las formas más directas de lograr alta **cohesión**.
    
- **Ejemplo Claro:**
    
    - **Problema:** Una clase `Usuario` que maneja tanto los datos del usuario como la forma en que se guardan en una base de datos y cómo se muestran en la interfaz.
        
    - **¿Qué es la Responsabilidad Única?:**
        
        - **Gestión de Datos del Usuario:** Almacenar nombre, email, contraseña, etc.
            
        - **Persistencia del Usuario:** Guardar y cargar el usuario desde una base de datos.
            
        - **Visualización del Usuario:** Mostrar los datos del usuario en una interfaz de usuario.
            
    - **Aplicación SRP:** Dividimos la clase `Usuario` en tres clases con responsabilidades únicas.
        

```java
// MAL - Baja cohesión, múltiples razones para cambiar
public class Usuario {
    private String nombre;
    private String email;

    public void guardarEnBaseDeDatos() {
        // Lógica para guardar el usuario en la BD
        System.out.println("Guardando usuario en la BD...");
    }

    public void mostrarEnUI() {
        // Lógica para mostrar el usuario en la interfaz
        System.out.println("Mostrando usuario en la UI...");
    }
    // ... otros métodos de datos de usuario
}

// BIEN - Alta cohesión, una razón para cambiar por clase
public class UsuarioModelo { // Responsabilidad: modelar los datos del usuario
    private String nombre;
    private String email;

    public UsuarioModelo(String nombre, String email) {
        this.nombre = nombre;
        this.email = email;
    }
    // ... getters y setters
}

public class RepositorioUsuario { // Responsabilidad: persistencia de usuarios
    public void guardar(UsuarioModelo usuario) {
        // Lógica para guardar el usuario en la BD
        System.out.println("Guardando usuario " + usuario.getNombre() + " en la BD...");
    }

    public UsuarioModelo cargar(String email) {
        // Lógica para cargar usuario de la BD
        System.out.println("Cargando usuario con email " + email + " de la BD...");
        return new UsuarioModelo("Ejemplo", email); // Simulación
    }
}

public class VistaUsuario { // Responsabilidad: mostrar usuarios en la UI
    public void mostrar(UsuarioModelo usuario) {
        // Lógica para mostrar el usuario en la interfaz gráfica
        System.out.println("Mostrando usuario " + usuario.getNombre() + " en la UI.");
    }
}
```

---

## 2. Open/Closed Principle (OCP) - Principio Abierto/Cerrado

---

- **Definición Sencilla:** Las entidades de software (clases, módulos, funciones, etc.) deben estar **abiertas a la extensión, pero cerradas a la modificación**.
    
- **Explicación:** Este principio significa que deberías poder añadir nuevas funcionalidades a un sistema sin tener que modificar el código existente. Esto se logra generalmente a través del uso de interfaces y herencia, permitiendo que el comportamiento sea extendido sin alterar las clases que ya funcionan.
    
- **Ejemplo Claro:**
    
    - **Problema:** Un sistema de cálculo de salarios que necesita añadir nuevos tipos de empleados (por ejemplo, por comisión) en el futuro.
        
    - **¿Qué es Abierto a Extensión y Cerrado a Modificación?:**
        
        - **Abierto a Extensión:** Podemos añadir un nuevo tipo de empleado.
            
        - **Cerrado a Modificación:** No necesitamos cambiar la lógica de cálculo de salarios para los empleados existentes ni el código que los procesa.
            
    - **Aplicación OCP:** Usamos una interfaz `Empleado` con un método `calcularSalario()` y creamos diferentes implementaciones. El sistema principal opera sobre la interfaz, no sobre las clases concretas.
        


```java
// BIEN - Abierto a extensión, cerrado a modificación

// Abstracción: Interfaz que define el contrato
public interface Empleado {
    double calcularSalario();
}

// Implementación 1: Empleado a tiempo completo
public class EmpleadoTiempoCompleto implements Empleado {
    private double salarioBase;

    public EmpleadoTiempoCompleto(double salarioBase) {
        this.salarioBase = salarioBase;
    }

    @Override
    public double calcularSalario() {
        return salarioBase;
    }
}

// Implementación 2: Empleado por horas
public class EmpleadoPorHoras implements Empleado {
    private double tarifaPorHora;
    private int horasTrabajadas;

    public EmpleadoPorHoras(double tarifaPorHora, int horasTrabajadas) {
        this.tarifaPorHora = tarifaPorHora;
        this.horasTrabajadas = horasTrabajadas;
    }

    @Override
    public double calcularSalario() {
        return tarifaPorHora * horasTrabajadas;
    }
}

// Módulo que usa la abstracción (cerrado a modificación)
public class GestorSalarios {
    public void procesarSalario(Empleado empleado) {
        System.out.println("Salario de " + empleado.getClass().getSimpleName() + ": " + empleado.calcularSalario());
    }
}

// Para añadir un nuevo tipo de empleado (Empleado por Comisión), simplemente creamos una nueva clase:
public class EmpleadoPorComision implements Empleado {
    private double ventasRealizadas;
    private double porcentajeComision;

    public EmpleadoPorComision(double ventasRealizadas, double porcentajeComision) {
        this.ventasRealizadas = ventasRealizadas;
        this.porcentajeComision = porcentajeComision;
    }

    @Override
    public double calcularSalario() {
        return ventasRealizadas * porcentajeComision;
    }
}

// Y podemos usarlo sin modificar GestorSalarios:
// GestorSalarios gestor = new GestorSalarios();
// gestor.procesarSalario(new EmpleadoPorComision(10000, 0.10));
```

---

## 3. Liskov Substitution Principle (LSP) - Principio de Sustitución de Liskov

---

- **Definición Sencilla:** Los objetos de un programa deben ser **sustituibles por instancias de sus subtipos sin alterar la corrección del programa**.
    
- **Explicación:** Este principio significa que si tienes una clase `B` que hereda de una clase `A`, entonces deberías poder usar un objeto de tipo `B` en cualquier lugar donde se espere un objeto de tipo `A`, y el programa debería seguir funcionando correctamente, sin comportamientos inesperados o errores. Es clave para el polimorfismo efectivo.
    
- **Ejemplo Claro:**
    
    - **Problema:** Una clase `Rectangulo` y una clase `Cuadrado` que hereda de `Rectangulo`. Si al cambiar el ancho de un `Rectangulo` solo cambia el ancho, pero al cambiar el ancho de un `Cuadrado` también cambia el alto (para mantenerlo cuadrado), esto rompe LSP.
        
    - **¿Qué significa Sustituible?:** Si una función trabaja con `Rectangulo`, debería trabajar igual de bien con `Cuadrado` sin saber que es un `Cuadrado`.
        
    - **Aplicación LSP (Correcta):** En lugar de heredar `Cuadrado` de `Rectangulo` (que introduce un comportamiento inconsistente), es mejor hacer que ambos hereden de una interfaz común o de una clase base que solo defina el comportamiento de "área" o "lados", sin imponer la relación de igualdad de lados de un cuadrado sobre un rectángulo. O, si la herencia es necesaria, asegurarse de que `Cuadrado` nunca cambie el comportamiento esperado de `Rectangulo`.
        


```java
// MAL - Rompe LSP (al cambiar ancho de Cuadrado, cambia el alto, comportamiento inesperado para Rectangulo)
public class Rectangulo {
    protected int ancho;
    protected int alto;

    public void setAncho(int ancho) { this.ancho = ancho; }
    public void setAlto(int alto) { this.alto = alto; }
    public int getArea() { return ancho * alto; }
}

public class Cuadrado extends Rectangulo { // Problema aquí
    @Override
    public void setAncho(int ancho) {
        this.ancho = ancho;
        this.alto = ancho; // ¡Comportamiento adicional!
    }

    @Override
    public void setAlto(int alto) {
        this.alto = alto;
        this.ancho = alto; // ¡Comportamiento adicional!
    }
}

public class PruebaLSP {
    public static void main(String[] args) {
        Rectangulo r = new Cuadrado(); // Aquí se produce la sustitución
        r.setAncho(5);
        r.setAlto(10); // Esperaríamos ancho=5, alto=10, pero con Cuadrado, ancho=10
        System.out.println("Área: " + r.getArea()); // Imprime 100, no 50
    }
}

// MEJOR - LSP respetado (separando o redefiniendo la jerarquía)
// Opción 1: Interfaz común
public interface Forma {
    int getArea();
}

public class Rectangulo implements Forma {
    private int ancho;
    private int alto;
    // constructor, getters, setters
    @Override public int getArea() { return ancho * alto; }
}

public class Cuadrado implements Forma { // No hereda de Rectangulo
    private int lado;
    // constructor, getters, setters
    @Override public int getArea() { return lado * lado; }
}

// Opción 2: Si necesitas propiedades comunes en herencia, pero el contrato de seteo es diferente.
// O simplemente no usar setters que violen el principio para subclases.
// La clave es que los métodos de la subclase no deben invalidar las suposiciones de la superclase.
```

---

## 4. Interface Segregation Principle (ISP) - Principio de Segregación de Interfaces

---

- **Definición Sencilla:** Un cliente no debe ser forzado a depender de métodos que no utiliza. Es decir, es mejor tener **muchas interfaces pequeñas y específicas** que una interfaz grande y general.
    
- **Explicación:** Si una interfaz tiene demasiados métodos, las clases que la implementan pueden verse obligadas a implementar métodos que no necesitan, lo que lleva a un "acoplamiento inútil". Interfaces más pequeñas y enfocadas promueven un bajo acoplamiento y un diseño más limpio.
    
- **Ejemplo Claro:**
    
    - **Problema:** Una interfaz `Trabajador` con métodos para `comer()`, `trabajar()`, `dormir()`, `recibirSalario()`, `escribirCodigo()`. Un robot `TrabajadorRobot` no `come()`, `duerme()` o `recibeSalario()`.
        
    - **¿Qué significa Segregación?:** Dividir la interfaz grande en interfaces más pequeñas y especializadas.
        
    - **Aplicación ISP:** Creamos interfaces más específicas para diferentes tipos de capacidades de trabajador.
        

```java
// MAL - Interfaz gorda, forzando a implementaciones a tener métodos no relevantes
public interface Trabajador {
    void comer();
    void trabajar();
    void dormir();
    void recibirSalario();
    void escribirCodigo();
}

public class Humano implements Trabajador {
    @Override public void comer() { /* come */ }
    @Override public void trabajar() { /* trabaja */ }
    @Override public void dormir() { /* duerme */ }
    @Override public void recibirSalario() { /* recibe */ }
    @Override public void escribirCodigo() { /* escribe */ }
}

public class Robot implements Trabajador {
    @Override public void comer() { /* No aplica, pero debe implementarlo */ }
    @Override public void trabajar() { /* trabaja */ }
    @Override public void dormir() { /* No aplica, pero debe implementarlo */ }
    @Override public void void recibirSalario() { /* No aplica, pero debe implementarlo */ }
    @Override public void escribirCodigo() { /* escribe */ }
}

// BIEN - Interfaces segregadas
public interface IComedor { // Interfaz específica para "comer"
    void comer();
}

public interface IDormilon { // Interfaz específica para "dormir"
    void dormir();
}

public interface IAsalariado { // Interfaz específica para "recibir salario"
    void recibirSalario();
}

public interface IProgramador { // Interfaz específica para "escribir código"
    void escribirCodigo();
}

// Ahora, las clases solo implementan lo que necesitan:
public class Humano implements IComedor, IDormilon, IAsalariado, IProgramador {
    @Override public void comer() { System.out.println("Humano comiendo..."); }
    @Override public void trabajar() { System.out.println("Humano trabajando..."); } // Nota: Podría ser otra interfaz ITrabajador
    @Override public void dormir() { System.out.println("Humano durmiendo..."); }
    @Override public void recibirSalario() { System.out.println("Humano recibiendo salario..."); }
    @Override public void escribirCodigo() { System.out.println("Humano escribiendo código..."); }
}

public class Robot implements IProgramador { // Solo implementa lo que es relevante para un robot
    @Override public void escribirCodigo() { System.out.println("Robot escribiendo código..."); }
    @Override public void trabajar() { System.out.println("Robot trabajando..."); } // Si definimos ITrabajador
}
```

---

## 5. Dependency Inversion Principle (DIP) - Principio de Inversión de Dependencias

---

- **Definición Sencilla:** Los módulos de alto nivel **no deben depender de los módulos de bajo nivel**. Ambos deben depender de **abstracciones**. Además, las **abstracciones no deben depender de los detalles**, sino que los **detalles deben depender de las abstracciones**.
    
- **Explicación:** Este es uno de los principios más importantes y a menudo el que más cuesta entender al principio. Significa que, en lugar de que tu código principal (de alto nivel, la lógica de negocio) dependa directamente de detalles de implementación específicos (de bajo nivel, como una base de datos o un servicio web concreto), ambos deben depender de una interfaz o una clase abstracta. Esto se logra comúnmente a través de la **Inyección de Dependencias**.
    
- **Ejemplo Claro:**
    
    - **Problema:** Una clase `NotificadorEmail` que depende directamente de una clase `ServicioEmailGmail` para enviar correos. Si quieres cambiar a otro proveedor de email, debes modificar `NotificadorEmail`.
        
    - **¿Qué significa Inversión de Dependencias?:** En lugar de que `NotificadorEmail` dependa de un servicio de email concreto, ambos (el notificador y los servicios de email) dependerán de una interfaz `ServicioEmail`.
        
    - **Aplicación DIP:** Creamos una interfaz `ServicioEmail` y `NotificadorEmail` depende de esa interfaz. Luego, le "inyectamos" la implementación concreta que queramos usar.
        

```java
// MAL - Alto nivel (NotificadorEmail) depende de bajo nivel (ServicioEmailGmail)
public class ServicioEmailGmail { // Módulo de bajo nivel (detalle concreto)
    public void enviar(String destinatario, String mensaje) {
        System.out.println("Enviando por GMAIL a " + destinatario + ": " + mensaje);
    }
}

public class NotificadorEmail { // Módulo de alto nivel
    private ServicioEmailGmail servicio; // Dependencia directa y rígida

    public NotificadorEmail() {
        this.servicio = new ServicioEmailGmail(); // Crea la dependencia internamente
    }

    public void notificar(String destinatario, String mensaje) {
        servicio.enviar(destinatario, mensaje);
    }
}

// BIEN - Alto nivel y bajo nivel dependen de una abstracción (interfaz)

// 1. Abstracción
public interface IServicioEmail { // Interfaz (abstracción)
    void enviar(String destinatario, String mensaje);
}

// 2. Módulo de bajo nivel (detalle) depende de la abstracción
public class ServicioEmailGmail implements IServicioEmail {
    @Override
    public void enviar(String destinatario, String mensaje) {
        System.out.println("Enviando por GMAIL a " + destinatario + ": " + mensaje);
    }
}

// 3. Otro módulo de bajo nivel (otro detalle) depende de la abstracción
public class ServicioEmailOutlook implements IServicioEmail {
    @Override
    public void enviar(String destinatario, String mensaje) {
        System.out.println("Enviando por OUTLOOK a " + destinatario + ": " + mensaje);
    }
}

// 4. Módulo de alto nivel depende de la abstracción
public class NotificadorEmail {
    private final IServicioEmail servicio; // Depende de la INTERFAZ (abstracción)

    // Inyección de Dependencia (a través del constructor)
    public NotificadorEmail(IServicioEmail servicio) {
        this.servicio = servicio;
    }

    public void notificar(String destinatario, String mensaje) {
        servicio.enviar(destinatario, mensaje);
    }
}

// Uso en el método main:
// IServicioEmail miServicio = new ServicioEmailGmail(); // O new ServicioEmailOutlook();
// NotificadorEmail notificador = new NotificadorEmail(miServicio);
// notificador.notificar("usuario@ejemplo.com", "Hola!");
```








- - -


## **Composición** (Relación "parte-todo" fuerte)

Cuando una clase es **parte integral** de otra y **no puede existir sin ella**. Si el "todo" se destruye, la "parte" también. La "parte" se crea y destruye junto con el "todo".

```java
public class Motor {
    public void encender() {
        System.out.println("Motor encendido.");
    }
}

public class Coche { // Coche "tiene un" Motor
    private Motor motor; // El motor es una parte del coche

    public Coche() {
        this.motor = new Motor(); // El motor se crea con el coche
    }

    public void arrancar() {
        motor.encender();
        System.out.println("Coche arrancando.");
    }
    // Si el coche se destruye, el motor también (implícitamente en este modelo).
}
```

---

## **Asociación** (Relación "tiene un" más débil)

Una clase utiliza o está relacionada con otra, pero **ambas pueden existir independientemente**. Es una relación más flexible.

```java
public class Estudiante {
    private String nombre;
    // ... constructor, getters
    public String getNombre() { return nombre; }
}

public class Curso { // Curso "tiene" Estudiantes
    private List<Estudiante> estudiantes; // Un curso puede tener muchos estudiantes

    public Curso() {
        this.estudiantes = new ArrayList<>();
    }

    public void inscribirEstudiante(Estudiante e) {
        this.estudiantes.add(e);
        System.out.println(e.getNombre() + " inscrito en el curso.");
    }
    // Los estudiantes pueden existir sin el curso, y viceversa.
}
```

---

## **Dependencia** (Relación "usa un" temporal)

Una clase **usa temporalmente** otra clase o sus métodos, a menudo pasándola como parámetro a un método o creando una instancia dentro de un método. Es la relación más débil.

```java
public class Impresora {
    public void imprimir(String documento) {
        System.out.println("Imprimiendo: " + documento);
    }
}

public class GestorDocumentos {
    public void enviarAImprimir(String documento) {
        Impresora impresora = new Impresora(); // Crea una impresora para usarla
        impresora.imprimir(documento);
        // La impresora se usa solo dentro de este método y luego deja de ser relevante aquí.
    }

    public void enviarAImprimirConImpresora(String documento, Impresora impresora) { // Usa una impresora pasada por parámetro
        impresora.imprimir(documento);
        System.out.println("Documento enviado a imprimir.");
    }
}
```



- - -


```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TareaApp extends JFrame {

    // --- 1. Definición del ENUM ---
    // Un enum para representar los niveles de prioridad de una tarea.
    // Cada constante del enum puede tener atributos y métodos.
    public enum Prioridad {
        BAJA("Baja"),     // Cada prioridad tiene un nombre visible para el usuario
        MEDIA("Media"),
        ALTA("Alta");

        private final String nombreVisible; // Atributo para el nombre que se mostrará en la UI

        Prioridad(String nombreVisible) {
            this.nombreVisible = nombreVisible;
        }

        // Sobrescribimos toString() para que el JComboBox muestre el nombre legible
        @Override
        public String toString() {
            return nombreVisible;
        }
    }

    // Componentes de la UI
    private JTextField nombreTareaField;
    private JComboBox<Prioridad> prioridadComboBox; // JComboBox tipado con el ENUM
    private JTextArea resultadoTextArea;
    private JButton agregarTareaButton;

    public TareaApp() {
        super("Gestor de Tareas con Prioridad"); // Título de la ventana
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(400, 300);
        setLocationRelativeTo(null); // Centra la ventana en la pantalla

        initComponents(); // Inicializa los componentes de la interfaz
        setupLayout();    // Configura el diseño de la ventana
        addListeners();   // Añade los escuchadores de eventos
    }

    private void initComponents() {
        nombreTareaField = new JTextField(20);
        
        // --- 2. Usando el ENUM en JComboBox ---
        // Llenamos el JComboBox con todas las constantes del enum Prioridad.
        // Prioridad.values() devuelve un array con BAJA, MEDIA, ALTA.
        prioridadComboBox = new JComboBox<>(Prioridad.values());
        prioridadComboBox.setSelectedItem(Prioridad.MEDIA); // Selecciona MEDIA por defecto

        resultadoTextArea = new JTextArea(10, 30);
        resultadoTextArea.setEditable(false); // No permitimos que el usuario edite este texto
        
        agregarTareaButton = new JButton("Agregar Tarea");
    }

    private void setupLayout() {
        setLayout(new BorderLayout(10, 10)); // Usamos BorderLayout para el JFrame

        // Panel superior para la entrada de datos
        JPanel inputPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        inputPanel.add(new JLabel("Tarea:"));
        inputPanel.add(nombreTareaField);
        inputPanel.add(new JLabel("Prioridad:"));
        inputPanel.add(prioridadComboBox);
        inputPanel.add(agregarTareaButton);

        add(inputPanel, BorderLayout.NORTH); // Añadimos el panel de entrada arriba

        // Área de texto para mostrar los resultados
        JScrollPane scrollPane = new JScrollPane(resultadoTextArea);
        add(scrollPane, BorderLayout.CENTER); // Añadimos el área de resultados en el centro
    }

    private void addListeners() {
        agregarTareaButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                agregarTarea();
            }
        });
    }

    private void agregarTarea() {
        String nombreTarea = nombreTareaField.getText().trim();
        
        // --- 3. Obteniendo el valor del ENUM seleccionado ---
        Prioridad prioridadSeleccionada = (Prioridad) prioridadComboBox.getSelectedItem();

        if (nombreTarea.isEmpty()) {
            JOptionPane.showMessageDialog(this, "El nombre de la tarea no puede estar vacío.",
                                          "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }

        // Aquí podríamos guardar la tarea en una lista, base de datos, etc.
        // Por simplicidad, solo la mostramos en el área de texto.
        resultadoTextArea.append("Tarea: " + nombreTarea + " | Prioridad: " + prioridadSeleccionada.nombreVisible + "\n");
        
        // Opcional: limpiar el campo de texto después de agregar
        nombreTareaField.setText("");
        nombreTareaField.requestFocusInWindow(); // Vuelve el foco al campo de texto
    }

    public static void main(String[] args) {
        // Asegurarse de que la UI se ejecute en el Event Dispatch Thread (EDT)
        SwingUtilities.invokeLater(() -> {
            new TareaApp().setVisible(true);
        });
    }
}
```


- - -

## 1. Declaración Básica y Acceso a Constantes

---

La forma más sencilla de un `enum`.

```java
public enum DiaSemana {
    LUNES,
    MARTES,
    MIERCOLES,
    JUEVES,
    VIERNES,
    SABADO,
    DOMINGO
}

public class EjemploEnumBasico {
    public static void main(String[] args) {
        // Acceder a una constante del enum
        DiaSemana hoy = DiaSemana.JUEVES;
        System.out.println("Hoy es: " + hoy); // Salida: Hoy es: JUEVES

        // Comparar enums (siempre usar ==, nunca .equals() a menos que sea sobreescrito)
        if (hoy == DiaSemana.JUEVES) {
            System.out.println("¡Es jueves!");
        }

        // Iterar sobre todas las constantes del enum
        System.out.println("\nDías de la semana:");
        for (DiaSemana dia : DiaSemana.values()) { // .values() devuelve un array de todas las constantes
            System.out.println(dia);
        }

        // Obtener el nombre de la constante (como String)
        System.out.println("\nNombre de la constante: " + hoy.name()); // Salida: Nombre de la constante: JUEVES

        // Obtener la posición ordinal (índice, empieza en 0)
        System.out.println("Posición ordinal: " + hoy.ordinal()); // Salida: Posición ordinal: 3 (JUEVES es el 4to, índice 3)

        // Convertir String a enum
        String diaString = "LUNES";
        DiaSemana diaParseado = DiaSemana.valueOf(diaString);
        System.out.println("Día parseado: " + diaParseado); // Salida: Día parseado: LUNES

        // Manejo de error si el String no coincide
        try {
            DiaSemana diaInvalido = DiaSemana.valueOf("NOEXISTE");
        } catch (IllegalArgumentException e) {
            System.out.println("Error: 'NOEXISTE' no es un día de la semana válido.");
        }
    }
}
```

---

## 2. Enums con Atributos y Métodos

---

Los enums pueden tener constructores, atributos y métodos, lo que los hace muy poderosos.

```java
public enum EstadoPedido {
    PENDIENTE("Pendiente de pago", 1),
    PROCESANDO("En procesamiento", 2),
    ENVIADO("En camino", 3),
    ENTREGADO("Entregado al cliente", 4),
    CANCELADO("Cancelado", 0);

    private final String descripcion;
    private final int codigoEstado;

    // Constructor del enum (siempre private o implicitamente private)
    EstadoPedido(String descripcion, int codigoEstado) {
        this.descripcion = descripcion;
        this.codigoEstado = codigoEstado;
    }

    // Métodos para acceder a los atributos
    public String getDescripcion() {
        return descripcion;
    }

    public int getCodigoEstado() {
        return codigoEstado;
    }

    // Métodos utilitarios
    public boolean esFinalizado() {
        return this == ENTREGADO || this == CANCELADO;
    }

    // Sobreescribir toString() para una representación más amigable
    @Override
    public String toString() {
        return descripcion + " (Código: " + codigoEstado + ")";
    }
}

public class EjemploEnumAtributosMetodos {
    public static void main(String[] args) {
        EstadoPedido estadoActual = EstadoPedido.PROCESANDO;

        System.out.println("Estado actual: " + estadoActual);
        System.out.println("Descripción: " + estadoActual.getDescripcion());
        System.out.println("Código: " + estadoActual.getCodigoEstado());

        if (estadoActual.esFinalizado()) {
            System.out.println("El pedido ha finalizado.");
        } else {
            System.out.println("El pedido aún está en curso.");
        }

        EstadoPedido estadoFinalizado = EstadoPedido.ENTREGADO;
        System.out.println("\nEstado de entrega: " + estadoFinalizado);
        if (estadoFinalizado.esFinalizado()) {
            System.out.println("El pedido ha finalizado.");
        }

        // Buscar enum por código
        int codigoBuscado = 3;
        for (EstadoPedido estado : EstadoPedido.values()) {
            if (estado.getCodigoEstado() == codigoBuscado) {
                System.out.println("\nEstado encontrado por código " + codigoBuscado + ": " + estado.getDescripcion());
                break;
            }
        }
    }
}
```

---

## 3. Enums con Comportamiento Específico por Constante (Métodos Abstractos)

---

Cada constante del `enum` puede tener su propia implementación de un método abstracto. Esto es un ejemplo de **polimorfismo** dentro del `enum`.

```java
public enum OperacionMatematica {
    SUMA("+") {
        @Override
        public double ejecutar(double a, double b) {
            return a + b;
        }
    },
    RESTA("-") {
        @Override
        public double ejecutar(double a, double b) {
            return a - b;
        }
    },
    MULTIPLICACION("*") {
        @Override
        public double ejecutar(double a, double b) {
            return a * b;
        }
    },
    DIVISION("/") {
        @Override
        public double ejecutar(double a, double b) {
            if (b == 0) {
                throw new IllegalArgumentException("No se puede dividir por cero.");
            }
            return a / b;
        }
    };

    private final String simbolo;

    // Constructor
    OperacionMatematica(String simbolo) {
        this.simbolo = simbolo;
    }

    // Método abstracto que cada constante debe implementar
    public abstract double ejecutar(double a, double b);

    public String getSimbolo() {
        return simbolo;
    }
}

public class EjemploEnumPolimorfico {
    public static void main(String[] args) {
        double num1 = 10.0;
        double num2 = 5.0;

        // Ejecutar operaciones usando el polimorfismo del enum
        System.out.println(num1 + " " + OperacionMatematica.SUMA.getSimbolo() + " " + num2 + " = " +
                           OperacionMatematica.SUMA.ejecutar(num1, num2)); // Salida: 10.0 + 5.0 = 15.0

        System.out.println(num1 + " " + OperacionMatematica.RESTA.getSimbolo() + " " + num2 + " = " +
                           OperacionMatematica.RESTA.ejecutar(num1, num2)); // Salida: 10.0 - 5.0 = 5.0

        System.out.println(num1 + " " + OperacionMatematica.MULTIPLICACION.getSimbolo() + " " + num2 + " = " +
                           OperacionMatematica.MULTIPLICACION.ejecutar(num1, num2)); // Salida: 10.0 * 5.0 = 50.0

        System.out.println(num1 + " " + OperacionMatematica.DIVISION.getSimbolo() + " " + num2 + " = " +
                           OperacionMatematica.DIVISION.ejecutar(num1, num2)); // Salida: 10.0 / 5.0 = 2.0

        // Iterar y ejecutar todas las operaciones
        System.out.println("\nTodas las operaciones:");
        for (OperacionMatematica op : OperacionMatematica.values()) {
            try {
                System.out.println(op.name() + " (" + op.getSimbolo() + "): " + op.ejecutar(num1, num2));
            } catch (IllegalArgumentException e) {
                System.out.println(op.name() + " (" + op.getSimbolo() + "): " + e.getMessage());
            }
        }
    }
}
```

---

## 4. Enums Implementando Interfaces

---

Los enums pueden implementar interfaces, lo que es útil para agrupar comportamientos comunes bajo una misma abstracción.

```java
// Interfaz
public interface AccionPersonaje {
    void ejecutarAccion();
}

public enum TipoPersonaje implements AccionPersonaje {
    MAGO("Mago") {
        @Override
        public void ejecutarAccion() {
            System.out.println("El mago lanza un hechizo mágico.");
        }
    },
    GUERRERO("Guerrero") {
        @Override
        public void ejecutarAccion() {
            System.out.println("El guerrero ataca con su espada.");
        }
    },
    LADRON("Ladrón") {
        @Override
        public void ejecutarAccion() {
            System.out.println("El ladrón se escabulle en las sombras.");
        }
    };

    private final String nombre;

    TipoPersonaje(String nombre) {
        this.nombre = nombre;
    }

    public String getNombre() {
        return nombre;
    }
}

public class EjemploEnumInterfaz {
    public static void main(String[] args) {
        TipoPersonaje miPersonaje = TipoPersonaje.MAGO;
        System.out.println("Mi personaje es un " + miPersonaje.getNombre());
        miPersonaje.ejecutarAccion(); // Salida: El mago lanza un hechizo mágico.

        TipoPersonaje otroPersonaje = TipoPersonaje.GUERRERO;
        System.out.println("\nOtro personaje es un " + otroPersonaje.getNombre());
        otroPersonaje.ejecutarAccion(); // Salida: El guerrero ataca con su espada.

        // Puedes usar el enum en una variable de tipo interfaz
        AccionPersonaje personajeAccion = TipoPersonaje.LADRON;
        System.out.println("\nEl ladrón está en acción:");
        personajeAccion.ejecutarAccion(); // Salida: El ladrón se escabulle en las sombras.
    }
}
```
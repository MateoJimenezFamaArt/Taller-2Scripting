### Punto 1

#### i. ¿Qué son los principios SOLID y cómo contribuyen a un buen diseño orientado a objetos?


**S - Single Responsibility Principle (Principio de Responsabilidad Única):**

Cada clase debe tener una única responsabilidad o razón para cambiar. Es decir, una clase debe encargarse solo de una funcionalidad específica dentro del sistema. Esto facilita el mantenimiento y la comprensión del código.

**O - Open/Closed Principle (Principio Abierto/Cerrado):**

Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para extensión, pero cerradas para modificación. Esto significa que el comportamiento de una clase debe poder extenderse sin modificar su código fuente.

**L - Liskov Substitution Principle (Principio de Sustitución de Liskov):**

establece que una clase derivada (hija) debe poder sustituir a su clase base (padre) sin que el comportamiento del programa se vea afectado. Este principio es fundamental para asegurar que la herencia en la programación orientada a objetos sea correcta y no cause problemas inesperados en el código.

**I - Interface Segregation Principle (Principio de Segregación de Interfaces):**

Es mejor tener muchas interfaces pequeñas y específicas que varias grandes y generales. Los clientes no deben estar obligados a depender de interfaces que no usan, lo que mejora la flexibilidad y la cohesión.

**D - Dependency Inversion Principle (Principio de Inversión de Dependencias):**

El objetivo principal de DIP es reducir el acoplamiento entre los módulos de un sistema, es decir, disminuir la dependencia directa entre distintas partes del código para mejorar la flexibilidad, la mantenibilidad y la capacidad de adaptación del software.


#### ii. Explica cómo el patrón Singleton asegura que solo haya una instancia de una clase y cuáles son sus posibles usos

El patrón Singleton garantiza una sola instancia mediante las siguientes características clave:

**- Constructor Privado:**

Se define un constructor privado para evitar que otras clases creen nuevas instancias de la clase Singleton usando el operador new. Esto restringe la creación del objeto desde fuera de la clase.

**- Instancia Estática:**

La clase contiene una referencia estática (generalmente un campo privado) a la única instancia de sí misma.

**- Método Estático de Acceso:**

Un método público y estático (generalmente llamado getInstance()) controla el acceso a la instancia única. Este método crea la instancia si aún no existe y la devuelve en caso contrario.

Posibles Usos del Patrón Singleton:

**1.	Gestión de Configuración:**

Mantener una sola instancia de un gestor de configuración que lea y escriba parámetros de configuración de una aplicación, asegurando que todas las partes del programa compartan la misma configuración.

**2.	Conexión a Bases de Datos:**

Administrar una única conexión a la base de datos en lugar de crear nuevas conexiones cada vez que se necesiten, lo que ahorra recursos y mejora el rendimiento.

**3.	Gestión de Recursos Compartidos:**

Controlar el acceso a recursos compartidos, como impresoras o dispositivos de entrada/salida, asegurando que no haya conflictos o uso simultáneo no coordinado.

**4.	Log de Aplicaciones:**

Mantener una instancia de un logger para registrar mensajes de depuración o errores. Esto asegura que todos los mensajes vayan a un solo lugar.

**5.	Controladores de Estados Globales:**

En juegos o sistemas con estados globales (como un administrador de escena o de estado), un Singleton asegura que el estado se gestione desde una única fuente.



#### iii. ¿Cómo funciona el patrón Observer y en qué situaciones es útil?
El patrón Observer se compone principalmente de dos tipos de objetos:

**1.	Subject (Sujeto):**

Es el objeto que mantiene el estado y notifica a los observadores cuando hay cambios. El Subject tiene una lista de observadores y métodos para agregar (attach), eliminar (detach) y notificar (notify) a estos observadores.

**2.	Observers (Observadores):**

Son los objetos que desean estar informados sobre los cambios en el sujeto. Cada observador implementa una interfaz que define el método update(), que es llamado por el sujeto cuando hay un cambio.


#### iv. ¿Qué es un antipatrón? explique por medio de dos ejemplos
Un antipatrón es una solución comúnmente adoptada para un problema de diseño o programación que, aunque puede parecer efectiva o práctica a primera vista, resulta contraproducente, ineficiente o problemático a largo plazo. Los antipatrones suelen surgir de malas prácticas, falta de experiencia o decisiones apresuradas, y su uso puede conducir a sistemas difíciles de mantener, propensos a errores y con un rendimiento deficiente.

**Ejemplo 1: God Object**

Un "God Object" es un antipatrón donde una sola clase asume demasiadas responsabilidades, manejando una gran parte de la lógica del programa. Este objeto contiene demasiados métodos, tiene muchos campos, y se convierte en el "centro del universo" de la aplicación, haciéndose cargo de tareas que deberían estar distribuidas en otras clases.

Causas :
- Falta de comprensión de los principios de diseño orientado a objetos, como el Principio de Responsabilidad Única.
- Intento de simplificar la lógica agrupándola en un solo lugar, en lugar de delegar responsabilidades a otras clases.
  
Consecuencias:

- Dificultad para comprender y modificar el código debido a la alta complejidad y responsabilidad del objeto.
- Código altamente acoplado y poco reutilizable.

**Ejemplo 2: Big ball of Mud**

Es un antipatrón en el que el sistema de software carece de una arquitectura bien definida o estructurada, y su código se convierte en una maraña desorganizada y caótica. Los módulos y clases están pobremente organizados, con dependencias entrelazadas y sin un propósito claro o separación de responsabilidades.

Causas:
- Desarrollo sin planificación ni diseño previo.
- Falta de evaluación continua del código.

Consecuencias:

- El mantenimiento se vuelve extremadamente costoso y difícil.
- La adición de nuevas funcionalidades introduce errores debido a la alta complejidad y falta de claridad.
- La corrección de errores es lenta y tediosa, porque los cambios en una parte del sistema pueden afectar inesperadamente a otras partes.

### Punto 2
#### Ejercicio práctico: Implementación del patrón Singleton en una aplicación de consola.

Implemente una clase Configuracion que siga el patrón Singleton. Esta clase debe tener las propiedades NombreAplicacion y Version, que almacenen la información de configuración de una aplicación. Asegúrese de que solo una instancia de esta clase sea accesible durante toda la ejecución del programa.

Además, cree un método para mostrar los valores de configuración. En el método Main, obtenga la instancia de la configuración, modifique sus propiedades y verifique que solo existe una única instancia de la clase.

```csharp
using System;

namespace SingletonApp
{
    // Clase Singleton
    public class Configuracion
    {
        // Propiedades de configuración
        public string NombreAplicacion { get; set; }
        public string Version { get; set; }

        // Campo estático que contiene la única instancia de Configuracion
        private static Configuracion instancia;

        // Constructor privado para evitar la creación de instancias desde fuera
        private Configuracion()
        {
            NombreAplicacion = "MiAplicacion";
            Version = "1.0";
        }

        // Método estático para obtener la instancia única de Configuracion
        public static Configuracion ObtenerInstancia()
        {
            if (instancia == null)
            {
                instancia = new Configuracion();
            }
            return instancia;
        }

        // Método para mostrar la configuración actual
        public void MostrarConfiguracion()
        {
            Console.WriteLine($"Nombre de la Aplicación: {NombreAplicacion}");
            Console.WriteLine($"Versión: {Version}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Obtener la única instancia de Configuracion
            Configuracion config1 = Configuracion.ObtenerInstancia();
            config1.MostrarConfiguracion();

            // Cambiar los valores de la configuración
            config1.NombreAplicacion = "NuevaAplicacion";
            config1.Version = "2.0";

            // Obtener otra vez la instancia (será la misma)
            Configuracion config2 = Configuracion.ObtenerInstancia();
            config2.MostrarConfiguracion();

            // Verificar si config1 y config2 son la misma instancia
            if (config1 == config2)
            {
                Console.WriteLine("config1 y config2 son la misma instancia.");
            }

            Console.ReadKey();
        }
    }
}
```
#### Ejercicio práctico: Implementación del patrón Observer en una aplicación de consola.

Implemente un programa en C# que utilice el patrón de diseño Observer. En este ejercicio, se simulará un sistema de notificaciones donde varios observadores se suscriben a un sujeto y reciben actualizaciones cuando el estado del sujeto cambie.

```csharp
using System;
using System.Collections.Generic;

namespace ObserverApp
{
    // Interfaz del Observador
    public interface IObservador
    {
        void Actualizar(string mensaje);
    }

    // Interfaz del Sujeto
    public interface ISujeto
    {
        void Suscribir(IObservador observador);
        void Desuscribir(IObservador observador);
        void Notificar(string mensaje);
    }

    // Clase SujetoConcreto que implementa la interfaz ISujeto
    public class SujetoConcreto : ISujeto
    {
        private List<IObservador> observadores = new List<IObservador>();

        // Método para suscribir un observador
        public void Suscribir(IObservador observador)
        {
            observadores.Add(observador);
            Console.WriteLine("Observador suscrito.");
        }

        // Método para desuscribir un observador
        public void Desuscribir(IObservador observador)
        {
            observadores.Remove(observador);
            Console.WriteLine("Observador desuscrito.");
        }

        // Método para notificar a todos los observadores
        public void Notificar(string mensaje)
        {
            foreach (var observador in observadores)
            {
                observador.Actualizar(mensaje);
            }
        }

        // Método para cambiar el estado del sujeto y notificar a los observadores
        public void CambiarEstado(string nuevoEstado)
        {
            Console.WriteLine($"El estado ha cambiado a: {nuevoEstado}");
            Notificar($"Nuevo estado: {nuevoEstado}");
        }
    }

    // Clase ObservadorConcreto que implementa la interfaz IObservador
    public class ObservadorConcreto : IObservador
    {
        private string nombre;

        public ObservadorConcreto(string nombre)
        {
            this.nombre = nombre;
        }

        // Método que se llama cuando el sujeto notifica a este observador
        public void Actualizar(string mensaje)
        {
            Console.WriteLine($"{nombre} ha recibido la actualización: {mensaje}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Crear el sujeto concreto
            SujetoConcreto sujeto = new SujetoConcreto();

            // Crear observadores concretos
            ObservadorConcreto observador1 = new ObservadorConcreto("Observador 1");
            ObservadorConcreto observador2 = new ObservadorConcreto("Observador 2");
            ObservadorConcreto observador3 = new ObservadorConcreto("Observador 3");

            // Suscribir observadores al sujeto
            sujeto.Suscribir(observador1);
            sujeto.Suscribir(observador2);

            // Cambiar el estado del sujeto y notificar a los observadores
            sujeto.CambiarEstado("Activo");

            // Desuscribir un observador
            sujeto.Desuscribir(observador2);

            // Cambiar el estado nuevamente
            sujeto.CambiarEstado("Inactivo");

            // Suscribir otro observador
            sujeto.Suscribir(observador3);

            // Cambiar el estado una vez más
            sujeto.CambiarEstado("Esperando");

            Console.ReadKey();
        }
    }
}
```
## Punto 4 

### Configurar el proyecto para usar otros patrones de diseño. Implementar dos de los siguientes patrones en una aplicación sencilla: 

Explica el patrón de diseño Decorator y cómo puede utilizarse para agregar responsabilidades adicionales a los objetos de forma dinámica sin modificar su clase original. Implementa un ejemplo donde un procesador de datos básico se extienda para medir el tiempo de procesamiento y, además, invertir el contenido de los datos procesados.

El patrón Decorator permite agregar responsabilidades adicionales a objetos de manera dinámica. Se utiliza una clase decoradora que contiene una referencia a un objeto del mismo tipo, de modo que cuando se llama a un método del decorador, este ejecuta su propia lógica adicional y luego delega la ejecución en el objeto decorado.

Aquí está el ejemplo de un procesador de datos que se extiende con un decorador para medir el tiempo de procesamiento y otro para invertir el contenido de los datos:
```c#

// Interfaz común
public interface IDataProcessor
{
    void Process(string data);
}

// Clase concreta
public class BasicProcessor : IDataProcessor
{
    public void Process(string data)
    {
        Console.WriteLine($"Procesamiento básico: {data}");
    }
}

// Decorador base
public abstract class ProcessorDecorator : IDataProcessor
{
    protected IDataProcessor _processor;

    public ProcessorDecorator(IDataProcessor processor)
    {
        _processor = processor;
    }

    public virtual void Process(string data)
    {
        _processor.Process(data);
    }
}

// Decorador para medir el tiempo
public class TimingProcessor : ProcessorDecorator
{
    public TimingProcessor(IDataProcessor processor) : base(processor) { }

    public override void Process(string data)
    {
        var start = DateTime.Now;
        base.Process(data);
        var end = DateTime.Now;
        Console.WriteLine($"Tiempo de procesamiento: {end - start}");
    }
}

// Decorador para invertir el texto
public class ReverseProcessor : ProcessorDecorator
{
    public ReverseProcessor(IDataProcessor processor) : base(processor) { }

    public override void Process(string data)
    {
        var reversedData = new string(data.Reverse().ToArray());
        Console.WriteLine($"Datos invertidos: {reversedData}");
    }
}
```

// Uso del decorador
var processor = new ReverseProcessor(new TimingProcessor(new BasicProcessor()));
processor.Process("Hola Mundo");

Explica el patrón de diseño Facade y cómo puede utilizarse para simplificar la interacción con un sistema complejo. Implementa un ejemplo donde un sistema de manejo de archivos realiza operaciones de lectura, compresión y encriptación, utilizando una interfaz simplificada.

El patrón Facade proporciona una interfaz simplificada para acceder a subsistemas complejos. Actúa como una puerta de entrada, delegando las solicitudes a las clases adecuadas dentro del sistema y ocultando las complejidades al usuario.

Aquí está el ejemplo de un sistema de manejo de archivos con operaciones de lectura, compresión y encriptación, simplificado mediante una fachada:// Subsistema complejo

```c#
public class FileReader
{
    public string ReadFile(string filePath)
    {
        return $"Contenido del archivo: {filePath}";
    }
}

public class FileCompressor
{
    public string Compress(string data)
    {
        return $"Archivo comprimido: {data}";
    }
}

public class FileEncryptor
{
    public string Encrypt(string data)
    {
        return $"Archivo encriptado: {data}";
    }
}

// Fachada
public class FileFacade
{
    private FileReader _fileReader;
    private FileCompressor _fileCompressor;
    private FileEncryptor _fileEncryptor;

    public FileFacade()
    {
        _fileReader = new FileReader();
        _fileCompressor = new FileCompressor();
        _fileEncryptor = new FileEncryptor();
    }

    public void ProcessFile(string filePath)
    {
        var content = _fileReader.ReadFile(filePath);
        var compressedContent = _fileCompressor.Compress(content);
        var encryptedContent = _fileEncryptor.Encrypt(compressedContent);
        Console.WriteLine(encryptedContent);
    }
}

// Uso de la fachada
var fileFacade = new FileFacade();
fileFacade.ProcessFile("ruta/del/archivo.txt");

```


## Punto 5

Porfavor presiona este [link](https://ablequesawea.itch.io/xaca) para probar la demo en unity

### Explicacion rapida

En la primer pantalla un singleton alberga todos los posibles colores que puede tomar el bloque central y mediante el uso de botones le decimos que color debe tomar del singleton

En la segunda pantalla le decimos una cantidad de objetos que queremos agregar a la pool e instanciamos esos objetos, luego podemos dispararlos o usarlos para finalmente hacer un recall y volver a reestablecer las balas a un estado util, este poolin emplea el metodo observer puesto que las balas se subscriben y desuscriben de un handler del pool que les permite estar en la escena activas y luego desactivarse y luego reciclarse
##

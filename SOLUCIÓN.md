### Punto 1
#### Ejercicio teorico:

**¿Qué son los principios SOLID y cómo contribuyen a un buen diseño orientado a objetos?**




**Explica cómo el patrón Singleton asegura que solo haya una instancia de una clase y cuáles son sus posibles usos**




**¿Cómo funciona el patrón Observer y en qué situaciones es útil?**




**¿Qué es un antipatrón? explique por medio de dos ejemplos**






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
## ejercico 2 

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

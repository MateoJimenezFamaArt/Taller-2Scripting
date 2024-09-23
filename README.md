# Taller-2Scripting


## Enunciado:

Implementar y probar las siguientes características en un proyecto utilizando C#:

- Aplicar los principios S.O.L.I.D en el diseño de software orientado a objetos.
  
- Implementar el patrón de diseño Singleton para asegurar una única instancia de una clase en el sistema.
  
- Aplicar el patrón de diseño Observer para notificar a los objetos sobre cambios en el estado de otro objeto.

- Utilizar delegados para crear una funcionalidad personalizada en el sistema.

- Desarrollar una pequeña aplicación en Unity y en consola que demuestre estos patrones y principios. (Uno en Unity y Uno en Consola)

## Puntos

### Punto 1 Teoria
- Responder las siguientes preguntas teóricas:

  1. ¿Qué son los principios SOLID y cómo contribuyen a un buen diseño orientado a objetos?
  2. Explica cómo el patrón Singleton asegura que solo haya una instancia de una clase y cuáles son sus posibles usos.
  3. ¿Cómo funciona el patrón Observer y en qué situaciones es útil?
  4. ¿Qué es un antipatrón? explique por medio de dos ejemplos.

### Punto 2 Desarrollo sencillo
- Desarrollar ejercicios prácticos sencillos, similares a los siguientes:

  1. Ejercicio practico con Singleton (Hacer Una ConsoleApp)
  2. Ejercicio practico con Observer (Hacer Una ConsoleApp)

### Punto 3 Desarrollo de Consultas

- Consulte un código o librería nativo de C# que use el patrón decorador.

- Definir y utilizar delegados para implementar el patrón observer. (Hacer Una ConsoleApp)

### Punto 4 Realizar App con dos patrones de diseño

- Configurar el proyecto para usar otros patrones de diseño. Implementar dos de los siguientes patrones en una aplicación sencilla: (Hacer Una ConsoleApp)
1. Patrón Decorador
2. Patrón Facade
3. Patrón Strategy
4. Patrón Adapter

## ejercico 2 

### Configurar el proyecto para usar otros patrones de diseño. Implementar dos de los siguientes patrones en una aplicación sencilla: 

Explica el patrón de diseño Decorator y cómo puede utilizarse para agregar responsabilidades adicionales a los objetos de forma dinámica sin modificar su clase original. Implementa un ejemplo donde un procesador de datos básico se extienda para medir el tiempo de procesamiento y, además, invertir el contenido de los datos procesados.

El patrón Decorator permite agregar responsabilidades adicionales a objetos de manera dinámica. Se utiliza una clase decoradora que contiene una referencia a un objeto del mismo tipo, de modo que cuando se llama a un método del decorador, este ejecuta su propia lógica adicional y luego delega la ejecución en el objeto decorado.

Aquí está el ejemplo de un procesador de datos que se extiende con un decorador para medir el tiempo de procesamiento y otro para invertir el contenido de los datos:

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

// Uso del decorador
var processor = new ReverseProcessor(new TimingProcessor(new BasicProcessor()));
processor.Process("Hola Mundo");

Explica el patrón de diseño Facade y cómo puede utilizarse para simplificar la interacción con un sistema complejo. Implementa un ejemplo donde un sistema de manejo de archivos realiza operaciones de lectura, compresión y encriptación, utilizando una interfaz simplificada.

El patrón Facade proporciona una interfaz simplificada para acceder a subsistemas complejos. Actúa como una puerta de entrada, delegando las solicitudes a las clases adecuadas dentro del sistema y ocultando las complejidades al usuario.

Aquí está el ejemplo de un sistema de manejo de archivos con operaciones de lectura, compresión y encriptación, simplificado mediante una fachada:// Subsistema complejo
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




## Punto 5 Ejemplos cortos y comparaciones entre C# puro y Unity

- Realice ejemplos cortos, realice su implementación en unity y en c sharp por separado 
- ¿Que diferencias hay en cada implementación del patrón?
- ¿Qué beneficios existen al usar patrones?
- Crear una presentación donde se publiquen las evidencias del taller
- Realizar una exposición con los resultados en clase


### Porcentajes

- (10%) Asistencia a clase
- (10%) Diapositivas y exposición en clase
- (10%) Argumentación individual
- (10%) Uso del repositorio
- (20%) Aplicación de los principios SOLID y patrones de diseño
- (20%) Trabajo en equipo y nuevo grupo
- (20%) Funcionalidad y claridad del código en C#


## Tareas Correspondientes

1. Manuela Buritica -> 1,3
3. Esteban Araujo -> 2, 4
4. Mateo Jimenez -> 5

## Presentacion

[Click aca pofabo](https://docs.google.com/presentation/d/1_T3JnpX077LiF-M-6WlWR2Rxr351SXsEcoAU2Wq5_N0/edit?usp=sharing)







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
Ejercicio práctico: Implementación del patrón Observer en una aplicación de consola.

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


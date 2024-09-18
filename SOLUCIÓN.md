





### Punto 3
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



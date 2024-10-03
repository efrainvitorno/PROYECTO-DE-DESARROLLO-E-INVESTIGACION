# PROYECTO DE DESARROLLO E INVESTIGACION
## Nombre: Efrain Vitorino Marin     - Codigo: 160337



# Conjunto de Operaciones en C#

Este programa implementa una clase `CConjunto` que permite realizar operaciones entre conjuntos como la unión, intersección, diferencia, y diferencia simétrica. El conjunto es representado mediante un arreglo de enteros y se asegura que no existan duplicados.

## Estructura de la Clase

### CConjunto

- **Atributos:**
  - `elementos`: Un arreglo estático de enteros que representa los elementos del conjunto.
  - `tam`: Un entero que indica el tamaño actual del conjunto.

- **Constructores:**
  - `CConjunto()`: Constructor vacío que inicializa el conjunto con un tamaño máximo de 100 elementos.
  - `CConjunto(int[] pElementos)`: Constructor que recibe un arreglo de enteros e inserta los elementos en el conjunto evitando duplicados.

- **Métodos:**
  - `insertar(int elemento)`: Inserta un elemento en el conjunto si no existe previamente.
  - `pertenece(int elemento)`: Verifica si un elemento pertenece al conjunto.
  - `union(CConjunto otro)`: Retorna un nuevo conjunto con la unión de dos conjuntos.
  - `interseccion(CConjunto otro)`: Retorna un nuevo conjunto con la intersección de dos conjuntos.
  - `diferencia(CConjunto otro)`: Retorna un nuevo conjunto con la diferencia de dos conjuntos.
  - `diferenciaSimetrica(CConjunto otro)`: Retorna un nuevo conjunto con la diferencia simétrica de dos conjuntos.
  - `mostrarConjunto()`: Muestra los elementos del conjunto en la consola.

## Ejecución del Programa

```csharp
using System;

class CConjunto
{
    private int[] elementos; // Arreglo estático
    private int tam; // Tamaño actual del conjunto

    // Constructor vacío
    public CConjunto()
    {
        elementos = new int[100]; // Tamaño máximo estático
        tam = 0;
    }

    // Constructor que recibe un arreglo de enteros
    public CConjunto(int[] pElementos)
    {
        elementos = new int[100];
        tam = 0;
        foreach (var elem in pElementos)
        {
            insertar(elem);
        }
    }

    // Método para insertar un elemento (evitar duplicados)
    public void insertar(int elemento)
    {
        if (!pertenece(elemento))
        {
            elementos[tam] = elemento;
            tam++;
        }
    }

    // Método para verificar si un elemento pertenece al conjunto
    public bool pertenece(int elemento)
    {
        for (int i = 0; i < tam; i++)
        {
            if (elementos[i] == elemento)
            {
                return true;
            }
        }
        return false;
    }

    // Método para la unión de dos conjuntos
    public CConjunto union(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        for (int i = 0; i < tam; i++)
        {
            resultado.insertar(elementos[i]);
        }
        for (int i = 0; i < otro.tam; i++)
        {
            resultado.insertar(otro.elementos[i]);
        }
        return resultado;
    }

    // Método para la intersección de dos conjuntos
    public CConjunto interseccion(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        for (int i = 0; i < tam; i++)
        {
            if (otro.pertenece(elementos[i]))
            {
                resultado.insertar(elementos[i]);
            }
        }
        return resultado;
    }

    // Método para la diferencia de dos conjuntos
    public CConjunto diferencia(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        for (int i = 0; i < tam; i++)
        {
            if (!otro.pertenece(elementos[i]))
            {
                resultado.insertar(elementos[i]);
            }
        }
        return resultado;
    }

    // Método para la diferencia simétrica de dos conjuntos
    public CConjunto diferenciaSimetrica(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        CConjunto dif1 = diferencia(otro);
        CConjunto dif2 = otro.diferencia(this);

        // Unir las dos diferencias
        for (int i = 0; i < dif1.tam; i++)
        {
            resultado.insertar(dif1.elementos[i]);
        }

        for (int i = 0; i < dif2.tam; i++)
        {
            resultado.insertar(dif2.elementos[i]);
        }

        return resultado;
    }

    // Método para mostrar el conjunto
    public void mostrarConjunto()
    {
        for (int i = 0; i < tam; i++)
        {
            Console.Write(elementos[i] + " ");
        }
        Console.WriteLine();
    }
}

class Program
{
    static void Main(string[] args)
    {
        int[] A = { 1, 2, 3, 4 };
        CConjunto C1 = new CConjunto(A);

        int[] B = { 3, 4, 5, 6 };
        CConjunto C2 = new CConjunto(B);

        Console.WriteLine("Conjunto A: ");
        C1.mostrarConjunto();

        Console.WriteLine("Conjunto B: ");
        C2.mostrarConjunto();

        // Unión
        CConjunto union = C1.union(C2);
        Console.WriteLine("Unión de A y B: ");
        union.mostrarConjunto();

        // Intersección
        CConjunto interseccion = C1.interseccion(C2);
        Console.WriteLine("Intersección de A y B: ");
        interseccion.mostrarConjunto();

        // Diferencia
        CConjunto diferencia = C1.diferencia(C2);
        Console.WriteLine("Diferencia A - B: ");
        diferencia.mostrarConjunto();

        // Diferencia Simétrica
        CConjunto diferenciaSimetrica = C1.diferenciaSimetrica(C2);
        Console.WriteLine("Diferencia Simétrica A Δ B: ");
        diferenciaSimetrica.mostrarConjunto();

        // Evitar cierre inmediato de la consola
        Console.ReadKey();
    }
}
```

---

## Ejecución del Programa:

Supongamos que los conjuntos son:
- **Conjunto A**: {1, 2, 3, 4}
- **Conjunto B**: {3, 4, 5, 6}

Los resultados de las operaciones serían:

- **Unión de A y B**: {1, 2, 3, 4, 5, 6}
- **Intersección de A y B**: {3, 4}
- **Diferencia A - B**: {1, 2}
- **Diferencia Simétrica A Δ B**: {1, 2, 5, 6}
--------------------------
# Conjunto de Operaciones en C# (Listas Dinámicas)

Este programa implementa una clase `CConjunto` que permite realizar operaciones entre conjuntos como la unión, intersección, diferencia, y diferencia simétrica utilizando **listas dinámicas** en lugar de arreglos estáticos.

## Estructura de la Clase

### CConjunto

- **Atributos:**
  - `aElementos`: Una lista dinámica de enteros (`List<int>`) que representa los elementos del conjunto.

- **Constructores:**
  - `CConjunto()`: Constructor vacío que inicializa el conjunto como una lista vacía.
  - `CConjunto(int[] pElementos)`: Constructor que recibe un arreglo de enteros e inserta los elementos en el conjunto evitando duplicados.

- **Métodos:**
  - `insertar(int elemento)`: Inserta un elemento en el conjunto si no existe previamente.
  - `union(CConjunto otro)`: Retorna un nuevo conjunto con la unión de dos conjuntos.
  - `interseccion(CConjunto otro)`: Retorna un nuevo conjunto con la intersección de dos conjuntos.
  - `diferencia(CConjunto otro)`: Retorna un nuevo conjunto con la diferencia de dos conjuntos.
  - `diferenciaSimetrica(CConjunto otro)`: Retorna un nuevo conjunto con la diferencia simétrica de dos conjuntos.
  - `mostrarConjunto()`: Muestra los elementos del conjunto en la consola.

---

## Ejecución del Programa

```csharp
using System;
using System.Collections.Generic;

class CConjunto
{
    private List<int> aElementos;

    // Constructor vacío
    public CConjunto()
    {
        aElementos = new List<int>();
    }

    // Constructor que recibe un arreglo de enteros
    public CConjunto(int[] pElementos)
    {
        aElementos = new List<int>();
        foreach (var elem in pElementos)
        {
            insertar(elem);
        }
    }

    // Método para insertar un elemento en el conjunto
    public void insertar(int elemento)
    {
        if (!aElementos.Contains(elemento))
        {
            aElementos.Add(elemento);
        }
    }

    // Método para la unión de dos conjuntos
    public CConjunto union(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        foreach (var elem in aElementos)
        {
            resultado.insertar(elem);
        }
        foreach (var elem in otro.aElementos)
        {
            resultado.insertar(elem);
        }
        return resultado;
    }

    // Método para la intersección de dos conjuntos
    public CConjunto interseccion(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        foreach (var elem in aElementos)
        {
            if (otro.aElementos.Contains(elem))
            {
                resultado.insertar(elem);
            }
        }
        return resultado;
    }

    // Método para la diferencia de dos conjuntos
    public CConjunto diferencia(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();
        foreach (var elem in aElementos)
        {
            if (!otro.aElementos.Contains(elem))
            {
                resultado.insertar(elem);
            }
        }
        return resultado;
    }

    // Método para la diferencia simétrica de dos conjuntos
    public CConjunto diferenciaSimetrica(CConjunto otro)
    {
        CConjunto resultado = new CConjunto();

        // Elementos en A pero no en B
        foreach (var elem in aElementos)
        {
            if (!otro.aElementos.Contains(elem))
            {
                resultado.insertar(elem);
            }
        }

        // Elementos en B pero no en A
        foreach (var elem in otro.aElementos)
        {
            if (!aElementos.Contains(elem))
            {
                resultado.insertar(elem);
            }
        }

        return resultado;
    }

    // Método para mostrar el conjunto
    public void mostrarConjunto()
    {
        foreach (var elem in aElementos)
        {
            Console.Write(elem + " ");
        }
        Console.WriteLine();
    }
}

class Program
{
    static void Main(string[] args)
    {
        int[] A = { 3, 6, 4, 1, 2 };
        CConjunto C1 = new CConjunto(A);

        int[] B = { 1, 2, 5, 7, 6 };
        CConjunto C2 = new CConjunto(B);

        Console.WriteLine("Conjunto A: ");
        C1.mostrarConjunto();

        Console.WriteLine("Conjunto B: ");
        C2.mostrarConjunto();

        // Unión
        CConjunto union = C1.union(C2);
        Console.WriteLine("Unión de A y B: ");
        union.mostrarConjunto();

        // Intersección
        CConjunto interseccion = C1.interseccion(C2);
        Console.WriteLine("Intersección de A y B: ");
        interseccion.mostrarConjunto();

        // Diferencia
        CConjunto diferencia = C1.diferencia(C2);
        Console.WriteLine("Diferencia A - B: ");
        diferencia.mostrarConjunto();

        // Diferencia Simétrica
        CConjunto diferenciaSimetrica = C1.diferenciaSimetrica(C2);
        Console.WriteLine("Diferencia Simétrica A Δ B: ");
        diferenciaSimetrica.mostrarConjunto();

        // Evitar cierre inmediato de la consola
        Console.ReadKey();
    }
}
```

---

## Ejecución del Programa:

Supongamos que los conjuntos son:
- **Conjunto A**: {3, 6, 4, 1, 2}
- **Conjunto B**: {1, 2, 5, 7, 6}

Los resultados de las operaciones serían:

- **Unión de A y B**: {3, 6, 4, 1, 2, 5, 7}
- **Intersección de A y B**: {1, 2, 6}
- **Diferencia A - B**: {3, 4}
- **Diferencia Simétrica A Δ B**: {3, 4, 5, 7}
------------------------
# Añada la clase CAdministrativo que considere nombres, DNI, código y area de trabajo e integre esta clase al trabajo definido en polimorfismo para alumnos y docenes.



```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppHerencia
{
    internal class Program
    {
        public static void mostrarDatos(CPersona persona)
        {
            persona.mostrar();  // Polimorfismo en acción
        }

        static void Main(string[] args)
        {
            // Crear instancias de cada tipo
            CAlumno a1 = new CAlumno("Waldo alumno Ibarra", "8888888", "Informatica", "codigo info");
            CDocente d1 = new CDocente("Waldo DOCENTE Ibarra", "DDDDDDNI", "Departamento Informatica", "codigo docente");
            CAdministrativo t1 = new CAdministrativo("Waldo TRABAJADOR ADMINISTRATIVO Ibarra", "DDDDDDNI", "CENTRO DE COMPUTO", "codigo ADMINISTRATIVO");

            // Mostrar los datos de cada instancia
            Console.WriteLine("Datos de cada persona sin polimorfismo:");
            a1.mostrar();
            d1.mostrar();
            t1.mostrar();

            // Ejemplo de polimorfismo con asignación de referencias
            Console.WriteLine("\nDatos mostrados con polimorfismo:");
            CPersona p1 = a1; // Referencia a CAlumno
            CPersona p2 = d1; // Referencia a CDocente
            CPersona p3 = t1; // Referencia a CAdministrativo

            p1.mostrar();
            p2.mostrar();
            p3.mostrar();

            // Segundo ejemplo de polimorfismo usando método mostrarDatos
            Console.WriteLine("\nSegundo ejemplo de polimorfismo con método mostrarDatos:");
            mostrarDatos(a1); // Polimorfismo en acción
            mostrarDatos(d1); // Polimorfismo en acción
            mostrarDatos(t1); // Polimorfismo en acción

            Console.ReadKey();
        }
    }
}
```

- La clase ``CAdministrativo`` que ya has definido es la siguiente: 
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AppHerencia
{
    internal class CAdministrativo : CPersona
    {
        /* ******************    ATRIBUTOS    ************** */
        private string aCodigo;
        private string aArea;

        /* ******************     METODOS     ************** */
        /* ================= Constructores ================= */
        public CAdministrativo() : base()
        {
            aCodigo = "";
            aArea = "";
        }

        /* -------------------------------------------------*/
        public CAdministrativo(string pNombres, string pDNI, string pCodigo, string pArea) : base(pNombres, pDNI)
        {
            aCodigo = pCodigo;
            aArea = pArea;
        }

        /* ================= Modificadores ================= */
        public void modificarCodigo(string pCodigo)
        {
            aCodigo = pCodigo;
        }

        /* -------------------------------------------------*/
        public void modificarArea(string pArea)
        {
            aArea = pArea;
        }

        /* =================   Selectores  ================= */
        public string codigo()
        {
            return aCodigo;
        }

        /* -------------------------------------------------*/
        public string area()
        {
            return aArea;
        }

        /* ================  Otros Métodos  ================ */
        public new string ToString()
        {
            return aNombres + " - " + aDNI + " - " + aCodigo + " - " + aArea;
        }

        /* -------------------------------------------------*/
        public new bool Equals(Object pCodigo)
        {
            return aCodigo.Equals(pCodigo.ToString());
        }

        /* -------------------------------------------------*/
        public override void mostrar()
        {
            Console.WriteLine();
            Console.WriteLine("Datos del TRABAJADOR ADMINISTRATIVO");
            Console.WriteLine("====================================");
            Console.WriteLine("Nombres   : " + aNombres);
            Console.WriteLine("DNI       : " + aDNI);
            Console.WriteLine("Código    : " + aCodigo);
            Console.WriteLine("Área      : " + aArea);
        }
    }
}
```
-------------
### Atributos
- **aCodigo y aArea**: Estos atributos almacenan el código y el área de trabajo del trabajador administrativo.

### Métodos modificadores
- **modificarCodigo y modificarArea**: Permiten modificar el código y el área de trabajo del trabajador administrativo.

### Métodos selectores
- **codigo y area**: Devuelven el código y el área de trabajo, respectivamente.

### ToString()
- Retorna una cadena que concatena los atributos de la clase, combinando los valores de `aNombres`, `aDNI`, `aCodigo` y `aArea`.

### Equals()
- Compara el código del trabajador administrativo con otro objeto para verificar si son equivalentes.

### mostrar()
- Sobrescribe el método `mostrar()` de la clase `CPersona` para mostrar los datos específicos del trabajador administrativo, incluyendo nombre, DNI, código y área de trabajo.

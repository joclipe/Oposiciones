

# INTRODUCCIÓN

El corazón de cualquier programa informático reside en su capacidad para manipular y transformar datos. Estos datos pueden representar infinidad de cosas según el contexto: desde las notas de estudiantes en una aplicación educativa hasta los movimientos financieros en una app bancaria. Mientras el programa está en ejecución, la información se guarda en memoria RAM mediante variables, lo cual permite realizar operaciones sobre ella. Sin embargo, cuando el programa se cierra, estos datos desaparecen, lo que no es útil si se desea mantener registros permanentes.

Piensa en una empresa que necesita registrar diariamente los pedidos de sus clientes. Si los datos se perdieran cada vez que se apaga el sistema, el negocio simplemente no podría funcionar. Por esta razón, surge la necesidad de almacenar la información en archivos ubicados en soportes externos como discos duros o memorias USB.

La forma más directa y estandarizada de hacerlo es mediante el uso del sistema de archivos que proporciona el sistema operativo. Este sistema permite guardar datos en dispositivos de almacenamiento de manera estructurada y persistente. Java nos brinda herramientas muy útiles para trabajar con archivos gracias al paquete `java.io`. En esta unidad veremos cómo crear, leer, modificar y eliminar archivos y carpetas, y también cómo almacenar objetos completos mediante serialización.

---

# GESTIÓN DE ARCHIVOS

Los sistemas operativos modernos ofrecen interfaces gráficas y de línea de comandos para gestionar archivos. A pesar de que los mecanismos internos pueden variar entre distintos dispositivos (por ejemplo, discos magnéticos frente a memorias sólidas), la forma de representar los archivos suele seguir una estructura jerárquica basada en carpetas y subcarpetas.

Desde el mundo laboral, pensemos en un diseñador que organiza sus proyectos por cliente y dentro de cada carpeta guarda imágenes, diseños y documentos. Un programa que automatice la generación de informes o el respaldo de estos archivos debería poder navegar por estas estructuras y acceder a cada fichero. Es aquí donde entra en juego la posibilidad de gestionar archivos desde el propio código Java.

Java incluye clases como `File` que permiten manipular archivos directamente desde el programa. Los exploradores de archivos como el de Windows o Mac no son más que programas que utilizan estas mismas capacidades, solo que con una interfaz visual.

---

# LA CLASE `File`

La clase `File` del paquete `java.io` es la herramienta fundamental para interactuar con archivos y directorios. No representa directamente el contenido del archivo, sino su ruta dentro del sistema.

```java
import java.io.File;
File archivo = new File("ruta/del/archivo.txt");
```

Este objeto puede representar un archivo o una carpeta, exista o no. Por ejemplo, si en una oficina se quiere guardar un reporte mensual en `C:/Reportes/Junio/ventas.txt`, podemos usar `File` para verificar si la carpeta existe, crearla si no, y luego guardar el archivo.

### Consideraciones sobre las rutas

- En Windows, las rutas suelen empezar con una letra de unidad: `C:\`, `D:\`, etc.
- En Unix/Linux, comienzan con `/`.

Java permite usar `/` como separador en cualquier sistema operativo, lo que facilita escribir código más portable.

## Ejemplo:

```java
File carpeta = new File("/home/user/Proyectos");
File archivo = new File("/home/user/Proyectos/informe.txt");
```

Para representar varias ubicaciones se deben crear varios objetos `File`.

---

# RUTAS ABSOLUTAS Y RELATIVAS

- **Ruta absoluta**: especifica la localización completa del archivo desde la raíz del sistema de archivos.

  - Ejemplo en Windows: `C:/Documentos/Finanzas/enero.xlsx`
  - Ejemplo en Unix: `/usr/local/datos/config.ini`

- **Ruta relativa**: se basa en el directorio de trabajo actual del programa.

  - Ejemplo: `datos/clientes.csv`

Supongamos que una consultora financiera comparte una aplicación de gestión de clientes. Si el programa usa rutas absolutas, todos los usuarios tendrán que tener las mismas carpetas en su sistema. Con rutas relativas, basta con mantener la misma estructura dentro del proyecto, facilitando la distribución.

## Ejemplo:

```java
File f = new File("reportes/enero/ventas.txt");
```

Dependiendo del lugar desde el que se ejecuta el programa, esa ruta puede apuntar a diferentes ubicaciones físicas.

---

# MÉTODOS DE LA CLASE `File`

## Información de la ruta

- `getParent()` → Devuelve la carpeta contenedora.
- `getName()` → Devuelve el nombre del archivo o carpeta.
- `getAbsolutePath()` → Devuelve la ruta completa.

```java
File f = new File("datos/clientes.csv");
System.out.println(f.getParent());
System.out.println(f.getName());
System.out.println(f.getAbsolutePath());
```

## Verificaciones

- `exists()` → Comprueba si el archivo o carpeta existe.
- `isFile()` → Verifica si es un archivo.
- `isDirectory()` → Verifica si es un directorio.

```java
if (f.exists()) {
    if (f.isFile()) System.out.println("Es un archivo");
    if (f.isDirectory()) System.out.println("Es una carpeta");
} else {
    System.out.println("No existe");
}
```

Esto puede servir, por ejemplo, en un software de logística para validar si existe el directorio donde se deben guardar los registros de envíos.

---

# PROPIEDADES DE LOS ARCHIVOS

- `length()` → Devuelve el tamaño en bytes.
- `lastModified()` → Retorna la fecha de última modificación (en milisegundos desde 1970).

### Ejemplo:

```java
File f = new File("backup.txt");
System.out.println("Tamaño: " + f.length());
System.out.println("Modificado: " + new Date(f.lastModified()));
```

Un departamento de IT puede usar este código para verificar cuándo fue la última vez que se actualizó una copia de seguridad.

---

# CONCLUSIÓN

Trabajar con archivos es una necesidad habitual en el desarrollo de software, especialmente en entornos profesionales donde la persistencia de la información es clave. Java, mediante su clase `File`, nos brinda un conjunto potente y flexible de herramientas para acceder al sistema de archivos, independientemente del sistema operativo. Desde aplicaciones de gestión empresarial hasta sistemas de respaldo automático, comprender y utilizar estas herramientas permite desarrollar soluciones robustas y escalables.


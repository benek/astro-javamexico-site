---
title: "Mejoras a partir de Java 5 y 6"
description: Probablemente habrá alguien que no haya notado todas las bondades que nos brindan las nuevas versiones de Java 5 y 6.
pubDatetime: 2007-09-03T16:46:25Z
tags:
  - java
draft: false
---
Probablemente habrá alguien que no haya notado todas las bondades que nos brindan las nuevas versiones de Java 5 y 6.

Es el motivo por el cual hago la siguiente recopilación.

**Java 5** **Lanzado en:** Tercer trimestre de 2mil4

**Características del Java 5** El principal objetivo de esta versión JDK 5 es la facilidad de desarrollo con las nuevas características como tipos de datos genéricos, el loop for-each, autoboxing/unboxing, enums, varargs, static imports y anotaciones.

El JDK 5 está diseñado para hacer que los programas se estructuren de manera más ordenada, más corta y fortificando la seguridad. Además, proporciona un soporte lingüístico para idiomas comunes.

El objetivo de este artículo es entender fácilmente JDK 5, para así empezarlo a usar en nuestro desarrollo. Veamos las diferentes características de la 5.0.

**Tipos genéricos, For-Each y Autoboxing/unboxing** Quizá la mejora más significante que tiene el lenguaje Java sea la introducción de los tipos genéricos. Ya no será necesario hacer castings de objetos para subir o bajar en la jerarquía de Clases.

*Continúa...* Los tipos genéricos nos permiten especificar el tipo de elemento de un Collection en tiempo de compilación. En lugar de especificar una lista, especificamos su contenido, por ejemplo: Double.

El siguiente código usa la nueva sintaxis del For-each para iterar a través de una Lista llamada “todo” que no es más que una lista de Double. Notemos que no hay necesidad de hacer casting y el for es muy fácil de leer:

```java
public double sumar(Collection todo) {
    double total = 0;
    for (Double i : todo) {
        total += i;
    }
    return total;
}
```

Una pregunta que se ha escuchado bastante es Porqué ":" en lugar de "in". La respuesta es que "in" ya es una palabra usada (por ejemplo, System.in) y además porque no se quiso introducir una palabra reservada más. La única palabra nueva en el JDK 5 es "enum".

Autoboxing: conversión automática de int a Integer.

Unboxing: conversión automática de Integer a int.

Por ejemplo, podemos fácilmente hacer lo siguiente:

```java
Integer i = new Integer(5);
Map map = new HashMap();
map.put("result", i + 1);
```

Notemos que el tipo Integer es convertido a int para la suma, y luego es vuelto a convertir a Integer cuando se introduzca al Map.

**¿Cuándo usar los tipos de datos genéricos?** Toda vez que sea posible, al menos que tengamos que ejecutar nuestra aplicación en máquinas virtuales anteriores a la 5.0. Usando los tipos de datos genéricos mejoraremos la claridad en el código y evitaremos problemas con los tipos de datos.

**¿Cuándo usar el For-each?** Toda vez que sea posible, porque realmente hace el código más legible. Quizás este sea el menor cambio que trae el 5.0 pero es uno de lo favoritos. Podemos usar for-each en los siguientes casos:

Eliminar elementos mientras recorremos un Collection.
Modificar la posición actual en un arreglo o lista.
Iterar en múltiples Collections o arrays.

**¿Cuando usar autoboxing?** Cuando hay una incompatibilidad entre las tipos de referencia y los datos primitivos. Aunque esto no es apropiado para cálculos científicos. Un Integer no es un substituto para un int. El autoboxing y unboxing simplemente ocultan las diferencias entre los wrappers y los datos primitivos.

**Enumerated Types (enums)** Un enumerated type es un tipo de dato que contiene un conjunto de valores constantes.

JDK 5 incluye soporte lingüístico para los tipos de datos enumerados. Las características avanzadas de la OO incluyen la capacidad de agregar los métodos y campos a los enums. Esto es más ordenado, más seguro y más potente que las alternativas existentes.

enum Season (WINTER, SPRING, SUMMER, FALL)

Enums son Comparable y Serializables. Las constantes de Enum deberían ser nombradas de manera similar que las constantes. Enums son básicamente un nuevo tipo de Clase. Hasta el momento no he usado Enums en mi código, es que todavía no pienso cómo debería usarlo. Quizás los desarrolladores de frameworks lo encontrarán útil.

**¿Cuando debería usar Enums?** Tipos de enumerados naturales: días de la semana, fases de la luna, estaciones.
Otros conjuntos donde sepamos todos los valores posibles: opciones de un menú, etc.
Como reemplazo de los flags (EnumSet)

**Static Imports** Los programadores pueden usar las variables y métodos estáticos con el nombre de la Clase (Math.PI). Para evitar eso, algunos programadores colocan las constantes en una interface y lo implementan, lo cual está mal (Constant Interface Antipattern). Ellos han cometido este error en el JDK, el java.util.jar tiene este patrón. Los Static imports permiten acceso a los miembros estáticos extendiendo el tipo. Todos los campos estáticos, métodos, etc. estarán disponibles para nuestra Clase usando los static imports. Por ejemplo:

```java
import static java.lang.Math.*;

...
r = cos(PI * theta);
```

**¿Cuándo debería usar los Static imports?** Con moderación, el empleo excesivo hace al programa inelegible.

Solo usarlo cuando se tienda a abusar de la herencia.

**Varargs** Los Varargs son métodos que reciben un número arbitrario de argumentos que Ud. requiere para crear un arreglo. Varargs automatiza y oculta el proceso. James Gosling contribuyó con la sintaxis de los 3 puntos (...). Varargs siempre tiene que ser el último parámetro. MessageFormat.format ha sido mejorado con varargs en el JDK 5:

```java
public static String format(String pattern, Object... arguments);

String result = MessageFormat.format("At {1,time} on {1,date}, there was {2} on planet " + "{0,number,integer}.", 7, new Date(), "a disturbance in the Force");
```

**¿Cuándo usar Varargs?** Si está diseñando su propio API, se recomienda usarlo con moderación.
Sólo cuando el beneficio es convincente. No sobrecargue un método varargs.
En clientes, cuando el API los soporta: reflection, message formatting, printf.

**Metadata** El Java 5 ahora soporta la inclusión de metadata relacionada a las Clases Java, interfaces, campos y métodos. Las herramientas de desarrollo son lo que usarán el soporte de esta metadata para la inserción automática de código fuente adicional, para debug, y para la creación y modificación de archivos XML externos.

Formato Original: http://javamexico.blogspot.com/2007/04/lo-nuevo-del-java-50.html

::::::::

**Java 6** **Lanzado en:** Diciembre de 2mil6

**Características del Java 6** Las aplicaciones Java se ejecutan más rápidamente sobre la versión 6 de la plataforma, al tiempo que se integran de una forma más coherente con las características de cada sistema operativo en particular, especialmente en Windows, Linux y Solaris. Se trata, además, de la primera versión de Java preparada para operar sobre el nuevo Windows Vista. De cara a los programadores, el JDK para Java SE 6 incorpora un servidor web de desarrollo, que facilita la comprobación de aplicaciones de servidor sin necesidad de recurrir a la plataforma J2EE, así como todo lo necesario para implementar servicios web.

**Interfaces de usuario** En este sentido, esta revisión 6 incorpora un numeroso abanico de mejoras que, si bien pueden considerarse, en su mayor parte, como pequeños avances, en conjunto contribuirán a facilitar considerablemente el trabajo del programador.

En el AWT existen dos nuevas clases, llamadas SystemTray y TrayIcon, que hacen posible colocar en el área de notificaciones de la barra de tareas iconos con menús asociados, algo muy habitual en Windows y que también resulta posible en escritorios como KDE y Gnome.

La primera clase cuenta con un método que los programas deben utilizar para saber si existe o no la barra de tareas, o un elemento de interfaz equivalente, utilizando la segunda para agregar su icono de aplicación. Los componentes Swing de Java 6 han sido rediseñados para, al funcionar sobre Windows XP y Windows Vista, efectuar el rendering de los componentes a través del API de UxTheme, conocida por ser la base de WindowsBlinds.

El resultado es que **las interfaces diseñadas con Java 6 se comportan en Windows Vista como lo harían las nativas**, algo que no ocurría con versiones previas. Además del rendimiento, que se ha incrementado de forma que las interfaces de Java ya no aparentan ser lentas respecto a las nativas al actualizar su interfaz de usuario, también se ha mejorado la visualización del texto en pantallas tipo LCD, haciendo más cómoda la lectura. Para ello, se utiliza una técnica basada en subpíxeles, similar a la conocida ClearType de Microsoft, disponible en todos los sistemas sobre los que se ejecuta esta plataforma sin necesidad de que el programador la active explícitamente.

Otra novedad interesante es la denominada Desktop API, un conjunto de métodos y acciones que permiten a las aplicaciones Java interactuar con servicios de escritorio del sistema operativo subyacente para, por ejemplo, lanzar la ejecución del programa asociado con un determinado tipo de archivo, abrir el navegador por defecto para ir a un cierto lugar o enviar un trabajo de impresión. Además de las ya mencionadas, existen otras novedades relativas a interfaces de usuario, como la posibilidad de mostrar una ventana de tipo splash mientras se inicializa la máquina virtual y se carga la aplicación, un conjunto nuevo de opciones a la hora de mostrar ventanas modales o un notable incremento en el rendimiento de las clases que efectúan entrada/salida de archivos gráficos.

**Web y bases de datos** Hasta la versión previa de la plataforma Java, si se precisaba desarrollar servicios web, había que recurrir a la edición empresarial Java EE (Enterprise Edition). La nueva iteración, por el contrario, nos permite crear tanto servicios web como consumidores de dichos servicios, para lo cual incorpora JAX-WS 2.0 (Java API for XML Web Services).

La designación de una clase como servicio web se efectúa mediante anotaciones Java (Java annotations), una técnica similar a los atributos que se utilizan en la plataforma Microsoft .NET, tras lo cual es preciso utilizar una herramienta que se encarga de generar, a partir de las anotaciones y el código de la clase, todos los elementos precisos para publicar un servicio web, incluyendo la descripción WSDL (Web Services Description Language), que es el estándar a la hora de informar a los potenciales consumidores sobre las características del servicio que se ofrece.

La depuración de este tipo de proyectos se ve simplificada gracias a la inclusión de un servidor web de desarrollo en la propia plataforma, una posibilidad que ya existía en otros productos, de forma que no es imprescindible contar con una instalación de Apache o IIS, los dos servidores HTTP más usuales, para comprobar el funcionamiento del servicio web. Asimismo, el consumo de los servicios se ve en gran medida automatizado gracias a una herramienta que, partiendo de la descripción WSDL, genera los módulos de código apropiados para acceder a ellos como si fuesen objetos locales. En cuanto al trabajo con bases de datos se refiere, aparte de una renovada versión de JDBC, el mecanismo estándar en Java para acceder a servidores de datos, Java SE 6 incluye la nueva Java DB.

Programada completamente en Java y desarrollada en la Fundación Apache bajo la denominación Derby, se caracteriza principalmente por su reducido tamaño, apenas de 2 Mbytes, ofreciendo, sin embargo, servicios similares a cualquier RDBMS, incluyendo el estándar SQL y el uso de transacciones. Lo que ha hecho Sun es crear a partir de Apache Derby una versión a medida para Java SE 6, siendo el resultado Java DB.

Java DB puede ser instalada a través de una interfaz web sin ninguna intervención por parte del usuario final, resultando también una solución adecuada para aplicaciones que han de ejecutarse en entornos con recursos reducidos, como PDA, teléfonos móviles de última generación y, en general, todo tipo de dispositivos que utilicen J2ME (Java 2 Micro Edition). La licencia Apache con que se distribuye Java DB permite su uso libre por parte de empresas y organizaciones.

**Integración con lenguajes de script** El uso de lenguajes de guiones o script no es algo nuevo, pero en los últimos tiempos su uso está extendiéndose, ya que cuentan con múltiples ventajas cuando se aplican en ámbitos concretos, como la creación rápida de prototipos, dado su carácter dinámico, sin comprobación estricta de tipos y relativa sencillez. Hasta el momento, no existía un mecanismo que permitiese acceder desde un guión, desde código escrito en un lenguaje de script, a objetos alojados en módulos de clases Java.

Esto impedía, por ejemplo, generar contenido web en un servidor Java directamente desde un guión, siendo preciso utilizar código en este lenguaje previamente compilado. Estas posibilidades se han implementando en la versión 6 gracias a una API abierta basada en la especificación JSR 223, que también hace posible embeber motores de scripting dentro de aplicaciones Java.

En principio, utilizando la mencionada API JSR 223, sería posible incorporar a la nueva plataforma cualquier motor de ejecución de guiones, sin importar el lenguaje. Por defecto se incluye el motor Mozilla Rhino, que permite emplear el lenguaje JavaScript dentro de aplicaciones escritas en Java. Cada motor aparece para las aplicaciones Java como un objeto ScriptEngine, a través del cual es posible evaluar dinámicamente sentencias en el lenguaje de script que corresponda.

**Puntos finales** Con esta versión para entornos de escritorio, Sun ha dado un paso en la mejora de la experiencia de los usuarios al incrementar la integración con las características de cada sistema en particular y al aumentar el rendimiento de ejecución de las aplicaciones, dos factores que históricamente han sido sus obstáculos frente a otras soluciones, en equipos de escritorio.

También es destacable que ciertos elementos de la edición empresarial de Java, como los relacionados con el desarrollo de servicios web, se hayan traslado a la versión de escritorio que nos ocupa.
El SDK para Java SE 6 puede obtenerse opcionalmente con NetBeans 5.5, un entorno muy recomendable y cuyas nuevas características le permitirán competir mejor con Eclipse, el rey de los entornos para Java.

**Formato Original:** http://www.pc-actual.com/Laboratorio/Productos/Inform%C3%A1tica_personal/Software/20070531026

**Más características de Java 6** * Desarrollo más abierto, colaboraron 330 personas externas y unas 160 compañías.
* Mejoras de apariencia en Windows y GTK.
* Doble búffer, para que no salga el rectángulo gris al restaurar a primer plano.
* Ahora el arrastrar y soltar (drag&drop) en Swing es más fácil de programar.
* Ya puedes incluir cualquier cosa en las pestañas, no sólo icono y/o texto.
* El formato del caché interno ha cambiado, los programas que lo usaban fallarán.
* En rendimiento ahora supera a todas las máquinas de la competencia.
* Nueva clase Console y método para leer una contraseña sin que ésta se muestre.
* Métodos de File para saber el espacio libre del disco, y para cambiar permisos.
* Apache Derby, una base relacional de datos implementada enteramente en Java.
* Las pantallas y diálogos de Java Web Start y Java Plug-in han mejorado.
* Cambios en Collections: linkedList implementa la interfaz Deque, la cola doble. El nuevo ArrayDeque implementa un array que cambia de tamaño eficientemente. TreeSet y TreeMap ahora implementan NavigableSet y NavigableMap, que incluyen ahora métodos para recorrerlos en ambos sentidos, en lugar de usar SortedMap. Eficientes métodos copyOf y copyOfRange de Array para para manipular subarrays
* Mejoras en la presentación de texto que lo igualan al de cada plataforma
* Nueva API que soporta la normalización de texto internacional Unicode.
* Mejoras de escritorio en AWT, como pantalla de "splash" al iniciar programas. Corrección de la entrada por teclado de caracteres no ingleses en Linux. Ahora una aplicación puede ser añadida al panel o barra de tareas.
* Soporte para firefox de Java Plug-in y Java Web Start.
* Java en Linux ahora no requiere que cambies el PATH.
* El programa gráfico para monitorizar rendimiento JConsole ya es oficial.
* Nuevas clases de red que encapsulan direcciones IP, MAC, subredes, etc.
* La parte de red ya soporta nombres de dominio internacionales.
* Gestor de Cookies ahora implementado por defecto, antes sólo era interfaz.
* Nuevos paquetes que permiten crear un servidor HTTP ligero para tus programas.
* Métodos de "reflection" genéricos, deben hacerse cambios o avisará al compilar.
* Nuevos flujos que comprimen y descomprimen datos automáticamente.
* Mejoras en las limitaciones de la implementación de los ficheros Jar y Zip.
* Especificación y API que permitirá a lenguajes de script interoperar con java. Incluye el motor Rhino, de Mozilla, una implementación de Javascript en Java.
* Mejor depuración, puede iniciarse un depurador en tiempo de ejecución.

Espero que les sea de utilidad.

---
title: "Threads en Java"
description: Hola chavos, disculpen que no habia posteado, pero he andado super ocupado con un proyecto y no habia podido entrar...
pubDatetime: 2007-09-03T16:46:25Z
tags:
  - java
draft: false
---
Hola chavos, disculpen que no habia posteado, pero he andado super ocupado con un proyecto y no habia podido entrar...

Creo que me parece interesante postear sobre lo que estoy desarrollando, dentro del proyecto he aprendido un par de cosas que desconocia sobre nuestro hermoso lenguaje **JAVA**, una de ellas son los Threads, que normalmente no los usamos, pero me he dado cuenta que son totalmente utiles, y de hecho son la base de los procesos que estoy desarrollando.

Pues a los hechos... **¿Qué es un Thread?** La Máquina Virtual Java (JVM) es un sistema multi-thread. Es decir, es capaz de ejecutar varias secuencias de ejecución (programas) simultáneamente. La JVM gestiona todos los detalles, asignación de tiempos de ejecución, prioridades, etc, de forma similar a como gestiona un Sistema Operativo múltiples procesos. La diferencia básica entre un proceso de Sistema Operativo y un Thread Java es que los Threads corren dentro de la JVM, que es un proceso del Sistema Operativo y por tanto comparten todos los recursos, incluida la memoria y las variables y objetos allí definidos. A este tipo de procesos donde se comparte los recursos se les llama a veces 'procesos ligeros' (lightweight process).

Java da soporte al concepto de Thread desde el mismo lenguaje, con algunas clases e interfaces definidas en el [package java.lang](http://java.sun.com/j2se/1.4.2/docs/api/java/lang/Thread.html) y con métodos específicos para la manipulación de Threads en la clase Object.

Desde el punto de vista de las aplicaciones los threads son útiles porque permiten que el flujo del programa sea divido en dos o más partes, cada una ocupándose de alguna tarea. Por ejemplo un Thread puede encargarse de la comunicación con el usuario, mientras otros actuan en segundo plano, realizando la transmisión de un archivo, accediendo a recursos del sistema (cargar sonidos, leer archivos ...), etc. De hecho todos los programas con interface gráfico (AWT o Swing) son multithread porque los eventos y las rutinas de dibujado de las ventanas corren en un thread distinto al principal.

A continuacion les pongo un pequeño ejemplillo que pueden ejecutar desde su IDE favorito para que se den cuenta de como funcionan los threads...

**La Clase Thread** La forma más directa para hacer un programa multi-thread es extender la clase Thread, y redefinir el método run(). Este método es invocado cuando se inicia el thread (mediante una llamada al método start() de la clase thread). El thread se inicia con la llamada al método run y termina cuando termina éste. El ejemplo ilustra estas ideas:

public class ThreadEjemplo extends Thread {
public ThreadEjemplo(String str) {
super(str);
}
public void run() {
for (int i = 0; i < 10 ; i++)
System.out.println(i + " " + getName());
System.out.println("Termina thread " + getName());
}
public static void main (String [] args) {
new ThreadEjemplo("Pepe").start();
new ThreadEjemplo("Juan").start();
System.out.println("Termina thread main");
}
}

Compila y ejecuta el programa. La salida, será algo asi:

Termina thread main
0 Pepe
1 Pepe
2 Pepe
3 Pepe
0 Juan
4 Pepe

1 Juan
5 Pepe
2 Juan
6 Pepe
3 Juan
7 Pepe
4 Juan
8 Pepe

5 Juan
9 Pepe
6 Juan
Termina thread Pepe
7 Juan
8 Juan
9 Juan
Termina thread Juan

Ejecuta varias veces el programa. Verás que no siempre se ejecuta igual.

Esta es solo una de las 2 formas de implementar theads para sus aplicaciones, pero no siempre se puede utilizar ya que como todos sabemos solo podemos exender de 1 sola clase, y si la clase donde vamos a usar theads es una subclase de otra no podemos extender diectamente desde la clase **Thread**, por lo tanto necesitamos un metodo alternativo **La Interface Runnable** La interface Runnable proporciona un método alternativo a la utilización de la clase Thread, para los casos en los que no es posible hacer que nuestra clase extienda la clase Thread. En este caso nuestra clase debe implantar la interface Runnable, variando ligeramente la forma en que se crean e inician los nuevos threads.

El siguiente ejemplo es equivalente al del apartado anterior, pero utilizando la interface Runnable:

public class ThreadEjemplo implements Runnable {
public void run() {
for (int i = 0; i < 5 ; i++)
System.out.println(i + " " + Thread.currentThread().getName());
System.out.println("Termina thread " + Thread.currentThread().getName());

}
public static void main (String [] args) {
new Thread ( new ThreadEjemplo() , "Pepe").start();
new Thread ( new ThreadEjemplo() , "Juan").start();
System.out.println("Termina thread main");
}
}

Espero que con esto puedan empezar a trabajar con nuestros bellisimos y utiles threads, los cuales pueden resultar muy utiles a la hora de desarrollar aplicaciones que requieran de varias tareas simultaneas o repetitivas :D

Saludos...

**Mad**

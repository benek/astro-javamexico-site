---
title: "Haciendo un Pequeño Callback"
description: Bien ahora que tengo un poco de tiempo describiré que es y como funciona un Callback, que en pocas palabras es una técnica que consiste en crear un objeto y que el objeto creado obtenga una referencia de quien lo instanció y pueda enviarle una respuesta.
pubDatetime: 2007-09-03T16:46:25Z
tags:
  - java
draft: false
---
Bien ahora que tengo un poco de tiempo describiré que es y como funciona un Callback, que en pocas palabras es una técnica que consiste en crear un objeto y que el objeto creado obtenga una referencia de quien lo instanció y pueda enviarle una respuesta.

Más fácil, los callbacks permiten a un objeto A asignar una tarea a un objeto B, es entonces cuando el objeto B puede notificar al objeto A (de manera asincrónica) cuando la tarea es completada.

Con esto separamos muy bien las responsabilidades entre objetos y mejoramos el uso de recursos :-)

**Clase A - Cliente.java**

```java
package hss;

public class Cliente {

    Cliente() {
        Lanza lanza = new Lanza(this, 8);
        lanza.run();
    }

    public static void main(String args[]) {
        new Cliente();
    }


    public void lanzada() {
        System.out.println("Lanzada!!!");
    }

}
```

**Clase B - Lanza.java**

```java
package hss;

public class Lanza {

    int intervalo;
    Cliente cliente;

    Lanza(Cliente cliente, int intervalo) {
        this.intervalo = intervalo;
        this.cliente = cliente;
    }

    void run() {
        for (int i = 0; i < intervalo; i++) {
            cliente.lanzada();
        }
    }

}
```

Voy a explicarlo como si corriera en modo de debug, es decir tal cual es el flujo del programa.

**Cliente.java - Método main()**

```java
public static void main(String args[]) {
    new Cliente();
}
```

El método main por default es el primer método invocado, y crea una nueva instancia de la clase Cliente (crea una instancia de la misma clase en la que está)

**Cliente.java - Constructor default**

```java
Cliente() {

    Lanza lanza = new Lanza(this, 8);
```

Al ser instanciada la clase Cliente, el constructor por default es ejecutado, quien a su vez crea una nueva instancia de la clase Lanza y de nombre 'lanza', a quien le manda como parámetros 'this' (que es nuestro objeto Client actual, es como si se enviara él mismo) y un entero (8).

**Lanza.java - Constructor que recibe Cliente y entero**

```java
Lanza(Cliente cliente, int intervalo){
    this.intervalo = intervalo;
    this.cliente = cliente;
}
```

El constructor de Lanza es ejecutado, recibe el objeto Cliente enviado con 'this' desde el objeto Client y el número entero, luego los copia a el 'Cliente' e 'intervalo' locales.

**Cliente.java - Constructor default**

```java
lanza.run();
```

la ejecución regresa al objeto Cliente y continúa con la siguiente línea en donde ejecuta el método run() del objeto lanza instanciado.

**Lanza.java - Método run()**

```java
void run() {
    for (int i = 0; i < intervalo; i++) {
        cliente.lanzada();
    }
}
```

Se ejecuta el método run() y tomamos la variable 'intervalo' que ya había guardado el constructor para iterar el número de veces que le dijimos.

**Cliente.java - Método lanzada()**

```java
public void lanzada() {
    System.out.println("Lanzada!!!");
}
```

En cada iteración utilizamos el objeto Cliente que recibió el constructor para lanzar su método 'lanzada()' y reportar a Cliente que Lanza hizo ya lo que tenía que hacer, es aqui donde se realiza el Callback desde la clase instanciada hacia la clase que la instanció!

:::

Como verán, es un poco enredoso el seguimiento de un Callback, pero les sugiero que prueben el código en modo de debug en su IDE preferido para que lo vean correr paso a paso :-P

**Espero que esta técnica les sea de utilidad, saludos!**

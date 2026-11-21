---
title: "Usando SWT para crear interfaces gráficas (GUI)."
description: SWT es un framework para crear interfaces gráficas en Java (como Swing o Awt) que crea a través de JNI (Java Native Interface) interfaces gráficas nativas del Sistema Operativo en donde ejecutemos nuestra aplicación SWT.
pubDatetime: 2007-09-02T16:46:25Z
tags:
  - java
draft: false
---
**¿Qué es SWT?** SWT es un framework para crear interfaces gráficas en Java (como Swing o Awt) que crea a través de JNI (Java Native Interface) interfaces gráficas nativas del Sistema Operativo en donde ejecutemos nuestra aplicación SWT. Esto quiere decir que con el mismo código visualizaremos en cada Sistema Operativo nuestras ventanas como si hubieran sido creadas para ese SO en específico.

**Por ejemplo:** Windows
![](http://www.eclipse.org/swt/images/win-example.png) Linux/Gtk
![](http://www.eclipse.org/swt/images/lin-example.png) Mac OS X
![](http://www.eclipse.org/swt/images/mac-example.png) Motif
![](http://www.eclipse.org/swt/images/mot-example.png) Photon
![](http://www.eclipse.org/swt/images/pho-example.png) Ahora bien, enumeraré las que a mi parecer son las más visibles ventajas y desventajas de este framework.
**Ventajas:**

- \* Ya que crea nativamente la GUI dependiendo del SO, es más rápido que Swing
- \* Consume menos recursos
- \* La interfaz gráfica se verá como las demás aplicaciones de tu SO
- \* Está en constante desarrollo

*Continúa...* **Desventajas:**

- Muy escasa documentación
- Ya que SWT fue creado por la Fundación Eclipse y pensada para el desarrollo de Eclipse IDE, hay controles o widgets que no consideraron ya que Eclipse no los ocupa, aunque sigue en desarrollo.
- Se tiene que agregar la biblioteca al proyecto a desarrollar, no viene por default en las librerías de Java

**Algunas aplicaciones creadas con SWT:**

- Eclipse IDE (Quizá el más completo IDE para desarrollo en Java)
- Azureus (Uno de los más conocidos clientes torrent)

**Bien, ahora comencemos:** - Creemos un nuevo proyecto de Java en nuestro IDE preferido (para este tuto utilizaremos Eclipse IDE). El proyecto en este ejemplo se llamará ‘tests’
- Descarguemos SWT de http://www.eclipse.org/swt/ y lo dejamos dentro de nuestro proyecto..
- Importamos SWT al proyecto, en Eclipse IDE es en File/Import.. ![import](http://bnk.hackerss.com/import.jpg) - Luego en General elegimos ‘Existing proyect into Workspace’ ![existing](http://bnk.hackerss.com/existing_proyect.jpg) - Luego seleccionamos el zip que bajamos con swt y el nombre del proyecto ‘org.eclipse.swt’ ![SWT](http://bnk.hackerss.com/import_zip.jpg) - Ya tenemos SWT dentro de nuestro Workspace, ahora tenemos que agregarlo como dependencia de nuestro proyecto ‘tests’, entonces vamos a las propiedades de ‘tests’ (click derecho en tests/properties), luego damos click en Java Build Path, vamos a la pestaña de Projects y le damos ‘add..’ seleccionamos ‘org.eclipse.swt’, y luego OK y de nuevo OK. ![SWT](http://bnk.hackerss.com/javabuildpath.jpg) - Bien, ya tenemos nuestro proyecto listo para implementar SWT, ahora debemos saber algunos conocimientos teóricos.
SWT se compone de principales elementos, que interactúan entre ellos para lograr la interfaz nativa que tanto le caracteriza:

- JNI. Java Native Interface, es el primer y más bajo nivel, que interactúa directamente con el Sistema Operativo en el que estemos. En claro que cada SO necesita diferente configuración y librerías, pero JNI nos simplifica el trabajo para que todo lo escribamos de una sola manera y él se encarga de lo demás, así tenemos cumplida la visión de Java ‘write Once, run anywhere’
- Display. Esta clase de SWT es la responsable de traducir o comunicar la Clase Shell con el JNI.
- Shell. No chicos, no es ninguna shell que se pueda rootear! Shell es otra clase de SWT, que representa una ventana y quien es la responsable de administrar los widgets (componentes) que tendremos en la misma. Tendremos una instancia de la clase Shell por cada ventana en nuestro proyecto. Para poder instanciar la clase Shell debemos hacer referencia a un Display anteriormente instanciado.

**Ahora un poco de código para mover esto..** Así implementamos una nueva ventana vacía:

```java
package lol;

import org.eclipse.swt.widgets.Display;
import org.eclipse.swt.widgets.Shell;

public class testings {
    public static void main(String lol[]) {
        Display display = new Display();
        Shell shell = new Shell();
        shell.setText("javaMexico.org");
        shell.setVisible(true);
        shell.setSize(400, 300);
        shell.open();
        while (!shell.isDisposed()) {
            if (!display.readAndDispatch())
                display.sleep();
        }
        display.dispose();
    }
}
```

**Que es lo que hacemos ahi?**

```java
import org.eclipse.swt.widgets.Display;
import org.eclipse.swt.widgets.Shell;
```

Importamos las clases Display y Shell, imprescindibles en cualquier proyecto SWT.

```java
Display display = new Display();
Shell shell = new Shell();
```

Instanciamos un Display y después una Shell, a la que le asignamos la Display que creamos.

```java
shell.setText("javaMexico.org");
shell.setVisible(true);
shell.setSize(400, 300);
shell.open();
```

Como ya habíamos mencionado, ’shell’ es nuestra ventana, así que con ’setText’ definimos su título, con ’setVisible’ si queremos que sea mostrada, con ’setSize’ el tamaño y con ‘open’ la iniciamos.

```java
while (!shell.isDisposed()) {
    if (!display.readAndDispatch())
        display.sleep();
}
```

Este bucle while es muy importante, ya que es nuestro ‘manejador de eventos’, lo que hace es que una vez mostrada la ventana y si la misma no está ejecutando algún evento lanza un bucle que deja la ventana en espera (sleep) de otro evento venidero, así que está constantemente en escucha de algún otro evento que se dispare.

```java
display.dispose();
```

por último, liberamos la aplicación con dispose(), quien finaliza ‘display’ y todos los shells que ‘display’ contiene, esto solo ocurre cuando la ventana ha sido cerrada, cuando damos click en cerrar la ventana automáticamente el ciclo while no se cumple y salta al siguiente paso ‘display.dispose()’**Resultado:** ![ventanita](http://bnk.hackerss.com/ventanita.jpg) **Utilizando Widgets.** Bueno, iba a explicar detalladamente como poner widgets en layouts y algunos tips más, pero desde ayer interrumpí este tuto por cuestiones de trabajo, así que hice esta pequeña aplicación con una caja de texto, un botón y un listener que ejecutan una acción..

Aqui está el código, por favor examínenlo y vean la manera de implementar los widgets en el Grid(layout), y también chequen la acción que lleva a cabo el listener que le puse al botón.

```java
package lol;

import org.eclipse.swt.SWT;
import org.eclipse.swt.events.SelectionAdapter;
import org.eclipse.swt.events.SelectionEvent;
import org.eclipse.swt.layout.GridData;
import org.eclipse.swt.layout.GridLayout;
import org.eclipse.swt.widgets.Button;
import org.eclipse.swt.widgets.Display;
import org.eclipse.swt.widgets.Shell;
import org.eclipse.swt.widgets.Text;
import org.eclipse.swt.widgets.ToolTip;
import org.eclipse.swt.widgets.Tray;
import org.eclipse.swt.widgets.TrayItem;

/**
 * Clase que implementa SWT en la aplicación!
 *
 * @author jBenek
 * @version v1.0
 */
public class testings {
    /**
     * Método que crea una ventana con un widget Text y
     * <p>
     * un widget Button de SWT, y agrega un listener al
     * botón para desplegar un ToolTip en la bandeja del
     * sistema (Tray) con el texto introducido!
     *
     * @param lol - Arreglo de Strings por default del
     *            método main que guarda la entrada de datos al inicio
     *            de la ejecución del programa!
     */
    public static void main(String[] lol) {
        final Display display = new Display();
        final Shell shell = new Shell();
        shell.setText("Hackerss.com");
        shell.setVisible(true);
        GridLayout layout = new GridLayout();
        layout.numColumns = 4;
        shell.setLayout(layout);
        final Text texto = new Text(shell, SWT.BORDER);
        texto.setEditable(true);
        texto.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, true, true, 3, 1));
        final Button boton = new Button(shell, SWT.PUSH);
        boton.setText("Envia");
        boton.setLayoutData(new GridData(SWT.FILL, SWT.CENTER, true, true, 1, 1));
        SelectionAdapter sel = new SelectionAdapter() {
            public void widgetSelected(SelectionEvent e) {
                final ToolTip hssTip = new ToolTip(shell,
                        SWT.BALLOON | SWT.ICON_WORKING);
                hssTip.setMessage(texto.getText());
                Tray hssTray = display.getSystemTray();
                if (hssTray != null) {
                    TrayItem hssItem = new TrayItem(hssTray, SWT.NONE);
                    hssTip.setText("Hackerss.com :P");
                    hssItem.setToolTip(hssTip);
                    hssTip.setVisible(true);
                }
            }
        };
        boton.addSelectionListener(sel);
        shell.pack();
        shell.setSize(400, 100);
        shell.open();
        while (!shell.isDisposed()) {
            if (!display.readAndDispatch()) {
                display.sleep();
            }
        }
        display.dispose();
    }
}
```

Lo que muestra al iniciar la aplicación es esta ventanita:![app ok](http://bnk.hackerss.com/app_ok.jpg) y al dar click el listener ejecuta esta acción: ![tooltip](http://bnk.hackerss.com/tooltip.jpg) :::::::::::::::

Examínenlo y córranlo, cualquier duda pónganla aqui :-)

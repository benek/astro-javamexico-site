---
title: "Selenium Remote Control"
description: Es una herramienta para hacer test de las diversas funcionalidades que tenga tu aplicación vía web.
pubDatetime: 2007-09-03T16:46:25Z
tags:
  - java
draft: false
---
Es una herramienta para hacer test de las diversas funcionalidades que tenga tu aplicación vía web. En un principio se utilizaba el Selenium IDE que es un plugin que te permite grabar tus pruebas atraves de un plugin para Firefox y desde hace ya un tiempo se saco el Selenium Remote Control para que ejecutes tus test de forma automatica una vez que las hayas desarrollado todas en Java. Y es tan sencillo como lo siguiente:

```java
//Mi primer test_case

import com.thoughtworks.selenium.*;
import junit.framework.*;

public class Portal extends TestCase {
    private Selenium sel;

    public void setUp() {
        sel = new DefaultSelenium("localhost", 4444, "*firefox", "http:///");
        sel.start();
    }

    public void testPortal() throws Exception {
        sel.open("http://");
        sel.type("userId", "usuario");
        sel.type("password", "password");
        sel.click("Login");
        sel.waitForPageToLoad("30000");
    }

    public void tearDown() {
        sel.stop();
    }
}
```

Mandas correr tu cliente de selenium-remote-control y desde tu clase principal mandas llamas tu test_case. Algo asi te debe de quedar en tu clase principal

```java
//Clase Principal
public class selenium {
    public static void main(String[] args) {
// TODO, add your application code
        System.out.println("Empieza Test Edgar Ramirez!");
        try {
            Portal at = new Portal();
            at.setUp();
            at.testPortal();
            at.tearDown();
        } catch (Throwable e) {
            e.printStackTrace();
        }
    }
}
```

Mandalo correr y woala, tendras tu primer test_case.

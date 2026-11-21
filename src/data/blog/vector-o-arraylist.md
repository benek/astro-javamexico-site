---
title: "Vector o ArrayList"
description: Clase Vector o Clase ArrayList. ¿Qué es mejor usar en Java? ¿Un Vector o un ArrayList?
pubDatetime: 2007-09-03T16:46:25Z
tags:
  - java
draft: false
---
Clase Vector o Clase ArrayList
¿Qué es mejor usar en Java? ¿Un Vector o un ArrayList?

- Sincronización: La clase Vector es sincronizada (synchronized), por tanto, su contenido está protegido de otros hilos, es decir, es thread-safe([Wiki](http://es.wikipedia.org/wiki/Thread-Safety)).

Y al contrario, los ArrayList no son sincronizados y por tanto no son thread-safe. Hay que tener en cuanta esto porque los vectores tienen un coste en tiempo de ejecución que no tienen los ArrayList. Si no necesitas thead-safe, usa ArrayList.

- Tamaño de los datos:Ambas estructuras necesitan un Array para almacenar los datos internamente. Cuando se insertan datos, tanto unos como otros tienen que crecer para que no haya un desbordamiento. He aquí la diferencia:
  Los vectores crecen duplicando su espacio
  Los ArrayList crecen añadiendo el 50% de su espacio anterior.

:)

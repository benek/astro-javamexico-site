---
title: "ISO-8583 En Java"
description: Para inaugurar mi blog, hablaré de un proyecto de software libre que tengo, j8583, también conocido como Java-ISO8583.
pubDatetime: 2007-09-03T16:46:25Z
author: Enrique Zamudio
tags:
  - java
featured: true
draft: false
---
Para inaugurar mi blog, hablaré de un proyecto de software libre que tengo: [j8583](http://j8583.sourceforge.net/), también conocido como Java-ISO8583. Es una implementación semi-abstracta del protocolo transaccional de comunicación **ISO-8583**, que puede ser algo complicado y/o tedioso de implementar. **UPDATE:** [Aquí](http://j8583.sourceforge.net/desc8583es.html) he puesto una breve descripción en español.

ISO8583 es un protocolo transaccional de comunicación, muy utilizado en bancos, también se usa con puntos de venta (las terminales de tarjeta de crédito por ejemplo), y últimamente también se está usando para transaccionar con carriers de telefonía celular. No voy a entrar a detalle en el protocolo como tal. Se puede obtener (pagando) del sitio de ISO.

Para poder utilizar esta librería, se requiere conocer el protocolo en sí. Tiene licencia LGPL, de modo que se puede usar en aplicaciones comerciales cerradas; si hacen una aplicación que se redistribuye (software que venden, etc) solamente deben entregar los fuentes de la librería, junto con cualquier modificación que le hagan.

El paquete incluye ejemplos de una implementación de un cliente que envía y recibe mensajes de ISO8583, así como un server que recibe conexiones y atiende a varios clientes usando ISO8583. Se puede usar de modo binario o ASCII (lo más común).

La página del proyecto es http://github.com/chochos/j8583 y por supuesto http://j8583.sourceforge.net/

La documentación y la página las puse en inglés para no excluir a gente de otros países que puedan usar el proyecto. No he tenido tiempo de traducir nada (los javadoc de hecho no sabría cómo generarlos en español, fuera de tomar los HTML generados y traducirlos). La configuración de la fábrica de mensajes (la parte central de la librería) es bastante sencilla, a través de un archivo XML donde se definen plantillas para los tipos de mensaje que se van a crear, así como definiciones de los mensajes que se van a leer, indicando los campos esperados, con su longitud y tipo. De los campos indicados en las definiciones de respuestas, solamente se leen los que se indiquen en el bitmap de una respuesta. De esta manera, leer los mensajes ya es algo automático, todo el código para parseo de respuestas está en la fábrica de mensajes, no es necesario implementar algo adicional.

Los mensajes creados por la fábrica de mensajes son editables, pueden modificarse, agregarse o quitarse campos. La idea es que la fábrica genere nuevos mensajes ya con todos los valores fijos para el tipo de mensaje, y que solamente se tengan que asignar los valores que cambian. Incluso los dos valores que generalmente cambian, los campos 7 (fecha) y 11 (trace), se pueden asignar por la fábrica, poniendo la fecha actual a cada mensaje recién creado y usando un TraceNumberGenerator (una interfaz cuya implementación pueden proveer ustedes) para asignarle un trace en el campo 11 a cada mensaje generado.

Espero les sea de utilidad. Cualquier duda me pueden contactar directamente en SourceForge, registrando cualquier defecto que encuentren y poniendo ahí sus dudas.

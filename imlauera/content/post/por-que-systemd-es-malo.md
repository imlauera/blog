---
title: "Porque Systemd es malo para Linux"
date: 2022-11-02T08:38:19-03:00
categories: ['linux']
tags: ['systemd']
---
![systemd logo](/img/systemd.png)  

No es malo en sí, el problema es que es un monolito que sigue agregando utilidades que reemplazan el trabajo de otra herramienta. Debido a que es tan omnipresente, los desarrolladores de software comienzan a escribir aplicaciones que dependen de systemd en lugar de los estándares (o al menos convenciones que no son del todo estándares).

Por ejemplo, la gente comienza a escribir software usando temporizadores systemd en lugar de cronjobs, y ahora ya no es portátil en sistemas Unix, o incluso en distribuciones Linux, es solo compatible con Linux con systemd.

Tene en cuenta que cron o timers no tienen nada que ver con init. **Systemd no tiene la intención de ser un sistema de inicio, tiene la intención de ser el sistema completo eventualmente**.

Pero es malo porque quiere ser el nuevo estándar, y eso es malo para Linux porque se vuelve cada vez menos convencional para Unix y más propio, similar a Apple. El software systemd no está mal escrito y, por lo general, las personas que afirman que lo está no pueden señalar realmente una mala práctica de diseño de software.  El problema es que no es Unix, y las personas a las que les gusta Unix quieren Unix y no systemd.

Para aquellos que no tienen ningún apego a la forma Unix de hacer las cosas, o que nunca han usado algo que no sea Linux, todo esto no tiene sentido para ellos y las quejas parecen bastante tontas.

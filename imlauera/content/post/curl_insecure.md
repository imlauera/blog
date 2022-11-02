+++
title = "curl --insecure"
date = "2022-10-20"
description = "Cómo funciona curl insecure"
tags = [
    "curl",
]
categories = [
    "linux",
]
+++


```bash
curl --insecure
```

Si está intentando acceder a un sitio web a través de la URL https y curl le muestra que el certificado ha caducado o que no es de confianza.

¡Buenas noticias! Todavía puede anular este comportamiento ejecutando curl con la línea de comando --insecure.

Ejemplo:
```bash
curl --insecure https://imlauera.github.io
```

*ADVERTENCIA* ¡asegúrese de saber lo que está haciendo! esto es especialmente cierto para saber a qué sitio web está intentando acceder. Puede estar bien ignorar las advertencias de SSL para un entorno de desarrollo local en su computadora portátil o para acceder a URL internas en su infraestructura privada. Pero cualquier cosa en la Internet pública que le brinde una advertencia de SSL debe revisarse antes de que progrese.

Cómo funciona: curl --insecure deshabilitará las comprobaciones de certificados, pero aún cifrará el tráfico y descargará la URL https que proporcionó.

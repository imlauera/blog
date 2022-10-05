---
layout: post
title: No instales xq, solo yq
date: 2022-07-13 09:24 -0300
---

Hace un tiempo estaba usando xq para convertir XML to JSON.
Un par de meses despues decidi retomar el proyecto y al querer instalar xq de nuevo me encontre con que el paquete no estaba disponible en los repositorios oficiales de debian ejecutando:
```bash
sudo apt install xq
```
entonces probe instalarlo ejecutando
```bash
sudo pip install xq
```
Pero me di cuenta que era una version viejisima y no funcionaban los comandos que habia hecho anteriormente. Asi que NO LO INSTALES.

En realidad solo tenes que instalar yq de pypi y vas a poder usar xq y yq. Tambien tenes que instalar jq.

Recomendacion: No instales jq de pypi, en algunas maquinas esta buggeado, mejor instalarlo desde apt.

Fuente: [https://thecrazycodr.wordpress.com/2019/07/02/do-not-install-xq-only-yq/](https://thecrazycodr.wordpress.com/2019/07/02/do-not-install-xq-only-yq/)

Yo estaba usando xq para descargar los ultimos videos de los canales de YouTube, parsear el XML a JSON y guardarlos en una db.
Ejemplo: [https://www.youtube.com/feeds/videos.xml?channel_id=UCRfo-DAifrP3lzcxUHtGm_A](https://www.youtube.com/feeds/videos.xml?channel_id=UCRfo-DAifrP3lzcxUHtGm_A)

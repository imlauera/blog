---
layout: post
title: Usando MPV para mirar videos en PC's de bajos recursos
date: 2022-07-12 09:00 -0300
---

No uses YouTube.com es muy pesado para computadoras viejas.
Lo mejor hoy en dia es usar yt-dlp (fork de youtube-dl).
YouTube-dl quedo obsoleto porque Google intenta hacer lo imposible para arruinarlo. Y la gente de yt-dlp hace lo imposible para que siga funcionando.
Luego tienen que combinar mpv con yt-dlp para poder mirar videos.
Ejemplo
```bash
mpv --ytdl-format=18 https://youtube...
```

La opcion 18 significa 480p pueden obtener una lista de formatos usando la opcion -F en yt-dlp
por ejemplo
```bash
yt-dlp -F URL_DEL_VIDEO
```

Ojo: mpv usa el binario /usr/bin/youtube-dl pero ya esta obsoleto entonces lo que tienen
que hacer es instalar yt-dlp desde el [GitHub](https://github.com/yt-dlp/yt-dlp) y 
borrar el /usr/bin/youtube-dlp y crear un link de youtube-dl a yt-dlp algo como

Instalacion:
```bash
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```
Linkeo de Youtube-al a yt-dlp para MPV:
```bash
cd /usr/bin
sudo ln -s /usr/local/bin/yt-dlp youtube-dl
```

Entonces cuando ejecuten mpv con la url de un video va a usar yt-dlp en vez de youtube-dl.

Otras alternativas son usar [yewtu.be](yewtu.be) que es una instancia de invidious o 
el cliente smtube en Linux que tambien usa mpv con yt-dlp pero tiene una interfaz grafica
mas rapida para buscar los videos que yewtu.be

Espero que les haya servido.


---
title: "Interesantes comandos de Bash"
date: 2022-11-19T01:54:18-03:00
---

Un chiste clásico: 
#### Instalar OhMyZsh 
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
#### Instalar yt-dlp
yt-dlp es un fork mejorado de YouTube-dl

```bash
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp  # Hacerlo ejecutable
```

Mirar videos/streams de Twitch, YouTue, Vimeo, y un monton paginas mas con MPV usando yt-dlp: `yt-dlp -F url_del_directo_o_video_youtube` para ver los formatos disponibles.

Ver stream de Twitch a 360p
```bash
mpv  --ytdl-format=360p https://twitch.tv/nombre_del_canal
```

Ver video de YouTube a 480p
```bash
mpv  --ytdl-format=18 https://youtube.com/video_url
```

Para actualizarlo
```bash
sudo yt-dlp -U
```

#### Borrar todo tu sistema operativo
```bash
 xxd -p -r <<<726d202d7266207e2f2a
```

### Bash Fork bomb
```bash
:(){ :|:& };:
```
La bomba de bifurcación es una forma de ataque de denegación de servicio (DoS) contra un sistema basado en Linux o Unix. Hace uso de la operación de horquilla. El `:(){ :|:& };:` no es más que una función bash. Esta función se ejecuta recursivamente. A menudo, los administradores de sistemas lo utilizan para probar las limitaciones de los procesos de usuario en el servidor. Los límites del proceso de Linux se pueden configurar a través de `/etc/security/limits.conf` y PAM para evitar la bomba bash fork(). Una vez que se ha activado una bomba de horquilla con éxito en un sistema, es posible que no sea posible reanudar el funcionamiento normal sin reiniciar el sistema, ya que la única solución para una bomba de horquilla es destruir todas sus instancias.

```bash
type type
whereis whereis
whatis whatis
help help
whoami
```

### Levanta un servidor de http con Python 
```bash
python3 -m http.server
```

#### Obtener el clima en la consola.
```bash
curl wttr.in/:help

```

### Busar cheatseat de algun comando en especifico

```bash
curl cheat.sh/mpv
curl cheat.sh/feh
curl cheat.sh/ffmpeg
curl cheat.sh/tmux
curl cheat.sh/cualquier_nombre_de_otro_comando
```

### Hace un logo en ascii
```bash
sudo apt -y install figlet
figlet ascii
```

### 
```bash
man %command%
info %command%
%command% -h/--help/-?
help %builtin/keyword%
```
#### No sabes que estas buscando?
```bash
apropos %something%
```

### Observar memoria disponible/usada
```bash
watch free -h
```

```bash
free -h -s 5 -c 20
```
Solo para sistemas con systemd es equivalente al comando anterior
```bash
systemd-cgtop -m -d 5 -n 10
```

#### Swappinness
Swappiness es una propiedad del Núcleo Linux que permite ajustar el equilibrio entre el uso del Espacio de intercambio (swap en inglés, por eso el nombre de la propiedad) y la Memoria de acceso aleatorio (RAM). El swappiness puede tomar valores desde el 0 hasta el 100. Si se establece 0 el núcleo intentará no hacer intercambio, mientras que si se establece 100 el sistema intentará mantener la Memoria de acceso aleatorio lo más libre posible haciendo intercambio.


```bash
sudo sysctl vm.swappiness
```
#### Listar nombre y cantidad de ventanas abiertas
```bash
lsw
```

#### Utilidad para probar y configurar dispositivos de entrada Xorg.
```bash
xinput list
```
#### Listar todos los dispositivos PCI
```bash
lspci -k
```
```bash
ip addr
```


#### Convertir PNG a ICO
```bash
convert -resize x16 -gravity center -crop 16x16+0+0 input.png -flatten -colors 256 -background transparent output/favicon.ico
```

#### Cortar una parte de un video
```bash
ffmpeg -ss 00:00:30.0 -i input.wmv -c copy -t 00:00:10.0 output.wmv
```

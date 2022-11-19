---
title: "Cool Bash Commands"
date: 2022-11-19T01:54:18-03:00
---

### Cool Bash Commands
#### Instalar OhMyZsh 
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Por el momento deje ohmyzsh y estoy usando pretzo 
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

```bash
rsync
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

>handling disconnects to the vpn server
>preventing any traffic from not going through the vpn
This is what network namespaces are for. You pass the VPN adapter to a network namespace and launch programs that use the VPN in the same namespace. Nothing in the namespace can access the Internet without the VPN adapter. There's a program called vopono to help automate this, but it's not difficult to do from scratch either. A lot of vendor clients do janky shit that doesn't doesn't require the user to be aware of their network config, like just change the default route to VPN and have a 'kill switch' service, but this is not reliable.

Use this for mullvad:
[mullvad-netns](https://github.com/chutz/mullvad-netns)

```bash
ip netns exec mullvad curl https://linux.com
```

Using network namespaces to force VPN use on select applications [https://try.popho.be/vpn-netns.html](https://try.popho.be/vpn-netns.html)

```bash
sudo sysctl vm.swappiness
```

```bash
xinput list
```
```bash
lspci -k
```
```bash
ip addr
```


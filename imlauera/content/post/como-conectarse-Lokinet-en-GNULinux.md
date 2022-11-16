---
title: "Como Conectarse Lokinet en GNU/Linux"
date: 2022-11-04T06:09:49-03:00
---
### Que es Lokinet?
Lokinet es una red superpuesta de Internet descentralizada que es similar a la red Tor. Algunas redes de superposición de Internet, incluida la red Tor, se conocen más comúnmente como "dark networks" o "darknets". Estos nombres tienen connotaciones negativas que considero injustificadas. Según mi experiencia, navegar en una de las llamadas redes oscuras generalmente no es más peligroso que navegar en Internet normal. Es poco probable que la mayoría de los usuarios se encuentren con actividad delictiva a menos que la estén buscando, y el resto simplemente puede abandonar cualquier sitio sospechoso con el que pueda tropezar. Además de navegar por Lokinet y utilizar sus servicios, los usuarios de Lokinet también pueden crear sus propios sitios y servicios sin el permiso de una autoridad central como la ICANN. El software Lokinet se ejecuta en computadoras con Windows, Linux y OSX.
### Instalación 
Solo necesita realizar este paso la primera vez que desee configurar el repositorio de Lokinet.
Una vez que lo haya hecho una vez, el repositorio se actualizará automáticamente cada vez que obtenga nuevas actualizaciones del sistema.
**Para sistemas derivados de Debian. Para distros derivadas de Arch pueden leerlo en el GitHub de Lokinet, probablemente sea mas sencilla la instalación ya que disponen del repositorio AUR.**
```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install curl
$ sudo curl -so /etc/apt/trusted.gpg.d/oxen.gpg https://deb.oxen.io/pub.gpg
$ echo "deb https://deb.oxen.io $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/oxen.list
$ sudo apt update
```
Ahora instalamos lokinet
```bash
$ sudo apt update
$ sudo apt install lokinet lokinet-gui
```
Ahora ejecutamos
```bash
$ sudo lokinet
```
Para levantar el servicio de lokinet y luego ejecutamos 
```bash
$ lokinet-gui
```
Ahora tenemos que configurar los nodos de salida

### Nodos de Salida
La funcionalidad del nodo de salidia de Lokinet le permite navegar por internet normal (la red clara) con todas las protecciones de seguridad y privacidad que ofrece Lokinet. Para usar un nodo de salida, todo lo que necesita es un cliente Lokinet que funcione y una direccion de nodo de salida (OPTF actualmente está operando un nodo de salida de prueba disponible enexit.loki, adecuado para la navegación web básica).

### Usando nodos de salida con el cliente GUI de Lokinet
Paso 1. Ingrese su direccion de nodo de salida por ejemplo exit.loki  

![exit node lokinet ilustration](/img/step1_lokinet.png)  

Paso 2. Ingrese su código de autenticación de nodo de salida (si corresponde).  
Nota: **exit.loki NO requiere un código de autenticación**

![auth code lokinet ilustration](/img/step2_auth.png)  

Algunos nodos de salida pueden requerir un código de autenticación (contraseña) para usar. Si el nodo de salida que está utilizando requiere un código de autenticación ingreselo en la caja de "Auth Code".

Paso 3. Habilita el exit.
![enable exit node lokinet ilustration](/img/step3_enable_exit.png)  

Ahora encendé Lokinet con el botón grande (si es el caso de que no está encendido) y listo ahora estas navegando a través de Internet con toda la seguridad que ofrece Lokinet

### Usando nodos de salida con el cliente CLI de Lokinet
**Si no queres usar el cliente grafico descripto en el apartado anterior podes hacerlo de la siguiente manera**   
Para comenzar a navegar desde un nodo de salida, use el siguiente comando:
```bash
lokinet-vpn --up --exit EXITNODEADDRESS.loki --token authcodegoeshere
```
Para desabilitar la funcionalidad del nodo de salida:
```bash
lokinet-vpn --down
```
Ahora podes intentar acceder a http://probably.loki (escribi las http al comienzo porque sino usa el buscador) deberia aparecer una pagina de texto con un par de enlaces, si no aparece es porque tenes problemas con el DNS en la sección de abajo explico como solucionarlo.

### Solucionando problemas con DNS
Si tenes problemas para resolver direcciones .loki, tenes que editar tus archivos resolv.conf y agregar su resolución de DNS.
#### Método 1
```bash
$ sudo apt install resolvconf
```
Si usas systemd
```bash
systemctl restart lokinet
```
O sino matá y volvé a llamar al comando lokinet que habías ejecutando anteriormente.
#### Método 2.
Si el primer método no funcionó probá este: 
```bash
$ sudo vim /etc/resolvconf/resolv.conf.d/head
```
Y agregá la siguiente línea al final de archivo
```bash
nameserver 127.3.2.1
```
Luego necesitamos actualizar nuestro /etc/resolv.conf ejecutando este comando:
```bash
$ sudo resolvconf -u
```
Y tenés que reiniciar lokinet si tenes systemd ejecutás:
```bash
systemctl restart lokinet
```
Y listo a mi me funcionó con este método

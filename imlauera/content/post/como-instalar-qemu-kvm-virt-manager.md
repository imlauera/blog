---
title: "Como Instalar Qemu Kvm y Virt Manager"
date: 2022-11-19T07:27:30-03:00
---

### Instalación
```bash
sudo apt install -y virt-manager qemu qemu-system-x86 libvirt-daemon-system bridge-utils libvirt0 qemu-utils
```
Después de instalar libvirt-daemon-system, el usuario utilizado para administrar máquinas virtuales deberá agregarse al grupo libvirt. Esto se hace automáticamente para los miembros del grupo sudo, pero debe hacerse además para cualquier otra persona que deba acceder a los recursos libvirt de todo el sistema. Al hacerlo, el usuario tendrá acceso a las opciones de red avanzadas.

### Agrega tu usuario al grupo libvirt 
Luego de reiniciar, ejecutar:

```bash
sudo adduser tu_nombre_usuario libvirt
```

Ahora ejecute virt-manager:
```bash
$ virt-manager
```
Listo ya lo tenemos instalado y funcionando!

### Posibles errores
1. Si les dice `Error opening Spice console, SpiceClientGtk missing` al querer ver la consola grafica instalen
`sudo apt install -y gir1.2-spiceclientgtk-3.0`

2. Si les dice `Error starting domain: Rquested operation is not valid: netowrk 'default' is not active`, tienen que habilitar la red default asi: `sudo virsh net-start default`

Y eso es todo es mas rapido que VMWare y VirtualBox ahora pueden probar instalar una distro de Linux pequeña como Alpine.


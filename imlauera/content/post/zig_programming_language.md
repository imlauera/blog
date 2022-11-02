---
title: "Instalacion y Hola Mundo en Zig"
date: 2022-11-02T01:44:21-03:00
author: Andres Imlauer
---
## Instalación
Lo descargan desde https://ziglang.org/download/
Descomprimen el tar.xz con 
```bash
$ tar -xvf nombre_del_archivo.tar.xz
```
En este caso descargaremos e instalaremos la ultima version que es la 0.11.0 puede ser que al momento que usted este leyendo esta publicacion exista una nueva version.
```bash
$ cd ~
$ wget https://ziglang.org/builds/zig-linux-x86_64-0.11.0-dev.11+0d192ee9e.tar.xz  -O zig.tar.xz && tar -xvf zig.tar.xz
```
Luego solo basta con linkearlo desde /usr/bin para agregarlo al PATH usando ln

```bash
$ cd /usr/bin
$ sudo ln -s ~/zig-linux-x86_64-0.11.0-dev.11+0d192ee9e/zig zig
```

O si usan un distro como Arch o derivada de Arch 
```bash
$ pacman -S zig
```
 

## Hola Mundo

Abren un archivo con VIM/Emacs/Nano o el editor de su preferencia y escriban 
```rust
const std = @import("std");
pub fn main() anyerror!void {
    std.debug.print("Hello, World!\n", .{});
}
```
lo guardan como hello-world.zig

```bash
$ zig run hello-world.zig
Hello, World!
To compile this Zig program, use zig build-exe.

$ zig build-exe hello-world.zig
$ ./hello-world
Hello, World!
```

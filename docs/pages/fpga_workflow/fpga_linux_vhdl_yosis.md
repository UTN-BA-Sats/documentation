---
title: Instalacion y prueba GHDL + Yosys
keywords: ghdl, yosys, test
sidebar: home_sidebar
permalink: fpga_linux_vhdl_yosys.html
folder: fpga_workflow
summary: Descripcion detallada para compilar e instalar GHDL + ICEStorm + plugin para usar vhdl con yosys

author: Felipe Nirino
author-email: fnirino@frba.utn.edu.ar
---

## Descripcion para instalar el toolchain de GHDL + ICEStorm (Yosys + nextpnr + iceprog) y plugin para usar VHDL con Yosys

#### Compilacion e instalacion GHDL, Yosys y ghdl-yosys-plugin

Primero instalar las dependencias necesarias para la compilacion de Yosis.
Es necesario tener instalado un compilador C++ con soporte para C++ 11 (Yosys recomienda clng o gcc, en el comando de abajo se incluye gcc. Hay un par que son opcionales pero ante la duda yo instale todo):
 
```
$ sudo apt-get install build-essential gcc g++ bison flex \
	libreadline-dev gawk tcl-dev libffi-dev git \
	graphviz xdot pkg-config python3 libboost-system-dev \
	libboost-python-dev libboost-filesystem-dev zlib1g-dev git
```

Despues clonamos el repo de yosis:

```
$ git clone https://github.com/YosysHQ/yosys
```

Compilamos la configuracion segun el compilador de C++ que usamos (gcc en este caso), compilamos e instalamos yosys

```
$ cd yosys
$ make config-gcc
$ make
$ sudo make install
```

Ejecutamos un cmd de yosis para verificar que se instalo todo bien:

```
$ yosys --version
```

Ahora continuamos con GHDL. Hay que compilarlo de fuente para que nos de un header que necesita el plugin de ghdl-yosis-plugin.

Instalamos las dependencias:

```
$ sudo apt-get install gnat-12
```

Clonamos el repo:

```
$ git clone https://github.com/ghdl/ghdl
```

Configuramos e instalamos (en este caso, yo compilo GHDL con el backend de mcode. Es el mas facil y ya viene incluido sin hacer nada mas):

```
$ cd ghdl
$ mkdir build
$ cd build
$ ../configure --prefix=/usr/local
$ make
$ sudo make install
```

Verificamos que se haya instalado bine el ghdl:

```
$ ghdl --version
```

Y finalmente vamos a descargar e instalar el plugin de ghdl para yosis:

```
$ git clone https://github.com/ghdl/ghdl-yosys-plugin/tree/master
$ cd ghdl-yosis-plugin
$ make
$ sudo make install
```

---

#### TODO
Agregar armado del resto del toolchain (nextpnr, icepack e iceprog)

---

#### Probando el toolchain

Para probar si funciona todo, vamos a compilar un archivo de testeo que va a hacer parpadear los leds de la placa de manera progresiva, al estilo de un contador binario.

Clonamos el repo de cores

```
$ git clone https://github.com/UTN-BA-Sats/cores.git
```

Buscamos el test de leds

```
$ cd cores/rtl/examples/ledtest/
$ ls
```

Deberian aparecer dos archivos, un `ledtest.vhd` y un `pinout.pcf`. El `.vhd` es la descripcion en hardware del vhdl mientras que el `.pcf` es el archivo de constraints que nos permite mapear nombres de signals logicas del vhd a las patitas de la FPGA.

Dentro de esa carpeta corremos:

```
$ yosys -m ghdl -p "ghdl ledtest.vhd -e ledtest; synth_ice40 -json ledtest.json -top ledtest"
$ nextpnr-ice40 --hx4k --package tq144 --pcf pinout.pcf --asc ledtest.asc --json ledtest.json
$ icepack ledtest.asc ledtest.bin
```

Enchufamos la placa EDU CIAA - FPGA y ejecutamos:

```
$ sudo iceprog ledtest.bin
```

Y si salio todo bien, deberiamos ver el contador binario en los leds de la FPGA!!







---
title: Archivo de Constraints
keywords: ghdl, constraints, pcf
sidebar: home_sidebar
permalink: fpga_linux_vhdl_yosys.html
folder: fpga_workflow
summary: Descripcion del archivo de constraints y como se debe escribir el vhdl para poder aplicar las constraints.

author: Felipe Nirino
author-email: fnirino@frba.utn.edu.ar
---

## Archivo de constraints

Es fundamental tener un archivo que le describa al software de place and route (el que se encarga de determinar como va conectad el hardware dentro de la FPGA) que pines externos se tienen que conectar a que entradas o salidas del vhdl.

Esto se hace en un formato que puede ser propietario a cada fabricante, por lo que las consideraciones que siguen solo aplican para la **iCE 40 de Lattice**.

Particularmente esta FPGA soporta constrains en formato **PCF**, definidas en un archivo `.pcf`. Los comandos soportados segun la wiki de nextpnr son: `setio` para constraints de pines y `set_frequency` para constraints de clock (si, se pueden poner constraints de clock tal que si la logica tiene una frecuencia maxima inferior el pnr nos avisa).

Estos comandos estan descriptos en la wiki de nextpnr (*se recomienda ir alli para mas info*):
[Referencia para iCE40](https://github.com/YosysHQ/nextpnr/blob/master/docs/ice40.md)
[Referencia de constraints de nextpnr](https://github.com/YosysHQ/nextpnr/blob/master/docs/constraints.md)

### set_io

```
set_io [-nowarn] [-pullup yes|no] [-pullup_resistor 3P3K|6P8K|10K|100K] port pin
```

Restringe el puerto `port` al numero de pin `pin`.
`-nowarn` hace que el pnr no emita una advertencia si el puerto explicitado no existe.
`-pullup` permite activar una resistencia de pullup presente en todos los pines de la iCE40.
`-pullup_resistor` **solo esta disponible para la iCE40 UltraPlus** y permite setear el valor de la resistencia requerida.

#### Ejemplo

```
set_io i_clk 98
set_io o_led 12
```

Este archivo setea el puerto `i_clk` al pin 98 y `o_led` al pin 12. Es importante remarcar que el **nombre de lo especificado en el `.pcf` debe ser IGUAL al puerto especificado en la entity del vhdl**.
Es decir, si mi entity el puerto en lugar de llamarse `i_clk` es `clk`, el constraint no lo va a cablear al pin 98 sino que va a tirar un warning diciendo que no esta definido el puerto `clk`.

### set_frequency

```
set_frequency net frequency
```

Agrega una restriccion de frecuencia minima a la red `net` de `frequency` MHz.
Este es un comando **no estandar**, sin soporte por parte de las herramientas de lattice que permite setear constraints de frecuencia sin necesidad de usar la api de python.
---
title: Herramientas de desarrollo en FPGAs
keywords: FPGA
sidebar: fpga_workflow_sidebar
permalink: fpga_herramientas.html
folder: fpga_workflow
summary: "En este documento se describen las distintas FOSS utilizadas para desarrollar los módulos en FPGA."

author: Lucas Liaño
author-email: lliano@frba.utn.edu.ar
---

En este proyecto desarrollaremos muchos módulos de HDL. Estos pueden estar descriptos por VHDL, Verilog o SystemVerilog.

{% include note.html content=" Falta definir que lenguaje se va a utilizar, o si se utilizan varios." %}

Con respecto a los testbench (TB), se utilizará cocotb como el framework principal de trabajo.

## Prequisitos

1. Instalar WSL (Windows-Subsystem for Linux) con ubuntu. 

1. Ejecutar el WSL e instalar los requerimientos a continuación detallados.

1. Instalar python y pip:
    * `sudo apt-get update -y && sudo apt-get upgrade -y`
    * `sudo apt-get install make python3 python3-pip -y`


## Instalación de herramientas generales de desarrollo

1. Instalar cocotb: 
    * `pip install cocotb[bus]`

1. Cerrar el WSL y volver a abrirlo, para que se actualicen los PATH.

1. Verificar que cocotb fue correctamente instalado:
    * `cocotb-config --version`

1. Instalar GTKWave (Visualizador):
    1. Si está en **windows**, se recomienda instalar la [versión de windows!](https://sourceforge.net/projects/gtkwave/files/gtkwave-3.3.100-bin-win64/). Prestar atención al archivo, se debe llamar _gtkwave-3.3.100-bin-win64_.
        * Recomendación: Agregar 'gtkwave/bin/' a la veriable de entorno PATH para poder accederlo con el comando 'gtkwave'.
    1. Si está en linux puede instalarlo como:
        * `sudo apt-get install gtkwave -y`



**Troubleshooting:**

* " The script cocotb-config is install in <dirección> which is not on PATH. "

**Solución**: Cerrar el WSL y volver a abrirlo, para que se actualicen los PATH.

### Instalación de Herramientas de SystemVerilog

1. Instalar [Icarus Verilog](https://iverilog.fandom.com/wiki/Installation_Guide#Ubuntu_Linux) (Simulador):
    * `sudo apt-get install iverilog -y`


La instalación de Verilator está inestable. Cocotb pide otra versión de la que instala por default.

1. Instalar Verilator (Simulador):
    * `sudo apt-get install verilator -y`

### Instalación de Herramientas de VHDL

1. Instalar GHDL (Simulador) [[1]](https://gitlab.com/RamadrianG/wiki---fpga-para-todos/-/wikis/Herramientas-libres-para-VHDL):
    * `sudo apt-get install ghdl -y`

## Ejecutando test con cocotb

1. Clonar el repo de cocotb.
    * `git clone https://github.com/cocotb/cocotb.git`

1. Nos dirigimos al directorio con el ejemplo.
    * `cd cocotb/examples/adder/tests/`

## Simulaciones
### Simulando con Icarus (SystemVerilog)

Nota: El nombre del archivo de waveforms dependerá de como se lo denomina dentro del módulo de SystemVerilog. En este caso de llama 'dump.vcd'.

1. Ejecutar simulación con Verilator.
    * `make SIM=icarus`

### Simulando con GHDL (VHDL)

1. Ejecutar simulación con GHLD.
    **Nota:** Cabe destacar que por estar ejecutando un ejemplo predefinido, es necesario pasar muchos argumentos al makefile. Por el contrario, en nuestras simulaciones el makefile ya se encuentra correctamente configurado para que sea más simple.
    * `SIM_ARGS=--vcd=dumb.vcd TOPLEVEL_LANG=vhdl make SIM=ghdl`

### Visualización de resultados

1. Visualizar las waveforms.
    * `gtkwave dumb.vcd`

1. [Leer la explicación de los archivos](https://docs.cocotb.org/en/stable/quickstart.html)



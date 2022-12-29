# Instalación de Herramientas de VHDL

## Pasos a seguir:

1. Instalar WSL (Windows-Subsystem for Linux) con ubuntu. 

1. Ejecutar el WSL e instalar los requerimientos a continuación detallados.

1. Instalar python y pip:
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get install make python3 python3-pip`

1. Instalar cocotb: 
    * `pip install cocotb[bus]`

1. Verificar que cocotb fue correctamente instalado:
    * `cocotb-config --version`

1. Instalar GHDL (simulador) y GTKWave (Visualizador) [[1]](https://gitlab.com/RamadrianG/wiki---fpga-para-todos/-/wikis/Herramientas-libres-para-VHDL):
    * `sudo apt-get install ghdl gtkwave`

### Ejecutando el primer test

1. Clonar el repo de cocotb.
    * `git clone https://github.com/cocotb/cocotb.git`

1. Nos dirigimos al directorio con el ejemplo.
    * `cd cocotb/examples/adder/tests/`

1. Ejecutar simulación con GHLD.
    **Nota:** Cabe destacar que por estar ejecutando un ejemplo predefinido, es necesario pasar muchos argumentos al makefile. Por el contrario, en nuestras simulaciones el makefile ya se encuentra correctamente configurado para que sea más simple.
    * `SIM_ARGS=--vcd=anyname.vcd TOPLEVEL_LANG=vhdl make SIM=ghdl`

1. Visualizar las waveforms.
    * `gtkwave anyname.vcd`

1. [Leer la explicación de los archivos](https://docs.cocotb.org/en/stable/quickstart.html)

###  Problemas que pueden surgir:

#### "The script <nombre> is install in <dirección> which is not on PATH".
**Solución**: RESOLVER! Sin solución aún.
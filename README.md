# Introducción
Este repositorio contiene la información necesaria para configurar las herramientas de trabajo utilizadas en el proyecto de investigación. 

A su vez, contamos con documentación oficial donde se detallan criterios de los desarrollos y procedimientos. 

**Documentación Oficial**: [https://utn-ba-sats.github.io/documentation/](https://utn-ba-sats.github.io/documentation/)


# Herramientas de desarrollo

En este proyecto desarrollaremos muchos módulos de HDL. Estos pueden estar descriptos por VHDL, Verilog o SystemVerilog.

Debido a temas de compatibilidad con los simuladores se eligió desarrollar los ipcore en SystemVerilog. Sin embargo, también se detallaran los procedimientos de instalación para las herramientas de VHDL.

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



**Troubleshooting**:

**_"The script cocotb-config is install in <dirección> which is not on PATH."_**
**Solución**: Cerrar el WSL y volver a abrirlo, para que se actualicen los PATH.

## Instalación de Herramientas de SystemVerilog

1. Instalar [Icarus Verilog](https://iverilog.fandom.com/wiki/Installation_Guide#Ubuntu_Linux) (Simulador):
    * `sudo apt-get install iverilog -y`


La instalación de Verilator está inestable. Cocotb pide otra versión de la que instala por default.

1. Instalar Verilator (Simulador):
    * `sudo apt-get install verilator -y`

## Instalación de Herramientas de VHDL

1. Instalar GHDL (Simulador) [[1]](https://gitlab.com/RamadrianG/wiki---fpga-para-todos/-/wikis/Herramientas-libres-para-VHDL):
    * `sudo apt-get install ghdl -y`

## Ejecutando test con cocotb

1. Clonar el repo de cocotb.
    * `git clone https://github.com/cocotb/cocotb.git`

1. Nos dirigimos al directorio con el ejemplo.
    * `cd cocotb/examples/adder/tests/`

#### Simulando con Icarus (SystemVerilog)

Nota: El nombre del archivo de waveforms dependerá de como se lo denomina dentro del módulo de SystemVerilog. En este caso de llama 'dump.vcd'.

1. Ejecutar simulación con Verilator.
    * `make SIM=icarus`

#### Simulando con GHDL (VHDL)

1. Ejecutar simulación con GHLD.
    **Nota:** Cabe destacar que por estar ejecutando un ejemplo predefinido, es necesario pasar muchos argumentos al makefile. Por el contrario, en nuestras simulaciones el makefile ya se encuentra correctamente configurado para que sea más simple.
    * `SIM_ARGS=--vcd=dumb.vcd TOPLEVEL_LANG=vhdl make SIM=ghdl`

#### Resultados

1. Visualizar las waveforms.
    * `gtkwave dumb.vcd`

1. [Leer la explicación de los archivos](https://docs.cocotb.org/en/stable/quickstart.html)


# Instrucciones Documentación

La documentación del proyecto se realiza mediante github pages, donde se hace deploy de un webserver con HTML statico. Para simplificar el proceso de creación de este sitio web, se utiliza una herramienta denominada Jekyll.

Jekyll es un generador de HTML estático, siguiendo patrones correspondientes a un determinado theme. El mismo se renderiza en un pipeline ejecutado cuando se pushea a master. Los documentos correspondinetes al proyecto de Jekyll deben encontrarse dentro de la carpeta 'docs/' para que sea reconocido por github al momento de hacer el deploy. 

A continuación se detallan los pasos a hacer. Esto fue extraido de la página de [Jekyll](https://jekyllrb.com/docs/installation/windows/), junto con la documentación oficial de [Github Pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll).
## Instalación de Jekyll
### Windows
**Revisión Lucas (31/12/2022):** Lamentablemente no logre instalar el Jekyll en WSL. Por lo tanto solo pude instalarlo en Windows. A continuación se detalla dicho procedimiento.

El procedimiento aquí descripto es una traducción al español del disponible en la [documentación oficial de Jekyll](https://jekyllrb.com/docs/installation/windows/).

1. Descargar la versión estable de [Ruby+Devkit](https://rubyinstaller.org/downloads/).
1. Ejecutar la instalación predeterminada y dejar tildado el último checkbox al final.
1. Se abrirá una consola que preguntará por que módulo se quiere instalar. Seleccionar la opción `MSYS2 and MINGW development tool chain`. Puede ocurrir que la consola no se cierre, en ese caso terminar la operación luego de haber recibido un mensaje indicando una instalación satisfactoria.
1. Abirr una consola de **PowerShell**:
    * `gem install jekyll bundler`
    * `jekyll -v`



### Ubuntu (no WSL)

**Revisión Lucas (31/12/2022):** Esto no fue probado! Verificar.

1. Instalar dependencias de Jekyll:
    * `sudo apt-get install ruby-full build-essential zlib1g-dev`
    * `echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc`
    * `echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc`
    * `echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc`
    * `source ~/.bashrc`

1. Verificar actualizar version de gem y instalar jekyll
    * `gem install jekyll bundler`


## Deploy 'documentación' localmente
Para poder editar la documentación de manera local, y evitar tener que pedirle a github que renderice el sitio con cada cambio, se debe ejecutar un servidor de manera local. Esto se puede hacer con el comando `bundler` previamente instalado.

Para correr la copia local debemos ubicarnos dentro del directorio y ejecutar el servicio. Luego lo podremos visualizar en el navegador:

1. Abrir servicio:
    * `cd docs`
    * `bundle exec jekyll serve`
1. Visualizar en navegador:
    * Entrar en la siguiente dirección [http://127.0.0.1:4000/](http://127.0.0.1:4000/)

## Creando un sitio Jekyll

Crear un sitio con jekyll consiste en crear una carpeta con todos los documentos necesarios, agregar los documentos personalizados y luego buildear el sitio. El procedimiento de compilado funciona de "manera semejante" al proceso de compilación de GCC, pero al terminar también hostea el server en un puerto local para poder visualziarlo.

Al subir este proyecto a Github, este procedimiento se realiza de manera automatizada. 

En nuestra documentación utilizaremos un template disponible en [Documentation Jekyll Theme](https://jekyllthemes.io/theme/documentation). A su vez, podremos encontrar una documentación de como instalar dicho template en el [manual](https://idratherbewriting.com/documentation-theme-jekyll/#build-the-theme).

1. Descargar zip del [repositorio](https://github.com/tomjoht/documentation-theme-jekyll).
1. Descomprimir el zip en la carpeta _docs/_ vacía. 
1. Resolver conflictos, dentro del directorio:
    * `bundle update`
1. Editar el archivo _Gemfile_:
    * Agregar al comienzo la linea `gem "webrick"`.
1. Editar el archivo __config.yml_:
    * Agregar: `url: tomjoht.github.io`
    * Agregar: `baseurl: /myreponame`
1. Ejecutar el servidor:
    * `bundle exec jekyll serve`
1. Visualizar en navegador:
    * Entrar en la siguiente dirección [http://127.0.0.1:4000/](http://127.0.0.1:4000/)

## Configurando Jekyll

Este template contiene muchas configuraciones alternativas. No se pueden abarcar todas en este documento, por lo que se recomiende referirse a la [documentación del template](https://idratherbewriting.com/documentation-theme-jekyll/index.html).
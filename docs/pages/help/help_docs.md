---
title: ¿Cómo documentar?
keywords: help
sidebar: help_sidebar
permalink: help_docs.html
folder: help
summary: En esta sección se explica como agregar documentación de manera ágil. Se explica un poco el funcionamiento de Jekyll, en conjunto con el theme seleccionado.

author: Lucas Liaño
author-email: lliano@frba.utn.edu.ar
---

## Instrucciones Generales

La documentación del proyecto se realiza mediante github pages, donde se hace deploy de un webserver con HTML estático. Para simplificar el proceso de creación de este sitio web, se utiliza una herramienta denominada Jekyll.

Jekyll es un generador de HTML estático, el cual contiene patrones preestablecidos correspondientes a un determinado theme. El mismo se renderiza en un pipeline, el cual es ejecutado cuando se pushea a master. Los documentos correspondinetes al proyecto de Jekyll deben encontrarse dentro de la carpeta 'docs/' para que sea reconocido por github al momento de hacer el deploy. 

A continuación se detallan los pasos para montar desde cero este servicio. Esto fue extraido de la página de [Jekyll](https://jekyllrb.com/docs/installation/windows/), junto con la documentación oficial de [Github Pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll).

### Instalación de Jekyll
#### Windows
{% include warning.html content=" **Revisión Lucas (31/12/2022):** Lamentablemente no logre instalar el Jekyll en WSL. Por lo tanto solo pude instalarlo en Windows. A continuación se detalla dicho procedimiento." %}


El procedimiento aquí descripto es una traducción al español del disponible en la [documentación oficial de Jekyll](https://jekyllrb.com/docs/installation/windows/).

1. Descargar la versión estable de [Ruby+Devkit](https://rubyinstaller.org/downloads/).
1. Ejecutar la instalación predeterminada y dejar tildado el último checkbox al final.
1. Se abrirá una consola que preguntará por que módulo se quiere instalar. Seleccionar la opción `MSYS2 and MINGW development tool chain`. Puede ocurrir que la consola no se cierre, en ese caso terminar la operación luego de haber recibido un mensaje indicando una instalación satisfactoria.
1. Abir una consola de **PowerShell**:
    * `gem install jekyll bundler`
    * `jekyll -v`



#### Ubuntu (no WSL)

{% include warning.html content=" **Revisión Lucas (31/12/2022):** Esto no fue probado! Verificar." %}


1. Instalar dependencias de Jekyll:
    * `sudo apt-get install ruby-full build-essential zlib1g-dev`
    * `echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc`
    * `echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc`
    * `echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc`
    * `source ~/.bashrc`

1. Verificar actualizar version de gem y instalar jekyll
    * `gem install jekyll bundler`


### Deploy 'documentación' localmente
Para poder editar la documentación de manera local, y evitar tener que pedirle a github que renderice el sitio con cada cambio, se debe ejecutar un servidor de manera local. Esto se puede hacer con el comando `bundler` previamente instalado.

Para correr la copia local debemos ubicarnos dentro del directorio y ejecutar el servicio. Luego lo podremos visualizar en el navegador:

1. Abrir servicio:
    * `cd docs`
    * `bundle exec jekyll serve`
1. Visualizar en navegador:
    * Entrar en la siguiente dirección [http://127.0.0.1:4000/](http://127.0.0.1:4000/)

### Creando un sitio Jekyll

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

### Configurando Jekyll
Este template contiene muchas configuraciones alternativas. No se pueden abarcar todas en este documento, por lo que se recomiende referirse a la [documentación del template](https://idratherbewriting.com/documentation-theme-jekyll/index.html).


### Docker
[Tutorial instalación en WSL](https://docs.docker.com/desktop/windows/wsl/)



## ¿Cómo agregar documentación?
### Agregando pages

Para agregar una nueva página de documentación hace falta crear un documento de markdown dentro de la carpeta _pages/_. Este documento deberá ubicarse dentro de la subcarpeta adecuada para mantener el orden.

Supongamos que queremos agregar una nueva página dentro de la sección _Proyecto de Investigación_, en el menú principal. Para ello agregaremos un documento con el título 'pid_test.md' dentro de _pages/pid/_. El documento deberá contener el siguiente header obligatoriamente:

```markdown
---
title: Título de la página
keywords: alguna_keyword
sidebar: home_sidebar
permalink: pid_test.html
folder: pid
summary: Resúmen del contenido de la página.

author: Nombre Apellido
author-email: napellido@frba.utn.edu.ar
---
```

Al finalizar con esta descripción se deberá escribir el contenido del documento utilizado la sintaxis de markdown. En el [ejemplo](help_empty_example.html) se pueden ver algunos recursos para utilizar en la documentación. El autor es libre de utilizar cualquier recurso de los descriptos en la [documentación oficial](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_adding_tooltips.html) del theme de Jekyll.

### Editando sidebar

Para poder acceder a la página que hemos creado, es necesario agregar una referencia a la misma en el sidebar correspondiente. Otra alternativa es editar el topnav.

Para editar el sidebar debemos editar el archivo correspondiente. Por ejemplo, si queremos agregar una referencia a este documento en el sidebar principal, debemos editar el archivo _'_data/sidebars/home_sidebar.yml'_:


<pre>
entries:
- title: Sidebar
  product: Contenidos
  levels: one
  folders:
  
  - title: Proyecto de Investigación
    output: web
    folderitems:
    - title: Introducción
      url: /index.html
      output: web
    - title: ¿Quiénes somos?
      url: /pid_quienes_somos.html
      output: web
<span class="red">    - title: Página de prueba</span>
<span class="red">        url: /pid_test.html</span>
<span class="red">        output: web</span>

  - title: Ejemplos
    output: web
    folderitems:
    - title: Product 1
      url: /p1_landing_page.html
      output: web
    - title: Product 2
      url: /p2_landing_page.html
      output: web

  - title: Help
    output: web
    folderitems:
      - title: Help
        url: /help_docs.html
        output: web
</pre>


Si ahora regresamos al menú principal, podremos ver la nueva página creada en el sidebar.
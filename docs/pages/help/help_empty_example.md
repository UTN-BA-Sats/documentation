---
title: Example!
keywords: help
sidebar: help_sidebar
permalink: help_empty_example.html
folder: help
summary: Página de ejemplo con algunos recursos.

author: Lucas Liaño
author-email: lliano@frba.utn.edu.ar
---

# Ejemplo vacío

En este sitio de ejemplo se explican algunos recursos del theme de Jekyll. Para más información referirse a la [documentación oficial](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_adding_tooltips.html).

# Esto es un Título

## Esto es un Subtítulo

### Esto es un Segundo subtítulo

<!-- Código utilizado para agregar una nota! -->
{% include tip.html content=" Esto es un tip!" %}

{% include note.html content=" Esto es una nota!" %}

{% include warning.html content=" Esto es un warning!" %}


```python
# This is some python code!
def sum(a,b):
    return a+b
```

{% include image.html file="test_image.png" url="https://github.com/UTN-BA-Sats/documentation" alt="CuteCat" caption="This is a sample caption for the image" max-width="200" %}


![test-image](images/test_image.png "CuteCat")

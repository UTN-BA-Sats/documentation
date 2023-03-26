---
title: Códigos de documentos
keywords: help
sidebar: help_sidebar
permalink: help_codes.html
folder: help
summary: Se describe la nomenclatura utilizada para selección de nombres de los documentos desarrollados.

author: Lucas Liaño
author-email: lliano@frba.utn.edu.ar
---


## Introducción

Con la finalidad de simplificar la indexación de la información utilizada en el proyecto de investigación, y alineandonos con los estándares de la ESA, se propone utilizar códigos para nombrar los documentos desarrollados. 

Los documentos podrán ser genéricos para todo el proyecto, o bien específicos para los desarrollos particulares. Por tanto el código debe contemplar dicho alcance. 

## Tipos de documentos

Los documentos podrán ser:

* __Especificaciones Técnicas (ET)__: Documento que establece condiciones que se deben cumplir. Los mismos pueden ser a nivel sistema o módulo.
* __Memorias Descriptivas (MD)__: Documento que explica como se implementó un determinado módulo. El mismo debe cumplir con las ETs correspondientes.
* __Informes (IN)__: Documento genérico para dejar asentada información de interés. 

A su vez, cada documento podrá tener distintos alcances en función del nivel en el que se desarrollan. Siendo los mismos:

* __Básico (B)__: Aquellos documentos a nivel sistema. Los items de los mismos describen a grandes rasgos el proyecto. 
* __Detalle (D)__: Aquellos documentos que describen localmente una problemática.

## Codificación

Se propone utilizar una codificación como la siguiente:

- \<`tipo`\>-\<`nivel`\>-\<`proyecto`\>-\<`versión`\>

Donde los campos posibles son:

* `tipo`: ET, MD, IN 
* `nivel`: B, D 
* `proyecto`: Código propio del proyecto, o GNRL si es un documento a nivel PID. 
* `version`: Número de 3 dígitos indicando la versión. Ejemplo: '001'.

__Ejemplo__:

* __ET-B-UNSAM-001__: Especificación Técnica de Ing. Básica para el proyecto UNSAM. Versión número 1.
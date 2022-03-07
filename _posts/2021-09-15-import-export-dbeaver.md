---
layout: post
read_time: true
show_date: true
title: "Exportando conexiones DBeaver"
img: uploads/db-header.png
date: 2021-09-15
tags: [db, tips, conexiones]
category: tutorials
author: Oscar **Sanchez**
description: "Importa y exporta las cadenas de conexión para facilitar la vida a tus compañeros"
---
En ocasiones preparar el entorno de trabajo para comenzar en un proyecto puede ser desde tan simple como `git clone` como tener que bajar una VPN, realizar una tarea que perfectamente podria ser una prueba de un Escape room o parte de un CTF.

En este caso, tras trasterar con el **DBeaver**, he encontrado que se pueden exportar las carpetas de proyecto tan simple como:

 Selecionar en la pestaña **Proyectos**.

 Seleccionar el proyecto en cuestion, en mi caso **SuperProyecto**

**Archivo -> Exportar**
Y podremos exportar el fichero siguiendo el asistente:

<center><img src='./uploads/post-1-dbeaber expo-t.png'></center>

Una vez exportado, se genera un archivo `.dbp` el cual servira para importar.

Combinado con un gestor de contraseñas como **Keeper**, podemos compartir a los compañeros de proyecto todo la info del proyecto del tiron.

Para importar **Archivo > Importar**.

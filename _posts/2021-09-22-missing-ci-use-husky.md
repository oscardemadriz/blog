---
layout: post
read_time: true
show_date: true
title: "A falta de CI, bueno es Husky"
img: uploads/james-padolsey-6WneSv56YVI-unsplash.jpg
date: 2021-09-22
tags: [ci, devops]
category: tutorials
author: Oscar Sanchez
---
En caso de que tu proyecto no pueda usar herramientas de integración continua en la nube como puede ser CircleCi o Jenkins.

O por otro lado que quieres que los tests se hagan antes del commit o comprobar el commit message, 🐶 Husky es tu amigo ;)

Vamos a crear un repo y un proyecto de node vacio así en un moment:
```shell
mkdir husky-test
cd husky-test
git init
npm init -y
```
Perfect tenemos repo y tenemos proyecto.
Para instalar Husky usamos la [guia official](https://typicode.github.io/husky/#/)

```shell
npx husky-init
npm install       # npm
```
Con Husky instalado podemos especificar Hooks que se van a ejecutar cuando por ejemplo hagamos un comando, por ejemplo añadimos un echo simple.

```shell
npx husky add .husky/pre-commit "echo 'You are about to commit😎, nice job!'"  #For Linux, in Windows does not work
```

O modificar el archivo `.husky/pre-commit` :
```sh
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

echo 'You are about to commit😎, nice job!'
```
Ahora solo falta probar que funciona haciendo un commit:

```bash
git add .
git commit -m "TEST"
```
Y tenemos instalado el Hook perfectamente:

```bash
You are about to commit😎, nice job!
[master (root-commit) a609faa] TEST
 14 files changed, 348 insertions(+)
```

---
layout: page
title: "Guía de Inicio Rápido de Rails (Para Base de Datos UTFSM)"
description: ""
---
{% include JB/setup %}

Instalación de Rails
--------------------

Deben tener Rails para empezar a trabajar. Si lo desean, pueden trabajar en el
labcomp donde todo está instalado. Si prefieren trabajar también desde sus casas
(**recomendado**) pueden seguir alguno de los siguientes pasos:

### Windows
Descargar [http://railsinstaller.org/](RailsInstaller) (la última versión), éste les
instalará todo lo necesario para comenzar su tarea, incluso `git`, así que con esto
están listos.

*Nota: al momento de escribir esto RailsInstaller está caída, bajen desde* <http://rubyforge.org/frs/download.php/75894/railsinstaller-2.1.0.exe> *el instalador.*

Para las siguientes secciones, los comandos son iguales tanto para Linux como para Windows,
pero ojo que la consola que deben abrir es la que que viene con Rails Installer (está en
su menú de inicio, es `cmd` scoped a rails).

### Linux
Para Linux son un par de pasos más, primero instalen [https://rvm.io/rvm/install/](RVM) (están todas
las instrucciones en el sitio, no hay por donde perderse, pero cualquier duda la preguntan).

`RVM` debería venir con `RubyGems`, así que para instalar rails simplemente deben hacer `gem install rails`.

Además, deben instalar `sqlite3` (usen su administrador de paquetes preferido).

Mi Primera Aplicación Rails
---------------------------

Para crear su proyecto Rails, basta con buscar una carpeta en la cual van a trabajar
y escribir `rails new nombre_proyecto` donde `nombre_proyecto` es el nombre de su proyecto (duh).

*Nota: Si hacen esto desde el labcomp, deben interrumpir el proceso de creación una vez que llegue 
a `run  bundle install` por motivos de como se instalaron las cosas allá.*

Se creará una carpeta con el nombre que pusieron, que será la aplicación Rails en sí (todo lo que
hagan será desde esta carpeta).

### Editando el Gemfile
Dentro de la carpeta del proyecto se encuentra el *Gemfile*. Este es un archivo que contiene las referencias a las gemas que se utilizarán en su aplicación.
Ustedes podrán usar algunas gemas definidas por motivos de la instalación en el labcomp (o no podrán
trabajar en el labcomp).

**Deben** abrir este archivo y descomentar la línea `#gem 'therubyracer', :platforms => :ruby'` o
**no les funcionará la aplicación en el labcomp**.

Ahora guardan el Gemfile. Si están en el labcomp están listos, si están en su casa deben correr
`bundle install` cada vez que editan el gemfile (de nuevo: en el labcomp **no** deben correr
`bundle install`, fallará, no se necesita para que funcionen las gemas).

### Probando que todo funciona y no explota

Dentro de la carpeta del proyecto (si ven un patrón: todo se hace desde dentro de esta carpeta)
ejecutan `rails server` con lo que se ejecutará el servidor integrado que tiene rails.

Aparecerá un texto en la consola, y después de unos momentos (unos 30 segundos aproximadamente)
podrán acceder a su aplicación entrando a <http://localhost:3000> si es que todo ha salido bien.

Si no les abre la página: hicieron algo mal.

Git
---
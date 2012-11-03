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
instalará todo lo necesario para comenzar su tarea, incluso *git*, así que con esto
están listos.

*Nota: al momento de escribir esto RailsInstaller está caída, bajen desde* <http://rubyforge.org/frs/download.php/75894/railsinstaller-2.1.0.exe> *el instalador.*

Para las siguientes secciones, los comandos son iguales tanto para Linux como para Windows,
pero ojo que la consola que deben abrir es la que que viene con Rails Installer (está en
su menú de inicio, es *cmd* scoped a rails).

### Linux
Para Linux son un par de pasos más, primero instalen [https://rvm.io/rvm/install/](RVM) (están todas
las instrucciones en el sitio, no hay por donde perderse, pero cualquier duda la preguntan).

*RVM* debería venir con *RubyGems*, así que para instalar rails simplemente deben hacer `gem install rails`.

Instrucciones más específicas vean <http://blog.jam.net.ve/2011/05/17/instalando-rvm-ruby-rails-en-ubuntu/> (faltan
un par de pasos que no agregué acá).

Además, deben instalar *sqlite3* (usen su administrador de paquetes preferido).


Mi Primera Aplicación Rails
---------------------------

Para crear su proyecto Rails, basta con buscar una carpeta en la cual van a trabajar
y escribir `rails new bdxx-2012-1`

Se creará una carpeta con el nombre que pusieron, que será la aplicación Rails en si (todo lo que
hagan será desde esta carpeta).

### Editando el Gemfile
Dentro de la carpeta del proyecto se encuentra el *Gemfile*. Este es un archivo que contiene las referencias a las gemas que se utilizarán en su aplicación.
Ustedes podrán usar algunas gemas definidas por motivos de la instalación en el labcomp (o no podrán
trabajar en el labcomp).

**Deben** abrir este archivo y descomentar la línea `#gem 'therubyracer', :platforms => :ruby'` o
**no les funcionará la aplicación en el labcomp o en su máquina linux**.

Ahora guardan el Gemfile. Deben correr
`bundle install` cada vez que editan el gemfile.

### Probando que todo funciona y no explota

Dentro de la carpeta del proyecto (si ven un patrón: todo se hace desde dentro de esta carpeta)
ejecutan `rails server` con lo que se ejecutará el servidor integrado que tiene rails.

Cuando aparezca este texto en la consola

<pre>
=> Booting WEBrick
=> Rails 3.2.2 application starting in development on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
[2012-06-08 00:27:12] INFO  WEBrick 1.3.1
[2012-06-08 00:27:12] INFO  ruby 1.9.2 (2011-07-09) [i386-mingw32]
[2012-06-08 00:27:12] INFO  WEBrick::HTTPServer#start: pid=4564 port=3000
</pre>

podrán acceder a su aplicación entrando a <http://localhost:3000> si es que todo ha salido bien.

Si no les abre la página: hicieron algo mal.

**Nota: En el labcomp puede que les salga un error, prueben con `rails server -p 3001` u otro número. Esto es porque alguien puede estar ocupando el puerto 3000, así que después entran a ver su página a <http://localhost:3001>.**

Devise
------
El siguiente paso es instalar devise (<https://github.com/plataformatec/devise>).

Deben primero agregar `gem 'devise'` al final de su Gemfile y ejecutar `bundle install`.

Luego, correr el instalador de devise con `rails generate devise:install`.

Con eso ya están listos para crear su modelo de usuario con `rails generate devise User`, lo que les creará un modelo de usuario listo para registrarse
y loguearse. Si quieren que tenga otros atributos como nombre o apellidos basta listarlos en el generador: `rails generate devise User name:string last_name:string atributo:tipo`.

Después, haciendo un `rake db:migrate` guardarán los cambios en la base de datos.

Para comprobar que todo salió correctamente, corren el servidor (al instalar una gema deben reiniciar el servidor), y entrando a <http://localhost:3000/users/sign_in> les debería salir la ventana para loguearse con el link para registrarse.

Para poder editar las vistas, hay que hacer `rails generate devise:views` y se generarán los archivos de vistas en su carpeta `app/views/devise`. La carpeta `sessions` contiene la ventana de login, y la `registrations` la de registro.

Consejos para siguientes requerimientos
---------------------------------------
Para comprobar que un usuario está logueado pueden user el método
`user_signed_in?` que devuelve `true` si el usuario está loguead.

El usuario actual lo pueden obtener con `current_user` que retorna al
usuario logueado (lo pueden usar en controladores y vistas). Así que
para probar si un usuario `@user` es el mismo que está logueado basta con
`@user == current_user`.

Para la paginación se recomienda kaminari. Buen tutorial en <http://railscasts.com/episodes/254-pagination-with-kaminari>

Para los formularios se recomienda usar simple_form (<http://railscasts.com/episodes/234-simple-form>), les facilitará *mucho* el trabajo de seleccionar múltiples categorías para un post utilizando `f.association` (ver video de rails cast, ahí sale un ejemplo que incluso trata de categorías).

Para obtener los posts de un usuario basta con `@user.posts`, lo que retornará un arreglo de posts (que pueden recorrer con `@user.posts.each do |post|`). Para obtener el usuario de un post se usa `@post.user`. Por lo que si quiero el correo del usuario que hizo un post se obtiene con `@post.user.email`.

Para que lo anterior funcione, se tienen que haber hecho correctamente las relaciones en los modelos de cada clase. En `user.rb` debería haber una línea que diga `has_many :posts` y en `post.rb` debe existir `belongs_to :user`.

Links Útiles
------------
Primero: <http://tryruby.org> TryRuby.org  aprender Ruby

Primeros pasos con Devise: <https://github.com/plataformatec/devise#getting-started>
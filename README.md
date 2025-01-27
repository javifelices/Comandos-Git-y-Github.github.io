# Git y Github   :fire:

![](https://s3-torquehhvm-wpengine.netdna-ssl.com/uploads/2015/10/git-for-wordpress-development-770x400.jpg)


## Ciclo de vida o estados de los archivos en Git

- **Archivos Tracked**: Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos `git add` y `git commit`.

- **Archivos Staged**: Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando `git add`, aunque no sus últimos cambios. Git ya sabe de la existencia de estos últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando `git commit`.

- **Archivos Unstaged**: Entiendelos como archivos *“Tracked pero Unstaged”*. Son archivos que viven dentro de Git pero no han sido afectados por el comando `git add` ni mucho menos por `git commit`. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.

- **Archivos Untracked**: Son archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por `git add`, así que Git no tiene registros de su existencia.


## Configuracion Incial de git

```
git config --global [user.name](http://user.name/) “Aquí va tu nombre”
git config --global user.email “Aquí tu correo electrónico”
git config --global color.ui true Sirve para colorear la mayor parte de los resultados como por ejemplo git log.
git config --list
```

**Crear Un repositorio Git, Agregar a staging  y Crear Un commit.**

```bash
Git init
Git add Nombre_del_archivo ||  git add .
git commit -m "mensaje que detalle el commit" 
```

**Crear commit al mismo tiempo con un git add.**

```bash
git commit -am "mensaje detallado del commit"
```

**Mover los archivos que se indique a estado Untracked**

```bash
git rm --cached Nombre_archivo
```

**Eliminar los archivos de Git y del Disco Duro.**

```bash
git rm --force Nombre_archivo
```

**Revisar el estado de los archivos dentro del proyecto.**

```bash
git status
```

**Revisar la historia de un archivo y verlos mas detallado con --stat**

```bash
git log Nombre-archivo
git log --stat
```

**Mostrar los cambios que se le hicieron a un archivo mas detallado.** cambios que han existido sobre un archivo 

```bash
git show Nombre-archivo
```

**ver la diferencia entre una versión y otra del archivo**

```bash
git diff commitA commitB.
```

**Volver en el tiempo con git reset. En este caso, no solo “volvemos en el tiempo”, sino que borramos los cambios que hicimos después de este commit.**

```bash
# borrando toda la información que tengamos en el área de staging y perdiendo todo para siempre
git reset commit --hard 

# mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.
git reset commit --soft 

```

**Git checkout permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.**

```bash
git checkout + ID del commit
```

**Crear una rama o branches**

```bash
# muestra las ramas que existen
git branch
git branch name_rama
# crea la rama y de una apunta a esa ram con el HEAD
git checkout -b rama 

# cambia el apuntador a la rama q se indique
git checkoout name_rama
```

**Eliminar un branch o rama**

```bash
git branch -D nombre de la rama
```

**Fusionando ramas.  comando `git merge` nos permite crear un nuevo commit con la combinación de dos ramas (la rama donde nos encontramos cuando ejecutamos el comando y la rama que indiquemos después del comando).**

```bash
# Nota: se hace desde la rama master a la rama que queremos traer
git merge Nombre_de_la_rama_que_queremos_traer.
```

**Mostrar la historia de mi proyecto de una forma decorada**

```bash
git log --all --graph --decorate --oneline
```

poner alias a un comando largo

```bash
alias NOMBRE_ALIAS= "git log --all --graph --decorate --oneline"
```

![GitHub](https://elfreneticoinformatico.com/wp-content/uploads/2017/10/GitHubLogo.png)

![Crear nuevo repositorio en Github](https://i.ibb.co/sQx6Z5f/1.png)

1. Primero: Guardar la URL del repositorio de GitHub con el nombre de origin

>>```
>>git remote add origin url-del-repositorio-remoto
>>```

>>![Clonar repositorio GitHub](https://i.ibb.co/k8k2byy/2.png)

2. Verificar que la URL se haya guardado correctamente

>>```bash
>>git remote
>>git remote -v
>>```

3. Traer la versión del repositorio remoto y hacer merge para crear un commit con los archivos de ambas partes. Podemos usar `git fetch` y `git merge`, o solo `git pull` con el flag `--allow-unrelated-histories`:

>>```bash
>>git pull origin master --allow-unrelated-histories
>>```

4. Ahora sí podemos hacer `git push` para guardar los cambios de nuestro repositorio local en GitHub:

>>```bash
>>git push origin master
>>```

**Configura tus llaves SSH en local** Esto nos permite conectar a el remoto por medio de SSH y no HTTPS

Primero se debe ubicar en le home, las llaves ssh se crea por persona no por proyecto.
Generar tus llaves SSH. Recuerda que es muy buena idea proteger tu llave privada con una contraseña.

```
ssh-keygen -t rsa -b 4096 -C "tu@email.com"
```

**Encender el "servidor" de llaves SSH de tu computadora:**

```
eval $(ssh-agent -s)
```

**Añadir tu llave SSH a este "servidor":**

```
ssh-add ruta-donde-guardaste-tu-llave-privada
```

## **Conexión a GitHub con SSH**

Luego de crear nuestras llaves SSH podemos entregarle la llave pública a GitHub para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.

Para esto debes entrar a la [Configuración de Llaves SSH en GitHub](https://github.com/settings/keys), crear una nueva llave con el nombre que le quieras dar y el contenido de la llave pública de tu computadora.

![Añadir llave SSH a GitHu](https://i.ibb.co/CnCqHvq/3.png)

![Clonar repositorio GitHub con SSH](https://i.ibb.co/k1Q8YLt/4.png)

**Ahora se clona con SSH**

Ahora podemos actualizar la URL que guardamos en nuestro repositorio remoto, solo que, en vez de guardar la URL con HTTPS, vamos a usar la URL con SSH:

```bash
git remote set-url origin url-ssh-del-repositorio-en-git
```

## Tags y versiones en Git y GitHub

Los tags o etiquetas nos permiten asignar versiones a los commits con cambios más importantes o significativos de nuestro proyecto

Crear un nuevo tag y asignarlo a un commit
```bash
git tag -a nombre-del-tag -m "mensaje" id-del-commit.
eje: git tag -a V0.1 -m "primera version" IDCOMMIT
```
Para ver a que commit esta relacionado un tag es:

```bash
git show-ref --tags
```

Listar los tags de nuestro repositorio local: 

```bash
git tag o git show-refs --tags.
```

Borrar un tag en el repositorio local:

```bash
git tag -d nombre-del-tag
```

Publicar un tag en el repositorio remoto

```
git push origin --tags.
```

Borrar un tag del repositorio local y  remoto:

```bash
git tag -d nombre-del-tag 
git pull origin master
git push origin --tags
```

borrado de manera especial apra borrar de git hub
```bash
git push origin :refs/tags/nombre-del-tag.
```

## Manejo de ramas en GitHub

Mostrar las ramas que se han creado local

```bash
git show-branch --all
```

**Mostrar la historia de mi proyecto de una forma mas visual local**

```
gitk
```

Publicar una rama local al repositorio remoto

```
git push origin nombre-de-la-rama
```

## Configurar múltiples colaboradores en un repositorio de GitHub

Por defecto, cualquier persona puede clonar o descargar tu proyecto desde GitHub, pero no pueden crear commits, ni ramas, ni nada.

Existen varias formas de solucionar esto para poder aceptar contribuciones. Una de ellas es añadir a cada persona de nuestro equipo como colaborador de nuestro repositorio.

Solo debemos entrar a la configuración de colaboradores de nuestro proyecto <u>***(`Repositorio > Settings > Collaborators`)***</u> y añadir el email o username de los nuevos colaboradores.

**Comando en GIT  para traer un proyecto de otro lado, omo colaborador.**

```bash
git clone url-del repositorio-remoto
```

## Creando un Fork, contribuyendo a un repositorio

![Haciendo Fork a un repositorio](https://i.ibb.co/XSY0zKk/5.png)

* Se da clic en el botón de fork pra traer el proyecto a mi repositorio

* estando en mi repositorio git local con el comando git clone traigo  el proyecto fork a mi repositorio local

* se pueden realizar los cambios y subirlos a mi repositorio remoto y alli hacer un pull request hacia el repositrorio remoto original.

**Pull request es un commit intermedio**


**Actualizando mi repositorio que esta mas atrasado de el repositorio al que se le hizo fork**

en mi repositorio local se crea un origin para traer los cambios de master de el repositorio remoto- normalmente se le llama upstream

![Upstream](https://i.ibb.co/G26jDNw/6.png)

Ahora si se puede hacer un git pull pra traer los cambios de el repositorio remoto original a mi repositorio local

```bash
git pull upstream master
```

Con el siguiente comando se puede actualizar mi repositorio remoto fork

```
git push origin master
```

## Ignorar archivos en el respositorio con .gitignore

No todos los archivos que agregas a un proyecto deberían ir a un repositorio, por ejemplo cuando tienes un archivo donde están tus contraseñas que comúnmente tienen la extensión `.env` o cuando te estás conectando a una base de datos; **son archivos que nadie debe ver**.

Se crea un nuevo archivo en la raiz del proyecto y se debe llamar .gitignore, es una lista de los archivos a ignorar

![Creando archivo .gitignore](https://i.ibb.co/GP16yfK/7.png)

Ahora si se puede agregar el archivo .gitignore con git add y git commit, y enviarlos al repositorio remoto con git push

Es una mala practica guardar archivos binarios en un repositorio.

## Tu sitio web público con [GitHub Pages](https://pages.github.com/)

Se abre settings de mi repositorio y despues se busca github pages

![GitHub Pages](https://i.ibb.co/ZL0djqt/9.png)

En source se selecciona la rama master branch, y en repositorio name se coloca el nombre del repositorio con la extension .github.io

![Settings](https://i.ibb.co/q5tVfZk/10.png)

## Git Stash: Guardar cambios en memoria y recuperarlos después

Cuando necesitamos regresar en el tiempo porque borramos alguna línea de código pero no queremos pasarnos a otra rama porque nos daría un error ya que debemos pasar ese “mal cambio” que hicimos a stage, podemos usar `git stash` para regresar el cambio anterior que hicimos.

`git stash` es típico cuando estamos cambios que no merecen una rama o no merecen un *rebase* si no simplemente estamos probando algo y luego quieres volver rápidamente a tu versión anterior la cual es la correcta.

Guardamos un estado temporal
```bash
git stash
```

Vemos la lista de stash que tenemos
```bash
git stash list
```

Restablecemos el estado que teniamos guardado
```bash
git stash pop
```

Despues de haber creado un stash en memoria podemos crear una nueva rama con se cambio que esta en stash
```bash
git stash branch nombre-rama
```

Borramos un stash ya guardado
```bash
git stash drop
```

## Git Clean: Limpiar tu proyecto de archivos no deseados

A veces creamos archivos cuando estamos realizando nuestro proyecto que realmente no forman parte de nuestro directorio de trabajo, que no se debería agregar y lo sabemos.

- Para saber qué archivos vamos a borrar tecleamos `git clean --dry-run`
- Para borrar todos los archivos listados (que no son carpetas) tecleamos `git clean -f`

## Git cherry-pick: Traer commits viejos al head de un branch

Existe un mundo alternativo en el cual vamos avanzando en una rama pero necesitamos en *master* uno de esos avances de la rama, para eso utilizamos el comando `git cherry-pick IDCommit`.

![git cherry-pick](https://i.ibb.co/kJcCPgm/11.png)

se hace en la rama master y se trae el commit que queremos actualizar en master de la otra rama.

## Reconstruír commits en Git con amend

A veces hacemos un commit, pero resulta que no queríamos mandarlo porque faltaba algo más. Utilizamos `git commit --amend`, *amend* en inglés es remendar y lo que hará es que los cambios que hicimos nos lo agregará al commit anterior.

## Git Reset y Reflog: Úsese en caso de emergencia

¿Qué pasa cuando todo se rompe y no sabemos qué está pasando? Con `git reset HashDelHEAD` nos devolveremos al estado en que el proyecto funcionaba.

- `git reset --soft HashDelHEAD` te mantiene lo que tengas en staging ahí.
- `git reset --hard HashDelHEAD` resetea absolutamente todo incluyendo lo que tengas en staging.

>**git reset es una mala práctica, no deberías usarlo en ningún momento; debe ser nuestro último recurso.**

>**Git reflog**: con este comando se ve todo lo q se hizo. aca se busca el ultimo head donde todo era correcto.

## Buscar en archivos y commits de Git con Grep y log

A medida que nuestro proyecto se hace grande vamos a querer buscar ciertas cosas.

Por ejemplo: ¿cuántas veces en nuestro proyecto utilizamos la palabra *color*?

Para buscar utilizamos el comando `git grep color` y nos buscará en todo el proyecto los archivos en donde está la palabra *color*.

- Con `git grep -n color` nos saldrá un output el cual nos dirá en qué línea está lo que estamos buscando.
- Con `git grep -c color` nos saldrá un output el cual nos dirá cuántas veces se repite esa palabra y en qué archivo.
- Si queremos buscar cuántas veces utilizamos un atributo de HTML lo hacemos con `git grep -c "<p>"`.

**si queremos buscar una palabra q usaste en un commit se usa:**

```bash
git log -S "palabrabuscar"
```

## Comandos y recursos colaborativos en Git y Github

Ver cuantos commits a hecho los miembros del equipo
```bash
git shortlog
```

Ver las personas que han hecho ciertos commits
```bash
git shortlog -sn
```

Ver todos los commits (también los borrados)
```bash
git shortlog -sn --all
```

```bash
git shortlog -sn --all --no-merges

# ALIAS
git config --global alias.stats “shortlog -sn --all --no-merges”
```


Quien ha hecho cambios en dicho archivo
```bash
git blame -c index.js
```

```bash
git blame --help
```

Ramas remotas en el servidor
```bash
git branch -r
```

<br>

>**Created BY AugusTCaceresSuarez** :fire: :slightly_smiling_face:
>
>[@ACasuarz](https://twitter.com/ACasuarz) 
>
>[Github](https://github.com/UtoSkydive)

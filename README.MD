## Comandos basicos
inicializar un repositorio

    git init 

muestra los cambios realizados 

    git status

podemos ver que ha sido modificado

    git diff

realizamos un commit con un mensaje 

    git -m commit " " 

asi quitamos del stage 

    git reset nombre_del_archivo 

modificar un mensaje mal 

    git commit --amend -m "nuevo mensaje" 

cambiar el nombre y que git lleve control

    git mv nombre_del_archivo nuevo_nombre_del_archivo 

Este comando nos ayuda a eliminar archivos de Git sin eliminar su historial del sistema de versiones. Esto quiere decir que si necesitamos recuperar el archivo solo debemos “viajar en el tiempo” y recuperar el último commit antes de borrar el archivo en cuestión.

    git rm nombre_del_archivo 

 Elimina los archivos de nuestro repositorio local y del área de staging, pero los mantiene en nuestro disco duro. Básicamente le dice a Git que deje de trackear el historial de cambios de estos archivos, por lo que pasaran a un estado untracked.

    git rm --cached nombre_del_archivo

Elimina los archivos de Git y del disco duro. 

    git rm --force nombre_del_archivo

### git reset 
Este comando nos ayuda a volver en el tiempo. Pero no como git checkout que nos deja ir, mirar, pasear y volver. Con git reset volvemos al pasado sin la posibilidad de volver al futuro. Borramos la historia y la debemos sobreescribir. No hay vuelta atrás.

Hay dos formas de utilizar git reset: con el argumento --hard, borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre). O, un poco más seguro, con el argumento --soft, que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.

 Borramos todo el historial y los registros de Git pero guardamos los cambios que tengamos en Staging, así podemos aplicar las últimas actualizaciones a un nuevo commit.

    git reset --soft

Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.

    git reset --hard

git hace una marcha hacia el commit,

    git reset --soft id_commit 

devolvemos los archivos prsesentes en ese commit **CUIDADO: esto hace que todo lo que hubieras hecho antes de hacer el reset desaparezca**


    git reset --hard id_commit 

 Este es el comando para sacar archivos del área de staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.

    git reset HEAD

con eso  vemos el historial asi hallamos utilizado reset --hard

    git reflog 

va a un putno de nuestro 

    git reset --mixed id_commit 

muestra los cambios especificos que se hicieron en este commit 

    git log --stat

para ver los cambios un anterior version de un archivos usar: 

    git checkout id_commit <nombre del archivo(opcional )>
## Practica
**AHORA USEMOS ESTO QUE VIMOS PARA EMPEZAR**

### CASO 1 :
 Digamos que has creado tu proyecto de desde cero, te paras en la ruta raiz de tu proyecto
y abres una terminal en este sitio, lo primero que tienes que hacer es inicializar el 
repositorio git con el siguiente comando:

    git init 

ahora necsitamos agregar todos nuestros archivos para que git lleve historial de estos entonces:

    git add .

esto agrega todo si no quieres agregar todo y solo quieres llevar unos pues:

    git add <nombre del archivo que quieres agregar >

bueno entonces ahora ya quieres guardar este punto en la historia hacemos un commit :

    git commit -m "mensaje descriptivo del commit"

listo en este punto ya estamos listo para pasar todo a la nube pero primero tenemos que agregar a donde enviarla:

    git remote add <nombre que le quieras poner > <url del servicio qu estes usando (github,gitlab, etc..)>

esto agrega la ruta dode subiremos y ahora si lo subimos:

    git push <nombre que le pusiste en el paso anterior> -u

y listo ahi ya tendrias tu repo en la nube actualizado por primera vez conn lo que tienes en local.


### CASO 2 :
 digamos que ahora quieres colaborar en un repositorio, vamos a descargar todo el repo con :

    git clone <url del repo>

con esto lo obtenemos todo el repo en nuestra computadora nos movemos  a la nueva carpeta creada

    cd <nombre de la carpeta>

hacemos nuestras modificaciones y es hora de subirlo al repositorio

    git add .
    git commit -m "mensaje"
    git push <nombre que le colocaste al remote> <nombre de la rama>




## RAMAS
delete branch

    git branch -d branch_name 

crea una nueva rama

    git branch nombre_dela_rama 

muestra todo y las ramas que existen

    git log --oneline --decorate --all --graph 

se mueve a la rama mencionada

    git checkout nombre_dela_rama 

esto conecta ramas se tiene que estar parado en la rama a la que quiere que se una nombre_dela_rama
    
    git merge nombre_dela_rama

elimina la rama nombre_dela_rama

    git branch -d nombre_dela_rama 

crea una nueva rama nombre_dela_rama y nos dirige a ella

    git checkout -b nombre_dela_rama 
    
vuelve al anterior commit

    git reset --hard HEAD~1 

vuelve al anterior stage

    git reset --soft HEAD~1  


## MERGE CON CONFLICTOS
cuando estamos modificando en la misma linea hemos modificado 
abrimos el archivo borramos los temas en conflicto que aparecen con <<<HEAD >>>>nombre_dela_rama 
y ponemos el archivo como queremos que quede luego ejecutamos git add . despues git commit -m " mensaje" y quedara unido



## ETIQUETAS
crea una etiqueta que se le coloca a la rama

    git tag nombre_etiqueta

eliminar etiqueta nombre_etiqueta

    git rag -d nombre_etiqueta 

v1.0.0 la letra significa version el primer numero la mas alta version el segundo un cambio moderado y el tercero un cambio minimo

    git tag -a nombre_etiqueta -m "mensaje" 

nos muestra los cambios de la rama con esa etiqueta

    git show nombre_etiqueta

se etiqueta un commit 

    git tag -a nombre_etiqueta id_commit -m "mensaje"

## GIT HUB
**ESTO PARA SUBIR DE MI LOCAL AL github**
Inicializamos el repositorio

    git init

Agregamos un archivo readme.MD por buena practica para explicar nuestro proyecto y como correrlo

    git add README.md 

Hacemos nuestro primer punto en la historia del proyecto

    git commit -m "first commit"

Agregamos el repositorio remoto donde vamos a almacenar todos los cambios

    git remote add origin link_repo 

Actualizamos nuestro repo local con el remote

    git pull origin master 

subimos nuestras cosas al repositorio

    git push -u origin master 

Con esto sabemos la url a donde apunta el remote origin

    git config --get remote.origin.url 

Checar si tenemos problemas con la conexion al repo en github

    ssh -T git@github.com 



Es importante destacar que cuando recuperas (fetch) nuevas ramas remotas, no obtienes automáticamente una copia editable local de las mismas. En otras palabras, en este caso, no tienes una nueva rama serverfix. Sino que únicamente tienes un puntero no editable a origin/serverfix.

Para integrar (merge) esto en tu actual rama de trabajo, puedes usar el comando git merge origin/serverfix. Y si quieres tener tu propia rama serverfix, donde puedas trabajar, puedes crearla directamente basaádote en rama remota



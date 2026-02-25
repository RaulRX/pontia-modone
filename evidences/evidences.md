# Repositorio: pontia-repository

###### owner: Raúl Sánchez Serrano
###### url: https://github.com/RaulRX/pontia-modone.git
###### ssh: git@github.com:RaulRX/pontia-modone.git

# Flujo de trabajo, resolución de conflictos y funcionamiento de workflow

En primer lugar, se ha creado el repositorio en github con el nombre pontia-modone. Después, se ha ejecutado el comando **git init** sobre una carpeta local para inicializar el repositorio vacio y, posteriormente, se ha añadido a la configuración de git en local el nuevo reporitorio remoto creado en github con el comando **git remote add origin <repositorio_remoto>**

Una vez hecho esto, se ha creado el primer commit. Después, se ha protegido la rama master contra commits directos para que se deban crear pull request para mergear cambios en la rama principal (incluyendo los administradores)

Una vez protegida la rama **master**, se ha añadido el fichero **.gitignore** para evitar subir ficheros o carpetas innecesarios al repositorio remoto.

Se han creado dos ramas (**feature/suma** y **feature/resta**) con el objetivo de generar un conflicto en un fichero compartido por ambas ramas.

El conflicto se produjo siguiendo los siguientes pasos:

1. La rama **feature/suma** mergeo en la rama **master** el fichero **operations.py** con dos métodos: info y suma
2. Posteriormente, se quiso mergear nuevos cambios en el fichero **operations.py** desde la rama **feature/resta** a la rama **master**, la cual ya tenia cambios previamente mergeados sobre el mismo fichero.

¿Cómo se resolvió? Desde local, primero se actualizo la rama local **master**. Después, mergeamos la rama **master** contra la rama local **feature/resta** para obtener los conflictos y poder modificar el fichero afectado **operations.py** manualmente, quedándonos con los cambios que nos interesan. Una vez resueltos, pusheamos los cambios de la rama **feature/resta** y, de esta forma, desbloqueamos al pull request creada previamente para mergear los cambios contra la rama **master**

**¿Cómo funciona el workflow de GitHub Actions?** Github, al detectar una acción sobre una rama, busca los archivos yml en la carpeta .github/workflows. Por cada uno de ellos, ejecuta los jobs sobre una máquina definida en el fichero yml y ejecuta los steps definidos en él (primero hace checkout del código, prepara el entorno y ejecuta las acciones dentro del step). Si todos los jobs y steps se ejecutan ok, se marca el workflow como correcto. Si falla algun stepe de algun job, se notifica el error.

# 1. Creación del repositorio y primer commit
En primer lugar, se ha creado un repositorio remoto en Github con el nombre pontia-modone. Una vez creado, se ha creado una carpeta en local con el nombre del repositorio remoto, y hemos ejecutado el comando **git init** para inicializar el repositorio local con la carpeta .git, donde se recogerá toda la información referente al repositorio remoto. En este momento, se ha creado la rama master (en adelante, la rama *main*)

una vez inicializado el repositorio local con la carpeta **.git**, se ha creado el fichero **README.md** con el nombre completo y la fecha de creación

##### Comando ejecutado junto con el 
 ![Ejemplo de imagen](./images/ejercicio_1/git_init.png)

##### Documento README.md creado
 ![Ejemplo de imagen](./images/ejercicio_1/README.png)

Después, se ha procedido a realizar realizar los siguientes pasos:

1. Añadir el repositorio remoto a la configuración de git como origin
2. Hacer commit del nuevo fichero **README.md**
3. Hacer push de fichero a la rama **master** con el fichero añadido

##### Añadir repositorio remoto, commit y push del fichero README.md
 ![Ejemplo de imagen](./images/ejercicio_1/primer_commit_push_add_remote.png)

# 2. Configuración y protección de la rama principal (master)

Para proteger la rama master contra loc commits directos, desde el repositorio remoto se ha configurado en los settings de las ramas la configuración de la siguiente imagen:

##### Regla *Required a pull request before merging* directamente en la rama master
 ![Ejemplo de imagen](./images/ejercicio_2/restriccion_rama_master_github.png)

##### Regla *Required a pull request before merging* sobre rama master configurada
 ![Ejemplo de imagen](./images/ejercicio_2/confirmacion_regla_rama_master.png)

Adicionalmente, se ha configurado la siguiente regla para que los administradores o roles de administración del repositorio remoto no puedan saltarte la anterior configuración

##### Regla adicional directamente en la rama master
 ![Ejemplo de imagen](./images/ejercicio_2/additional_option.png)

Una vez configurada las reglas de la rama master para el repositorio remoto, se ha procedido a comprobar si la regla se ha configurado correctamente realizando un commit directamente sobre la rama **master**

#### Intento fallido de commit sobre la rama master
 ![Ejemplo de imagen](./images/ejercicio_2/push_falla_restricciones_rama_master.png)

### 2.1. ¿Por qué es recomendable proteger la rama principal en un proyecto real?

La razón es la siguiente: En un proyecto real habrá muchos colaboradores trabajando en un mismo repositorio. Si todos los colaboradores suben cambios del proyecto sobre la rama main, esto puede provocar un crecimiento descontrolado y cometer errores. Además, imposibilita el trabajo en paralelo por parte de los colaboradores, haciendo muy poco eficiente el trabajo diario

Con pull request, evitamos un mayor número de errores al verificar los cambios de otros colaboradores, además de hacer más eficiente el trabajo en paralelo.

# 3. Uso del archivo *gitignore*

En primer lugar, debido a que la rama master esta protegida ante commits, se ha creado la rama **feature/gitignore**

![Ejemplo de imagen](./images/ejercicio_3/creacion_rama_gitignore.png)

Posteriormente, se ha creado con el comando ***touch*** el fichero **.gitignore** añadiendo los siguientes paths: **\*\*/*.logs** y **\_\_pycache\_\_** para poder ignorar lo siguiente:
- Ficheros con extension .log, localizados en la raiz del proyecto o dentro de cualquier carpeta o subcarpeta
- Carpeta \_\_pycache\_\_ junto con su contenido

##### Prueba de ficheros ignorados con el comando **git check-ignore** y verificando con git status que no se añaden los ficheros con extension .log ni la carpeta \_\_pycache\_\_
![Ejemplo de imagen](./images/ejercicio_3/ignorando_ficheros.png)

A continuación, se ha procedido a realizar la merge request,  mergeando la rama **feature/gitignore** en la rama master

##### Creación de la pull request
![Ejemplo de imagen](./images/ejercicio_3/merge_pr_gitignore.png)

##### Mergeo de la pull request
![Ejemplo de imagen](./images/ejercicio_3/merged_gitignore_master.png)

Añadido, tenemos el fichero gitignore-status.txt donde podemos ver la salida del comando **git status --ignored**, donde la opcion **--ignore** nos permite visualizar los ficheros que serán ignorados

##### Fichero gitignore-status.txt
![Ejemplo de imagen](./images/ejercicio_3/gitignore_status_file.png)

### 3. Justificación del uso del fichero *.gitignore*

El fichero *gitignore* permite a git no rastrear carpetas o ficheros que no queremos tener en cuenta a la hora de subir cambios al repositorio.

La gran ventaja es no almacenar ficheros o carpetas que consumen almacenamiento innecesario, los cuales pueden ser muy pesados (Ejemplo: node_modules o pycache)


# 4. Creación de ramas

Antes de crear ramas, he actualizado la rama master con los últimos cambios realizados. A partir de aqui, he creado la ramas **ferature/suma** y **feature/resta** a partir de la rama master con el comando **git switch -c nombre_rama**

##### Creación de ramas feature/suma y feature/resta
![Ejemplo de imagen](./images/ejercicio_4/creacion_ramas_suma_resta.png)

Una vez creadas ambas ramas, se ha procedido a crear en cada una de ellas el fichero **operations.py**.
En primer lugar, en la rama **feature/suma** se han añadido las funciones **suma** e **info**. Después, en la rama **feature/resta** se han creado las funciones **info** y **resta**
Una vez se han creado en ambas ramas las funciones, se ha procedido a subir los cambios de cada rama al repositorio remoto

##### Fichero operations.py con funciones info y suma
![Ejemplo de imagen](./images/ejercicio_4/push_feature_suma.png)

##### Fichero operations.py con funciones info y resta
![Ejemplo de imagen](./images/ejercicio_4/push_feature_resta.png)

Una vez hecho push de ambas ramas, se han creado las pull request de cada una de ellas sin realizar el merge

##### Pull request de la rama feature/suma
![Ejemplo de imagen](./images/ejercicio_4/pr_feature_suma.png)

##### Pull request de la rama feature/suma
![Ejemplo de imagen](./images/ejercicio_4/pr_feature_resta.png)

# 5. Simulación y resolución de conflictos

Del anterior ejercicio, teníamos dos Pull request de las ramas **feature/suma** y **feature/resta** pendientes de mergear contra la rama **master**. Para provocar un conflicto y resolverlo, se realizó los siguientes pasos:

1. Mergeo de la pull request de la rama **feature/suma** en la rama **master**
2. Mergeo de la pull request de la rama **feature/suma** en la rama **master**. Esto provocará un conflicto, dado que el fichero *operations.py* ya fue modificado en la rama **feature/suma**.

##### Mergeo rama feature/suma en main
![Ejemplo de imagen](./images/ejercicio_5/merged_feature_suma.png)

##### Mergeo de la rama feature/resta en main (conflictos no permiten mergear)
![Ejemplo de imagen](./images/ejercicio_5/conflicts_merge_feature_resta.png)

Ahora, para mergear la pull request de la rama **feature/resta** se han de resolver los conflictos del repositorio local. Para ello, primero se ha actualizado la rama **master** en local y, después, mergearemos en la rama **feature/resta** la rama **master**

##### Actualización rama master en local
![Ejemplo de imagen](./images/ejercicio_5/update_master_feature_suma.png)

##### Mergear rama feature/resta contra master y ver conflictos generados
![Ejemplo de imagen](./images/ejercicio_5/conflicts_to_resolve_feature_resta.png)

Visto los conflictos que se han generado, ahora hay que resolverlos manualmente:

##### Resolución de los conflictos (Dejamos las funciones info, suma y resta)
![Ejemplo de imagen](./images/ejercicio_5/conflict_solved_feature_resta.png)

Una vez se han solucionado, pushearemos los cambios en la rama **feature/resta**, actualizando la pull request asociada a la rama, y desbloqueando la pull request para poder mergearla contra la rama remota **master**. Una vez se desbloqué la pull request, se procedió a realizar el merged de la pull request contra la rama **master**

##### Push de la resolución de los conflictos
![Ejemplo de imagen](./images/ejercicio_5/pushed_solved_conflicts.png)

##### Desbloqueo de la pull request para mergear contra la rama master
![Ejemplo de imagen](./images/ejercicio_5/merged_available_after_conflicts_solved.png)

##### Aprobación y mergeo de la pull request contra la rama master completado
![Ejemplo de imagen](./images/ejercicio_5/pr_merged_after_conflicts_solved.png)

A continuación, comprobaremos con el comando **git log --oneline --graph --all** el log de git donde veremos la resolución del conflicto

##### Ejecución del comando git log --oneline --graph --all
![Ejemplo de imagen](./images/ejercicio_5/git_log_info.png)

##### Fichero git-log.txt con la ejecución del comando git log
![Ejemplo de imagen](./images/ejercicio_5/git_log_conflicts_solved.png)


# 6. Automatización con Github Actions

En primer lugar, para asegurar que la rama **master** en local esta actualizada contra la rama remota, nos movemos a la rama **master** y ejeuctamos el comando **git pull origin**

Una vez hecho esto, se crea la nueva rama **feature/ci** con el comando **git switch -c feature/ci**. Después, se crea la carpeta **.github**, dentro la subcarpeta **workflow** (ambos con el comando mkdir) y, por último, con el comando **touch**, se crea el fichero **demo.yml** el cual contendrá el workflow que queremos ejecutar

##### Creación rama feature/ci y las carpetas .github/workflow con el fichero demo.yml
![Ejemplo de imagen](./images/ejercicio_6/branch_featureci_create_workflow.png)
d
A continuación, se crea el workflow de tipo dispatch donde será necesario introducir el nombre y apellidos para ejecutarlo. Al ejecutarlo, se mostrará el nombre completo

##### Fichero demo.yml con el workflow generado
![Ejemplo de imagen](./images/ejercicio_6/workflow_data.png)

Una vez creado el workflow, pusheamos en la rama **feature/ci** el nuevo workflow al repositorio remoto

##### Commit y push de la rama feature/ci
![Ejemplo de imagen](./images/ejercicio_6/pushed_workflow.png)

Después, creamos la pull request de la rama para mergear los cambios de la rama **feature/ci** en la rama **master**

##### Creación de la pull request de la rama feature/ci
![Ejemplo de imagen](./images/ejercicio_6/pull%20request%20created.png)

##### Mergeo de la pull request feature/ci contra master
![Ejemplo de imagen](./images/ejercicio_6/pull%20request%20merged.png)

Al mergear en la rama master, se creará el action creado en el fichero demo.yml

##### Action creado
![Ejemplo de imagen](./images/ejercicio_6/workflow_created.png)

Como se puede comprobar en la siguiente imagen, el workflow todavía no se ha ejecutado, ya que debemos introducir el nombre y los apellidos

##### Inputs del workflow requeridos
![Ejemplo de imagen](./images/ejercicio_6/workflow_waiting_to_run.png)

Una vez introducidos los inputs, se ejecutará el workflow

##### Ejecución correcta del workflow
![Ejemplo de imagen](./images/ejercicio_6/workflow_run_successfully.png)

Ahora, verificamos que la salida de la ejecución es el nombre completo que hemos introducido antes de ejecutar el workflow

##### Salida de la ejecución del workflow
![Ejemplo de imagen](./images/ejercicio_6/printed_fullname.png)

Finalmente, generaremos un badge para introducir al final de este **README.md** y visualizar su estado cada vez que se ejecute

##### Badge generado y README.md actualizado
![Ejemplo de imagen](./images/ejercicio_6/status_badged_created.png)

##### Badge generado desde el workflow creado y su estado actual
 [![Workflow demo](https://github.com/RaulRX/pontia-modone/actions/workflows/demo.yml/badge.svg)](https://github.com/RaulRX/pontia-modone/actions/workflows/demo.yml)
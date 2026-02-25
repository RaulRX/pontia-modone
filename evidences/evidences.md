# Repositorio: pontia-repository

###### owner: Raúl Sánchez Serrano
###### url: https://github.com/RaulRX/pontia-modone.git
###### ssh: git@github.com:RaulRX/pontia-modone.git

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

##### Ejecución del comando git log
![Ejemplo de imagen](./images/ejercicio_5/git_log_conflicts_solved.png)

# 6. Automatización con Github Actions
## Comandos de GIT

GIT

	-- working directory
	-- staging area
	-- repository

Ver la versión de GIT

	git --version

Para configurar el nombre de usuario

	git config --global user.name '[NAME]'

Para configurar el email del usuario

	git config --global user.email "[EMAIL]"

Para ver la configuracion en general

	git config --global -e

Indicar a GIT que VScode es nuestro editor de texto por defecto

	git config --global core.editor "vim"
	git config --global core.editor "nvim"
	git config --global core.editor 'code --wait'

Indicar el nombre por defecto de la rama principal, por defecto viene en 'master', pero se recomienda que tenga el nombre de 'main'

	git config --global init.defaultBranch [NAME]

Variable de nuevo salto de linea

	git config --global core.autocrlf true (en caso de que sea windows)
	git config --global core.autocrlf input (en caso de que sea linux o mac)

Para iniciar un nuevo proyecto

	git init

Para ver el estado de nuestros archivos

	git status

Agregar archivos al staging area

	git add [FILE]

Agregar todos los archivos al staging area

	git add .

Para crear el primer punto de control del código

	git commit -m '[MENSAJE	]'

Para ver todos los commits que hemos creado

	git log

Revertir cambios de los archivos

	git checkout -- [FILE]

Ver la diferencia hechas en los archivos

	git diff [FILE]

Ver la diferencia hechas en los archivos en el area de stage

	git diff --staged [FILE]

Excluir un archivo del proyecto

	→ crear un archivo llamado .gitignore y dentro de este añadir los nombres de los archivos a ignorar.

Ver las lineas principales del proyecto

	git branch

Crear una rama del proyecto principal

	git branch [NAME]

Crear una rama del proyecto y moverse a ella

	git checkout -b [BRANCHNAME]

Moverse a una rama del proyecto	

	git checkout [BRANCHNAME]

Sacar un archivo del área de stage

	git restore --staged [FILE]  

Restaurar un archivo

	git restore [FILE]

Renombrar un archivo con el comando git

	git mv [OLDNAME] [NEWNAME]

Ver un resumen del status de los archivos

	git status -s

Ver los commits mostrando el hash

	git log --oneline
	git log --oneline --reverse

Traer los comandos de la rama a la rama principal

	git merge [RAMA]

Agregar un servidor remoto

	git remote add origin https:#github.com/luis-am/lalala.git

Subimos nuestro codigo

	git push -u origin [RAMA]

Ver la ayuda de git

	git config -h

Ver los archivos en el stage area

	git ls-files

Borrar un file de manera directa

	git rm [FILE]

Sacar un file del staging area

	git rm -r --cached [FILE]

Ver los detalles de commits

	git show [FINGERPRINT]

 Ver los commits

	git ls-tree [FINGERPRINT] 

Eliminar los archivos untracked

	git clean -fd

Cambiar un nombre del commit
	git commit --amend -m "MESSAGE"

Cambiar el nombre del archivo

	git mv [OLD FILENAME] [NEW FILENAME]

Si no estan sincronizados el repositorio local con el remoto hacer lo siguiente

	git pull --rebase origin main
	git push origin main

Abreviación rápida

	git init
	git config --global user.name "Luis Ayala"
	git config --global user.email voltluis220@gmail.com
	git config --global core.autocrlf true
	git config --global -e

	git add [FILENAME]
	git commit -m "Primer commit."
	git remote add origin https:#github.com/luis-am/lalala.git

## Pasos de Freddy:

PASO 1:
	git remote add upstream REPOSITORIO PRINCIPAL
PASO 2:
	git remote -v
PASO 3:
	git fetch upstream
PASO 4:
	git checkout main  # Cambia a la rama principal de tu fork
PASO 5: 
	git merge upstream/main

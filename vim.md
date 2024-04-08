## Comandos de VIM

Modo comando o normal

	ESC

Modo insertar

	i

Modo agregar

	a

Mover el cursor arriba

	k

Mover el cursor abajo

	j

Mover el cursor a la derecha

	l

Mover el cursor a la izquierda

	h

Mover el cursor al inicio de la palabra

	b

Mover el cursor al final de la palabra

	e

Mover el cursor al inicio de la linea

	0

Mover el cursor al final del archivo

	G

Mover el cursor al inicio del archivo

	gg

Mover el cursor al termino de la pantalla

	L

Mover el cursor para que haga match con parentesis

	%

Mover el cursor a la funcion start

	[[

Mover el cursor a la funcion end

	]]

Mover el cursor a la funcion block start

	[{

Abrir una nueva pestana

	:tabnew

Ir a la siguiente pestana

	gt

Copiar el texto seleccionado

	y

Pega el texto seleccionado

	p

Copia la palabra al buffer

	yiw

Corta la linea actual

	dd

Cortar lineas consecutivas

	#dd [example: 2dd]

Copia la linea actual

	yy

Copia hasta el final de la linea

	y$

Copia hasta el inicio de la linea

	y0

Corta hasta el final

	D

Cambia la linea entera:

	cc

Cambia hasta el final de la linea:
	C

Cambia la letra uppercase o lowercase:

	~

Poner a minusculas toda la linea

	Vu

Poner a mayusculas toda la linea

	VU
	V~

Incrementa el numero que esta despues del cursor

	ctrl + a

Decrementa el numero que esta despues del cursor

	ctrl + x

Guardar el archivo

	:w

Guardar el archivo y salir

	:wq

Salir sin guardar el archivo

	:q!

Guardar como

	:sav [nuevo archivo].txt

Buscar el texto que esta debajo del cursor

	*

Eliminar el caracter antes del cursor

	x

Borrar una palabra completa hasta el ultimo caracter

	dw

Borrar una palabra completa sin incluir el ultimo caracter

	de

Borrar desde una palabra hasta el final de la linea

	d$

Moverse al final de palabras siguientes

	#w [example 2w]

Moverse al inicio de palabras siguientes

	#e [example 2e]

Moverse al inicio de la linea

	0

Eliminar el numero de palabras siguientes

	d#w [example d2w]

Deshacer ultimo comando
	u

Arregla la linea actual a su estado original

	U

Rehacer ultima accion

	ctrl + r

Reemplazar un caracter

	r[letra por el que se va cambiar]

Reemplazar hasta el final de la palabra

	ce
	ciw
	caw
	cw
	
Reemplazar hasta el final de la linea

	c$

Ver status del file

	ctrl + g

Ir a una linea en concreto

	[numero]G [example quiero ir a la linea 2 entonces es 2G]

Para buscar una palabra

	/[palabra]

Para seguir buscando la misma palabra [forward]

	n

Para seguir buscando la misma palabra [backward]

	N

Para ir a donde empezamos

	ctrl + o

Sustituir una palabra en la misma linea

	s/oldword/newword/g

Sustituir una palabra en todo el file

	%s/oldword/newword/g

Sustituir una palabra en todo el file preguntando primero

	%s/oldword/newword/gc

Ver la lista de archivos en el directorio actual

	:!dir

Entrar al modo visual y guardarlo en otro archivo

	v
	:w [nuevo archivo]

Eliminar texto seleccionado

	v luego d

Retrieve texto de otro archivo

	:r [archivo existente en directorio]

Entrar al modo insercion una linea después del cursor

	o

Entrar al modo insercion una linea antes del cursor
	O

Borrar desde posicion actual hasta final del archivo

	dG

Ir al inicio del archivo

	H

Ir al medio del archivo

	M

Ir al final del archivo

	L 

Dejando en blanco una linea

	cc

Borrar una palabra alrededor del cursor y pone en modo insercion

	caw 

Borrar una palabra alrededor del cursor

	daw 

Indentar

	shift + <

Regresar indentacion

	<

Abrir un nuevo file y abre horizontalmente 

	:sp

Abrir un nuevo file y abre verticalmente

	:vsp

Listar los buffers abiertos

	:ls

Splits windows horizontally

	ctrl + ws

Splits windows vertically

	ctrl + wv

Switch between windows

	ctrl + ww

Quit a window

	ctrl + wq

Mueve el cursor a la ventana izquierda

	ctrl + wh

Mueve el cursor a la ventana derecha

	ctrl + wl

Mueve el cursor a la ventana de abajo

	ctrl + wj

Mueve el cursor a la ventana de arriba

	ctrl + wk

Comenzar el modo visual

	v

Linewise visual mode

	V

Visual block mode (select columnas)

	ctrl + v

Una vez seleccionado swap case

	altgr + +

Crear un nuevo tab

	:tabedit file

Moverse al siguiente tab

	gt

Moverse al previo tab

	gT

Lista todos los tabs

	:tabs

Cerrar el tab actual

	:tabclose
	
Listar los archivos actuales

	:e + SPACE + ctrl+D

Comment multiple lines

	primero ctrl + v
	segundo seleccionamos las lineas a comentar
	tercero shift + I
	cuarto escribe la letra
	quinto ESC

	ctrl + v
	shift + g
	shift + i
	#
	esc

Borrar lineas en blanco

	:g/^$/d

Limpiar el resaltado luego de una busqueda

	:noh

Guardar los cambios (atajo)

	shift + zz

Repetir el último comando:

	. →→ punto

Activar / desactivar vista líneas a la izquierda:

	:set number
	:set nonumber

Unir el texto de otro archivo al actual:

	:r [FILE2]

Scroll up half a screen

	ctrl + u

Scroll down half a screen

	ctrl + d

Scroll up half a screen

	ctrl + b

Scroll down half a screen

	ctrl + f

Scroll the screen up one line, without moving the cursor

	ctrl + e

Scroll the screen down one line, without moving the cursor

	ctrl + y

Scrolls the page so the current line in the middle of the screen

	zz

Copiar todas las lineas del file

	ggVGy

Copiar todas las lineas del file (nvim)

	:%y+
	,all

Poner marca en una linea

	m[LETRA]
	ejemplo: ma
	ejemplo: mb

Ir a la linea donde esta la marca

	'[LETRA]
	ejemplo: 'a
	ejemplo: 'b

Ver todas las marcas

	:marks

Borrar todas las marcas

	:delm!

Cambiar el size de la indentacion

	:set shiftwidth=#

Copiar todo contenido del parentesis
Copiar todo contenido incluyendo los simbolos de parentesis

	vib
	vab

Copiar todo contenido del bracket
Copiar todo contenido incluyendo los simbolos de brackets

	viB
	vaB

Cambiar los alrededores, en el ejemplo se muestra el cambio de comillas dobles a comillas simples

    "Hola, esto es una prueba."
    comando: cs"'
    'Hola, esto es una prueba.'



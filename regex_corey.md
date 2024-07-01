## Expresiones Regulares Posix & Metacaracteres

[:blank:]
[:digit:]
[:lower:]
[:upper:]
[:punct:]

Meta - The digit

	\d

Meta - The dot

	.

Meta - Match con caracteres específicos

	[abc]

Meta - Excluyendo caracteres específicos

	[^abc]
	
	hog
	dog
	bog
	[^b]og

Meta - Rango de caracteres

	[a-z]
	[A-Z]
	[0-9]

Meta - Repeticiones

	wazup	
	wazzzup
	wazzzzzup

	waz{3,5}up


Meta - Mr. Kleener (ejemplo)

	a+ : un caracter 'a' a más.	
	a* : cero caracteres a más.

Meta - Caracteres Opcionales

	abc? : la 'c' vendría ser opcional entonces el resultado sería ab o abc

Meta - Todos son espacios en blanco

	space (_)
	tab (\t)
	new line (\n)
	whitespace (\s)

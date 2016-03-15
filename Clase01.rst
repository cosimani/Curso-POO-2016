.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 01 - POO 2016
===================

    :Autor: César Osimani
    :Correo: cosimani@ubp.edu.ar - cesarosimani@gmail.com
    :Fecha: 15 de marzo de 2016
    :Regularidad: 
    	- 2 parciales 
	- 1 TPU como tercer parcial
	- Presentación de trabajos en CoNaIISI 2016
		- http://www.ucasal.edu.ar/conaiisi2016/ – Hasta 16 de septiembre
			- Se presentan avances en lugar de cada parcial y TPU
	    	- Pueden proponer otro congreso
    :Temas principales: 
		- Espacio de nombres
		- inline y const
		- std, vector, string
		- Aritmética de punteros
		- Funciones genéricas
		- Herencia y herencia múltiple
		- Polimorfismo
		- Funciones virtuales
		- Clases abstractas
		- Modificador friend
		- Biblioteca Qt
			- Uso de documentación
			- slots y signals
			- QtNetwork
			- Interfaz gráfica de usuario (widgets, layouts, etc.)
			- QPainter y captura de eventos del teclado y del mouse
			- QTimer
			- QtDesigner
		- OpenGL (glOrtho, gluPerspective, glLookAt, rotación, traslación, texturas, ...)
		- Base de datos (SELECT e INSERT).
		- Resolver los problemas consultando documentación técnica de distintas fuentes


Biblioteca estándar de C++
==========================

.. figure:: images/clase01/comparacion_cpp_c.png

Espacio de nombres (namespace)
==============================

- Permite agrupar declaraciones (de clases, funciones, etc.).
- Permite declarar identificadores (nombre de variables) sin que se solapen. Es decir, identificadores iguales en distinto namespace.
- Se pueden incluir las definiciones en un namespace pero mejor no.
- Un espacio de nombre es un ámbito.

Ejemplos con namespace
======================

- Ejemplo 1:
.. code-block:: c

	#include <iostream>
	using namespace std;

	namespace enteros  {
	    int var1 = 5;
	    int var2 = 7;
	}

	namespace con_decimales  {
	    float var1 = 5.14;
	    float var2 = 7.13;
	}

	int main()  {
	    cout << enteros::var1 << endl;
	    cout << con_decimales::var1 << endl;
	    return 0;
	}

- ¿Cuál es la salida por consola?

 <!--- Need blank line before this line (and the .. line above).
 HTML comment written with 3 dashes so that Pandoc suppresses it.
 Blank lines may appear anywhere in the comment.

 All non-blank lines must be indented at least one space.
 HTML comment close must be followed by a blank line and a line
 that is not indented at all (if necessary that can be a line
 with just two periods followed by another blank line).
 --->



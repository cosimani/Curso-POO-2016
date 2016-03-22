.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 03 - POO 2016
===================

Punteros
========

**Declaración**

.. code-block:: c

	int* entero;     // entero es un puntero a int
	char* caracter;  // puntero a char

	entero 	es el puntero
	*entero 	es el contenido


**Punteros a variables**

.. code-block:: c

	int entero;         // entero es una variable int
	int* pEntero;       // pEntero es un puntero a int
	pEntero = &entero;  // &entero es la dirección de memoria donde se almacena entero

**Arrays y punteros**

.. code-block:: c

	int miArray[10];	// miArray es como un puntero al primer elemento
	int* puntero;

	puntero = miArray;  // similar a:  puntero = &miArray[0];
	(*puntero)++;       // equivale a miArray[0]++;  // incrementa
	puntero++;          // equivale a &miArray[1];  // se mueve una posición

	puntero = puntero + 3;  // se desplaza 3 posiciones int

**Array como parámetro en funciones**

.. code-block:: c

	#include <iostream>
	using namespace std;

	void funcion(int miArray[]);
	// Le estamos pasando un puntero al primer elemento del array.

	int main()  {
	    int miA[5] = {0, 1, 2, 3, 4};

	    funcion(miA);

	    cout << miA[0] << miA[1] << miA[2] << miA[3] << miA[4];
	}

	void funcion(int miArray[])  {
	    miArray[0] = 5;  // Las modificaciones quedarán.

	    miArray[3] = 5; 
	} 

**Ejercicio:** Escribir la salida por consola de la siguiente aplicación:

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication app(argc, argv);

	    int a = 10, b = 100, c = 30, d = 1, e = 54;
	    int m[10] = {10, 9, 80, 7, 60, 5, 40, 3, 20, 1};
	    int *p = &m[3], *q = &m[6];

	    ++q;
	    qDebug() << a + m[d/c] + b-- / *q + 10 + e--;

	    p = m;
	    qDebug() << e + *p + m[9]++;

	    return 0;
	}

**Función con número indefinido de parámetros**

- Requiere #include <cstdarg>
- Imprime los enteros que se pasen como parámetro
- Se puede comprender la sintaxis de:

.. code-block:: c

	int printf(const char* format, ...)

.. code-block:: c

	void imprimirParametros(int cantidad, ...)  {

	    va_list argumentos; // esta linea declara la lista de parametros

	    // esta linea empieza el bucle sobre la lista de parametros (sin saber
	    // el numero de parametros)
	    va_start(argumentos, cantidad); 

	    for (int i=0 ; i<cantidad ; i++)  {

	        int valor = va_arg( argumentos, int );  // Devuelve en formato de int

	        cout << valor << endl;
	    }

	    va_end(argumentos);  // Para limpiar la pila de parametros
	}
	
	
Primer aplicación en Qt con interfaz gráfica
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Qt(Quasar Toolkit) 
	- Biblioteca para desarrollo de software de Quasar Technologies
	- Se llamó también Trolltech
	- Biblioteca multiplataforma
	- En el 2008 lo compró Nokia
	- Aplicaciones escritas con C++ (Qt)
		- KDE
		- VLC Media Player
		- Skype
		- VirtualBox
		- Google Earth 
	- En 2012 Digia compra Qt y comercializa las licencias 
	- Digia desarrolló herramientas para usar Qt en iOS, Android y Blackberry.
		
.. code-block:: c

	#include <QApplication>	
	// - Administra los controles de la interfaz
	// - Procesa los eventos
	// - Existe una única instancia
	// - Analiza los argumentos de la línea de comandos

	int main(int argc, char** argv)  {	
	    // app es la instancia y se le pasa los parámetros de la línea
	    // de comandos para que los procese.
	    QApplication app(argc, argv); 

	    QLabel hola("<H1 aling=right> Hola </H1>");
	    hola.resize(200, 100);
	    hola.setVisible(true);

	    app.exec();  // Se le pasa el control a Qt
	    return 0;
	}

Signals y slots
^^^^^^^^^^^^^^^

- signal y slot son funciones.
- Las signals de una clase se comunican con los slots de otra.
- Se deben conectar con la función connect de QObject.
- Un evento puede generar una signal.
- Los slots reciben estas signals.
- SIGNAL() y SLOT() son macros (convierten a cadena).
- emisor y receptor son punteros a QObject:

.. code-block:: c

	QObject::connect(emisor, SIGNAL(signal), receptor, SLOT(slot));
	
- Se puede remover la conexión:

.. code-block:: c

	QObject::disconnect(emisor, SIGNAL(signal), receptor, SLOT(slot));

**Ejemplo:** QPushButton para cerrar la aplicación.

.. code-block:: c

	#include <QApplication>
	#include <QPushButton>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);
	    QPushButton* boton = new QPushButton("Salir");

	    QObject::connect(boton, SIGNAL(clicked()), &a, SLOT(quit()));
	    boton->setVisible(true);
		
	    return a.exec();
	}

**Ejemplo:** Control de volúmen

.. code-block:: c

	#include <QApplication>
	#include <QWidget>
	#include <QHBoxLayout>
	#include <QSlider>
	#include <QSpinBox>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    QWidget* ventana = new QWidget;  // Es la ventana padre (principal)
	    ventana->setWindowTitle("Volumen"); 
	    ventana->resize(300, 50);

	    QSpinBox* spinBox = new QSpinBox;
	    QSlider* slider = new QSlider(Qt::Horizontal);
	    spinBox->setRange(0, 100);
	    slider->setRange(0, 100);

	    QObject::connect(spinBox, SIGNAL(valueChanged(int)), slider, SLOT(setValue(int)));
	    QObject::connect(slider, SIGNAL(valueChanged(int)),  spinBox, SLOT(setValue(int)));

	    spinBox->setValue(15);

	    QHBoxLayout* layout = new QHBoxLayout;
	    layout->addWidget(spinBox);
	    layout->addWidget(slider);
	    ventana->setLayout(layout);
	    ventana->setVisible(true);	

	    return a.exec();
	}

**Ejercicio 2:**

- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor (de 0 a 100). 
	

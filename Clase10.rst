.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 10 - POO 2016
===================

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/UFfZlUgfQ6U/0.jpg)](http://www.youtube.com/watch?v=UFfZlUgfQ6U)


Polimorfismo
^^^^^^^^^^^^

- Lo utilizamos con punteros.
- Nos permite acceder a objetos de la clase derivada usando un puntero a la clase base.
- Sin embargo, sólo podemos acceder a datos y funciones que existan en la clase base.
- Los datos y funciones propias de la derivada quedan inaccesibles.

.. code-block:: c

	class Persona  {
	public:
	    Persona(QString nombre) : nombre(nombre)  {  }
	    QString verNombre()  {  return "Nombre: " + nombre;  }

	protected:  // Para acceso desde las clases derivadas
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	    void mostrarAlgo()  {  qDebug() << "Algo";  }
	};

	class Estudiante : public Persona  {
	public:
	    Estudiante(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Estudiante: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    {
	    Persona *jose = new Estudiante("Jose");
	    Persona *carlos = new Empleado("Carlos");

	    qDebug() << carlos->verNombre();
	    qDebug() << jose->verNombre();
	    //  carlos->mostrarAlgo();  // No compila. mostrarAlgo() no es de Persona

	    delete jose;
	    delete carlos;
	    }

	    return a.exec();
	}

Funciones virtuales
^^^^^^^^^^^^^^^^^^^

- Puede ser interesante llamar a la función de la derivada (en polimorfismo).
- Al declarar una función como virtual en la clase base, si se superpone en la derivada, al invocar usando el puntero a la clase base, se ejecuta la versión de la derivada.

.. code-block:: c

	class Persona  {
	public:
	    Persona(QString nombre) : nombre(nombre)  {  }
	    virtual QString verNombre()  {  return "Persona: " + nombre;  }

	protected:  
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado(QString nombre) : Persona(nombre)  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main(int argc, char** argv)  {
	    QApplication a(argc, argv);

	    {
	    Persona *carlos = new Empleado("Carlos");

	    qDebug() << carlos->verNombre();

	    delete carlos;
	    }

	    return a.exec();
	}











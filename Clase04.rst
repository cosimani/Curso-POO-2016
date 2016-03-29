.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 04 - POO 2016
===================

**Ejemplo:** Control de volumen

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

**Ejercicio:**

- Cuando el valor del QSlider se modifique, colocar como título de la ventana el mismo valor (de 0 a 100). 
	

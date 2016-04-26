.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 12 - POO 2016
===================

**Algunos argentinos que también explican como los mexicanos** 

- Clic sobre los GIF para abrir los videos 

**Crear base de datos**

|ImageLink|_ 

.. |ImageLink| image:: /images/clase12/crearBase.gif
.. _ImageLink: https://www.youtube.com/watch?v=U9iE6pM0bxM

**Crear tabla**

|ImageLink|_ 

.. |ImageLink| image:: /images/clase12/crearTabla.gif
.. _ImageLink: https://www.youtube.com/watch?v=_-hKca2k784

**Insertar registro**

|ImageLink|_ 

.. |ImageLink| image:: /images/clase12/insertarRegistro.gif
.. _ImageLink: https://www.youtube.com/watch?v=RggFhFZnCPU

**Consultar datos**

|ImageLink|_ 

.. |ImageLink| image:: /images/clase12/consultarDatos.gif
.. _ImageLink: https://www.youtube.com/watch?v=8emd37mvN2E

Clase QCryptographicHash
^^^^^^^^^^^^^^^^^^^^^^^^

- Provee la generación de la clave hash 
- Soporta MD5, MD4 y SHA-1

.. code-block:: c

	enum Algorithm { Md4, Md5, Sha1 }

	QCryptographicHash(Algorithm metodo)

	void addData(const QByteArray & data)
	
	void reset()

	QByteArray result() const

**Método estático**

.. code-block:: c

	QByteArray hash(const QByteArray & data, Algorithm metodo)

**Otros métodos útiles**

.. code-block:: c

	QByteArray QByteArray::toHex()
	// Devuelve en hexadecimal
	// Útil para enviar por url una clave hash MD5
	// Hexadecimal tiene sólo caracteres válidos para URL

**Ejemplo**: Obtener MD5 de la clave ingresada en un QlineEdit:

.. code-block:: c

	QcryptographicHash::hash(leClave->text().toUtf8(), QCryptographicHash::Md5).toHex()

Registrar eventos (logs)
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: c

	bool AdminDB::insertLog(QString log)  {
	    QSqlQuery query(db);

	    return query.exec("INSERT INTO logs (evento) VALUES ('" + log + "')");
	}

**Ejercicio**

- Diseñar una aplicación con un login inicial que valide contra la base
- Almacenar sólo el hash en MD5 de las contraseñas
- Si el usuario es válido mostrar cualquier widget ya creado (Maps, Imagen, paint)
- Registrar en la tabla 'logs' los intentos fallidos de logueo











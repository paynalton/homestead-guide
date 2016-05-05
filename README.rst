*****************************
Guía-Homestead
*****************************
|Gitter|

.. |Gitter| image:: https://badges.gitter.im/ethereum/homestead-guide.svg
   :target: https://gitter.im/ethereum/homestead-guide?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge

La guía para Ethereum Homestead es la documentación de referencia que acompaña a la publicación de la versión Homestead del proyecto Ethereum.

`Hosted on ReadTheDocs`_

¿COMO PUEDO AYUDAR?
================================================================================
**Iniciativa de Documentación para Homestead Documentation**

No importa si se es principiante o experto, hay muchas maneras de ayudar.

Escriba contenido para la guía
--------------------------------------------------------------------------------
Ayude a transferir y actualizar contenido desde el wiki de Ethereum, La guía para Frontier de Ethereum, el Ethereum Stack Exchange, o cualquier otra fuente reconocida a páginas relevantes para la guía Homestead. Alternativamente, escriba su propio contenido para la guía basandose en su propia experiencia.

Asegurese de que la documentación que está aportando se mantenga verás y respete nuestra guia para los documentos de Homestead (https://ethereum-homestead.readthedocs.org/en/latest/about.html).

Revise lo que ha escrito
--------------------------------------------------------------------------------
Revise nuestra guía (https://ethereum-homestead.readthedocs.org/en/latest/) y retroaliméntenos visitando nuestra sala de chat en Gitter (https://gitter.im/ethereum/homestead-guide), realice un pull request ó reporte un problema en este repositorio. Muy sencillo.

¿Y qué hay para mi?
--------------------------------------------------------------------------------
Su nombre será por siempre inmortalizado, tanto en nuestro corazón como en la página Contribuidores de esta guía.
Como un efecto colateral, también le quedará ese agradable sentimiento que llega cuando se ayuda a mejorar una documentación :-)

DONDE EMPEZAR
======================

Este proyecto utiliza Sphinx (http://www.sphinx-doc.org/en/stable/index.html) para crear el html que está publicado para "Read the Docs". Para usar esta documentación en su propia computadora debería hacer lo siguiente:

Prerequisitos
--------------------------------------------------------------------------------
* Python 2.6 o superior
* pypa
* git

Instalar Sphinx, etc
--------------------------------------------------------------------------------
Para usuarios OSX/Linux (basado en instrucciones encontradas aquí: https://read-the-docs.readthedocs.org/en/latest/getting_started.html)

* En la línea de comandos: ``sudo pip install sphinx``

Para usuarios Windows:

* http://www.sphinx-doc.org/en/stable/install.html#windows-install-python-and-sphinx

Obtener el código fuente
--------------------------------------------------------------------------------
* git clone: https://github.com/ethereum/homestead-guide.git

Compilar una nueva vista HTML
--------------------------------------------------------------------------------
* En una ventana de terminal, vaya a su directorio homestead-guide.
* ``make html``
* ``cd build/html``
* ``open index.html`` (abrir en el navegador web)
* Tip: cada vez que ejecute ``make html``, simplemente refresque su navegador para ver los cambios


RECURSOS
================================================================================

**Homestead**

* Guía en línea para Homestead: https://ethereum-homestead.readthedocs.org/en/latest/index.html
* Github: https://github.com/ethereum/homestead-guide
* Gitter: https://gitter.im/ethereum/homestead-guide
* Google doc: https://docs.google.com/document/d/1rVjrNgaDRAQdPp4rGqWrEk5fPgiHff0xsYGCyf06oM8/edit

**Documentos Heredados**

* Ethereum Wiki: https://github.com/ethereum/wiki/wiki
* Guía para Frontier: https://ethereum.gitbooks.io/frontier-guide/content/ (vea archivos convertidos más abajo)
* Lista gigante de Recursos Ethereum en Souptacular: https://souptacular.gitbooks.io/ethereum-tutorials-and-tips-by-hudson/content/giant_ethereum_resource_list.html

**Lea los Documentos y Sphinx**

- Lea los Documentos: https://read-the-docs.readthedocs.org/en/latest/getting_started.html
- Documentos para Sphinx: http://www.sphinx-doc.org/en/stable/contents.html
- reStructuredText Primer: http://www.sphinx-doc.org/en/stable/rest.html
- Referencia para RST: https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst

Estructura de Directorios
=========================

.. code-block::

    homestead-guide
      build    - Directorio de trabajo, no agregar al repositorio
      source   - contenido actual en rst
        conf.py - configuración de sphinx
      old-docs-for-reference (Cosillas del tiempo de Frontier)
        wiki    - la vieja wiki
        gitbook - los viejos recursos de gitbook (convertidos a rst)
      make.bat - comandos de windows para compilar documentos
      Makefile - para plataformas con make para compilar docs


Historial de la Guía para Homestead (Viejo)
================================================================================

* boilerplate using sphinx-quickstart
* settings in `conf.py`
* code up index with proposed structure
* compile/deploy on readthedocs
* include cheatsheat, rst/sphinx/readthedocs resources
* reach out to community reddit - homestead documentation initiative
* allocate chapters to people (ideally author and reviewer)
* migrate old wiki under frontier/wiki (all md files converted to rst)
* migrate old frontier-guide content under frontier/gitbook (all md content converted to rst)
* script to annotate entire wiki with legacy warning

Estrategia para migrar viejos contenidos de fronter-guide (Viejo)
========================================================

* temporaritly include resources about the documentation project within the book itself
  * rst cheatsheet
  * rst/sphinx/readthedocs resources
  * compilation/deployment instructions
  * link to issues and process
  * style guide, conventions
* include the rst conversion of the wiki
* include the rst conversion of the gitbook

.. _Publicado en ReadTheDocs: https://ethereum-homestead.readthedocs.org/en/latest/

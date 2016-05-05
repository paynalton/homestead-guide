***************************************
La iniciativa de Documentación para Homestead
***************************************
|Gitter|

.. |Gitter| image:: img/homestead-guide.svg
   :target: https://gitter.im/ethereum/homestead-guide?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge

Propósito y audiencia
===============================================================================

Esta guía debería servir como punto de inicio para todos los usuarios y desarrolladores de Ethereum.
La meta es crear documentación con información, tutoriales cortos y ejemplos que cubran los fundamentos y funcionalidades de nivel medio al usar Ethereum para interactividad con dapps o desarrollar una dapp.

Cualquier información que sea demasiado específica, técnica o no necesaria para cumplir las metas de la documentación se debe mantener en el Wiki del Github de Ethereum. De esta manera puede usarse como referencia en esta guía si es necesario.

A pesar de que mucha de la información será similar entre la Guía para Frontier y la guía para Homestead, se requiere un esfuerzo para asegurarse de que la información heredada sigue siendo precisa.
Este documento no está casado con ningún cliente, los ejemplos y tutoriales pueden basarse en cualquier cliente sobre el que el autor decida escribir, siempre y cuando se haga la aclaración sobre que cliente está siendo usado en los ejemplos/tutoriales.

Aunque las especificaciones excesivas y la documentación técnica no serán incluidas en las primeras versiones de esta guía, el uso de la comunidad y la popularidad de esta guía dictarán futuras decisiones para mover la documentación del wiki de Github a este formato.

Los ejemplos con especificaciones excesivas e información técnica incluyen:

* ETHash, CASPER, ABI, RLP, u otros aspectos técnicos.
* Guías completas de API para protocolos. Advertencia: Si un ejemplo, información o tutorial necesita referenciar llamadas de API para un cliente o interface para poder cubrir correctamente un ejemplo, es aceptable referencias la llamada específica. Asegúrese de hacer referencias en donde el usuario pueda encontrar las piezas restantes de la documentación específica que pudieran encontrarse en el wiki de GitHub.

Recursos para Documentación Ejemplar
===============================================================================

Aquí hay unos ejemplos previos de documentación Ethereum + buenos ejemplos de documentación.

* Solidity Docs - https://ethereum.github.io/solidity/docs/home/
* Frontier Guide - https://ethereum.gitbooks.io/frontier-guide/content/
* Gav’s TurboEthereum Guide - https://gavofyork.gitbooks.io/turboethereum/content/
* Ancient EthereumBuilder’s Guide - https://ethereumbuilders.gitbooks.io/guide/content/en/index.html
* Other Ethereum Links: https://souptacular.gitbooks.io/ethereum-tutorials-and-tips-by-hudson/content/giant_ethereum_resource_list.html
* Django Docs - https://docs.djangoproject.com/en/1.9/

Etiquetado de Texto Reestructurado, Sphinx
===============================================================================

* Best Cheat Sheet - https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst
* Quick Reference - http://docutils.sourceforge.net/docs/user/rst/quickref.html
* Official Cheat Sheet - http://docutils.sourceforge.net/docs/user/rst/cheatsheet.txt -> http://docutils.sourceforge.net/docs/user/rst/cheatsheet.html
* RST Primer http://sphinx-doc.org/rest.html
* http://sphinx-doc.org/markup/inline.html

Compilación y Desarrollo
===============================================================================

Usamos `make` con el `Makefile` read-the-docs para compilar el documento.

.. code-block:: bash

    git clone https://github.com/ethereum/homestead-guide
    cd homestead-guide
    make html

Consejos de Procesamiento
===============================================================================

Iguale las líneas delimitadoras (use siempre líneas de 80 caracteres para tener el tamaño correcto, a menos que el título sea mayor a 80 caracteres)

.. code-block:: bash

    for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\=+$/================================================================================/' > $f.o; mv $f.o $f; done; done
    for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\*+$/********************************************************************************/' > $f.o; mv $f.o $f; done
    for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\-+$/--------------------------------------------------------------------------------/' > $f.o; mv $f.o $f; done
    for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\++$/++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++/' > $f.o; mv $f.o $f; done
    for f in `ls source/*/*.rst`; do cat $f|perl -pe 's/\#+$/################################################################################/' > $f.o; mv $f.o $f; done

Documentación de Referencia Antigua
===============================================================================

La carpeta old-docs-for-reference tiene todo el Gitbook de Frontier y documentación de la wiki de Ethereum. Sientase libre de copiar/pegar información de estos documentos si lo considera relevante.

Migrar y Convertir Contenido Antiguo de la Wiki Usando Pandoc
===============================================================================

Si aun desea clonar el definitivamente último wiki de Ethereum Wiki y documentos de la Guía para Frontier:

.. code-block:: bash

    git clone git@github.com:ethereum/go-ethereum.wiki.git
    git clone git@github.com:ethereum/wiki.wiki.git

    mkdir main-wiki.rst
    mkdir go-ethereum-wiki.rst

    for f in `ls wiki.wiki/*.md`; do pandoc $f -o main-wiki.rst/`basename $f .md`.rst; done
    for f in `ls go-ethereum.wiki/*.md`; do pandoc $f -o go-ethereum-wiki.rst/`basename $f .md`.rst; done

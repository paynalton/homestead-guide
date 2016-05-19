********************************************************************************
Administración de Cuentas
********************************************************************************

.. _Accounts:

Cuentas
================================================================================

Las cuentas juegan un role especial en Ethereum. Existen dos tipos de cuentas: *cuentas de propiedad externa* (EOAs) y *cuentas contractuales*. Nos centraremos en cuentas de propiedad externa, a las que llamaremos simplemente *cuentas*. A las cuentas contractuales las llamaremos *contratos* y son :ref:`discutidas a detalle en Contratos <Contracts>`. Esta noción genérica de cuenta que asume tanto cuentas de propiedad externas como contractuales se justifica en que esas dos entidades son tambien llamadas *objetos de estado*. Esas entidades tienen un estado: Las cuentas tienen balance y los contratos tienen tanto balance como almacenamiento de contrato. El estado de todas las cuentas es el estado de la red Ethereum el cual es actualizado con cada bloque y sobre el que la red en verdad necesita alcanzar un concenso.
Las cuentas son esenciales para que los usuarios interactúen con las cadenas de bloques de Ethereum a través de transacciones.

Si restringimos Ethereum a cuentas de propiedad externa y transacciones entre ellas sólamente, habremos conseguido un sistema de criptomoneda alternativo menos poderoso que el propio bitcon y que sólamente puede ser usado para transferir esa moneda.

Las cuentas representan identidades de agentes externos (p.e., personas humanas, mineros o agentes automatizados). Las cuentas utilizan criptografía de llave pública para firmar transaccion para que la EVM pueda validar con seguridad la identidad de un origen de transacción.

Keyfiles
================================================================================

Cada cuenta está definida por un par de llaves, una pública y otra privada. Las cuentas se indexan por su *dirección*, que se deriva de la llave pública al tomar los últimos 20 bytes de esta. Cada par de llave/dirección es codificada en un *keyfile*. Keyfiles ason archivos de texto JSON que pueden ser abiertos y leidos en cualquier editor de texto. El componente crítico del keyfile, la llave privada de la cuenta, siempre está encriptado usando la contraseña que se ingresa al crear la cuenta. Los keyfiles se encuentran en la carpeta ``keystore`` del directorio de datos del nodo Ethereum. ¡Asegurese de respaldar sus keyfiles regularmente! Vea la sección :ref:`backup-and-restore-accounts` para más información.

La creación de una llave es sinónimo de la creación de una cuenta.

* No necesita decirle a nadie lo que está haciendo
* No necesita sincronizar con la cadena de bloques
* No necesita ejecutar un cliente
* Ni siquiera necesita estar conectado a internet

Por supuesto su nueva cuenta no contendrá ningún Ether, pero será suya y puede tener la certeza de que sin su llave y su password nadie podrá accesarla nunca.

Es seguro transferir un directorio compleno o cualquier keyfile individual entre nodos Ethereum.

.. Advertencia:: Notese que en casi de que añada keyfiles a su nodo desde un nodo distinto, el orden de las cuentas puede cambiar. Así que no confíe o cambie el índice en sus escripts o snippets.

.. _creating_an_account:

Creando una Cuenta
================================================================================

.. Advertencia:: **Recuerde sus contraseñas y `respalde sus keyfiles <backup-and-restore-accounts>`_.** Para poder enviar transacciones desde una cuenta, incluyendo el envío de ehter, se deben poseer AMBOS, el keyfile y la contraseña. Asegúrese de tener una copia de su keyfile, recuerde la contrasela de ese keyfile, y almacene ambos de la manera más segura posible. No hay alternativas aquí; pierda el keyfile u olvide la contraseña y todo su ether se habrá esfumado. No se puede acceder a su cuenta sin una contraseña y no existe ninguna opción de *recuperar mi contraseña* aquí. No lo olvide.

Usando ``geth account new``
--------------------------------------------------------------------------------

Una vez que se tiene el cliente geth instalado, crear una cuenta se reduce a ejecutae el comando ``geth account new`` en una terminal.

Tome en cuenta que no necesita iniciar el cliente geth o sincronizar con la cadena de bloques para usar el comando ``geth account``.

.. code-block:: Bash

  $ geth account new

    Your new account is locked with a password. Please give a password. Do not forget this password.
    Passphrase:
    Repeat Passphrase:
    Address: {168bc315a2ee09042d83d7c5811b533620531f67}

Para un uso no interactivo, debe proporcionar un archivo de contraseña en texto plano como argumento para el parámetro ``--password``. Los datos en el archivo consisten a la forma binaria de la contraseña seguido opcionalmente de una nueva línea.

.. code-block:: Bash

  $ geth --password /path/to/password account new

..  Advertencia:: El uso del parámetro ``--password`` está enfocado sólamente a pruebas o automatización en entornos seguros. Es una mala idea almacenar la contraseña en un archivo o exponerla de cualquier otra manera. Si hace uso de la propiedad ``--password`` con un archivo de contraseña, asegurese de que el archivo no puede ser leído o siquiera listado por nadie demás de usted. En sistemas Mac/Linux se puede hacer de la siguiente manera:

.. code-block:: Bash

  touch /path/to/password
  chmod 700 /path/to/password
  cat > /path/to/password
  >I type my pass


Para listar todas las cuentas con keyfiles que se encuentran actualmente en su carpeta ``keystore`` utilice el subcomando ``list`` del comando ``geth account``:

.. code-block:: Bash

  $ geth account list

  account #0: {a94f5374fce5edbc8e2a8697c15331677e6ebf0b}
  account #1: {c385233b188811c9f355d4caec14df86d6248235}
  account #2: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}


Los nombres de archivo de los keyfiles tienen el formato ``UTC--<fecha_creacion UTC ISO8601>-<direccion hexadecimal>``. El orden de las cuentas cuando son listadas es lexicografico, pero como una consecuencia del formato timestamp, esto es igual que el orden de creación.


Usando la consola geth
--------------------------------------------------------------------------------

Para poder crear una nueva cuenta usando geth, primero debemos iniciar geth en modo consola (o bien puede usar ``geth attach`` para vincular a una consola que se encuentre ya en ejecución):

.. code-block:: Bash

  > geth console 2>> file_to_log_output
  instance: Geth/v1.4.0-unstable/linux/go1.5.1
  coinbase: coinbase: [object Object]
  at block: 865174 (Mon, 18 Jan 2016 02:58:53 GMT)
  datadir: /home/USERNAME/.ethereum

La consola le permite interactuar con su nodo local escribiendo comandos. Por ejemplo, pruebe con el comando para listar sus cuentas:

.. code-block:: Javascript

  > eth.accounts

  {
  code: -32000,
  message: "no keys in store"
  }

Esto muestra que no posee cuentas. Cuede también crear una cuenta desde la consola:

.. code-block:: Javascript

  > personal.newAccount()
  Passphrase:
  Repeat passphrase:
  "0xb2f69ddf70297958e582a0cc98bce43294f1007d"

.. Nota:: Recuerde usar una contraseña fuertey aleatoria.

Acabamos de crear nuestra primera cuenta. Si intentamos listar nuestras cuentas de nuevo podremos ver nuestra nueva cuenta:

.. code-block:: Javascript

  > eth.accounts
  ["0xb2f69ddf70297958e582a0cc98bce43294f1007d"]


.. _using-mist-ethereum-wallet:

Usando la Cartera Mist Ethereum
--------------------------------------------------------------------------------

Como rival de la línea de comando, existe una opción GUI para crear cuentas: La Cartera Mist de Ethereum “oficial”. La cartera Mist de Ethereum y su padre, el proyecto Mist, comenzaron a ser desarrollados bajo el auspicio de la fundación Ethereum Foundation, por ello el estatus de “oficial”. Versiones de la cartera están disponibles para Linux, Mac OS X, y Windows.

.. Advertencia:: La cartera Mist se encuentra en fase beta. Tenga cuidado y úsela bajo su propio riesgo.

Crear una cuenta usando la Cartera Mist de Ethereum no podría ser más sencillo. De hecho su primera cuenta es creada durante la instalación de la aplicación.

1. `Descargue la última versión de la cartera <https://github.com/ethereum/mist/releases>`_  para su sistema operativo. Al abrir la aplicación comenzará a sincronizar una copia de la cadena de bloques de Ethereum completa en su computadora, por lo que desde ese momento estará operando efectivamente sobre un nodo geth completo.

2. Descomprima la carpeta descargada e inicie el archivo ejecutable Ethereum-Wallet.

.. image:: img/51Downloading.png
   :width: 582px
   :height: 469px
   :scale: 75 %
   :alt: downloading-mist
   :align: center

3. Espere a que se complete la sincronización de la cadena de bloques, a continuación siga las instrucciones en la pantalla y su primera cuenta será creada.

4. Tras iniciar la cartera Mist Ethereum por primera vez, verá la cuenta que ha creado durante el proceso de instalación.Por defecto se llamará MAIN ACCOUNT (ETHERBASE).

.. image:: img/51OpeningScreen.png
   :width: 1024px
   :height: 938px
   :scale: 50 %
   :alt: opening-screen
   :align: center

5. Crear cuentas adicionales es sencillo; simplemente haga click en ADD ACCOUNT dentro de la pantalla principal e ingrese la contraseña solicitada.

.. Nota:: La cartera Mist se encuentra en continuo desarrollo, así que los detalles sobre los pasos señalados arriba podrían sufrir cambios en futuras actualizaciones.


Crear una cartera MultiFirma en Mist
--------------------------------------------------------------------------------

La cartera Mist Ethereum tiene una opción para asegurar el balance de su cartera usando una cartera multifirma. La ventaja de usar una cartera multifirma es que esta requiere autorización de más de una cuenta para obtener fondos de su balance. Antes de poder crear una cartera multifirma necesitará crear más de una cuenta.

Es muy sencillo crear archivos de cuenta en Mist. En la sección 'Accounts' haga click en 'Add Account'. Utilice una contraseña fuerte y fácil de recordar (recuerde que no existe manera de recuperar una contraseña), confirme la contraseña y su cuenta ha sido creada. Cree al menos dos cuentas. Las cuentas secundarias pueden ser creadas en computadoras separadas iniciando Mist sio así lo prefiere (y teóricamente hace su multifirma más segura de esta manera). Usted sólo necesita las llaves públicas (su dirección de depósito) de sus cuentas cuando se crea la cartera multifirma (copie y pegue, nunca las escriba a mano). Su cuenta primaria necesitará crear el contrato de cartera multifirma, así que esta debe estar en la computadora en la que usted creó la cartera multifirma.

Ahora que sus cuentas están configuradas, realice un respaldo (si su computadora estalla perderá todo su balance si no tiene un respaldo). Haga click en 'Backup' en el menú superior. Escoja la carpeta 'keystore', click secundario en él y escoja 'copy' (NO elija 'cut', eso podría ser mul malo). Vaya a su escritorio, click secundario en un área vacía y escoja 'paste'. Tal vez quiera renombrar esta nueva copia de la carpeta 'keystore' a algo como 'Ethereum-keystore-respaldo-YYYY-mm-dd' para así poder reconocerla fácilmente en el futuro.En este punto puede agregar los contenidos de la carpeta a un archivo zip / rar (y después proteger cel archivo con otra contraseña fuerte y fácil de recordar si se respalda en internet), copielo en un soporte USB externo, grabe en un CD / DVD, o súbalo a algún sistema de almacenamiento en línea  (Dropbox / Google Drive / etc).

Ahora debería agregar aproximadamente no menos de 0.02 ETH a su cuenta primaria (la cuenta con la que inició la creación de la cartera multifirma). Esta es la tarifa requerida por la transacción cuando se crea el contrato de cartera multifirma. Un 1 ETH adicional (o mas) es necesario también, pues Mist actualmente lo requiere para asegurarse de que las transacciones del contrato de cartera tendrán suficiente 'gas' para ejecutarse apropiadaente...así que se necesita almenos 1.02 ETH en total para iniciar.

Ingresará la dirección completa de todas las cuentas que formarán parte de esta cartera multifirma al crearla. Recomiendo copiar y pegar cada dirección dentro de un editor de texto plano (notepad / kedit / etc), después de ir a la página de detalles de cada cuenta en Mist y elegir 'copy address' de la columna de botones de lado derecho. Nunca escriba una dirección a mano, puesto que corre un alto riesgo de cometer errores y perder su balance al enviar transacciones a la dirección equivocada.

Ahora estamos listos para crear la cartera multifirma. En 'Wallet Contracts', seleccione 'Add Wallet Contract'. Asigne un nombre para la cartera, seleccione la cuenta propietaria primaria y escoja 'Multisignature Wallet Contract'. Verá aparecer algo como esto:

"This is a joint account controlled by X owners. You can send up to X ether per day. Any transaction over that daily limit requires the confirmation of X owners."

Establezca la cantidad de propietarios (cuentas) que se agregarán a la cartera multifirma, lo que desee establecer como límite de retiro diario (que solo requiere una cuenta para retirar ese monto), y cuantos propietarios (cuentas) se necesitan para aprovar cualquier monto por encima del límite diario establecido.

Ahora agregue las direcciones de las cuentas que ha copiado en su editor de texto plano, confirme que todas las opciones son correctas y haga click en 'Create' en la parte de abajo. Ahora deberá ingresar su contraseña para enviar la transacción. En la sección 'Wallet Contracts' podrá ver su nueva cartera y el mensaje 'creating'.

Cuando la creación de la cartera se haya completado podrá ver su dirección de contrato en la pantalla. Seleccione la dirección completa y copiela a un nuevo archivo de texto en su editor de texto. Guarde el archivo en su escritorio como 'Dirección-Cartera-Ethereum.txt', o como desee llamarle.

Lo único que falta por hacer es respaldar el archivo 'Dirección-Cartera-Ethereum.txt' de la misma manera en que respaldo sus archivos de cuentas y estará listo para abrir su nueva cartera multifirma con ETH usando esa dirección.

Si va a restaurar desde un respaldo, simplemente copie los archivos dentro de la carpeta 'Ethereum-keystore-backup' al interior de la carpeta 'keystore' que mencionamos en la primera sección de este instructivo. PSI, deberá crear la carpeta 'keystore' si es una instalación nueva de  Mist en una maquina en la que no se había instalado antes (la primera vez que se crea una cuenta es cuando se crea esta carpeta). Así mismo, para restaurar una cartera multifirma, en vez de escoger 'Multisignature Wallet Contract' como hicimos durante la creación, escogemos 'Import Wallet'.

Solución de problemas:

* Mist no sincroniza. Una solución que funciona bien es sincronizar el reloj de hardware de su PC con un servidor NTP para que el tiempo sea exacto y entonces reiniciar.

* Mist inicia después de sincronizar, pero es una pantalla vacía. En caso de estar usando los controladores de video "xorg" en un sistema basado en Linux (Ubuntu, Linux Mint, etc). Intente instalar los controladores de video del fabricante en su lugar.

* Notificación "Wrong password". Parece haber una notificación equivocada ocasionalmente en las versiones actuales de Mist. Reinicie Mist y el problema desaparecerá (Necesitará ingresar la contraseña correcta).


Usando Eth
--------------------------------------------------------------------------------

Cada una de las opciones relacionadas con el manejo de llaves disponibles usando geth tambien están disponibles en eth.

Debajo verá las opciones relacionadas a "cuenta":

.. code-block:: Javascript

  > eth account list  // Lista todas las llaves disponibles en la cartera.
  > eth account new   // Crea una nueva llave y la agrega a la cartera.
  > eth account update [<uuid>|<address> , ... ]  // Desencripta y reencripta las llaves dadas.
  > eth account import [<uuid>|<file>|<secret-hex>] // Importa llaves desde el recurso dado y las coloca en cartera.

Debajo están las opciones relacionadas a "cartera":

.. code-block:: Javascript

  > eth wallet import <file> //Importa una cartera previa.

.. Nota:: la opción 'account import' sólo puede ser usada para importar archivos de llave genéricos. La opción 'wallet import' sólo puede ser usada para importar una cartera previa.

>También es posible acceder a la administración de llaves desde la consola integrada (usando la consola integrada o adjunta geth):

.. code-block:: Javascript

  > web3.personal
  {
	listAccounts: [],
	getListAccounts: function(callback),
	lockAccount: function(),
	newAccount: function(),
	unlockAccount: function()
  }


Usando EthKey (desaconsejado)
--------------------------------------------------------------------------------

Ethkey es una herramienta CLI de la implementación de C++ que le permite interactuar con la cartera Ethereum. Con ella usted puede listar, inspeccionar, crear y modificar llaves, e inspeccionar crear y firmar transacciones.

Asumiremos que aun no ha iniciado un cliente como eth o alguno de los clientes de la serie Aleth. Si lo ha hecho, puede saltarse esta sección.
Para crear una cartera, ejecute ``ethkey`` con el comando ``createwallet``:

.. code-block:: Bash

  > ethkey createwallet

Por favor ingrese una contraseña MAESTRA para proteger su almacenamiento de llaves (¡Una buena contraseña!):
Se le pedirá la contraseña "maestra". Esto protege su privacidad y actua como contraseña por defecto para cualquier llave. Debe confirmar la contraseña escribiendo el mismo texto una vez más.

.. Nota:: Utilice una contraseña fuerte con caracteres aleatorios.

Podemos enlistar las llaves dentro de la cartera simplemente usando el comando list:

.. code-block:: Bash

  > ethkey list

  No keys found.

Aun no hemos creado ninguna llave, ¡Eso nos dice algo! Vamos a crear una.

To create a key, we use the ``new`` command. To use it we must pass a name - this is the name we'll give to this account in the wallet. Let's call it "test":

.. code-block:: Bash

  > ethkey new test

Ingrese una contraseña para asegurar esta cuenta (o nada para usar la contraseña maestra).
Esto le llevará a ingresar una contraseña para proteger esta llave. Si así lo desea, sólo presione "Entrar", esto provocará el uso de la contraseña "maestra" por defecto. Tipicamente esto significa que usted no necesita ingresar la contraseña cuando desee usar la cuenta (debido a que se recuerda la contraseña maestra). En general, debería de usar una contraseña distinta para cada llave, pues esto previene el acceso a otras cuentas en caso de una contraseña comprometida.

Aquí, vamos a darle la increíblemente compleja e imaginativa contraseña de "123". (Nunca utilice contraseñas simples como esta para nada más que meras cuentas de prueba).
Una vez que ha ingresado una contraseña, se le pedirá confirmarla ingresandola de nuevo. Ingrese "123" una vez más.
Debido a que usted tiene su propia contraseña, también se le pedirá que ingrese una pista para esta contraseña, la cual será mostrada cada vez que se le pida la contraseña. La pista es almacenada en la cartera y está también protegida por la contraseña maestra. Ingrese la realmente útil pista de "321 al revés".

.. code-block:: Bash

  > ethkey new test

  Enter a passphrase with which to secure this account (or nothing to use the master passphrase):
  Please confirm the passphrase by entering it again:
  Enter a hint to help you remember this passphrase: 321 backwards
  Created key 055dde03-47ff-dded-8950-0fe39b1fa101
    Name: test
    Password hint: 321 backwards
    ICAP: XE472EVKU3CGMJF2YQ0J9RO1Y90BC0LDFZ
    Raw hex: 0092e965928626f8880629cec353d3fd7ca5974f

Toras las direcciones ICAP comienzan con XE así que debería ser capaz de reconocerlas fácilmente. Podrá ver que la llave tiene otro identificador después de Created key. A esto se le conoce como UUID. Se trata de un identificador único que no tiene absolutamente nada que hacer con la cuenta en si misma. Conocerla no ayuda a ningún atacante a descubrir que se encuentra en la red. Esto pasa también con el nombre del archivo de la llave, que se puede encontrar ya sea en ~/.web3/keys (Mac or Linux) o en $HOME/AppData/Web3/keys (Windows).
Ahora vamos a asegurarnos de que funciona adecuadamente en la cartera:

.. code-block:: Bash

  > ethkey list
  055dde03-47ff-dded-8950-0fe39b1fa101 0092e965… XE472EVKU3CGMJF2YQ0J9RO1Y90BC0LDFZ  test

Esto reporta una llave en cada línea (un total de una llave aquí). En este caso nuestra llave está almacenada en un archivo 055dde... y tiene una dirección ICAP que comienza con XE472EVK.... No son cosas especialmente sencillas de recordar, así que es muy útil que tengan su propio nombre, prueba, también.

Importando su cartera de preventa
================================================================================


Usando la Cartera Mist Ethereum
--------------------------------------------------------------------------------

Importar su cartera de preventa usando la cartera gráfica Mist Ethereum es muy sencillo. De hecho se le preguntará si desea importar su cartera de preventa durante la instalación de la aplicación.

.. Advertencia:: la cartera Mist es un software beta. Tenga cuidado y uselo bajo su propio riesgo.

Las instrucciones sobre como instalar la cartera Mist Ethereum se encuentran en la sección :ref:`Creando una cuenta: Usando la cartera Mist Ethereum <using-mist-ethereum-wallet>`.

Simplemente arrastre su archivo de cartera de preventa ``.json`` en el área designada e ingrese su contraseña para importar su cuenta de preventa.

.. image:: img/51PresaleImportInstall.png
   :width: 582px
   :height: 469px
   :scale: 75 %
   :alt: presale-import
   :align: center

Si escoge no importar su cartera de preventa durante la instalación de la aplicación, puede importarla en cualquier momento seleccionando el menú ``Accounts`` en la barra de menú y escogiendo ``Import Pre-sale Accounts``.

.. Nota:: La cartera Mist se encuentra en desarrollo activo, por lo que los pasos específicos descritos arriba pueden cambiar en futuras actualizaciones.

Usando geth
--------------------------------------------------------------------------------

Si usted tiene una instalación en solitario de geth, importar su cartera de preventa se logra ejecutando el siguiente comando en una terminal:

.. code-block:: Bash

  geth wallet import /ruta/a/mi/cartera_de_preventa.json

Se le pedirá ingresar su contraseña.

Actualizando una cuenta
================================================================================

Usted es capaz de actualizar su archivo llave al último formato y/o actualizar la contraseña de su archivo llave.

Usando geth
--------------------------------------------------------------------------------

Puede actualizar una cuenta existente en la línea de comandos usando el subcomando ``update`` con la dirección de la cuenta o el índice como parámetro. Recuerde que el índice de la cuenta refleja el orden de creación (orden alfabético de los archivos llave por nombre que contiene la fecha de creación).

.. code-block:: Bash

  geth account update b0047c606f3af7392e073ed13253f8f4710b08b6

ó

.. code-block:: Bash

  geth account update 2

Por ejemplo:

.. code-block:: Bash

  $ geth account update a94f5374fce5edbc8e2a8697c15331677e6ebf0b

  Unlocking account a94f5374fce5edbc8e2a8697c15331677e6ebf0b | Attempt 1/3
  Passphrase:
  0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b
  account 'a94f5374fce5edbc8e2a8697c15331677e6ebf0b' unlocked.
  Please give a new password. Do not forget this password.
  Passphrase:
  Repeat Passphrase:
  0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b

La cuenta es guardada en la nueva versión de formato encriptado, se le pedirá una contraseña para desbloquear la cuenta y otra para guardar el archivo actualizado. Este mismo comando puede ser usado para migrar una cuenta de un formato obsoleto a un nuevo formato o para cambiar la contraseña de una cuenta.

Para un uso no interactivo la contraseña puede ser especificada en el parámetro ``--password`` :

.. code-block:: Bash

  geth --password <passwordfile> account update a94f5374fce5edbc8e2a8697c15331677e6ebf0bs

Debido a que de esta manera sólo se puede proveer una contraseña, sólo se puede hacer el cambio de formato. Cambiar la contraseña solo se puede hacer de manera interactiva.

.. Nota:: la actualización de cuentas tiene el efecto colateras de que el orden de sus cuentas puede cambiar. !Después de completar una actualización, todas las versiones/formatos anteriores de la misma llave serán eliminados!


.. _backup-and-restore-accounts:

Respaldar y restaurar cuentas
================================================================================

Respaldo/recuperación Manual
--------------------------------------------------------------------------------

Debe tener un archivo llave de cuenta para ser capaz de enviar cualquier transacción desde esa cuenta. Los archivos llave se encuentran en el subdirectorio keystore dentro del directorio de datos de su nodo Ethereum. La localización del directorio de datos por defecto depende de la plataforma:

- Windows: ``C:\Users\username\%appdata%\Roaming\Ethereum\keystore``
- Linux: ``~/.ethereum/keystore``
- Mac: ``~/Library/Ethereum/keystore``

Para respaldar sus archivos llave (cuentas), copie cada uno de los archivos llave individuales contenidos en el subdirectorio ``keystore`` o copie la carpeta ``keystore`` completa.

Para restaurar sus archivos llave (cuentas), copie los archivos de vuelta dentro del subdirectorio ``keystore``, en donde se encontraban originalmente.

Importando una llave privada sin encriptar
--------------------------------------------------------------------------------

La importación de una llave privada sin encriptar está soportado por ``geth``

.. code-block:: Bash

  geth account import /ruta/a/<archivo_llave>

Este comando importa ina llave no encriptada desde un archivo de texto plano ``<archivo_llave>``, crea una nueva cuenta y muestra su dirección.
Se asume que el archivo llave contiene una llave privada sin encriptar con bytes en bruto de EC canónico codificados en hexadecimal.
La cuenta es guardada en formato encriptado, se le pide una contraseña. Debe recordar dicha contraseña para desbloquear su cuenta en el futuro.

Un ejemplo en el que el directorio de datos es especificado. Si no se usa el parámetro ``--datadir``, la nueva cuenta será creada en el directorio de datos por defecto, por ejemplo, el archivo llave será colocado en el subdirectorio ``keyfiles`` dentro del directorio de datos.

.. code-block:: Bash

  $ geth --datadir /algunOtroDirectorioDeDatosEth  account import ./key.prv
  The new account will be encrypted with a passphrase.
  Please enter a passphrase now.
  Passphrase:
  Repeat Passphrase:
  Address: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}

Para un uso no interactivo la contraseña piede ser especificada usando el parámetro ``--password``:

.. code-block:: Bash

  geth --password <archivoDecontraseña> account import <archivo_llave>


.. Nota:: Debido a que puede copiar directamente sus cuentas encriptadas a otra instancia de Ethereum, este mecanismo de importación/exportación no es necesario cuando transfiere una cuenta entre nodos.

.. Advertencia:: Cuando copie llaves en el ``keystore`` de un nodo existente, el orden de cuentas que estaba usando puede cambiar. Por tanto asegurese de no confiar en el orden por completo o realice una doble revisión y actualice los índices usados en sus scripts.

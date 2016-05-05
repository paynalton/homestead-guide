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

Para For the command line averse, there is now a GUI-based option for creating accounts: The “official” Mist Ethereum wallet. The Mist Ethereum wallet, and its parent Mist project, are being developed under the auspices of the Ethereum Foundation, hence the “official” status. Versions of the wallet app are available for Linux, Mac OS X, and Windows.

.. Warning:: The Mist wallet is beta software. Please beware and use it at your own risk.

Creating an account using the GUI Mist Ethereum wallet couldn’t be easier. In fact, your first account is created during the installation of the app.

1. `Download the latest version of the wallet app <https://github.com/ethereum/mist/releases>`_  for your operating system. Opening the Wallet App will kick off syncing a full copy of the Ethereum blockchain on your computer, since you will in effect be running a full geth node.

2. Unzip the downloaded folder and run the Ethereum-Wallet executable file.

.. image:: img/51Downloading.png
   :width: 582px
   :height: 469px
   :scale: 75 %
   :alt: downloading-mist
   :align: center

3. Wait for the blockchain to fully sync, then follow the instructions on the screen and your first account will be created.

4. When you launch the Mist Ethereum wallet for the first time, you will see the account you created during the installation process. By default it will be named MAIN ACCOUNT (ETHERBASE).

.. image:: img/51OpeningScreen.png
   :width: 1024px
   :height: 938px
   :scale: 50 %
   :alt: opening-screen
   :align: center

5. Creating additional accounts is easy; just click on ADD ACCOUNT in the app’s main screen and enter the required password.

.. Note:: The Mist wallet is still in active development, so details of the steps outlined above may change with upgrades.


Creating a Multi-Signature Wallet in Mist
--------------------------------------------------------------------------------

The Mist Ethereum wallet has an option to secure your wallet balance with a multisig wallet. The advantage of using a multisig wallet is that it requires authorization from more than one account to withdrawal larger amounts from your balance. Before you can create a multisig wallet, you'll need to create more than one account.

It's very easy to create account files in Mist. In the 'Accounts' section click 'Add Account'. Pick a strong yet easy-to-remember password (remember there is no password recovery option), confirm it, and your account is created. Create at least 2 accounts. Secondary accounts can be created on separate computers running Mist if you prefer (and theoretically make your multisig more secure doing it this way). You only need the public keys (your deposit addresses) of your secondary accounts when creating the multisig wallet (copy/paste them, do not ever type them by hand). Your primary account will be needed to create the multisig wallet contract, so it must be on the computer you are creating the multisig wallet on.

Now that you have your accounts setup, be safe and back them up (if your computer crashes, you will lose your balance if you do not have a backup). Click 'Backup' in the top menu. Choose the 'keystore' folder, opposite-click on it / choose 'copy' (do NOT choose 'cut', that would be very bad). Navigate to your desktop, opposite-click in a blank area and choose 'paste'. You may want to rename this new copy of the 'keystore' folder to something like 'Ethereum-keystore-backup-year-month-day' so you have quick recognition of it later. At this point you can then add the folder contents to a zip / rar file (and even password-protect the archive with another strong yet easy-to-remember password if backing up online), copy it to a USB Drive, burn it to a CD / DVD, or upload it to online storage (Dropbox / Google Drive / etc).

You now should add approximately no less than 0.02 ETH to your primary account (the account you will initiate creation of a multisig wallet with). This is required for the transaction fee when you create the multisig wallet contract. An additional 1 ETH (or more) is also needed, because Mist currently requires this to assure wallet contract transactions have enough 'gas' to execute properly...so no less than about 1.02 ETH total for starters.

You will be entering the full addresses of all the accounts you are attaching to this multisig wallet, when you create it. I recommend copying / pasting each address into a plain text editor (notepad / kedit / etc), after going to each account's details page in Mist, and choosing 'copy address' from the right-side column of buttons. Never type an address by hand, or you run a very high risk of typos and could lose your balance sending transactions to the wrong address.

We are now ready to create the multisig wallet. Under 'Wallet Contracts', select 'Add Wallet Contract'. Give it a name, select the primary account owner, and choose 'Multisignature Wallet Contract'. You will see something like this appear:

"This is a joint account controlled by X owners. You can send up to X ether per day. Any transaction over that daily limit requires the confirmation of X owners."

Set whatever amount of owners (accounts) you are attaching to this multisig wallet, whatever you want for a daily withdrawal limit (that only requires one account to withdrawal that amount), and how many owners (accounts) are required to approve any withdrawal amount over the daily limit.

Now add the addresses of the accounts that you copied / pasted into your text editor earlier, confirm all your settings are correct, and click 'Create' at the bottom. You will then need to enter your password to send the transaction. In the 'Wallet Contracts' section it should show your new wallet, and say 'creating'.

When wallet creation is complete, you should see your contract address on the screen. Select the entire address, copy / paste it into a new text file in your text editor, and save the text file to your desktop as 'Ethereum-Wallet-Address.txt', or whatever you want to name it.

Now all you need to do is backup the 'Ethereum-Wallet-Address.txt' file the same way you backed up your account files, and then you are ready to load your new multisig wallet with ETH using this address.

If you are restoring from backup, simply copy the files inside the 'Ethereum-keystore-backup' folder over into the 'keystore' folder mentioned in the first section of this walkthrough. FYI, you may need to create the 'keystore' folder if it's a brand new install of Mist on a machine it was never installed on before (the first time you create an account is when this folder is created). As for restoring a multisig wallet, instead of choosing 'Multisignature Wallet Contract' like we did before when creating it, we merely choose 'Import Wallet' instead.

Troubleshooting:

* Mist won't sync. One solution that works well is syncing your PC hardware clock with an NTP server so the time is exactly correct...then reboot.

* Mist starts after syncing, but is a blank white screen. Chances are you are running the "xorg" video drivers on a Linux-based OS (Ubuntu, Linux Mint, etc). Try installing the manufacturer's video driver instead.

* "Wrong password" notice. This seems to be a false notice on occasion on current Mist versions. Restart Mist and the problem should go away (if you indeed entered the correct password).


Using Eth
--------------------------------------------------------------------------------

Every options related to key management available using geth can be used the same way in eth.

Below are "account" related options:

.. code-block:: Javascript

  > eth account list  // List all keys available in wallet.
  > eth account new   // Create a new key and add it to the wallet.
  > eth account update [<uuid>|<address> , ... ]  // Decrypt and re-encrypt given keys.
  > eth account import [<uuid>|<file>|<secret-hex>] // Import keys from given source and place in wallet.

Below are "wallet" related option:

.. code-block:: Javascript

  > eth wallet import <file> //Import a presale wallet.

.. Note:: the 'account import' option can only be used to import generic key file. the 'wallet import' option can only be used to import a presale wallet.

It is also possible to access keys management from the integrated console (using the built-in console or geth attach):

.. code-block:: Javascript

  > web3.personal
  {
	listAccounts: [],
	getListAccounts: function(callback),
	lockAccount: function(),
	newAccount: function(),
	unlockAccount: function()
  }


Using EthKey (deprecated)
--------------------------------------------------------------------------------

Ethkey is a CLI tool of the C++ implementation that allows you to interact with the Ethereum wallet. With it you can list, inspect, create, delete and modify keys and inspect, create and sign transactions.

We will assume you have not yet run a client such as eth or anything in the Aleth series of clients. If you have, you can skip this section.
To create a wallet, run ``ethkey`` with the ``createwallet`` command:

.. code-block:: Bash

  > ethkey createwallet

Please enter a MASTER passphrase to protect your key store (make it strong!):
You'll be asked for a "master" passphrase. This protects your privacy and acts as a default password for any keys. You'll need to confirm it by entering the same text again.

.. Note:: Use a strong randomly generated password.

We can list the keys within the wallet simply by using the list command:

.. code-block:: Bash

  > ethkey list

  No keys found.

We haven't yet created any keys, and it's telling us so! Let's create one.

To create a key, we use the ``new`` command. To use it we must pass a name - this is the name we'll give to this account in the wallet. Let's call it "test":

.. code-block:: Bash

  > ethkey new test

Enter a passphrase with which to secure this account (or nothing to use the master passphrase).
It will prompt you to enter a passphrase to protect this key. If you just press enter, it'll use the default "master" passphrase. Typically this means you won't need to enter the passphrase for the key when you want to use the account (since it remembers the master passphrase). In general, you should try to use a different passphrase for each key since it prevents one compromised passphrase from giving access to other accounts. However, out of convenience you might decide that for low-security accounts to use the same passphrase.

Here, let's give it the incredibly imaginative passphrase of 123. (Never ever use simple passwords like this for anything else than ephemeral test accounts).
Once you enter a passphrase, it'll ask you to confirm it by entering again. Enter 123 a second time.
Because you gave it its own passphrase, it'll also ask you to provide a hint for this password which will be displayed to you whenever it asks you to enter it. The hint is stored in the wallet and is itself protected by the master passphrase. Enter the truly awful hint of 321 backwards.

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

All normal (aka direct) ICAP addresses begin with XE so you should be able to recognize them easily. Notice also that the key has another identifier after Created key. This is known as the UUID. This is a unique identifier for the key that has absolutely nothing to do with the account itself. Knowing it does nothing to help an attacker discover who you are on the network. It also happens to be the filename for the key, which you can find in either ~/.web3/keys (Mac or Linux) or $HOME/AppData/Web3/keys (Windows).
Now let's make sure it worked properly by listing the keys in the wallet:

.. code-block:: Bash

  > ethkey list
  055dde03-47ff-dded-8950-0fe39b1fa101 0092e965… XE472EVKU3CGMJF2YQ0J9RO1Y90BC0LDFZ  test

It reports one key on each line (for a total of one key here). In this case our key is stored in a file 055dde... and has an ICAP address beginning XE472EVK.... Not especially easy things to remember so rather helpful that it has its proper name, test, too.

Importing your presale wallet
================================================================================


Using Mist Ethereum wallet
--------------------------------------------------------------------------------

Importing your presale wallet using the GUI Mist Ethereum wallet is very easy. In fact, you will be asked if you want to import your presale wallet during the installation of the app.

.. Warning:: Mist wallet is beta software. Beware and use it at your own risk.

Instructions for installing the Mist Ethereum wallet are given in the section :ref:`Creating an account: Using Mist Ethereum wallet <using-mist-ethereum-wallet>`.

Simply drag-and-drop your ``.json`` presale wallet file into the designated area and enter your password to import your presale account.

.. image:: img/51PresaleImportInstall.png
   :width: 582px
   :height: 469px
   :scale: 75 %
   :alt: presale-import
   :align: center

If you choose not to import your presale wallet during installation of the app, you can import it at any time by selecting the ``Accounts`` menu in the app’s menu bar and then selecting ``Import Pre-sale Accounts``.

.. Note:: The Mist wallet is still in active development, so details of the steps outlined above may change with upgrades.

Using geth
--------------------------------------------------------------------------------

If you have a standalone installation of geth, importing your presale wallet is accomplished by executing the following command in a terminal:

.. code-block:: Bash

  geth wallet import /path/to/my/presale-wallet.json

You will be prompted to enter your password.

Updating an account
================================================================================

You are able to upgrade your keyfile to the latest keyfile format and/or upgrade your keyfile password.

Using geth
--------------------------------------------------------------------------------

You can update an existing account on the command line with the ``update`` subcommand with the account address or index as parameter. Remember that the account index reflects the order of creation (lexicographic order of keyfile names containing the creation time).

.. code-block:: Bash

  geth account update b0047c606f3af7392e073ed13253f8f4710b08b6

or

.. code-block:: Bash

  geth account update 2

For example:

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

The account is saved in the newest version in encrypted format, you are prompted for a passphrase to unlock the account and another to save the updated file. This same command can be used to migrate an account of a deprecated format to the newest format or change the password for an account.

For non-interactive use the passphrase can be specified with the ``--password`` flag:

.. code-block:: Bash

  geth --password <passwordfile> account update a94f5374fce5edbc8e2a8697c15331677e6ebf0bs

Since only one password can be given, only format update can be performed, changing your password is only possible interactively.

.. Note:: account update has the side effect that the order of your accounts may change. After a successful update, all previous formats/versions of that same key will be removed!


.. _backup-and-restore-accounts:

Backup and restore accounts
================================================================================

Manual backup/restore
--------------------------------------------------------------------------------

You must have an account’s keyfile to be able to send any transaction from that account. Keyfiles are found in the keystore subdirectory of your Ethereum node’s data directory. The default data directory locations are platform specific:

- Windows: ``C:\Users\username\%appdata%\Roaming\Ethereum\keystore``
- Linux: ``~/.ethereum/keystore``
- Mac: ``~/Library/Ethereum/keystore``

To backup your keyfiles (accounts), copy either the individual keyfiles within the ``keystore`` subdirectory or copy the entire ``keystore`` folder.

To restore your keyfiles (accounts), copy the keyfiles back into the ``keystore`` subdirectory, where they were originally.

Importing an unencrypted private key
--------------------------------------------------------------------------------

Importing an unencrypted private key is supported by ``geth``

.. code-block:: Bash

  geth account import /path/to/<keyfile>

This command imports an unencrypted private key from the plain text file ``<keyfile>`` and creates a new account and prints the address.
The keyfile is assumed to contain an unencrypted private key as canonical EC raw bytes encoded into hex.
The account is saved in encrypted format, you are prompted for a passphrase. You must remember this passphrase to unlock your account in the future.

An example where the data directory is specified. If the ``--datadir`` flag is not used, the new account will be created in the default data directory, i.e., the keyfile will be places in the ``keyfiles`` subdirectory of the data directory.

.. code-block:: Bash

  $ geth --datadir /someOtherEthDataDir  account import ./key.prv
  The new account will be encrypted with a passphrase.
  Please enter a passphrase now.
  Passphrase:
  Repeat Passphrase:
  Address: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}

For non-interactive use the passphrase can be specified with the ``--password`` flag:

.. code-block:: Bash

  geth --password <passwordfile> account import <keyfile>


.. Note:: Since you can directly copy your encrypted accounts to another Ethereum instance, this import/export mechanism is not needed when you transfer an account between nodes.

.. Warning:: When you copy keys into an existing node's ``keystore``, the order of accounts you are used to may change. Therefore you make sure you either do not rely on the account order or double-check and update the indexes used in your scripts.

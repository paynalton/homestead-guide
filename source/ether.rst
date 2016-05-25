********************************************************************************
Ether
********************************************************************************

¿Qué es Ether?
================================================================================

Ether es el nombre de la moneda usada en Ethereum y es usada para pagar por computación dentro de la EVM. Esto se hace intercambiando directamente gas por ether tal y como se explica en _`Gas`.

Denominaciones
--------------------------------------------------------

Ethereum posee un sistema métrico de denominaciones usado como unidades de Ether. Cada denominación tiene su propio nombre único (algunos portan el apellido de figuras que han jugado un rol seminal en la evolución de las ciencias de la computación y la criptoeconomía). La denominación más baja ó *unidad base* de Ether se llama Wei. Debajo se encuentra una lista de nombres de denominaciones y su valor en Wei. siguiendo un patrón común (para algunos un poco ambíguo). Ether también designa una unidad (de 1e18 o un quintillón de Wei) de la moneda. Observe que la moneda no es llamada Ethereum como muchos equivocadamente suponen, tampoco es Ethereum una unidad.


+-------------------------+-----------+-------------------------------------------+
| Unidad                  | Valor en Wei  | Wei                                   |
+=========================+===========+===========================================+
| **wei**                 | 1 wei         | 1                                     |
+-------------------------+-----------+-------------------------------------------+
| **Kwei (babbage)**      | 1e3 wei       | 1,000                                 |
+-------------------------+-----------+-------------------------------------------+
| **Mwei (lovelace)**     | 1e6 wei       | 1,000,000                             |
+-------------------------+-----------+-------------------------------------------+
| **Gwei (shannon)**      | 1e9 wei       | 1,000,000,000                         |
+-------------------------+-----------+-------------------------------------------+
| **microether (szabo)**  | 1e12 wei      | 1,000,000,000,000                     |
+-------------------------+-----------+-------------------------------------------+
| **milliether (finney)** | 1e15 wei      | 1,000,000,000,000,000                 |
+-------------------------+-----------+-------------------------------------------+
| **ether**               | 1e18 wei      | 1,000,000,000,000,000,000             |
+-------------------------+-----------+-------------------------------------------+


Más sobre Ether
=========================

* https://blog.ethereum.org/2014/04/10/the-issuance-model-in-ethereum/
* https://www.reddit.com/r/ethereum/comments/44zy88/clarification_on_ether_supply_and_cost_of_gas/
* https://www.reddit.com/r/ethereum/comments/45vj4g/question_about_scarcity_of_ethereum_and_its/
* https://www.reddit.com/r/ethtrader/comments/48yqg6/is_there_a_cap_like_with_btc_with_how_many_ether/


Obteniendo ether
================================================================================

Para obtener Ether, usted puede:

* convertirse en minero Ethereum (vea _`Mining`)
* cambiar otras monedas por Ether usando servicios centralizados o de confianza
* utilizar la muy amigable `Cartera Mist Ethereum <https://github.com/ethereum/mist/releases>`_ que desde su versión Beta 6 introdujo la capacidad de comprar ether usando la API http://shapeshift.io/

Servicios de confianza
--------------------------------------------------------------------------------

Podrá notar que la plataforma Ethereum tiene la particularidad de que los contratos inteligentes permiten el uso de servicios de confianza, los cuales obvian la necesidad de terceras partes de confianza en una transacción de intercambio de divisas. Esto es, negocios de intercambio de divisas sin intermediarios.

Estos proyectoss (en estado alpha/prelanzamiento al momento de escribir esto) son:

* `BTCrelay <http://btcrelay.org/>`_
   * `Más información <https://medium.com/@ConsenSys/taking-stock-bitcoin-and-ethereum-4382f0a2f17>`_ (sobre pagos ETH/BTC de dos vías sin modificar código bitcoin).
   * `BTCrelay audit <http://martin.swende.se/blog/BTCRelay-Auditing.html>`_
* `Intercambio descentralizado EtherEx <https://etherex.org>`_.

Lista de mercados de intercambio centralizado
--------------------------------------------------------------------------------

========================== ============================
Cambiador                   Monedas
========================== ============================
Poloniex                   BTC
Kraken                     BTC, USD, EUR, CAD, GBP
Gatecoin                   BTC, EUR
Bitfinex                   BTC, USD
Bittrex                    BTC
Bluetrade                  BTC, LTC, DOGE
HitBTC                     BTC
Livecoin                   BTC
Coinsquare                 BTC
Bittylicious               GBP
BTER                       CNY
Yunbi                      CNY
Metaexchange               BTC
========================== ============================


Cambiadores de tasa fija Centralizados
-----------------------------------


========================== ============================
Cambiados                   Monedas
========================== ============================
`Shapeshift`_              BTC, LTC, DOGE, Other
`Bity`_                    BTC, USD, EUR, CHF
========================== ============================

.. _Bity: https://bity.com
.. _Shapeshift: shapeshift.io


Comercio y análisis de precios
--------------------------------------------------------------------------------

* `Lista exhaustiva de mercados ETH markets por volúmen en coinmarketcap <https://coinmarketcap.com/currencies/ethereum/#markets>`_
* Estadísticas de agregación en tiempo real de los principales mercados ETH:

  * `Tradeblock <https://tradeblock.com/ethereum>`_
  * `EthereumWisdom <http://ethereumwisdom.com>`_
  * `Cryptocompare <https://www.cryptocompare.com/coins/eth/overview>`_
  * `Coinmarketcap <https://coinmarketcap.com/currencies/ethereum/>`_


.. _online-wallets-and-storage-solutions:

Carteras en línea, carteras de papel y almacenamiento en frio
================================================================================

.. todo::
  Este es sólo un volcado de enlaces y notas.
  Favor de transformar esto en una forma de lista para ecosistema.

  Mantenga los ejemplos aquí, posiblemente explicar prácticas paranóicas, listar peligros

* Cartera Mist Ethereum
    * `Versiones para descargar <https://github.com/ethereum/mist/releases>`_
    * `Versión de desarrollo de la Cartera Mist Ethereum <https://blog.ethereum.org/2015/09/16/ethereum-wallet-developer-preview/>`_ - fundación, blog, avisos
    * `¡Qué sencillo es configurar la Cartera Mist! <https://www.youtube.com/watch?v=Z6lE0Ctaeqs>`_ - Tutorial por Tommy Economics
* Kryptokit Jaxx
    * `Sitio principal de Jaxx <http://jaxx.io/>`_
    * `Versión móvil <http://favs.pw/first-ethereum-mobile-app-released/#.VsHn_PGPL5c>`_
* Etherwall
    * `Sitio de Etherwall <http://www.etherwall.com/>`_
    * `Código fuente de Etherwall <https://github.com/almindor/etherwall>`_
* MyEtherWallet
    * Sitio de `MyEtherWallet <https://www.myetherwallet.com/>`_
    * `Código fuente de MyEtherWallet <https://github.com/kvhnuke/etherwallet/>`_
    * `Extensión para Chrome <http://sebfor.com/myetherwallet-chrome-extension-release/>`_
* Almacenamiento en frío
    * `Icebox <https://github.com/ConsenSys/icebox>`_ by `ConsenSys <https://consensys.net/>`_ - Almacenamiento en frio basado en  lightwallet con la librería HD integrada.
    * `Reddit discusión 1 <https://www.reddit.com/r/ethereum/comments/45uvmy/offline_cold_storage_question/offline_cold_storage_question>`_
    * `Cómo configurar una cartera de almacenamiento en frío <https://www.reddit.com/r/ethereum/comments/48wfbv/eli5_how_to_setup_a_cold_storage_wallet_as/>`_
* Cartera física
    * `reddit discusión 2 <https://www.reddit.com/r/ethereum/comments/45siaq/hardware_wallet/>`_
    * `reddit discusión 3 <https://www.reddit.com/r/ethereum/comments/4521o4/crowdfunding_ethereum_hardware_cold_storage_wallet/>`_
* Cartera inteligente
    * las carteras inteligentes no son seguras, no las use. https://www.reddit.com/r/ethereum/comments/45y8m7/brain_wallets_are_now_generally_shunned_by/
    * Cuidado extremo con las carteras inteligentes. Lea la reciente controversia: https://reddit.com/r/ethereum/comments/43fhb5/brainwallets contra http://blog.ether.camp/post/138376049438/why-brain-wallet-is-the-best
* Misc
    * `Herramienta de limpieza de cartera Kraken <https://www.kraken.com/ether>`_ - Importación de cartera de preventa
    * `Métodos recomendados para almacenar ether con seguridad <http://ethereum.stackexchange.com/questions/1239/what-is-the-recommended-way-to-safely-store-ether>`_
    * `Como comprar y almacenar ether <http://sebfor.com/how-to-buy-and-store-ether/>`_
    * `Una introducción legal a la fuerza bruta y porque no usar carteras inteligentes <http://www.fastcompany.com/3056651/researchers-find-a-crack-that-drains-supposedly-secure-bitcoin-wallets>`_
    * `Pyethsaletool <https://github.com/ethereum/pyethsaletool/blob/master/README.md>`_
    * `Cuenta contra cartera <https://www.reddit.com/r/ethereum/comments/47j3r5/eli5_accounts_vs_wallet_contracts_on_mist/>`_

Enviando ether
================================================================================

La `Cartera Ethereum <https://github.com/ethereum/mist/releases>`_  soporta el envío de ether por medio de una interface gráfica.

El Ether también puede transferirse usando la **consola geth**.

.. code-block:: console

    > var remitente = eth.accounts[0];
    > var remisor = eth.accounts[1];
    > var cantidad = web3.toWei(0.01, "ether")
    > eth.sendTransaction({from:remitente, to:remisor, value: cantidad})

Para más información sobre las transacciones de transferencia de Ether, vea :ref:`account-types-gas-and-transactions`.

Ethereum es único en el mundo de las criptomonedas en la manera en que su principal valor utilitario es como criptocombustible (llamado comúnmente "gas"). Más allá de cargos de tarifas de transacción, el gas es una aparte central de cada petición de red y requiere que el remitente pague por los recursos consumidos- El costo del gas es calculado dinámicamente basandose en el volúmen y compejidad de la petición y multiplicado por el precio actual del gas. Este valor como criptocombustible tiene el efecto de incrementar la estabilidad y duración de la demanda de ether y Ethereum  en general. Para más información vea :ref:`account-types-gas-and-transactions`.

Gas y ether
=============================

* https://www.reddit.com/r/ethereum/comments/271qdz/can_someone_explain_the_concept_of_gas_in_ethereum/
* https://www.reddit.com/r/ethereum/comments/3fnpr1/can_someone_possibly_explain_the_concept_of/
* https://www.reddit.com/r/ethereum/comments/49gol3/can_ether_be_used_as_a_currency_eli5_ether_gas/


Gas supone ser la constante de costo de uso/recursos de la red. Uno espera que el costo real de enviar una transacción sea siempre el mismo, así que nunca tendrá el Gas que ser realmente un problema, las monedas en general son volátiles.

En vez de eso el problema se queda en Ether, cuyo valor tiende a variar, pero también se define un Precio del Gas en términos de Ether. Si el precio de Ether se eleva, el precio del Gas, en términos del Ether, debería bajar para mantener el costo real del Gas estable.

El Gas tiene múltiples términos asociados a si mismo: Precio del Gas, Costo del Gas, Límite de Gas, y Tarifas del Gas. El principio detrás del Gas es tener un valor estable para toda transacción o costo de computación en la red Ethereum.

* Costo del Gas es un valor estático sobre cuanto cuesta un cómputo en términos de Gas, y la intención es que el valor real del Gas nunca cambie, así que el costo debería mantenerse siempre estable a lo largo del tiempo.
* Precio del Gas es el costo del Gas en términos de otra moneda o token como Ether. Para estabilizar el valor del gas, el Precio del Gas es un valor flotante que si el costo del token o moneda fluctua, el Precio del Gas cambia para mantener el mismo valor real. El Precio del Gas es establecido por el valor equilibrado de cuantos usuarios van a gastar y cuantos nodos de procesamiento están dispuestos a aceptar.
* Límite de Gas es el monto máximo de Gas que puede ser usado por bloque, esto considerando la máxima carga computacional, volúmen de transacción o tamaño de bloque, y los mineros pueden cambiar lentamente este valor sobre el tiempo.
* Tarifa de Gas es efectivamente el monto de Gas que debe pagarse para ejecutar una transacción en particular o programa (llamado contrato). Las tarifas de Gas de un bloque pueden usarse para implicar la carga computacional, volúmen de transacción o tamaño de un bloque. Las Tarifas de Gas se pagan a los mineros (o contractores garantizados en PoS).

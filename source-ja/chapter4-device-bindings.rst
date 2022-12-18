.. SPDX-License-Identifier: Apache-2.0

..
   .. _chapter-device-bindings:

   Device Bindings
   ===============

.. _chapter-device-bindings:

デバイスバインディング
===============

..
   This chapter contains requirements, known as bindings, for how specific
   types and classes of devices are represented in the devicetree. The
   compatible property of a device node describes the specific binding (or
   bindings) to which the node complies.
この章には、特定のタイプおよびクラスのデバイスがデバイスツリーでどのように表されるかについての、バインディングと呼ばれる要件が含まれています。
デバイスノードの互換性プロパティは、ノードが準拠する特定のバインディング（または複数のバインディング）を記述します。

..
   Bindings may be defined as extensions of other each. For example a new
   bus type could be defined as an extension of the simple-bus binding. In
   this case, the compatible property would contain several strings
   identifying each binding—from the most specific to the most general (see
   :numref:`sect-standard-properties-compatible`, compatible).
バインディングは、他のそれぞれの拡張として定義できます。
たとえば、新しいバスタイプは、シンプルバスバインディングの拡張として定義できます。
この場合、互換性のあるプロパティには、各バインディングを識別するいくつかの文字列が含まれます（最も具体的なものから最も一般的なものまで）（:numref:`sect-standard-properties-compatible`, compatible を参照）。

..
   Binding Guidelines
バインディングガイドライン
------------------

General Principles
~~~~~~~~~~~~~~~~~~

..
   When creating a new devicetree representation for a device, a binding
   should be created that fully describes the required properties and value
   of the device. This set of properties shall be sufficiently descriptive
   to provide device drivers with needed attributes of the device.
デバイスの新しいデバイスツリー表現を作成するときは、デバイスの必要なプロパティと値を完全に説明するバインディングを作成する必要があります。
この一連のプロパティは、デバイスドライバにデバイスの必要な属性を提供するために十分に説明的である必要があります。

..
   Some recommended practices include:
推奨されるプラクティスには次のようなものがあります。 

..
   1. Define a compatible string using the conventions described in
      :numref:`sect-standard-properties-compatible`.
1. :numref:`sect-standard-properties-compatible` で説明されている規則を使用して、互換性のある文字列を定義します。

..
   2. Use the standard properties (defined in
      :numref:`sect-standard-properties` and
      :numref:`sect-interrupts`) as
      applicable for the new device. This usage typically includes the
      ``reg`` and ``interrupts`` properties at a minimum.
2. 新しいデバイスに適用可能な標準プロパティ (:numref:`sect-standard-properties` および :numref:`sect-interrupts` で定義) を使用します。
   通常、この使用法には、少なくとも ``reg`` および ``interrupts`` プロパティが含まれます。

..
   3. Use the conventions specified in :numref:`chapter-device-bindings`
      (Device Bindings) if the new device fits into one the |spec| defined
      device classes.
3. 新しいデバイスが |spec| で定義されたデバイス クラスの 1 つに適合する場合は、 :numref:`chapter-device-bindings` (デバイス バインディング) で指定されている規則を使用します。

..
   4. Use the miscellaneous property conventions specified in
      :numref:`sect-misc-properties`, if applicable.
4. 該当する場合は、  :numref:`sect-misc-properties` で指定されたその他のプロパティ規則を使用します。

..
   5. If new properties are needed by the binding, the recommended format
      for property names is: ``"<company>,<property-name>"``, where ``<company>``
      is an OUI or short unique string like a stock ticker that identifies
      the creator of the binding.

   Example: ``"ibm,ppc-interrupt-server#s"``

5. バインディングで新しいプロパティが必要な場合、プロパティ名の推奨形式は ``"<company>,<property-name>"`` です。
   ここで、 ``<company>``は、OUI または、その作成者を識別する株式ティッカーのような短い一意の文字列でバインディングの作成者を識別します。

   例: ``"ibm,ppc-interrupt-server#s"``


.. _sect-misc-properties:

..
   Miscellaneous Properties
その他のプロパティ
~~~~~~~~~~~~~~~~~~~~~~~~

..
   This section defines a list of helpful properties that might be
   applicable to many types of devices and device classes. They are defined
   here to facilitate standardization of names and usage.
このセクションでは、多くのタイプのデバイスおよびデバイスクラスに適用できる有用なプロパティのリストを定義します。
これらは、名前と使用法の標準化を容易にするためにここで定義されています。

..
   ``clock-frequency`` Property
``clock-frequency`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``clock-frequency`` Property

      =========== ==============================================================
      Property    ``clock-frequency``
      =========== ==============================================================
      Value type  ``<prop-encoded-array>``
      Description Specifies the frequency of a clock in Hz. The value is a
                  ``<prop-encoded-array>`` in one of two forms:

                  a 32-bit integer consisting of one ``<u32>`` specifying the
                  frequency

                  a 64-bit integer represented as a ``<u64>`` specifying the
                  frequency
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``clock-frequency`` プロパティ

   =========== ==============================================================
   プロパティ     ``clock-frequency``
   =========== ==============================================================
   値のタイプ     ``<prop-encoded-array>``
   説明         クロックの周波数をHzで指定します。
               値は、次の2つの形式のいずれかの ``<prop-encoded-array>`` です。

               周波数を指定する1つの ``<u32>`` で構成される32ビット整数

               周波数を指定する ``<u64>`` として表される64ビット整数
   =========== ==============================================================

..
   ``reg-shift`` Property
``reg-shift`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``reg-shift`` Property

      =========== ==============================================================
      Property    ``reg-shift``
      =========== ==============================================================
      Value type  ``<u32>``
      Description The ``reg-shift`` property provides a mechanism to represent
                  devices that are identical in most respects except for the
                  number of bytes between registers. The ``reg-shift`` property
                  specifies in bytes how far the discrete device registers are
                  separated from each other. The individual register location
                  is calculated by using following formula: "registers address"
                  << reg-shift. If unspecified, the default value is 0.

                  For example, in a system where 16540 UART registers are
                  located at addresses 0x0, 0x4, 0x8, 0xC, 0x10, 0x14, 0x18,
                  and 0x1C, a ``reg-shift = <2>``
                  property would be used to specify register locations.
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``reg-shift`` プロパティ

   =========== ==============================================================
   プロパティ     ``reg-shift``
   =========== ==============================================================
   値のタイプ     ``<u32>``
   説明         ``reg-shift`` プロパティは、レジスタ間のバイト数を除いて、ほとんどの点で同一のデバイスを表すメカニズムを提供します。
               ``reg-shift`` プロパティは、ディスクリートデバイスレジスタが互いにどれだけ離れているかをバイト単位で指定します。
               個々のレジスタの場所は、式 「レジスタアドレス」<< reg-shift を使用して計算されます。
               指定しない場合、デフォルト値は0です。

               例えば、16540 UARTレジスタがアドレス 0x0、0x4、0x8、0xC、0x10、0x14、0x18、および0x1Cに配置されているシステムでは、 ``reg-shift=<2>`` プロパティを使用してレジスタの場所を指定します。
   =========== ==============================================================

..
   ``label`` Property
``label`` プロパティ
^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``label`` Property

      =========== ==============================================================
      Property    ``label``
      =========== ==============================================================
      Value type  ``<string>``
      Description The label property defines a human readable string describing
                  a device. The binding for a given device specifies the exact
                  meaning of the property for that device.
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``label`` プロパティ

   =========== ==============================================================
   プロパティ     ``label``
   =========== ==============================================================
   値のタイプ     ``<string>``
   説明         label プロパティは、デバイスを説明する人間が読める文字列を定義します。
               特定のデバイスのバインディングは、そのデバイスのプロパティの正確な意味を指定します。
   =========== ==============================================================

Serial devices
--------------

Serial Class Binding
~~~~~~~~~~~~~~~~~~~~

The class of serial devices consists of various types of point to point
serial line devices. Examples of serial line devices include the 8250
UART, 16550 UART, HDLC device, and BISYNC device. In most cases hardware
compatible with the RS-232 standard fit into the serial device class.

I\ :sup:`2`\ C and SPI (Serial Peripheral Interface) devices shall not
be represented as serial port devices because they have their own
specific representation.

``clock-frequency`` Property
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tabularcolumns:: | l J |
.. table:: ``clock-frequecy`` Property

   =========== ==============================================================
   Property    ``clock-frequency``
   =========== ==============================================================
   Value type  ``<u32>``
   Description Specifies the frequency in Hertz of the baud rate generator's
               input clock.
   Example     ``clock-frequency = <100000000>;``
   =========== ==============================================================

``current-speed`` Property
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tabularcolumns:: | l J |
.. table:: ``current-speed`` Property

   =========== ==============================================================
   Property    ``current-speed``
   =========== ==============================================================
   Value type  ``<u32>``
   Description Specifies the current speed of a serial device in bits per
               second. A boot program should set this property if it has
               initialized the serial device.
   Example     115,200 Baud: ``current-speed = <115200>;``
   =========== ==============================================================

National Semiconductor 16450/16550 Compatible UART Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Serial devices compatible to the National Semiconductor 16450/16550 UART
(Universal Asynchronous Receiver Transmitter) should be represented in
the devicetree using following properties.

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ns16550 UART Properties

   ======================= ===== ===================== ===============================================
   Property Name           Usage Value Type            Definition
   ======================= ===== ===================== ===============================================
   ``compatible``          R     <string list>         Value shall include "ns16550".
   ``clock-frequency``     R     ``<u32>``             Specifies the frequency (in Hz) of the baud
                                                       rate generator’s input clock
   ``current-speed``       OR    ``<u32>``             Specifies current serial device speed in bits
                                                       per second
   ``reg``                 R     ``<prop encoded       Specifies the physical address of the
                                 array>``              registers device within the address space of
                                                       the parent bus
   ``interrupts``          OR    ``<prop encoded       Specifies the interrupts generated by this
                                 array>``              device. The value of the interrupts property
                                                       consists of one or more interrupt specifiers.
                                                       The format of an interrupt specifier is
                                                       defined by the binding document describing the
                                                       node’s interrupt parent.
   ``reg-shift``           O     ``<u32>``             Specifies in bytes how far the discrete device
                                                       registers are separated from each other. The
                                                       individual register location is calculated by
                                                       using following formula: ``"registers address"
                                                       << reg-shift``. If unspecified, the default
                                                       value is 0.
   ``virtual-reg``         SD    ``<u32>``             See :numref:`sect-standard-properties-virtual-reg`.
                                 or                    Specifies an effective address that maps to the
                                 ``<u64>``             first physical address specified in the ``reg``
                                                       property. This property is required if this
                                                       device node is the system’s console.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


..
   Network devices
ネットワークデバイス
---------------

..
   Network devices are packet oriented communication devices. Devices in
   this class are assumed to implement the data link layer (layer 2) of the
   seven-layer OSI model and use Media Access Control (MAC) addresses.
   Examples of network devices include Ethernet, FDDI, 802.11, and
   Token-Ring.
ネットワークデバイスは、パケット指向の通信デバイスです。
このクラスのデバイスは、7層OSIモデルのデータリンク層（レイヤー2）を実装し、Media Access Control (MAC) アドレスを使用すると想定されています。
ネットワークデバイスの例には、イーサネット、FDDI、802.11、およびトークンリングが含まれます。

..
   Network Class Binding
ネットワーククラスバインディング
~~~~~~~~~~~~~~~~~~~~~

..
   ``address-bits`` Property
``address-bits`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``address-bits`` Property

      =========== ==============================================================
      Property    ``address-bits``
      =========== ==============================================================
      Value type  ``<u32>``
      Description Specifies number of address bits required to address the
                  device described by this node. This property specifies number
                  of bits in MAC address. If unspecified, the default value is 48.
      Example     ``address-bits = <48>;``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``address-bits`` プロパティ

   =========== ==============================================================
   プロパティ     ``address-bits``
   =========== ==============================================================
   値のタイプ     ``<u32>``
   説明         このノードによって記述されたデバイスをアドレス指定するために必要なアドレスビット数を指定します。
               このプロパティは、MAC アドレスのビット数を指定します。
               指定しない場合、デフォルト値は 48 です。
   例           ``address-bits = <48>;``
   =========== ==============================================================

..
   ``local-mac-address`` Property
``local-mac-address`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``local-mac-address`` Property

      =========== ==============================================================
      Property    ``local-mac-address``
      =========== ==============================================================
      Value type  ``<prop-encoded-array>`` encoded as an array of hex numbers
      Description Specifies MAC address that was assigned to the network device
                  described by the node containing this property.
      Example     ``local-mac-address = [ 00 00 12 34 56 78 ];``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``local-mac-address`` プロパティ

   =========== ==============================================================
   プロパティ     ``local-mac-address``
   =========== ==============================================================
   値のタイプ     16進数の配列としてエンコードされた ``<prop-encoded-array>``
   説明         このプロパティを含むノードによって記述されたネットワークデバイスに割り当てられた MAC アドレスを指定します。
   例           ``local-mac-address = [ 00 00 12 34 56 78 ];``
   =========== ==============================================================


..
   ``mac-address`` Property
``mac-address`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``mac-address`` Property

      =========== ==============================================================
      Property    ``mac-address``
      =========== ==============================================================
      Value type  ``<prop-encoded-array>`` encoded as an array of hex numbers
      Description Specifies the MAC address that was last used by the boot
                  program. This property should be used in cases where the MAC
                  address assigned to the device by the boot program is
                  different from the local-mac-address property. This property
                  shall be used only if the value differs from
                  local-mac-address property value.
      Example     ``mac-address = [ 02 03 04 05 06 07 ];``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``mac-address`` プロパティ

   =========== ==============================================================
   プロパティ     ``mac-address``
   =========== ==============================================================
   値のタイプ     16進数の配列としてエンコードされた ``<prop-encoded-array>``
   説明         ブートプログラムによって最後に使用された MAC アドレスを指定します。
               このプロパティは、ブートプログラムによってデバイスに割り当てられた MAC アドレスが local-mac-address プロパティと異なる場合に使用する必要があります。
               このプロパティは、値が local-mac-address プロパティ値と異なる場合にのみ使用されます。
   例           ``mac-address = [ 02 03 04 05 06 07 ];``
   =========== ==============================================================

``max-frame-size`` Property
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tabularcolumns:: | l J |
.. table:: ``max-frame-size`` Property

   =========== ==============================================================
   Property    ``max-frame-size``
   =========== ==============================================================
   Value type  ``<u32>``
   Description Specifies maximum packet length in bytes that the physical
               interface can send and receive.
   Example     ``max-frame-size = <1518>;``
   =========== ==============================================================

..
   Ethernet specific considerations
イーサネット固有の考慮事項
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
   Network devices based on the IEEE 802.3 collections of LAN standards
   (collectively referred to as Ethernet) may be represented in the devicetree
   using following properties, in addition to properties specified of
   the network device class.
LAN 規格の IEEE 802.3 コレクション (まとめてイーサネットと呼ばれる) に基づくネットワーク デバイスは、ネットワーク デバイス クラスで指定されたプロパティに加えて、次のプロパティを使用してデバイス ツリーで表すことができます。

..
   The properties listed in this section augment the properties listed in
   the network device class.
このセクションにリストされているプロパティは、ネットワーク デバイス クラスにリストされているプロパティを補強します。

..
   ``max-speed`` Property
``max-speed`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``max-speed`` Property

      =========== ==============================================================
      Property    ``max-speed``
      =========== ==============================================================
      Value type  ``<u32>``
      Description Specifies maximum speed (specified in megabits per second)
                  supported the device.
      Example     ``max-speed = <1000>;``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``max-speed`` プロパティ

   =========== ==============================================================
   Property    ``max-speed``
   =========== ==============================================================
   Value type  ``<u32>``
   Description デバイスがサポートする最大速度 (メガビット/秒で指定) を指定します。
   Example     ``max-speed = <1000>;``
   =========== ==============================================================

..
   ``phy-connection-type`` Property
``phy-connection-type`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``phy-connection-type`` Property

      =========== ==============================================================
      Property    ``phy-connection-type``
      =========== ==============================================================
      Value type  ``<string>``
      Description Specifies interface type between the Ethernet device and a
                  physical layer (PHY) device. The value of this property is
                  specific to the implementation.

                  Recommended values are shown in the following table.
      Example     ``phy-connection-type = "mii";``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``phy-connection-type`` プロパティ

   =========== ==============================================================
   Property    ``phy-connection-type``
   =========== ==============================================================
   Value type  ``<string>``
   Description イーサネット デバイスと物理層 (PHY) デバイス間のインターフェイス タイプを指定します。
               このプロパティの値は、実装に固有です。

               推奨値を次の表に示します。
   Example     ``phy-connection-type = "mii";``
   =========== ==============================================================

..
   .. tabularcolumns:: | l J |
   .. table:: Defined values for the ``phy-connection-type`` Property

      ================================================= ============
      Connection type                                   Value
      ================================================= ============
      Media Independent Interface                       ``mii``
      Reduced Media Independent Interface               ``rmii``
      Gigabit Media Independent Interface               ``gmii``
      Reduced Gigabit Media Independent                 ``rgmii``
      rgmii with internal delay                         ``rgmii-id``
      rgmii with internal delay on TX only              ``rgmii-txid``
      rgmii with internal delay on RX only              ``rgmii-rxid``
      Ten Bit Interface                                 ``tbi``
      Reduced Ten Bit Interface                         ``rtbi``
      Serial Media Independent Interface                ``smii``
      Serial Gigabit Media Independent Interface        ``sgmii``
      Reverse Media Independent Interface               ``rev-mii``
      10 Gigabits Media Independent Interface           ``xgmii``
      Multimedia over Coaxial                           ``moca``
      Quad Serial Gigabit Media Independent Interface   ``qsgmii``
      Turbo Reduced Gigabit Media Independent Interface ``trgmii``
      ================================================= ============
.. tabularcolumns:: | l J |
.. table:: ``phy-connection-type`` プロパティの定義済みの値

   ================================================= ============
   Connection type                                   Value
   ================================================= ============
   Media Independent Interface                       ``mii``
   Reduced Media Independent Interface               ``rmii``
   Gigabit Media Independent Interface               ``gmii``
   Reduced Gigabit Media Independent                 ``rgmii``
   rgmii with internal delay                         ``rgmii-id``
   rgmii with internal delay on TX only              ``rgmii-txid``
   rgmii with internal delay on RX only              ``rgmii-rxid``
   Ten Bit Interface                                 ``tbi``
   Reduced Ten Bit Interface                         ``rtbi``
   Serial Media Independent Interface                ``smii``
   Serial Gigabit Media Independent Interface        ``sgmii``
   Reverse Media Independent Interface               ``rev-mii``
   10 Gigabits Media Independent Interface           ``xgmii``
   Multimedia over Coaxial                           ``moca``
   Quad Serial Gigabit Media Independent Interface   ``qsgmii``
   Turbo Reduced Gigabit Media Independent Interface ``trgmii``
   ================================================= ============

..
   ``phy-handle`` Property
``phy-handle`` プロパティ
^^^^^^^^^^^^^^^^^^^^^^^

..
   .. tabularcolumns:: | l J |
   .. table:: ``phy-handle`` Property

      =========== ==============================================================
      Property    ``phy-handle``
      =========== ==============================================================
      Value type  ``<phandle>``
      Description Specifies a reference to a node representing a physical layer
                  (PHY) device connected to this Ethernet device. This property
                  is required in case where the Ethernet device is connected a
                  physical layer device.
      Example     ``phy-handle = <&PHY0>;``
      =========== ==============================================================
.. tabularcolumns:: | l J |
.. table:: ``phy-handle`` プロパティ

   =========== ==============================================================
   Property    ``phy-handle``
   =========== ==============================================================
   Value type  ``<phandle>``
   Description このイーサネット デバイスに接続されている物理層 (PHY) デバイスを表すノードへの参照を指定します。
               このプロパティは、イーサネット デバイスが物理層デバイスに接続されている場合に必要です。
   Example     ``phy-handle = <&PHY0>;``
   =========== ==============================================================

Power ISA Open PIC Interrupt Controllers
----------------------------------------

This section specifies the requirements for representing Open PIC
compatible interrupt controllers. An Open PIC interrupt controller
implements the Open PIC architecture (developed jointly by AMD and
Cyrix) and specified in The Open Programmable Interrupt Controller (PIC)
Register Interface Specification Revision 1.2 [b18]_.

Interrupt specifiers in an Open PIC interrupt domain are encoded with
two cells. The first cell defines the interrupt number. The second cell
defines the sense and level information.

Sense and level information shall be encoded as follows in interrupt
specifiers:

    ::

        0 = low to high edge sensitive type enabled
        1 = active low level sensitive type enabled
        2 = active high level sensitive type enabled
        3 = high to low edge sensitive type enabled

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: Open-PIC properties

   ======================== ===== ===================== ===============================================
   Property Name            Usage Value Type            Definition
   ======================== ===== ===================== ===============================================
   ``compatible``           R     ``<string>``          Value shall include ``"open-pic"``
   ``reg``                  R     ``<prop encoded       Specifies the physical address of the
                                  array>``              registers device within the address space of
                                                        the parent bus
   ``interrupt-controller`` R     ``<empty>``           Specifies that this node is an interrupt controller
   ``#interrupt-cells``     R     ``<u32>``             Shall be 2.
   ``#address-cells``       R     ``<u32>``             Shall be 0.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ====================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


.. _sect-bindings-simple-bus:

``simple-bus`` Compatible Value
-------------------------------

System-on-a-chip processors may have an internal I/O bus that cannot be
probed for devices. The devices on the bus can be accessed directly
without additional configuration required. This type of bus is
represented as a node with a compatible value of "simple-bus".

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``simple-bus`` Compatible Node Properties

   ======================== ===== ===================== ===============================================
   Property Name            Usage Value Type            Definition
   ======================== ===== ===================== ===============================================
   ``compatible``           R     ``<string>``          Value shall include "simple-bus".
   ``ranges``               R     ``<prop encoded       This property represents the mapping between
                                  array>``              parent address to child address spaces (see
                                                        :numref:`sect-standard-properties-ranges`,
                                                        ranges).
   ``nonposted-mmio``       O     ``<empty>``           Specifies that direct children of this bus
                                                        should use non-posted memory accesses (i.e. a
                                                        non-posted mapping mode) for MMIO ranges.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ====================================================================================================

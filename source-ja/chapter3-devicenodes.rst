.. SPDX-License-Identifier: Apache-2.0

.. _chapter-device-node-requirements:

..
   Device Node Requirements
デバイスノードの要件
========================

..
   Base Device Node Types
基本デバイスノードタイプ
----------------------

..
   The sections that follow specify the requirements for the base set of
   device nodes required in a |spec|-compliant devicetree.
次のセクションでは、 |spec| 準拠のデバイスツリーに必要なデバイスノードの基本セットの要件を指定します。

..
   All devicetrees shall have a root node and the following nodes shall be
   present at the root of all devicetrees:
すべてのデバイスツリーにはルートノードがあり、次のノードがすべてのデバイスツリーのルートに存在する必要があります。

..
   *  One ``/cpus`` node
*  1つの ``/cpus`` ノード 

..
   *  At least one ``/memory`` node
*  少なくとも1つの ``/memory`` ノード

..
   Root node
ルートノード 
---------

..
   The devicetree has a single root node of which all other device nodes
   are descendants. The full path to the root node is ``/``.
デバイスツリーには単一のルートノードがあり、他のすべてのデバイスノードはその子孫です。
ルートノードへのフルパスは ``/`` です。

..
   .. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
   .. table:: Root Node Properties

      =================== ===== ================= ===============================================
      Property Name       Usage Value Type        Definition
      =================== ===== ================= ===============================================
      ``#address-cells``  R     ``<u32>``         Specifies the number of ``<u32>`` cells to
                                                represent the address in the ``reg`` property in
                                                children of root.
      ``#size-cells``     R     ``<u32>``         Specifies the number of ``<u32>`` cells to
                                                represent the size in the ``reg`` property in
                                                children of root.
      ``model``           R     ``<string>``      Specifies a string that uniquely identifies
                                                the model of the system board. The recommended
                                                format is "manufacturer,model-number".
      ``compatible``      R     ``<stringlist>``  Specifies a list of platform architectures
                                                with which this platform is compatible. This
                                                property can be used by operating systems in
                                                selecting platform specific code. The
                                                recommended form of the property value is:

                                                ``"manufacturer,model"``

                                                For example:

                                                ``compatible = "fsl,mpc8572ds"``
      ``serial-number``   O     ``<string>``      Specifies a string representing the device's
                                                serial number.
      ``chassis-type``    OR    ``<string>``      Specifies a string that identifies the form-factor
                                                of the system. The property value can be one of:

                                                * ``"desktop"``
                                                * ``"laptop"``
                                                * ``"convertible"``
                                                * ``"server"``
                                                * ``"tablet"``
                                                * ``"handset"``
                                                * ``"watch"``
                                                * ``"embedded"``
      Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
      ===========================================================================================
.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ルートノードのプロパティ

   =================== ===== ================= ===============================================
   Property Name       Usage Value Type        Definition
   =================== ===== ================= ===============================================
   ``#address-cells``  R     ``<u32>``         ルートの子の *reg* プロパティのアドレスを表す ``<u32>`` セル数を指定します。
   ``#size-cells``     R     ``<u32>``         ルートの子の *reg* プロパティのサイズを表す ``<u32>`` セル数を指定します。
   ``model``           R     ``<string>``      システム基板のモデルを一意に識別する文字列を指定します。
                                               推奨される形式は "manufacturer,model-number" です。
   ``compatible``      R     ``<stringlist>``  このプラットフォームと互換性のあるプラットフォームアーキテクチャのリストを指定します。
                                               このプロパティは、オペレーティングシステムがプラットフォーム固有のコードを選択する際に使用できます。
                                               プロパティ値の推奨される形式は次のとおりです。

                                               ``"manufacturer,model"``

                                               例:

                                               ``compatible = "fsl,mpc8572ds"``
   ``serial-number``   O     ``<string>``      デバイスのシリアル番号を表す文字列を指定します。
   ``chassis-type``    OR    ``<string>``      システムのフォームファクターを識別する文字列を指定します。
                                               プロパティ値は次のいずれかになります。

                                               * ``"desktop"``
                                               * ``"laptop"``
                                               * ``"convertible"``
                                               * ``"server"``
                                               * ``"tablet"``
                                               * ``"handset"``
                                               * ``"watch"``
                                               * ``"embedded"``
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===========================================================================================


.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.

..
   ``/aliases`` node
``/aliases`` ノード
-----------------

..
   A devicetree may have an aliases node (``/aliases``) that defines one or
   more alias properties. The alias node shall be at the root of the devicetree
   and have the node name ``/aliases``.
デバイスツリーには、1つ以上のエイリアスプロパティを定義するエイリアスノード（``/aliases``）が含まれる場合があります。
エイリアスノードはデバイスツリーのルートにあり、ノード名は ``/aliases`` です。

..
   Each property of the ``/aliases`` node defines an alias. The property name
   specifies the alias name. The property value specifies the full path to
   a node in the devicetree. For example, the property serial0 =
   ``"/simple-bus@fe000000/serial@llc500"`` defines the alias ``serial0``.
``/aliases`` ノードの各プロパティは、エイリアスを定義します。
プロパティ名はエイリアス名を指定します。
プロパティ値は、デバイスツリー内のノードへのフルパスを指定します。
たとえば、プロパティ serial0 = ``"/simple-bus@fe000000/serial@llc500"`` は、エイリアス ``serial0`` を定義します。

..
   Alias names shall be a lowercase text strings of 1 to 31 characters from
   the following set of characters.
エイリアス名は、次の文字セットの1〜31文字の小文字のテキスト文字列でなければなりません。

.. tabularcolumns:: | c p{8cm} |
.. table:: Valid characters for alias names

   ========= ================
   Character Description
   ========= ================
   0-9       digit
   a-z       lowercase letter
   \-        dash
   ========= ================

..
   An alias value is a device path and is encoded as a string. The value
   represents the full path to a node, but the path does not need to refer
   to a leaf node.
エイリアス値はデバイスパスであり、文字列としてエンコードされます。
値はノードへのフルパスを表しますが、パスはリーフノードを参照する必要はありません。 

..
   A client program may use an alias property name to refer to a full
   device path as all or part of its string value. A client program, when
   considering a string as a device path, shall detect and use the alias.
クライアントプログラムは、エイリアスプロパティ名を使用して、デバイスの完全なパスをその文字列値のすべてまたは一部として参照する場合があります。
クライアントプログラムは、文字列をデバイスパスと見なす場合、エイリアスを検出して使用する必要があります。

**Example**

.. code-block:: dts

    aliases {
        serial0 = "/simple-bus@fe000000/serial@llc500";
        ethernet0 = "/simple-bus@fe000000/ethernet@31c000";
    };

Given the alias ``serial0``, a client program can look at the ``/aliases`` node
and determine the alias refers to the device path
``/simple-bus@fe000000/serial@llc500``.

..
   ``/memory`` node
``/memory`` ノード
----------------

..
   A memory device node is required for all devicetrees and describes the
   physical memory layout for the system. If a system has multiple ranges
   of memory, multiple memory nodes can be created, or the ranges can be
   specified in the *reg* property of a single memory node.
メモリデバイスノードはすべてのデバイスツリーに必要であり、システムの物理メモリレイアウトを記述します。
システムに複数のメモリ範囲がある場合は、複数のメモリノードを作成するか、単一のメモリノードの *reg* プロパティで範囲を指定できます。

..
   The *unit-name* component of the node name
   (see :numref:`sect-node-names`)
   shall be ``memory``.
ノード名の *unit-name* コンポーネント (:numref:`sect-node-names` を参照) は ``memory`` でなければなりません。

..
   The client program may access memory not covered by any memory
   reservations (see :numref:`sect-fdt-memory-reservation-block`)
   using any storage attributes it chooses. However, before changing the
   storage attributes used to access a real page, the client program is
   responsible for performing actions required by the architecture and
   implementation, possibly including flushing the real page from the
   caches. The boot program is responsible for ensuring that, without
   taking any action associated with a change in storage attributes, the
   client program can safely access all memory (including memory covered by
   memory reservations) as WIMG = 0b001x. That is:
クライアントプログラムは、選択したストレージ属性を使用して、メモリ予約 (:numref:`sect-fdt-memory-reservation-block` を参照)でカバーされていないメモリにアクセスできます。
ただし、実際のページへのアクセスに使用されるストレージ属性を変更する前に、クライアントプログラムは、キャッシュからの実際のページのフラッシュなど、アーキテクチャと実装に必要なアクションを実行する責任があります。
ブートプログラムは、ストレージ属性の変更に関連するアクションを実行せずに、クライアントプログラムが WIMG = 0b001x としてすべてのメモリ（メモリ予約でカバーされるメモリを含む）に安全にアクセスできるようにする責任があります。
あれは：

..
   * not Write Through Required
   * not Caching Inhibited
   * Memory Coherence
   * Required either not Guarded or Guarded
* ライトスルーは必要ありません 
* キャッシング禁止ではありません  
* メモリコヒーレンス 
* 保護されていないか保護されている必要があります

..
   If the VLE storage attribute is supported, with VLE=0.
VLEストレージ属性がサポートされている場合、VLE=0。

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/memory`` Node Properties

   ======================= ===== ========================= ===============================================
   Property Name           Usage Value Type                Definition
   ======================= ===== ========================= ===============================================
   ``device_type``         R      ``<string>``             Value shall be "memory"
   ``reg``                 R      ``<prop-encoded-array>`` Consists of an arbitrary number of address and
                                                           size pairs that specify the physical address
                                                           and size of the memory ranges.
   ``initial-mapped-area`` O      ``<prop-encoded-array>`` Specifies the address and size of the Initial
                                                           Mapped Area

                                                           Is a prop-encoded-array consisting of a
                                                           triplet of (effective address, physical
                                                           address, size). The effective and physical
                                                           address shall each be 64-bit (``<u64>`` value),
                                                           and the size shall be 32-bits (``<u32>`` value).
   ``hotpluggable``        O      ``<empty>``              Specifies an explicit hint to the operating
                                                           system that this memory may potentially be
                                                           removed later.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   =======================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.

``/memory`` node and UEFI
~~~~~~~~~~~~~~~~~~~~~~~~~~

When booting via [UEFI]_, the system memory map is obtained via the
GetMemoryMap() UEFI boot time service as defined in [UEFI]_ § 7.2,
and if present, the OS must ignore any ``/memory`` nodes.

``/memory`` Examples
~~~~~~~~~~~~~~~~~~~~

Given a 64-bit Power system with the following physical memory layout:

* RAM: starting address 0x0, length 0x80000000 (2 GB)
* RAM: starting address 0x100000000, length 0x100000000 (4 GB)

Memory nodes could be defined as follows, assuming ``#address-cells = <2>``
and ``#size-cells = <2>``.

**Example #1**

.. code-block:: dts

    memory@0 {
        device_type = "memory";
        reg = <0x000000000 0x00000000 0x00000000 0x80000000
               0x000000001 0x00000000 0x00000001 0x00000000>;
    };

**Example #2**

.. code-block:: dts

    memory@0 {
        device_type = "memory";
        reg = <0x000000000 0x00000000 0x00000000 0x80000000>;
    };
    memory@100000000 {
        device_type = "memory";
        reg = <0x000000001 0x00000000 0x00000001 0x00000000>;
    };

The ``reg`` property is used to define the address and size of the two
memory ranges. The 2 GB I/O region is skipped. Note that the
``#address-cells`` and ``#size-cells`` properties of the root node specify a
value of 2, which means that two 32-bit cells are required to define the
address and length for the ``reg`` property of the memory node.

..
   ``/reserved-memory`` Node
``/reserved-memory`` ノード
-------------------------

..
   Reserved memory is specified as a node under the ``/reserved-memory`` node.
   The operating system shall exclude reserved memory from normal usage.
   One can create child nodes describing particular reserved (excluded from
   normal use) memory regions.
   Such memory regions are usually designed for the special usage by various
   device drivers.
予約メモリは、 ``/reserved-memory`` ノードの下のノードとして指定されます。
オペレーティングシステムは、予約メモリを通常の使用から除外する必要があります。
特定の予約済み（通常の使用から除外される）メモリ領域を記述する子ノードを作成できます。
このようなメモリ領域は通常、さまざまなデバイスドライバによる特別な使用のために設計されています。

..
   Parameters for each memory region can be encoded into the device tree
   with the following nodes:
各メモリ領域のパラメータは、次のノードを使用してデバイスツリーにエンコードできます。

/reserved-memory parent node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: /reserved-memory Parent Node Properties

   =================== ===== ================= ===============================================
   Property Name       Usage Value Type        Definition
   =================== ===== ================= ===============================================
   ``#address-cells``  R     ``<u32>``         Specifies the number of ``<u32>`` cells to
                                               represent the address in the ``reg`` property in
                                               children of root.
   ``#size-cells``     R     ``<u32>``         Specifies the number of ``<u32>`` cells to
                                               represent the size in the ``reg`` property in
                                               children of root.
   ``ranges``          R     ``<prop encoded   This property represents the mapping between
                             array>``          parent address to child address spaces (see
                                               :numref:`sect-standard-properties-ranges`,
                                               ranges).
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===========================================================================================

``#address-cells`` and ``#size-cells`` should use the same values as for the root node,
and ``ranges`` should be empty so that address translation logic works correctly.

/reserved-memory/ child nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
   Each child of the reserved-memory node specifies one or more regions of
   reserved memory. Each child node may either use a ``reg`` property to
   specify a specific range of reserved memory, or a ``size`` property with
   optional constraints to request a dynamically allocated block of memory.
予約済みメモリノードの各子は、予約済みメモリの1つ以上の領域を指定します。
各子ノードは、 ``reg`` プロパティを使用して予約済みメモリの特定の範囲を指定するか、オプションの制約を使用して ``size`` プロパティを使用して動的に割り当てられたメモリブロックを要求できます。

..
   Following the generic-names recommended practice, node names should
   reflect the purpose of the node (ie. "*framebuffer*" or "*dma-pool*").
   Unit address (``@<address>``) should be appended to the name if the node
   is a static allocation.
総称名の推奨プラクティスに従って、ノード名はノードの目的（つまり、 "*framebuffer*" または "*dma-pool*"）を反映する必要があります。
ノードが静的割り当ての場合は、名前にユニットアドレス（``@<address>``）を追加する必要があります。

A reserved memory node requires either a ``reg`` property for static
allocations, or a ``size`` property for dynamics allocations.
Dynamic allocations may use ``alignment`` and ``alloc-ranges`` properties
to constrain where the memory is allocated from.
If both ``reg`` and ``size`` are present, then the region is treated as a
static allocation with the ``reg`` property taking precedence and ``size``
is ignored.

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/reserved-memory/`` Child Node Properties

   ======================= ===== ========================= ===============================================
   Property Name           Usage Value Type                Definition
   ======================= ===== ========================= ===============================================
   ``reg``                 O      ``<prop-encoded-array>`` Consists of an arbitrary number of address and
                                                           size pairs that specify the physical address
                                                           and size of the memory ranges.
   ``size``                O      ``<prop-encoded-array>`` Size in bytes of memory to reserve for
                                                           dynamically allocated regions.
                                                           Size of this property is based on parent node's
                                                           ``#size-cells`` property.
   ``alignment``           O      ``<prop-encoded-array>`` Address boundary for alignment of allocation.
                                                           Size of this property is based on parent node's
                                                           ``#size-cells`` property.
   ``alloc-ranges``        O      ``<prop-encoded-array>`` Specifies regions of memory that are acceptable
                                                           to allocate from.
                                                           Format is (address, length pairs) tuples in
                                                           same format as for ``reg`` properties.
   ``compatible``          O      ``<stringlist>``         May contain the following strings:

                                                           - ``shared-dma-pool``: This indicates a region of
                                                             memory meant to be used as a shared pool of DMA
                                                             buffers for a set of devices.
                                                             It can be used by an operating system to
                                                             instantiate the necessary pool management
                                                             subsystem if necessary.

                                                           - vendor specific string in the form
                                                             ``<vendor>,[<device>-]<usage>``
   ``no-map``              O      ``<empty>``              If present, indicates the operating system must
                                                           not create a virtual mapping of the region as
                                                           part of its standard mapping of system memory,
                                                           nor permit speculative access to it under any
                                                           circumstances other than under the control of
                                                           the device driver using the region.
   ``reusable``            O      ``<empty>``              The operating system can use the memory in this
                                                           region with the limitation that the device
                                                           driver(s) owning the region need to be able to
                                                           reclaim it back.
                                                           Typically that means that the operating system
                                                           can use that region to store volatile or cached
                                                           data that can be otherwise regenerated or
                                                           migrated elsewhere.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   =======================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.

The ``no-map`` and ``reusable`` properties are mutually exclusive and both must
not be used together in the same node.

Linux implementation notes:

- If a ``linux,cma-default`` property is present, then Linux will use the
  region for the default pool of the contiguous memory allocator.

- If a ``linux,dma-default`` property is present, then Linux will use the
  region for the default pool of the consistent DMA allocator.

Device node references to reserved memory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Regions in the ``/reserved-memory`` node may be referenced by other device
nodes by adding a ``memory-region`` property to the device node.

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: Properties for referencing reserved-memory regions

   ======================= ===== ========================= ===============================================
   Property Name           Usage Value Type                Definition
   ======================= ===== ========================= ===============================================
   ``memory-region``       O     ``<prop-encoded-array>``  phandle, specifier pairs to children of
                                                           ``/reserved-memory``
   ``memory-region-names`` O     ``<stringlist>>``         A list of names, one for each corresponding
                                                           entry in the ``memory-region`` property
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   =======================================================================================================

.. _sect-reserved-memory-uefi:

``/reserved-memory`` and UEFI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
When booting via [UEFI]_, static ``/reserved-memory`` regions must
also be listed in the system memory map obtained via the GetMemoryMap()
UEFI boot time service as defined in [UEFI]_ § 7.2.
The reserved memory regions need to be included in the UEFI memory map to
protect against allocations by UEFI applications.

Reserved regions with the ``no-map`` property must be listed in the memory
map with type ``EfiReservedMemoryType``.
All other reserved regions must be listed with type ``EfiBootServicesData``.

Dynamic reserved memory regions must not be listed in the [UEFI]_ memory map
because they are allocated by the OS after exiting firmware boot services.

``/reserved-memory`` Example
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This example defines 3 contiguous regions are defined for Linux kernel:
one default of all device drivers (named ``linux,cma`` and 64MiB in size),
one dedicated to the framebuffer device (named ``framebuffer@78000000``, 8MiB), and
one for multimedia processing (named ``multimedia@77000000``, 64MiB).

.. code-block:: dts

   / {
      #address-cells = <1>;
      #size-cells = <1>;

      memory {
         reg = <0x40000000 0x40000000>;
      };

      reserved-memory {
         #address-cells = <1>;
         #size-cells = <1>;
         ranges;

         /* global autoconfigured region for contiguous allocations */
         linux,cma {
            compatible = "shared-dma-pool";
            reusable;
            size = <0x4000000>;
            alignment = <0x2000>;
            linux,cma-default;
         };

         display_reserved: framebuffer@78000000 {
            reg = <0x78000000 0x800000>;
         };

         multimedia_reserved: multimedia@77000000 {
            compatible = "acme,multimedia-memory";
            reg = <0x77000000 0x4000000>;
         };
      };

      /* ... */

      fb0: video@12300000 {
         memory-region = <&display_reserved>;
         /* ... */
      };

      scaler: scaler@12500000 {
         memory-region = <&multimedia_reserved>;
         /* ... */
      };

      codec: codec@12600000 {
         memory-region = <&multimedia_reserved>;
         /* ... */
      };
   };

``/chosen`` Node
----------------

..
   The ``/chosen`` node does not represent a real device in the system but
   describes parameters chosen or specified by the system firmware at run
   time. It shall be a child of the root node.
``/chosen`` ノードは、システム内の実際のデバイスを表すものではありませんが、実行時にシステムファームウェアによって選択または指定されたパラメーターを記述します。
ルートノードの子になります。

..
   .. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
   .. table:: ``/chosen`` Node Properties

      ======================= ===== ===================== ===============================================
      Property Name           Usage Value Type            Definition
      ======================= ===== ===================== ===============================================
      ``bootargs``            O     ``<string>``          A string that specifies the boot arguments for
                                                         the client program. The value could
                                                         potentially be a null string if no boot
                                                         arguments are required.
      ``stdout-path``         O     ``<string>``          A string that specifies the full path to the
                                                         node representing the device to be used for
                                                         boot console output. If the character ":" is
                                                         present in the value it terminates the path.
                                                         The value may be an alias.
                                                         If the stdin-path property is not specified,
                                                         stdout-path should be assumed to define the
                                                         input device.
      ``stdin-path``          O     ``<string>``          A string that specifies the full path to the
                                                         node representing the device to be used for
                                                         boot console input. If the character ":" is
                                                         present in the value it terminates the path.
                                                         The value may be an alias.
      Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
      ===================================================================================================
.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/chosen`` ノードのプロパティ

   ======================= ===== ===================== ===============================================
   Property Name           Usage Value Type            Definition
   ======================= ===== ===================== ===============================================
   ``bootargs``            O     ``<string>``          クライアントプログラムのブート引数を指定する文字列。
                                                       ブート引数が不要な場合、値は潜在的に null 文字列になる可能性があります。
   ``stdout-path``         O     ``<string>``          ブートコンソール出力に使用されるデバイスを表すノードへのフルパスを指定する文字列。
                                                       値に文字 ":" が含まれている場合は、パスを終了します。
                                                       値はエイリアスである可能性があります。
                                                       stdin-path プロパティが指定されていない場合は、入力デバイスを定義するために stdout-path を想定する必要があります。
   ``stdin-path``          O     ``<string>``          ブートコンソール入力に使用されるデバイスを表すノードへのフルパスを指定する文字列。
                                                       値に文字 ":" が含まれている場合は、パスを終了します。
                                                       値はエイリアスである可能性があります。
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


..
   **Example**
**例**

.. code-block:: dts

    chosen {
        bootargs = "root=/dev/nfs rw nfsroot=192.168.1.1 console=ttyS0,115200";
    };

..
   Older versions of devicetrees may be encountered that contain a
   deprecated form of the *stdout-path* property called *linux,stdout-path*.
   For compatibility, a client program might want to support
   *linux,stdout-path* if a *stdout-path* property is not present. The meaning
   and use of the two properties is identical.
*linux,stdout-path* と呼ばれる非推奨の形式の *stdout-path* プロパティを含む古いバージョンのデバイスツリーが検出される場合があります。
互換性のために、 *stdout-path* プロパティが存在しない場合、クライアントプログラムは *linux,stdout-path* をサポートしたい場合があります。
2つのプロパティの意味と使用法は同じです。

``/cpus`` Node Properties
-------------------------

..
   A ``/cpus`` node is required for all devicetrees. It does not represent a
   real device in the system, but acts as a container for child ``cpu`` nodes
   which represent the systems CPUs.
``/cpus`` ノードはすべてのデバイスツリーに必要です。
これは、システム内の実際のデバイスを表すものではありませんが、システムのCPUを表す子 ``cpu`` ノードのコンテナーとして機能します。

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/cpus`` Node Properties

   ======================= ===== ===================== ===============================================
   Property Name           Usage Value Type            Definition
   ======================= ===== ===================== ===============================================
   ``#address-cells``      R     ``<u32>``             The value specifies how many cells each
                                                       element of the ``reg`` property array takes in
                                                       children of this node.
   ``#size-cells``         R     ``<u32>``             Value shall be 0. Specifies that no size is
                                                       required in the ``reg`` property in children of
                                                       this node.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


The ``/cpus`` node may contain properties that are common across ``cpu`` nodes.
See :numref:`sect-cpus-cpu-node-properties` for details.

For an example, see :numref:`sect-cpu-node-example`.

.. _sect-cpus-cpu-node-properties:

``/cpus/cpu*`` Node Properties
------------------------------

..
   A ``cpu`` node represents a hardware execution block that is sufficiently
   independent that it is capable of running an operating system without
   interfering with other CPUs possibly running other operating systems.
``cpu`` ノードは、他のオペレーティングシステムを実行している可能性のある他のCPUに干渉することなく、オペレーティングシステムを実行できるように、十分に独立したハードウェア実行ブロックを表します。

..
   Hardware threads that share an MMU would generally be represented under
   one ``cpu`` node. If other more complex CPU topographies are designed, the
   binding for the CPU must describe the topography (e.g. threads that
   don’t share an MMU).
MMU を共有するハードウェアスレッドは、通常、1つの ``cpu`` ノードで表されます。
他のより複雑なCPUトポグラフィが設計されている場合、CPUのバインディングは、トポグラフィ（MMU を共有しないスレッドなど）を記述する必要があります。

..
   CPUs and threads are numbered through a unified number-space that should
   match as closely as possible the interrupt controller’s numbering of
   CPUs/threads.
CPUとスレッドは、割り込みコントローラーのCPU/スレッドの番号付けと可能な限り一致する必要がある統一された番号スペースを介して番号付けされます。

..
   Properties that have identical values across ``cpu`` nodes may be placed in
   the ``/cpus`` node instead. A client program must first examine a specific
   ``cpu`` node, but if an expected property is not found then it should look
   at the parent ``/cpus`` node. This results in a less verbose representation
   of properties which are identical across all CPUs.
``cpu`` ノード間で同じ値を持つプロパティは、代わりに ``/cpus`` ノードに配置できます。
クライアントプログラムは最初に特定の ``cpu`` ノードを調べる必要がありますが、期待されるプロパティが見つからない場合は、親の ``/cpus`` ノードを調べる必要があります。
これにより、すべてのCPUで同一のプロパティの表現がより簡潔になります。

..
   The node name for every CPU node should be ``cpu``.
すべてのCPUノードのノード名は ``cpu`` である必要があります。

..
   General Properties of ``/cpus/cpu*`` nodes
``/cpus/cpu*`` ノードの一般的なプロパティ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
   The following table describes the general properties of ``cpu`` nodes. Some
   of the properties described in :numref:`table-cpu-node-props` are select
   standard properties with specific applicable detail.
次の表に、 ``cpu`` ノードの一般的なプロパティを示します。
:numref:`table-cpu-node-props` で説明されているプロパティの一部は、特定の適用可能な詳細を備えた選択された標準プロパティです。

..
   .. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
   .. _table-cpu-node-props:
   .. table:: ``/cpus/cpu*`` Node General Properties
      :class: longtable

      ====================== ===== ================== ===============================================
      Property Name          Usage Value Type         Definition
      ====================== ===== ================== ===============================================
      ``device_type``        | R   | ``<string>``     Value shall be ``"cpu"``.
      ``reg``                R     array              The value of *reg* is a ``<prop-encoded-array>``
                                                      that defines a unique CPU/thread id for the
                                                      CPU/threads represented by the CPU node.

                                                      If a CPU supports more than one thread (i.e.
                                                      multiple streams of execution) the *reg*
                                                      property is an array with 1 element per
                                                      thread. The *#address-cells* on the ``/cpus`` node
                                                      specifies how many cells each element of the
                                                      array takes. Software can determine the number
                                                      of threads by dividing the size of *reg* by
                                                      the parent node's *#address-cells*.

                                                      If a CPU/thread can be the target of an
                                                      external interrupt the *reg* property value
                                                      must be a unique CPU/thread id that is
                                                      addressable by the interrupt controller.

                                                      If a CPU/thread cannot be the target of an
                                                      external interrupt, then *reg* must be unique
                                                      and out of bounds of the range addressed by
                                                      the interrupt controller

                                                      If a CPU/thread's PIR (pending interrupt register)
                                                      is modifiable, a client
                                                      program should modify PIR to match the *reg*
                                                      property value. If PIR cannot be modified and
                                                      the PIR value is distinct from the interrupt
                                                      controller number space, the CPUs binding may
                                                      define a binding-specific representation of
                                                      PIR values if desired.
      ``clock-frequency``    | R   | array            Specifies the current clock speed of the CPU
                                                      in Hertz. The value is a ``<prop-encoded-array>``
                                                      in one of two forms:

                                                      * A 32-bit integer consisting of one ``<u32>``
                                                      specifying the frequency.
                                                      * A 64-bit integer represented as a ``<u64>``
                                                      specifying the frequency.

      ``timebase-frequency`` | R   | array            Specifies the current frequency at which the
                                                      timebase and decrementer registers are updated
                                                      (in Hertz). The value is a
                                                      <prop-encoded-array> in one of two forms:

                                                      * A 32-bit integer consisting of one ``<u32>``
                                                      specifying the frequency.
                                                      * A 64-bit integer represented as a ``<u64>``.

      ``status``             SD    ``<string>``       A standard property describing the state of a
                                                      CPU. This property shall be present for nodes
                                                      representing CPUs in a symmetric
                                                      multiprocessing (SMP) configuration. For a CPU
                                                      node the meaning of the ``"okay"``, ``"disabled"``
                                                      and ``"fail"`` values are as follows:

                                                      ``"okay"`` :
                                                         The CPU is running.

                                                      ``"disabled"`` :
                                                         The CPU is in a quiescent state.

                                                      ``"fail"`` :
                                                         The CPU is not operational or does not exist.

                                                      A quiescent CPU is in a state where it cannot
                                                      interfere with the normal operation of other
                                                      CPUs, nor can its state be affected by the
                                                      normal operation of other running CPUs, except
                                                      by an explicit method for enabling or
                                                      re-enabling the quiescent CPU (see the
                                                      enable-method property).

                                                      In particular, a running CPU shall be able to
                                                      issue broadcast TLB invalidates without
                                                      affecting a quiescent CPU.

                                                      Examples: A quiescent CPU could be in a spin
                                                      loop, held in reset, and electrically isolated
                                                      from the system bus or in another
                                                      implementation dependent state.

                                                      A CPU with ``"fail"`` status does not affect the
                                                      system in any way.
                                                      The status is assigned to nodes for which no
                                                      corresponding CPU exists.
      ``enable-method``      | SD  | ``<stringlist>`` Describes the method by which a CPU in a
                                                      disabled state is enabled. This property is
                                                      required for CPUs with a status property with
                                                      a value of ``"disabled"``. The value consists of
                                                      one or more strings that define the method to
                                                      release this CPU. If a client program
                                                      recognizes any of the methods, it may use it.
                                                      The value shall be one of the following:

                                                      ``"spin-table"`` :
                                                         The CPU is enabled with the
                                                         spin table method defined in the |spec|.

                                                      ``"[vendor],[method]"`` :
                                                         Implementation dependent string that
                                                         describes the method by which a CPU is
                                                         released from a ``"disabled"`` state. The
                                                         required format is: ``"[vendor],[method]"``,
                                                         where vendor is a string describing the name of
                                                         the manufacturer and method is a string
                                                         describing the vendor specific mechanism.

                                                      Example: ``"fsl,MPC8572DS"``

                                                      .. note:: Other methods may be added to later
                                                         revisions of the |spec| specification.
      ``cpu-release-addr``   | SD  | ``<u64>``        The cpu-release-addr property is required for
                                                      cpu nodes that have an enable-method property
                                                      value of ``"spin-table"``. The value specifies the
                                                      physical address of a spin table entry that
                                                      releases a secondary CPU from its spin loop.
      Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
      ===============================================================================================
.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. _table-cpu-node-props:
.. table:: ``/cpus/cpu*`` Node General Properties
   :class: longtable

   ====================== ===== ================== ===============================================
   Property Name          Usage Value Type         Definition
   ====================== ===== ================== ===============================================
   ``device_type``        | R   | ``<string>``     値は ``cpu`` にしなければならない。
   ``reg``                R     array              ``reg`` の値は、CPUノードによって表されるCPU/スレッドの一意のCPU/スレッドIDを定義する ``<prop-encoded-array>`` です。
   
                                                   CPUが複数のスレッド（つまり、複数の実行ストリーム）をサポートしている場合、 *reg* プロパティはスレッドごとに1つの要素を持つ配列です。
                                                   ``/cpus``ノードの *#address-cells* は、配列の各要素が取るセルの数を指定します。
                                                   ソフトウェアは、regのサイズを親ノードの *#address-cells* で割ることにより、スレッドの数を判別できます。

                                                   If a CPU/thread can be the target of an
                                                   external interrupt the *reg* property value
                                                   must be a unique CPU/thread id that is
                                                   addressable by the interrupt controller.

                                                   If a CPU/thread cannot be the target of an
                                                   external interrupt, then *reg* must be unique
                                                   and out of bounds of the range addressed by
                                                   the interrupt controller

                                                   If a CPU/thread's PIR (pending interrupt register)
                                                   is modifiable, a client
                                                   program should modify PIR to match the *reg*
                                                   property value. If PIR cannot be modified and
                                                   the PIR value is distinct from the interrupt
                                                   controller number space, the CPUs binding may
                                                   define a binding-specific representation of
                                                   PIR values if desired.
   ``clock-frequency``    | R   | array            Specifies the current clock speed of the CPU
                                                   in Hertz. The value is a ``<prop-encoded-array>``
                                                   in one of two forms:

                                                   * A 32-bit integer consisting of one ``<u32>``
                                                     specifying the frequency.
                                                   * A 64-bit integer represented as a ``<u64>``
                                                     specifying the frequency.

   ``timebase-frequency`` | R   | array            Specifies the current frequency at which the
                                                   timebase and decrementer registers are updated
                                                   (in Hertz). The value is a
                                                   <prop-encoded-array> in one of two forms:

                                                   * A 32-bit integer consisting of one ``<u32>``
                                                     specifying the frequency.
                                                   * A 64-bit integer represented as a ``<u64>``.

   ``status``             SD    ``<string>``       CPUの状態を説明する標準プロパティ。
                                                   このプロパティは、対称型マルチプロセッシング（SMP）構成のCPUを表すノードに存在します。
                                                   CPUノードの場合、 ``"okay"``, ``"disabled"``, ``"fail"`` の値の意味は次のとおりです。

                                                   ``"okay"`` :
                                                      CPUが実行されています。

                                                   ``"disabled"`` :
                                                      CPUは静止状態です。

                                                   ``"fail"`` :
                                                      CPUが動作していないか、存在しません。

                                                   静止CPUは、他のCPUの通常の動作に干渉できない状態にあり、静止CPUを有効または再度有効にする明示的な方法を除いて、他の実行中のCPUの通常の動作の影響を受けることもありません（enable-methodプロパティを参照）。

                                                   特に、実行中のCPUは、静止しているCPUに影響を与えることなく、ブロードキャストTLB無効化を発行できる必要があります。

                                                   Examples: A quiescent CPU could be in a spin
                                                   loop, held in reset, and electrically isolated
                                                   from the system bus or in another
                                                   implementation dependent state.

                                                   A CPU with ``"fail"`` status does not affect the
                                                   system in any way.
                                                   The status is assigned to nodes for which no
                                                   corresponding CPU exists.
   ``enable-method``      | SD  | ``<stringlist>`` Describes the method by which a CPU in a
                                                   disabled state is enabled. This property is
                                                   required for CPUs with a status property with
                                                   a value of ``"disabled"``. The value consists of
                                                   one or more strings that define the method to
                                                   release this CPU. If a client program
                                                   recognizes any of the methods, it may use it.
                                                   The value shall be one of the following:

                                                   ``"spin-table"`` :
                                                      The CPU is enabled with the
                                                      spin table method defined in the |spec|.

                                                   ``"[vendor],[method]"`` :
                                                      Implementation dependent string that
                                                      describes the method by which a CPU is
                                                      released from a ``"disabled"`` state. The
                                                      required format is: ``"[vendor],[method]"``,
                                                      where vendor is a string describing the name of
                                                      the manufacturer and method is a string
                                                      describing the vendor specific mechanism.

                                                   Example: ``"fsl,MPC8572DS"``

                                                   .. note:: Other methods may be added to later
                                                      revisions of the |spec| specification.
   ``cpu-release-addr``   | SD  | ``<u64>``        The cpu-release-addr property is required for
                                                   cpu nodes that have an enable-method property
                                                   value of ``"spin-table"``. The value specifies the
                                                   physical address of a spin table entry that
                                                   releases a secondary CPU from its spin loop.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===============================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/cpus/cpu*`` Node Power ISA Properties
   :class: longtable

   ============================ ===== ============== ===============================================
   Property Name                Usage Value Type     Definition
   ============================ ===== ============== ===============================================
   ``power-isa-version``        | O   | ``<string>`` A string that specifies the numerical portion
                                                     of the Power ISA version string. For example,
                                                     for an implementation complying with Power ISA
                                                     Version 2.06, the value of this property would
                                                     be ``"2.06"``.
   ``power-isa-*``              | O   | ``<empty>``  If the ``power-isa-version`` property exists, then
                                                     for each category from the Categories section
                                                     of Book I of the Power ISA version indicated,
                                                     the existence of a property named
                                                     ``power-isa-[CAT]``, where ``[CAT]`` is the
                                                     abbreviated category name with all uppercase
                                                     letters converted to lowercase, indicates that
                                                     the category is supported by the
                                                     implementation.

                                                     For example, if the power-isa-version property
                                                     exists and its value is ``"2.06"`` and the
                                                     power-isa-e.hv property exists, then the
                                                     implementation supports
                                                     [Category:Embedded.Hypervisor] as defined in
                                                     Power ISA Version 2.06.
   ``cache-op-block-size``      | SD  | ``<u32>``    Specifies the block size in bytes upon which
                                                     cache block instructions operate (e.g., dcbz).
                                                     Required if different than the L1 cache block
                                                     size.
   ``reservation-granule-size`` | SD  | ``<u32>``    Specifies the reservation granule size
                                                     supported by this processor in bytes.
   ``mmu-type``                 O     ``<string>``   Specifies the CPU’s MMU type.

                                                     Valid values are shown below:

                                                     * ``"mpc8xx"``
                                                     * ``"ppc40x"``
                                                     * ``"ppc440"``
                                                     * ``"ppc476"``
                                                     * ``"power-embedded"``
                                                     * ``"powerpc-classic"``
                                                     * ``"power-server-stab"``
                                                     * ``"power-server-slb"``
                                                     * ``"none"``
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   =================================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


Older versions of devicetree may be encountered that contain a
bus-frequency property on CPU nodes. For compatibility, a client-program
might want to support bus-frequency. The format of the value is
identical to that of clock-frequency. The recommended practice is to
represent the frequency of a bus on the bus node using a clock-frequency
property.

TLB Properties
~~~~~~~~~~~~~~

The following properties of a cpu node describe the translate look-aside
buffer in the processor’s MMU.


.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/cpu/cpu*`` Node Power ISA TLB Properties

   ============== ===== =========== ===============================================
   Property Name  Usage Value Type  Definition
   ============== ===== =========== ===============================================
   ``tlb-split``  SD    ``<empty>`` If present specifies that the TLB has a split
                                    configuration, with separate TLBs for
                                    instructions and data. If absent, specifies
                                    that the TLB has a unified configuration.
                                    Required for a CPU with a TLB in a split
                                    configuration.
   ``tlb-size``   SD    ``<u32>``   Specifies the number of entries in the TLB.
                                    Required for a CPU with a unified TLB for
                                    instruction and data addresses.
   ``tlb-sets``   SD    ``<u32>``   Specifies the number of associativity sets in
                                    the TLB. Required for a CPU with a unified TLB
                                    for instruction and data addresses.
   ``d-tlb-size`` SD    ``<u32>``   Specifies the number of entries in the data
                                    TLB. Required for a CPU with a split TLB
                                    configuration.
   ``d-tlb-sets`` SD    ``<u32>``   Specifies the number of associativity sets in
                                    the data TLB. Required for a CPU with a split
                                    TLB configuration.
   ``i-tlb-size`` SD    ``<u32>``   Specifies the number of entries in the
                                    instruction TLB. Required for a CPU with a
                                    split TLB configuration.
   ``i-tlb-sets`` SD    ``<u32>``   Specifies the number of associativity sets in
                                    the instruction TLB. Required for a CPU with a
                                    split TLB configuration.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


Internal (L1) Cache Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following properties of a cpu node describe the processor’s internal
(L1) cache.

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/cpu/cpu*`` Node Power ISA Cache Properties

   ======================= ===== ============= ===============================================
   Property Name           Usage Value Type    Definition
   ======================= ===== ============= ===============================================
   ``cache-unified``       SD    ``<empty>``   If present, specifies the cache has a unified
                                               organization. If not present, specifies that
                                               the cache has a Harvard architecture with
                                               separate caches for instructions and data.
   ``cache-size``          SD    ``<u32>``     Specifies the size in bytes of a unified
                                               cache. Required if the cache is unified
                                               (combined instructions and data).
   ``cache-sets``          SD    ``<u32>``     Specifies the number of associativity sets in
                                               a unified cache. Required if the cache is
                                               unified (combined instructions and data)
   ``cache-block-size``    SD    ``<u32>``     Specifies the block size in bytes of a unified
                                               cache. Required if the processor has a unified
                                               cache (combined instructions and data)
   ``cache-line-size``     SD    ``<u32>``     Specifies the line size in bytes of a unified
                                               cache, if different than the cache block size
                                               Required if the processor has a unified cache
                                               (combined instructions and data).
   ``i-cache-size``        SD    ``<u32>``     Specifies the size in bytes of the instruction
                                               cache. Required if the cpu has a separate
                                               cache for instructions.
   ``i-cache-sets``        SD    ``<u32>``     Specifies the number of associativity sets in
                                               the instruction cache. Required if the cpu has
                                               a separate cache for instructions.
   ``i-cache-block-size``  SD    ``<u32>``     Specifies the block size in bytes of the
                                               instruction cache. Required if the cpu has a
                                               separate cache for instructions.
   ``i-cache-line-size``   SD    ``<u32>``     Specifies the line size in bytes of the
                                               instruction cache, if different than the cache
                                               block size. Required if the cpu has a separate
                                               cache for instructions.
   ``d-cache-size``        SD    ``<u32>``     Specifies the size in bytes of the data cache.
                                               Required if the cpu has a separate cache for
                                               data.
   ``d-cache-sets``        SD    ``<u32>``     Specifies the number of associativity sets in
                                               the data cache. Required if the cpu has a
                                               separate cache for data.
   ``d-cache-block-size``  SD    ``<u32>``     Specifies the block size in bytes of the data
                                               cache. Required if the cpu has a separate
                                               cache for data.
   ``d-cache-line-size``   SD    ``<u32>``     Specifies the line size in bytes of the data
                                               cache, if different than the cache block size.
                                               Required if the cpu has a separate cache for
                                               data.
   ``next-level-cache``    SD    ``<phandle>`` If present, indicates that another level of
                                               cache exists. The value is the phandle of the
                                               next level of cache. The phandle value type is
                                               fully described in :numref:`sect-standard-properties-phandle`.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ===========================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


Older versions of devicetrees may be encountered that contain a
deprecated form of the next-level-cache property called ``l2-cache``.
For compatibility, a client-program may wish to support ``l2-cache``
if a next-level-cache property is not present.
The meaning and use of the two properties is identical.

.. _sect-cpu-node-example:

Example
~~~~~~~

Here is an example of a ``/cpus`` node with one child cpu node:

.. code-block:: dts

    cpus {
        #address-cells = <1>;
        #size-cells = <0>;
        cpu@0 {
            device_type = "cpu";
            reg = <0>;
            d-cache-block-size = <32>; // L1 - 32 bytes
            i-cache-block-size = <32>; // L1 - 32 bytes
            d-cache-size = <0x8000>; // L1, 32K
            i-cache-size = <0x8000>; // L1, 32K
            timebase-frequency = <82500000>; // 82.5 MHz
            clock-frequency = <825000000>; // 825 MHz
        };
    };

Multi-level and Shared Cache Nodes (``/cpus/cpu*/l?-cache``)
------------------------------------------------------------

Processors and systems may implement additional levels of cache hierarchy.
For example, second-level (L2) or third-level (L3) caches.
These caches can potentially be tightly integrated to the CPU or
possibly shared between multiple CPUs.

A device node with a compatible value of ``"cache"`` describes these types
of caches.

The cache node shall define a phandle property, and all cpu nodes or
cache nodes that are associated with or share the cache each shall
contain a next-level-cache property that specifies the phandle to the
cache node.

A cache node may be represented under a CPU node or any other
appropriate location in the devicetree.

Multiple-level and shared caches are represented with the properties in
Table 3-9. The L1 cache properties are described in Table 3-8.

.. tabularcolumns:: | p{4cm} p{0.75cm} p{4cm} p{6.5cm} |
.. table:: ``/cpu/cpu*/l?-cache`` Node Power ISA Multiple-level and Shared Cache Properties

   =============== ===== ============ ===============================================
   Property Name   Usage Value Type   Definition
   =============== ===== ============ ===============================================
   ``compatible``  R     ``<string>`` A standard property. The value shall include
                                      the string ``"cache"``.
   ``cache-level`` R     ``<u32>``    Specifies the level in the cache hierarchy.
                                      For example, a level 2 cache has a value of 2.
   Usage legend: R=Required, O=Optional, OR=Optional but Recommended, SD=See Definition
   ==================================================================================

.. note:: All other standard properties
   (:numref:`sect-standard-properties`) are allowed but are optional.


Example
~~~~~~~

See the following example of a devicetree representation of two CPUs,
each with their own on-chip L2 and a shared L3.

.. code-block:: dts

    cpus {
        #address-cells = <1>;
        #size-cells = <0>;
        cpu@0 {
            device_type = "cpu";
            reg = <0>;
            cache-unified;
            cache-size = <0x8000>; // L1, 32 KB
            cache-block-size = <32>;
            timebase-frequency = <82500000>; // 82.5 MHz
            next-level-cache = <&L2_0>; // phandle to L2

            L2_0:l2-cache {
                compatible = "cache";
                cache-unified;
                cache-size = <0x40000>; // 256 KB

                cache-sets = <1024>;
                cache-block-size = <32>;
                cache-level = <2>;
                next-level-cache = <&L3>; // phandle to L3

                L3:l3-cache {
                    compatible = "cache";
                    cache-unified;
                    cache-size = <0x40000>; // 256 KB
                    cache-sets = <0x400>; // 1024
                    cache-block-size = <32>;
                    cache-level = <3>;
                };
            };
        };

        cpu@1 {
            device_type = "cpu";
            reg = <1>;
            cache-unified;
            cache-block-size = <32>;
            cache-size = <0x8000>; // L1, 32 KB
            timebase-frequency = <82500000>; // 82.5 MHz
            clock-frequency = <825000000>; // 825 MHz
            next-level-cache = <&L2_1>; // phandle to L2
            L2_1:l2-cache {
                compatible = "cache";
                cache-unified;
                cache-level = <2>;
                cache-size = <0x40000>; // 256 KB
                cache-sets = <0x400>; // 1024
                cache-line-size = <32>; // 32 bytes
                next-level-cache = <&L3>; // phandle to L3
            };
        };
    };

.. highlight:: c
.. _libmaple-usart:

``usart.h``
===========

Universal Synchronous/Asynchronous Receiver/Transmitter (USART, or
commonly *serial port*) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: usart_reg_map
.. doxygenstruct:: usart_dev

Devices
-------

.. doxygenvariable:: USART1
.. doxygenvariable:: USART2
.. doxygenvariable:: USART3
.. doxygenvariable:: UART4
.. doxygenvariable:: UART5

Functions
---------

.. doxygenfunction:: usart_init
.. doxygenfunction:: usart_set_baud_rate
.. doxygenfunction:: usart_enable
.. doxygenfunction:: usart_disable
.. doxygenfunction:: usart_disable_all
.. doxygenfunction:: usart_foreach
.. doxygenfunction:: usart_rx
.. doxygenfunction:: usart_tx
.. doxygenfunction:: usart_putudec
.. doxygenfunction:: usart_putc
.. doxygenfunction:: usart_putstr
.. doxygenfunction:: usart_getc
.. doxygenfunction:: usart_data_available
.. doxygenfunction:: usart_reset_rx

Register Map Base Pointers
--------------------------

.. doxygendefine:: USART1_BASE
.. doxygendefine:: USART2_BASE
.. doxygendefine:: USART3_BASE
.. doxygendefine:: UART4_BASE
.. doxygendefine:: UART5_BASE

Register Bit Definitions
------------------------

Status Register
~~~~~~~~~~~~~~~

.. doxygendefine:: USART_SR_CTS_BIT
.. doxygendefine:: USART_SR_LBD_BIT
.. doxygendefine:: USART_SR_TXE_BIT
.. doxygendefine:: USART_SR_TC_BIT
.. doxygendefine:: USART_SR_RXNE_BIT
.. doxygendefine:: USART_SR_IDLE_BIT
.. doxygendefine:: USART_SR_ORE_BIT
.. doxygendefine:: USART_SR_NE_BIT
.. doxygendefine:: USART_SR_FE_BIT
.. doxygendefine:: USART_SR_PE_BIT

.. doxygendefine:: USART_SR_CTS
.. doxygendefine:: USART_SR_LBD
.. doxygendefine:: USART_SR_TXE
.. doxygendefine:: USART_SR_TC
.. doxygendefine:: USART_SR_RXNE
.. doxygendefine:: USART_SR_IDLE
.. doxygendefine:: USART_SR_ORE
.. doxygendefine:: USART_SR_NE
.. doxygendefine:: USART_SR_FE
.. doxygendefine:: USART_SR_PE

Data register
~~~~~~~~~~~~~

.. doxygendefine:: USART_DR_DR

Baud Rate Register
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: USART_BRR_DIV_MANTISSA
.. doxygendefine:: USART_BRR_DIV_FRACTION

Control Register 1
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: USART_CR1_UE_BIT
.. doxygendefine:: USART_CR1_M_BIT
.. doxygendefine:: USART_CR1_WAKE_BIT
.. doxygendefine:: USART_CR1_PCE_BIT
.. doxygendefine:: USART_CR1_PS_BIT
.. doxygendefine:: USART_CR1_PEIE_BIT
.. doxygendefine:: USART_CR1_TXEIE_BIT
.. doxygendefine:: USART_CR1_TCIE_BIT
.. doxygendefine:: USART_CR1_RXNEIE_BIT
.. doxygendefine:: USART_CR1_IDLEIE_BIT
.. doxygendefine:: USART_CR1_TE_BIT
.. doxygendefine:: USART_CR1_RE_BIT
.. doxygendefine:: USART_CR1_RWU_BIT
.. doxygendefine:: USART_CR1_SBK_BIT

.. doxygendefine:: USART_CR1_UE
.. doxygendefine:: USART_CR1_M
.. doxygendefine:: USART_CR1_WAKE
.. doxygendefine:: USART_CR1_WAKE_IDLE
.. doxygendefine:: USART_CR1_WAKE_ADDR
.. doxygendefine:: USART_CR1_PCE
.. doxygendefine:: USART_CR1_PS
.. doxygendefine:: USART_CR1_PS_EVEN
.. doxygendefine:: USART_CR1_PS_ODD
.. doxygendefine:: USART_CR1_PEIE
.. doxygendefine:: USART_CR1_TXEIE
.. doxygendefine:: USART_CR1_TCIE
.. doxygendefine:: USART_CR1_RXNEIE
.. doxygendefine:: USART_CR1_IDLEIE
.. doxygendefine:: USART_CR1_TE
.. doxygendefine:: USART_CR1_RE
.. doxygendefine:: USART_CR1_RWU
.. doxygendefine:: USART_CR1_RWU_ACTIVE
.. doxygendefine:: USART_CR1_RWU_MUTE
.. doxygendefine:: USART_CR1_SBK

Control Register 2
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: USART_CR2_LINEN_BIT
.. doxygendefine:: USART_CR2_CLKEN_BIT
.. doxygendefine:: USART_CR2_CPOL_BIT
.. doxygendefine:: USART_CR2_CPHA_BIT
.. doxygendefine:: USART_CR2_LBCL_BIT
.. doxygendefine:: USART_CR2_LBDIE_BIT
.. doxygendefine:: USART_CR2_LBDL_BIT

.. doxygendefine:: USART_CR2_LINEN
.. doxygendefine:: USART_CR2_STOP
.. doxygendefine:: USART_CR2_STOP_BITS_1
.. doxygendefine:: USART_CR2_STOP_BITS_POINT_5
.. doxygendefine:: USART_CR2_STOP_BITS_1_POINT_5
.. doxygendefine:: USART_CR2_STOP_BITS_2
.. doxygendefine:: USART_CR2_CLKEN
.. doxygendefine:: USART_CR2_CPOL
.. doxygendefine:: USART_CR2_CPOL_LOW
.. doxygendefine:: USART_CR2_CPOL_HIGH
.. doxygendefine:: USART_CR2_CPHA
.. doxygendefine:: USART_CR2_CPHA_FIRST
.. doxygendefine:: USART_CR2_CPHA_SECOND
.. doxygendefine:: USART_CR2_LBCL
.. doxygendefine:: USART_CR2_LBDIE
.. doxygendefine:: USART_CR2_LBDL
.. doxygendefine:: USART_CR2_LBDL_10_BIT
.. doxygendefine:: USART_CR2_LBDL_11_BIT
.. doxygendefine:: USART_CR2_ADD

Control Register 3
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: USART_CR3_CTSIE_BIT
.. doxygendefine:: USART_CR3_CTSE_BIT
.. doxygendefine:: USART_CR3_RTSE_BIT
.. doxygendefine:: USART_CR3_DMAT_BIT
.. doxygendefine:: USART_CR3_DMAR_BIT
.. doxygendefine:: USART_CR3_SCEN_BIT
.. doxygendefine:: USART_CR3_NACK_BIT
.. doxygendefine:: USART_CR3_HDSEL_BIT
.. doxygendefine:: USART_CR3_IRLP_BIT
.. doxygendefine:: USART_CR3_IREN_BIT
.. doxygendefine:: USART_CR3_EIE_BIT

.. doxygendefine:: USART_CR3_CTSIE
.. doxygendefine:: USART_CR3_CTSE
.. doxygendefine:: USART_CR3_RTSE
.. doxygendefine:: USART_CR3_DMAT
.. doxygendefine:: USART_CR3_DMAR
.. doxygendefine:: USART_CR3_SCEN
.. doxygendefine:: USART_CR3_NACK
.. doxygendefine:: USART_CR3_HDSEL
.. doxygendefine:: USART_CR3_IRLP
.. doxygendefine:: USART_CR3_IRLP_NORMAL
.. doxygendefine:: USART_CR3_IRLP_LOW_POWER
.. doxygendefine:: USART_CR3_IREN
.. doxygendefine:: USART_CR3_EIE

Guard Time and Prescaler Register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: USART_GTPR_GT
.. doxygendefine:: USART_GTPR_PSC

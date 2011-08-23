.. highlight:: c
.. _libmaple-i2c:

``i2c.h``
=========

Inter-Integrated Circuit (|i2c|) peripheral support.

.. contents:: Contents
   :local:

Important Note
--------------

There are some important known problems with the built-in I2C
peripherals.  For more information, see STM32F10xx8 and STM32F10xxB
Errata sheet (ST Doc ID 14574 Rev 8), Section 2.11.1, 2.11.2.  An
important consequence of these problems is that the |i2c| interrupt
must not be preempted.  Consequently, (by default) Wirish uses an
|i2c| interrupt priority which is the highest in the system (priority
level 0).  Other interrupt priorities are set lower.

Types
-----

.. doxygenstruct:: i2c_reg_map
.. doxygenenum:: i2c_state
.. doxygenstruct:: i2c_msg
.. doxygenstruct:: i2c_dev

Devices
-------

.. doxygenvariable:: I2C1
.. doxygenvariable:: I2C2

Functions
---------

.. doxygenfunction:: i2c_init
.. doxygenfunction:: i2c_master_enable
.. doxygenfunction:: i2c_master_xfer
.. doxygenfunction:: i2c_bus_reset
.. doxygenfunction:: i2c_disable
.. doxygenfunction:: i2c_peripheral_enable
.. doxygenfunction:: i2c_peripheral_disable
.. doxygenfunction:: i2c_write
.. doxygenfunction:: i2c_set_input_clk
.. doxygenfunction:: i2c_set_clk_control
.. doxygenfunction:: i2c_set_trise
.. doxygenfunction:: i2c_start_condition
.. doxygenfunction:: i2c_stop_condition
.. doxygenfunction:: i2c_enable_irq
.. doxygenfunction:: i2c_disable_irq
.. doxygenfunction:: i2c_enable_ack
.. doxygenfunction:: i2c_disable_ack

Register Map Base Pointers
--------------------------

.. doxygendefine:: I2C1_BASE
.. doxygendefine:: I2C2_BASE

Register Bit Definitions
------------------------

Control register 1
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: I2C_CR1_SWRST
.. doxygendefine:: I2C_CR1_ALERT
.. doxygendefine:: I2C_CR1_PEC
.. doxygendefine:: I2C_CR1_POS
.. doxygendefine:: I2C_CR1_ACK
.. doxygendefine:: I2C_CR1_START
.. doxygendefine:: I2C_CR1_STOP
.. doxygendefine:: I2C_CR1_PE

Control register 2
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: I2C_CR2_LAST
.. doxygendefine:: I2C_CR2_DMAEN
.. doxygendefine:: I2C_CR2_ITBUFEN
.. doxygendefine:: I2C_CR2_ITEVTEN
.. doxygendefine:: I2C_CR2_ITERREN
.. doxygendefine:: I2C_CR2_FREQ

Clock control register
~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: I2C_CCR_FS
.. doxygendefine:: I2C_CCR_DUTY
.. doxygendefine:: I2C_CCR_CCR

Status register 1
~~~~~~~~~~~~~~~~~

.. doxygendefine:: I2C_SR1_SB
.. doxygendefine:: I2C_SR1_ADDR
.. doxygendefine:: I2C_SR1_BTF
.. doxygendefine:: I2C_SR1_ADD10
.. doxygendefine:: I2C_SR1_STOPF
.. doxygendefine:: I2C_SR1_RXNE
.. doxygendefine:: I2C_SR1_TXE
.. doxygendefine:: I2C_SR1_BERR
.. doxygendefine:: I2C_SR1_ARLO
.. doxygendefine:: I2C_SR1_AF
.. doxygendefine:: I2C_SR1_OVR
.. doxygendefine:: I2C_SR1_PECERR
.. doxygendefine:: I2C_SR1_TIMEOUT
.. doxygendefine:: I2C_SR1_SMBALERT

Status register 2
~~~~~~~~~~~~~~~~~

.. doxygendefine:: I2C_SR2_MSL
.. doxygendefine:: I2C_SR2_BUSY
.. doxygendefine:: I2C_SR2_TRA
.. doxygendefine:: I2C_SR2_GENCALL
.. doxygendefine:: I2C_SR2_SMBDEFAULT
.. doxygendefine:: I2C_SR2_SMBHOST
.. doxygendefine:: I2C_SR2_DUALF
.. doxygendefine:: I2C_SR2_PEC

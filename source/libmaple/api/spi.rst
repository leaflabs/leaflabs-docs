.. highlight:: c
.. _libmaple-spi:

``spi.h``
=========

Serial Peripheral Interface (SPI) support.  Currently, there is no I2S
support beyond register bit definitions.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: spi_reg_map
.. doxygenstruct:: spi_dev
.. doxygenenum:: spi_mode
.. doxygenenum:: spi_baud_rate
.. doxygenenum:: spi_cfg_flag
.. doxygenenum:: spi_interrupt

Devices
-------

.. doxygenvariable:: SPI1
.. doxygenvariable:: SPI2
.. doxygenvariable:: SPI3

Functions
---------

.. doxygenfunction:: spi_init
.. doxygenfunction:: spi_gpio_cfg
.. doxygenfunction:: spi_master_enable
.. doxygenfunction:: spi_slave_enable
.. doxygenfunction:: spi_tx
.. doxygenfunction:: spi_foreach
.. doxygenfunction:: spi_peripheral_enable
.. doxygenfunction:: spi_peripheral_disable
.. doxygenfunction:: spi_peripheral_disable_all
.. doxygenfunction:: spi_tx_dma_enable
.. doxygenfunction:: spi_tx_dma_disable
.. doxygenfunction:: spi_rx_dma_enable
.. doxygenfunction:: spi_rx_dma_disable
.. doxygenfunction:: spi_is_enabled
.. doxygenfunction:: spi_irq_enable
.. doxygenfunction:: spi_irq_disable
.. doxygenfunction:: spi_dff
.. doxygenfunction:: spi_is_rx_nonempty
.. doxygenfunction:: spi_rx_reg
.. doxygenfunction:: spi_is_tx_empty
.. doxygenfunction:: spi_tx_reg
.. doxygenfunction:: spi_is_busy

Register Map Base Pointers
--------------------------

.. doxygendefine:: SPI1_BASE
.. doxygendefine:: SPI2_BASE
.. doxygendefine:: SPI3_BASE

Register Bit Definitions
------------------------

Control register 1
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SPI_CR1_BIDIMODE_BIT
.. doxygendefine:: SPI_CR1_BIDIOE_BIT
.. doxygendefine:: SPI_CR1_CRCEN_BIT
.. doxygendefine:: SPI_CR1_CRCNEXT_BIT
.. doxygendefine:: SPI_CR1_DFF_BIT
.. doxygendefine:: SPI_CR1_RXONLY_BIT
.. doxygendefine:: SPI_CR1_SSM_BIT
.. doxygendefine:: SPI_CR1_SSI_BIT
.. doxygendefine:: SPI_CR1_LSBFIRST_BIT
.. doxygendefine:: SPI_CR1_SPE_BIT
.. doxygendefine:: SPI_CR1_MSTR_BIT
.. doxygendefine:: SPI_CR1_CPOL_BIT
.. doxygendefine:: SPI_CR1_CPHA_BIT

.. doxygendefine:: SPI_CR1_BIDIMODE
.. doxygendefine:: SPI_CR1_BIDIMODE_2_LINE
.. doxygendefine:: SPI_CR1_BIDIMODE_1_LINE
.. doxygendefine:: SPI_CR1_BIDIOE
.. doxygendefine:: SPI_CR1_CRCEN
.. doxygendefine:: SPI_CR1_CRCNEXT
.. doxygendefine:: SPI_CR1_DFF
.. doxygendefine:: SPI_CR1_DFF_8_BIT
.. doxygendefine:: SPI_CR1_DFF_16_BIT
.. doxygendefine:: SPI_CR1_RXONLY
.. doxygendefine:: SPI_CR1_SSM
.. doxygendefine:: SPI_CR1_SSI
.. doxygendefine:: SPI_CR1_LSBFIRST
.. doxygendefine:: SPI_CR1_SPE
.. doxygendefine:: SPI_CR1_BR
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_2
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_4
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_8
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_16
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_32
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_64
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_128
.. doxygendefine:: SPI_CR1_BR_PCLK_DIV_256
.. doxygendefine:: SPI_CR1_MSTR
.. doxygendefine:: SPI_CR1_CPOL
.. doxygendefine:: SPI_CR1_CPOL_LOW
.. doxygendefine:: SPI_CR1_CPOL_HIGH
.. doxygendefine:: SPI_CR1_CPHA

Control register 2
~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SPI_CR2_TXEIE_BIT
.. doxygendefine:: SPI_CR2_RXNEIE_BIT
.. doxygendefine:: SPI_CR2_ERRIE_BIT
.. doxygendefine:: SPI_CR2_SSOE_BIT
.. doxygendefine:: SPI_CR2_TXDMAEN_BIT
.. doxygendefine:: SPI_CR2_RXDMAEN_BIT

.. doxygendefine:: SPI_CR2_TXEIE
.. doxygendefine:: SPI_CR2_RXNEIE
.. doxygendefine:: SPI_CR2_ERRIE
.. doxygendefine:: SPI_CR2_SSOE
.. doxygendefine:: SPI_CR2_TXDMAEN
.. doxygendefine:: SPI_CR2_RXDMAEN

Status register
~~~~~~~~~~~~~~~

.. doxygendefine:: SPI_SR_BSY_BIT
.. doxygendefine:: SPI_SR_OVR_BIT
.. doxygendefine:: SPI_SR_MODF_BIT
.. doxygendefine:: SPI_SR_CRCERR_BIT
.. doxygendefine:: SPI_SR_UDR_BIT
.. doxygendefine:: SPI_SR_CHSIDE_BIT
.. doxygendefine:: SPI_SR_TXE_BIT
.. doxygendefine:: SPI_SR_RXNE_BIT

.. doxygendefine:: SPI_SR_BSY
.. doxygendefine:: SPI_SR_OVR
.. doxygendefine:: SPI_SR_MODF
.. doxygendefine:: SPI_SR_CRCERR
.. doxygendefine:: SPI_SR_UDR
.. doxygendefine:: SPI_SR_CHSIDE
.. doxygendefine:: SPI_SR_CHSIDE_LEFT
.. doxygendefine:: SPI_SR_CHSIDE_RIGHT
.. doxygendefine:: SPI_SR_TXE
.. doxygendefine:: SPI_SR_RXNE

I2S configuration register
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: SPI_I2SCFGR_I2SMOD_BIT
.. doxygendefine:: SPI_I2SCFGR_I2SE_BIT
.. doxygendefine:: SPI_I2SCFGR_PCMSYNC_BIT
.. doxygendefine:: SPI_I2SCFGR_CKPOL_BIT
.. doxygendefine:: SPI_I2SCFGR_CHLEN_BIT

.. doxygendefine:: SPI_I2SCFGR_I2SMOD
.. doxygendefine:: SPI_I2SCFGR_I2SMOD_SPI
.. doxygendefine:: SPI_I2SCFGR_I2SMOD_I2S
.. doxygendefine:: SPI_I2SCFGR_I2SE
.. doxygendefine:: SPI_I2SCFGR_I2SCFG
.. doxygendefine:: SPI_I2SCFGR_I2SCFG_SLAVE_TX
.. doxygendefine:: SPI_I2SCFGR_I2SCFG_SLAVE_RX
.. doxygendefine:: SPI_I2SCFGR_I2SCFG_MASTER_TX
.. doxygendefine:: SPI_I2SCFGR_I2SCFG_MASTER_RX
.. doxygendefine:: SPI_I2SCFGR_PCMSYNC
.. doxygendefine:: SPI_I2SCFGR_PCMSYNC_SHORT
.. doxygendefine:: SPI_I2SCFGR_PCMSYNC_LONG
.. doxygendefine:: SPI_I2SCFGR_I2SSTD
.. doxygendefine:: SPI_I2SCFGR_I2SSTD_PHILLIPS
.. doxygendefine:: SPI_I2SCFGR_I2SSTD_MSB
.. doxygendefine:: SPI_I2SCFGR_I2SSTD_LSB
.. doxygendefine:: SPI_I2SCFGR_I2SSTD_PCM
.. doxygendefine:: SPI_I2SCFGR_CKPOL
.. doxygendefine:: SPI_I2SCFGR_CKPOL_LOW
.. doxygendefine:: SPI_I2SCFGR_CKPOL_HIGH
.. doxygendefine:: SPI_I2SCFGR_DATLEN
.. doxygendefine:: SPI_I2SCFGR_DATLEN_16_BIT
.. doxygendefine:: SPI_I2SCFGR_DATLEN_24_BIT
.. doxygendefine:: SPI_I2SCFGR_DATLEN_32_BIT
.. doxygendefine:: SPI_I2SCFGR_CHLEN
.. doxygendefine:: SPI_I2SCFGR_CHLEN_16_BIT
.. doxygendefine:: SPI_I2SCFGR_CHLEN_32_BIT

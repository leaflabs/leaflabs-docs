.. highlight:: c
.. _libmaple-dma:

``dma.h``
=========

Direct Memory Access (DMA) support.

.. contents:: Contents
   :local:

Types
-----

.. doxygenstruct:: dma_reg_map
.. doxygenstruct:: dma_dev
.. doxygenstruct:: dma_handler_config
.. doxygenenum:: dma_mode_flags
.. doxygenenum:: dma_xfer_size
.. doxygenenum:: dma_channel
.. doxygenenum:: dma_priority
.. doxygenenum:: dma_irq_cause
.. doxygenstruct:: dma_channel_reg_map

Devices
-------

.. doxygenvariable:: DMA1
.. doxygenvariable:: DMA2

Functions
---------

.. doxygenfunction:: dma_init
.. doxygenfunction:: dma_setup_transfer
.. doxygenfunction:: dma_set_num_transfers
.. doxygenfunction:: dma_set_priority
.. doxygenfunction:: dma_attach_interrupt
.. doxygenfunction:: dma_detach_interrupt
.. doxygenfunction:: dma_get_irq_cause
.. doxygenfunction:: dma_enable
.. doxygenfunction:: dma_disable
.. doxygenfunction:: dma_set_mem_addr
.. doxygenfunction:: dma_set_per_addr
.. doxygenfunction:: dma_channel_regs
.. doxygenfunction:: dma_is_channel_enabled
.. doxygenfunction:: dma_get_isr_bits
.. doxygenfunction:: dma_clear_isr_bits

Register Map Base Pointers
--------------------------

.. doxygendefine:: DMA1_BASE
.. doxygendefine:: DMA2_BASE

Register Bit Definitions
------------------------

Interrupt status register
~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DMA_ISR_TEIF7_BIT
.. doxygendefine:: DMA_ISR_HTIF7_BIT
.. doxygendefine:: DMA_ISR_TCIF7_BIT
.. doxygendefine:: DMA_ISR_GIF7_BIT
.. doxygendefine:: DMA_ISR_TEIF6_BIT
.. doxygendefine:: DMA_ISR_HTIF6_BIT
.. doxygendefine:: DMA_ISR_TCIF6_BIT
.. doxygendefine:: DMA_ISR_GIF6_BIT
.. doxygendefine:: DMA_ISR_TEIF5_BIT
.. doxygendefine:: DMA_ISR_HTIF5_BIT
.. doxygendefine:: DMA_ISR_TCIF5_BIT
.. doxygendefine:: DMA_ISR_GIF5_BIT
.. doxygendefine:: DMA_ISR_TEIF4_BIT
.. doxygendefine:: DMA_ISR_HTIF4_BIT
.. doxygendefine:: DMA_ISR_TCIF4_BIT
.. doxygendefine:: DMA_ISR_GIF4_BIT
.. doxygendefine:: DMA_ISR_TEIF3_BIT
.. doxygendefine:: DMA_ISR_HTIF3_BIT
.. doxygendefine:: DMA_ISR_TCIF3_BIT
.. doxygendefine:: DMA_ISR_GIF3_BIT
.. doxygendefine:: DMA_ISR_TEIF2_BIT
.. doxygendefine:: DMA_ISR_HTIF2_BIT
.. doxygendefine:: DMA_ISR_TCIF2_BIT
.. doxygendefine:: DMA_ISR_GIF2_BIT
.. doxygendefine:: DMA_ISR_TEIF1_BIT
.. doxygendefine:: DMA_ISR_HTIF1_BIT
.. doxygendefine:: DMA_ISR_TCIF1_BIT
.. doxygendefine:: DMA_ISR_GIF1_BIT

.. doxygendefine:: DMA_ISR_TEIF7
.. doxygendefine:: DMA_ISR_HTIF7
.. doxygendefine:: DMA_ISR_TCIF7
.. doxygendefine:: DMA_ISR_GIF7
.. doxygendefine:: DMA_ISR_TEIF6
.. doxygendefine:: DMA_ISR_HTIF6
.. doxygendefine:: DMA_ISR_TCIF6
.. doxygendefine:: DMA_ISR_GIF6
.. doxygendefine:: DMA_ISR_TEIF5
.. doxygendefine:: DMA_ISR_HTIF5
.. doxygendefine:: DMA_ISR_TCIF5
.. doxygendefine:: DMA_ISR_GIF5
.. doxygendefine:: DMA_ISR_TEIF4
.. doxygendefine:: DMA_ISR_HTIF4
.. doxygendefine:: DMA_ISR_TCIF4
.. doxygendefine:: DMA_ISR_GIF4
.. doxygendefine:: DMA_ISR_TEIF3
.. doxygendefine:: DMA_ISR_HTIF3
.. doxygendefine:: DMA_ISR_TCIF3
.. doxygendefine:: DMA_ISR_GIF3
.. doxygendefine:: DMA_ISR_TEIF2
.. doxygendefine:: DMA_ISR_HTIF2
.. doxygendefine:: DMA_ISR_TCIF2
.. doxygendefine:: DMA_ISR_GIF2
.. doxygendefine:: DMA_ISR_TEIF1
.. doxygendefine:: DMA_ISR_HTIF1
.. doxygendefine:: DMA_ISR_TCIF1
.. doxygendefine:: DMA_ISR_GIF1

Interrupt flag clear register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DMA_IFCR_CTEIF7_BIT
.. doxygendefine:: DMA_IFCR_CHTIF7_BIT
.. doxygendefine:: DMA_IFCR_CTCIF7_BIT
.. doxygendefine:: DMA_IFCR_CGIF7_BIT
.. doxygendefine:: DMA_IFCR_CTEIF6_BIT
.. doxygendefine:: DMA_IFCR_CHTIF6_BIT
.. doxygendefine:: DMA_IFCR_CTCIF6_BIT
.. doxygendefine:: DMA_IFCR_CGIF6_BIT
.. doxygendefine:: DMA_IFCR_CTEIF5_BIT
.. doxygendefine:: DMA_IFCR_CHTIF5_BIT
.. doxygendefine:: DMA_IFCR_CTCIF5_BIT
.. doxygendefine:: DMA_IFCR_CGIF5_BIT
.. doxygendefine:: DMA_IFCR_CTEIF4_BIT
.. doxygendefine:: DMA_IFCR_CHTIF4_BIT
.. doxygendefine:: DMA_IFCR_CTCIF4_BIT
.. doxygendefine:: DMA_IFCR_CGIF4_BIT
.. doxygendefine:: DMA_IFCR_CTEIF3_BIT
.. doxygendefine:: DMA_IFCR_CHTIF3_BIT
.. doxygendefine:: DMA_IFCR_CTCIF3_BIT
.. doxygendefine:: DMA_IFCR_CGIF3_BIT
.. doxygendefine:: DMA_IFCR_CTEIF2_BIT
.. doxygendefine:: DMA_IFCR_CHTIF2_BIT
.. doxygendefine:: DMA_IFCR_CTCIF2_BIT
.. doxygendefine:: DMA_IFCR_CGIF2_BIT
.. doxygendefine:: DMA_IFCR_CTEIF1_BIT
.. doxygendefine:: DMA_IFCR_CHTIF1_BIT
.. doxygendefine:: DMA_IFCR_CTCIF1_BIT
.. doxygendefine:: DMA_IFCR_CGIF1_BIT

.. doxygendefine:: DMA_IFCR_CTEIF7
.. doxygendefine:: DMA_IFCR_CHTIF7
.. doxygendefine:: DMA_IFCR_CTCIF7
.. doxygendefine:: DMA_IFCR_CGIF7
.. doxygendefine:: DMA_IFCR_CTEIF6
.. doxygendefine:: DMA_IFCR_CHTIF6
.. doxygendefine:: DMA_IFCR_CTCIF6
.. doxygendefine:: DMA_IFCR_CGIF6
.. doxygendefine:: DMA_IFCR_CTEIF5
.. doxygendefine:: DMA_IFCR_CHTIF5
.. doxygendefine:: DMA_IFCR_CTCIF5
.. doxygendefine:: DMA_IFCR_CGIF5
.. doxygendefine:: DMA_IFCR_CTEIF4
.. doxygendefine:: DMA_IFCR_CHTIF4
.. doxygendefine:: DMA_IFCR_CTCIF4
.. doxygendefine:: DMA_IFCR_CGIF4
.. doxygendefine:: DMA_IFCR_CTEIF3
.. doxygendefine:: DMA_IFCR_CHTIF3
.. doxygendefine:: DMA_IFCR_CTCIF3
.. doxygendefine:: DMA_IFCR_CGIF3
.. doxygendefine:: DMA_IFCR_CTEIF2
.. doxygendefine:: DMA_IFCR_CHTIF2
.. doxygendefine:: DMA_IFCR_CTCIF2
.. doxygendefine:: DMA_IFCR_CGIF2
.. doxygendefine:: DMA_IFCR_CTEIF1
.. doxygendefine:: DMA_IFCR_CHTIF1
.. doxygendefine:: DMA_IFCR_CTCIF1
.. doxygendefine:: DMA_IFCR_CGIF1

Channel configuration register
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygendefine:: DMA_CCR_MEM2MEM_BIT
.. doxygendefine:: DMA_CCR_MINC_BIT
.. doxygendefine:: DMA_CCR_PINC_BIT
.. doxygendefine:: DMA_CCR_CIRC_BIT
.. doxygendefine:: DMA_CCR_DIR_BIT
.. doxygendefine:: DMA_CCR_TEIE_BIT
.. doxygendefine:: DMA_CCR_HTIE_BIT
.. doxygendefine:: DMA_CCR_TCIE_BIT
.. doxygendefine:: DMA_CCR_EN_BIT

.. doxygendefine:: DMA_CCR_MEM2MEM
.. doxygendefine:: DMA_CCR_PL
.. doxygendefine:: DMA_CCR_PL_LOW
.. doxygendefine:: DMA_CCR_PL_MEDIUM
.. doxygendefine:: DMA_CCR_PL_HIGH
.. doxygendefine:: DMA_CCR_PL_VERY_HIGH
.. doxygendefine:: DMA_CCR_MSIZE
.. doxygendefine:: DMA_CCR_MSIZE_8BITS
.. doxygendefine:: DMA_CCR_MSIZE_16BITS
.. doxygendefine:: DMA_CCR_MSIZE_32BITS
.. doxygendefine:: DMA_CCR_PSIZE
.. doxygendefine:: DMA_CCR_PSIZE_8BITS
.. doxygendefine:: DMA_CCR_PSIZE_16BITS
.. doxygendefine:: DMA_CCR_PSIZE_32BITS
.. doxygendefine:: DMA_CCR_MINC
.. doxygendefine:: DMA_CCR_PINC
.. doxygendefine:: DMA_CCR_CIRC
.. doxygendefine:: DMA_CCR_DIR
.. doxygendefine:: DMA_CCR_TEIE
.. doxygendefine:: DMA_CCR_HTIE
.. doxygendefine:: DMA_CCR_TCIE
.. doxygendefine:: DMA_CCR_EN

.. highlight:: sh

.. _maple-native-b:

Maple Native β
==============

This page is a general resource for information specific to the Maple
Native Beta.  Since this is a beta release, the information here may
change slightly between now and the final Maple Native release.

.. contents:: Contents
   :local:

Technical Specifications
------------------------

* MCU: `STM32F103ZET6 <maple-native-b-stdocs>`, a 32-bit ARM Cortex M3
  microprocessor.
* Clock Speed: **72 MHz**
* **512 KB Flash**, **64 KB SRAM** (on-chip), **1 MB SRAM** (external)
* 106 :ref:`digital I/O pins <gpio>`
* 17 :ref:`PWM <pwm>` pins at 16 bit resolution
* 21 :ref:`analog input (ADC) <adc>` pins at 12-bit resolution
* 3 :ref:`SPI <spi>` peripherals
* 2 :ref:`I2C <i2c>` peripherals
* 12 Channels of Direct Memory Access (**DMA**) (:ref:`libmaple-dma`)
  with 2 DMA controllers
* 3 :ref:`USART (serial port) <usart>` peripherals, 2 **UART** peripherals
* 2 advanced, 4 general-purpose, and 2 basic :ref:`timers <timers>`
* Dedicated :ref:`USB <usb>` port for programming and communications
* :ref:`JTAG <jtag>`
* Nested Vectored Interrupt Controller (NVIC) (including
  :ref:`external interrupt <lang-attachinterrupt>` on GPIOs)
* Supplies up to 500 mA at 3.3 V, with :ref:`separate 250 mA digital
  and analog regulators <maple-native-b-adc-bank>` for low-noise analog
  performance
* :ref:`Open-source, four layer design <maple-native-b-hardware>`
* Support for low power, sleep, and standby modes (<500 μA)
* Operating Voltage: 3.3 V
* Input Voltage (recommended): 3 V — 12 V
* Dimensions: 4″ × 2.1″

.. _maple-native-b-powering:

Powering the Maple Native
-------------------------

The power source is determined by the header labeled "PWRSEL" on the
silkscreen. The Maple Native may be powered from USB (marked "USB" on
the PWRSEL header), a LiPo battery (marked "BAT"), or one of the two
"Vin" pins (marked "EXT").  Boards are shipped with a jumper on the
USB selector.  In order to power it off of an alternative source,
unplug the Maple Native, then move the jumper to the desired selector
before reconnecting power.

The "Vin" line is available on the pin labeled "Vin" on the vertical
header to the right of the PWRSEL header, as well as on the
unpopulated two-pin connector on the upper left corner of the
board. On this latter connector, polarity was accidentally left
unmarked: the leftmost, round pin should be power, while the square
pin should be ground.

When powering the Maple Native board from a battery or the Vin lines,
care must be taken not to over-voltage the board. In general, an upper
limit of 12V input is acceptable, but this may vary depending upon the
current draw requirements of the application. Please see :ref:`Power
Regulation on the Maple Native <maple-native-b-power-regulation>` for
more information.

.. _maple-native-b-power-regulation:

Power Regulation on the Maple Native
------------------------------------

Power regulation on the Maple Native is provided by two low dropout
linear voltage regulators. (The part is the MCP1703 from Microchip, in
the SOT-23A package. You can download the datasheet `here
<http://ww1.microchip.com/downloads/en/DeviceDoc/22049a.pdf>`_). One
of the regulators supplies power to the digital voltage plane; the
other supplies power to the analog voltage plane.

These voltage regulators nominally take an input of up to 16V. In
addition, while the maximum continuous output current for the board is
250mA, if you are powering the board off higher voltages the current
it can supply goes down, due to the regulators needing to dissipate
the extra power. So if you are powering the board off 12V, the max
current is about 40mA at room temperature. In general (again, at room
temperature) the max power dissipation (PD) for the chip is about
.37W, and output current = PD/(Vin-Vout). For exact max current
calculations, please refer to the datasheet linked above.

If you are planning to draw a lot of current from the Maple Native
board, it is necessary to provide input power as close to 3.3V as
possible. Powering the microcontroller circuitry and LEDs on the board
alone takes approximately 30mA, so if you are powering the board with
12V that leaves only 10mA (at best) available for powering any user
circuitry. Attempting to draw more than 10mA runs the risk of shorting
out the power regulators and bricking your board.

Using the Built-in Battery Charger
----------------------------------

Maple Native includes a built-in LiPo battery charger.  In order to
use it, put a jumper across the CHRG selector on the PWRSEL header and
across the USB, or EXT selectors, depending on whether you're charging
the battery via USB cable or Vin, respectively.  The LED labeled CHRG
will light up while the battery is being charged.  When the battery is
finished charging, the LED labeled DONE will light up.

.. _maple-native-b-gpios:

GPIO Information
----------------

The Maple Native features 106 total input/output pins, numbered ``D0``
through ``D105``.  In most cases, these numbers correspond to the
numeric values next to each header on the Maple Native's silkscreen.
However, pins ``D101`` through ``D105`` are broken out to the
:ref:`JTAG <jtag>` header, and are not numbered on the silkscreen.  In
addition, some other pins have other uses by default [#fusedpins]_.

.. _maple-native-b-but:

Pin ``D6`` is the Native's :ref:`button pin <lang-board-values-but>`.
It is thus mainly useful as an :ref:`input <lang-pin-levels>`.  The
pin will :ref:`read <lang-digitalread>` ``HIGH`` when the :ref:`button
is pressed <lang-isbuttonpressed>`.

.. _maple-native-b-led:

Pin ``D22`` is the Native's :ref:`LED pin <lang-board-values-led>`.
It is thus mainly useful as an :ref:`output <lang-pin-levels>`.  The
LED will glow when ``HIGH`` is :ref:`written <lang-digitalwrite>` to
it.

.. _maple-native-b-fsmc:

Many of the pins on the right header (pins ``D56`` through ``D100``,
the header is labeled :ref:`"FSMC" <fsmc>` on the silkscreen) are
connected to the SRAM chip.  Using these pins as GPIOs may render the
memory chip useless, which can cause your program to crash. For this
reason, we don't recommend that you use these pins unless you know
what you are doing. The following pins on the right header are not
connected to the SRAM and may be used with impunity: ``D57``, ``D60``,
``D63``, ``D66``, ``D69``, ``D72``, ``D75``, ``D80``, ``D83``.

.. _maple-native-b-jtag:

Pins ``D101`` through ``D105`` are connected to the pads on the
:ref:`JTAG <jtag>` header.  In order to use them as GPIOs, you must
first disable the Maple Native's debug ports.  You can do this by
calling :ref:`lang-disabledebugports`.  (Note that this means you
won't be able to use JTAG or SW-Debug to debug your program).

.. TODO [0.1.0] silkscreen pictures

.. _maple-native-b-pin-map-master:

Master Pin Map
^^^^^^^^^^^^^^

This table shows a summary the available functionality on every GPIO
pin, by peripheral type.  The "5 V?" column documents whether or not
the pin is :ref:`5 volt tolerant <gpio-5v-tolerant>`.

Note that this table is not exhaustive; on some pins, more peripherals
are available than are listed here.

**Top header:**

.. csv-table::
   :header: Pin, :ref:`GPIO <gpio>`, :ref:`ADC <adc>`, :ref:`Timer <timers>`, :ref:`I2C <i2c>`, :ref:`UART <usart>`, :ref:`SPI <spi>`, 5 V?

   D0,   PB10,  -,       -,       2_SCL,   3_TX,   -,       Yes
   D1,   PB11,  -,       -,       2_SDA,   3_RX,   -,       Yes
   D2,   PB12,  -,       1_BKIN,  2_SMBA,  3_CK,   2_NSS,   Yes
   D3,   PB13,  -,       -,       -,       3_CTS,  2_SCK,   Yes
   D4,   PB14,  -,       -,       -,       3_RTS,  2_MISO,  Yes
   D5,   PB15,  -,       -,       -,       -,      2_MOSI,  Yes
   D6,   PG15,  -,       -,       -,       -,      -,       Yes
   D7,   PC0,   1_CH10,  -,       -,       -,      -,       -
   D8,   PC1,   1_CH11,  -,       -,       -,      -,       -
   D9,   PC2,   1_CH12,  -,       -,       -,      -,       -
   D10,  PC3,   1_CH13,  -,       -,       -,      -,       -
   D11,  PC4,   1_CH14,  -,       -,       -,      -,       -
   D12,  PC5,   1_CH15,  -,       -,       -,      -,       -
   D13,  PC6,   -,       8_CH1,   -,       -,      -,       Yes
   D14,  PC7,   -,       8_CH2,   -,       -,      -,       Yes
   D15,  PC8,   -,       8_CH3,   -,       -,      -,       Yes
   D16,  PC9,   -,       8_CH4,   -,       -,      -,       Yes
   D17,  PC10,  -,       -,       -,       4_TX,   -,       Yes
   D18,  PC11,  -,       -,       -,       4_RX,   -,       Yes
   D19,  PC12,  -,       -,       -,       5_TX,   -,       Yes
   D20,  PC13,  -,       -,       -,       -,      -,       -
   D21,  PC14,  -,       -,       -,       -,      -,       -
   D22,  PC15,  -,       -,       -,       -,      -,       -
   D23,  PA8,   -,       1_CH1,   -,       1_CK,   -,       Yes
   D24,  PA9,   -,       1_CH2,   -,       1_TX,   -,       Yes
   D25,  PA10,  -,       1_CH3,   -,       1_RX,   -,       Yes
   D26,  PB9,   -,       4_CH4,   -,       -,      -,       Yes

**Bottom header:**

.. note:: ``D48``, ``D49``, ``D50``, ``D51`` are also connected to
   Timer 2 channels 1, 2, 3, and 4, respectively.

.. csv-table::
   :header: Pin, :ref:`GPIO <gpio>`, :ref:`ADC <adc>`, :ref:`Timer <timers>`, :ref:`I2C <i2c>`, :ref:`UART <usart>`, :ref:`SPI <spi>`, 5 V?

   D27,  PD2,   -,      3_ETR,  -,       5_RX,   -,       Yes
   D28,  PD3,   -,      -,      -,       -,      -,       Yes
   D29,  PD6,   -,      -,      -,       -,      -,       Yes
   D30,  PG11,  -,      -,      -,       -,      -,       Yes
   D31,  PG12,  -,      -,      -,       -,      -,       Yes
   D32,  PG13,  -,      -,      -,       -,      -,       Yes
   D33,  PG14,  -,      -,      -,       -,      -,       Yes
   D34,  PG8,   -,      -,      -,       -,      -,       Yes
   D35,  PG7,   -,      -,      -,       -,      -,       Yes
   D36,  PG6,   -,      -,      -,       -,      -,       Yes
   D37,  PB5,   -,      -,      1_SMBA,  -,      3_MOSI,  -
   D38,  PB6,   -,      4_CH1,  1_SCL,   -,      -,       Yes
   D39,  PB7,   -,      4_CH2,  1_SDA,   -,      -,       Yes
   D40,  PF11,  -,      -,      -,       -,      -,       Yes
   D41,  PF6,   3_CH4,  -,      -,       -,      -,       -
   D42,  PF7,   3_CH5,  -,      -,       -,      -,       -
   D43,  PF8,   3_CH6,  -,      -,       -,      -,       -
   D44,  PF9,   3_CH7,  -,      -,       -,      -,       -
   D45,  PF10,  3_CH8,  -,      -,       -,      -,       -
   D46,  PB1,   1_CH9,  3_CH4,  -,       -,      -,       -
   D47,  PB0,   1_CH8,  3_CH3,  -,       -,      -,       -
   D48,  PA0,   1_CH0,  5_CH1,  -,       2_CTS,  -,       -
   D49,  PA1,   1_CH1,  5_CH2,  -,       2_RTS,  -,       -
   D50,  PA2,   1_CH2,  5_CH3,  -,       2_TX,   -,       -
   D51,  PA3,   1_CH3,  5_CH4,  -,       2_RX,   -,       -
   D52,  PA4,   1_CH4,  -,      -,       2_CK,   1_NSS,   -
   D53,  PA5,   1_CH5,  -,      -,       -,      1_SCK,   -
   D54,  PA6,   1_CH6,  3_CH1,  -,       -,      1_MISO,  -
   D55,  PA7,   1_CH7,  3_CH2,  -,       -,      1_MOSI,  -

.. _maple-native-b-fsmc-map:

**Right (FSMC) header**

All of the following pins are 5V-tolerant.  Note that in the "FSMC"
column below, entries with a "Dn" value (D0, D1, etc.) don't refer to
pins; they refer to FSMC data lines.  See :ref:`RM0008
<maple-native-b-stdocs>` for more information.

.. warning:: Many of the pins on this header are used by the Maple
   Native's SRAM chip.  Don't use them as GPIOs unless you know what
   you're doing, or your program may crash.  :ref:`See above
   <maple-native-b-fsmc>` for more information.

.. csv-table::
   :header: Pin, :ref:`GPIO <gpio>`, :ref:`FSMC <fsmc>`

   D56,  PF0,   A0
   D57,  PD11,  A16
   D58,  P14,   D0
   D59,  PF1,   A1
   D60,  PD12,  A17
   D61,  PD15,  D1
   D62,  PF2,   A2
   D63,  PD13,  A18
   D64,  PD0,   D2
   D65,  PF3,   A3
   D66,  PE3,   A19
   D67,  PD1,   D3
   D68,  PF4,   A4
   D69,  PE4,   A20
   D70,  PE7,   D4
   D71,  PF5,   A5
   D72,  PE5,   A21
   D73,  PE8,   D8
   D74,  PF12,  A6
   D75,  PE6,   A22
   D76,  PE9,   D6
   D77,  PF13,  A7
   D78,  PE10,  D7
   D79,  PF14,  A8
   D80,  PG9,   NE2/NCE3
   D81,  PE11,  D8
   D82,  PF15,  A9
   D83,  PG10,  NCE4_1/NE3/NCE4_2
   D84,  PE12,  D9
   D85,  PG0,   A10
   D86,  PD5,   NWE
   D87,  PE13,  D10
   D88,  PG1,   A11
   D89,  PD4,   NOE
   D90,  PE14,  D11
   D91,  PG2,   A12
   D92,  PE1,   NBL1
   D93,  PE15,  D12
   D94,  PG3,   A13
   D95,  PE0,   NBL0
   D96,  PD8,   D13
   D97,  PG4,   A14
   D98,  PD9,   D14
   D99,  PG5,   A15
   D100, PD10,  D15

**JTAG header pins**

.. note:: See :ref:`above <maple-native-b-jtag>` for more information on
   these pins.

.. csv-table::
   :header: Pin, :ref:`GPIO <gpio>`, :ref:`SPI <spi>`, 5 V?

   D101, PA13,  -,       Yes
   D102, PA14,  -,       Yes
   D103, PA15,  3_NSS,   Yes
   D104, PB3,   3_SCK,   Yes
   D105, PB4,   3_MISO,  Yes

.. _maple-native-b-gpio-port-map:

GPIO Port Pin Map
^^^^^^^^^^^^^^^^^

The following tables show what pins are associated with each
:ref:`GPIO port <gpio-ports>`.

.. csv-table::
   :header: GPIOA, GPIOB, GPIOC, GPIOD

   PA0:  D48,     PB0:  D47,    PC0:  D7,    PD0: D64
   PA1:  D49,     PB1:  D46,    PC1:  D8,    PD1: D67
   PA2:  D50,     PB2:  -,      PC2:  D9,    PD2: D27
   PA3:  D51,     PB3:  D104,   PC3:  D10,   PD3: D28
   PA4:  D52,     PB4:  D105,   PC4:  D11,   PD4: D89
   PA5:  D53,     PB5:  D37,    PC5:  D12,   PD5: D86
   PA6:  D54,     PB6:  D38,    PC6:  D13,   PD6: D29
   PA7:  D55,     PB7:  D39,    PC7:  D14,   PD7: -
   PA8:  D23,     PB8:  -,      PC8:  D15,   PD8: D96
   PA9:  D24,     PB9:  D26,    PC9:  D16,   PD9: D98
   PA10: D25,     PB10: D0,     PC10: D17,   PD10: D100
   PA11: -,       PB11: D1,     PC11: D18,   PD11: D57
   PA12: -,       PB12: D2,     PC12: D19,   PD12: D60
   PA13: D101,    PB13: D3,     PC13: D20,   PD13: D63
   PA14: D102,    PB14: D4,     PC14: D21,   PD14: D58

.. csv-table::
   :header: GPIOE, GPIOF, GPIOG

   PE0: D95,    PF0: D56,    PG0: D85
   PE1: D92,    PF1: D59,    PG1: D88
   PE2: -       PF2: D62,    PG2: D91,
   PE3: D66,    PF3: D65,    PG3: D94
   PE4: D69,    PF4: D68,    PG4: D97
   PE5: D72,    PF5: D71,    PG5: D99
   PE6: D75,    PF6: D41,    PG6: D36
   PE7: D70,    PF7: D42,    PG7: D35
   PE8: D73,    PF8: D43,    PG8: D34
   PE9: D76,    PF9: D44,    PG9: D80
   PE10: D78,   PF10: D45,   PG10: D83
   PE11: D81,   PF11: D40,   PG11: D30
   PE12: D84,   PF12: D74,   PG12: D31
   PE13: D87,   PF13: D77,   PG13: D32
   PE14: D90,   PF14: D79,   PG14: D33

.. _maple-native-b-timer-map:

Timer Pin Map
^^^^^^^^^^^^^

The following table shows what pins are associated with a particular
timer's capture/compare channels.

There is no mistake between timers 2 and 5.  They really do share
those pins.  If you like, you can remap some of the timer 2 channels
to get extra PWM pins; see :ref:`afio_remap() (in gpio.h)
<gpio-h-afio-remap>`.

.. csv-table::
   :header: Timer, Ch. 1, Ch. 2, Ch. 3, Ch. 4
   :delim: |

   1 | D23 | D24 | D25 |
   2 | D48 | D49 | D50 | D51
   3 | D54 | D55 | D47 | D46
   4 | D38 | D39 |     | D26
   5 | D48 | D49 | D50 | D51
   8 | D13 | D14 | D15 | D16

.. _maple-native-b-exti-map:

EXTI Line Pin Map
^^^^^^^^^^^^^^^^^

The following table shows which pins connect to which :ref:`EXTI lines
<external-interrupts-exti-line>`.

.. list-table::
   :widths: 1 3
   :header-rows: 1

   * - EXTI Line
     - Pins
   * - EXTI0
     - D7, D47, D48, D56, D64, D85, D95
   * - EXTI1
     - D8, D46, D49, D59, D67, D88, D92
   * - EXTI2
     - D9, D27, D50, D62, D91
   * - EXTI3
     - D10, D28, D51, D65, D66, D94, D104
   * - EXTI4
     - D11, D52, D68, D69, D89, D97, D105
   * - EXTI5
     - D12, D37, D53, D71, D72, D86, D99
   * - EXTI6
     - D13, D29, D36, D38, D41, D54, D75
   * - EXTI7
     - D14, D35, D39, D42, D55, D70
   * - EXTI8
     - D15, D23, D34, D43, D73, D96
   * - EXTI9
     - D16, D24, D26, D44, D76, D80, D98
   * - EXTI10
     - D0, D17, D25, D45, D78, D83, D100
   * - EXTI11
     - D1, D18, D30, D40, D57, D81
   * - EXTI12
     - D2, D19, D31, D60, D74, D84
   * - EXTI13
     - D3, D20, D32, D63, D77, D87, D101
   * - EXTI14
     - D4, D21, D33, D58, D79, D90, D102
   * - EXTI15
     - D5, D6, D22, D61, D82, D93, D103

.. _maple-native-b-usart-map:

USART Pin Map
^^^^^^^^^^^^^

The Maple Native has 3 :ref:`USART <usart>` serial ports.  They
communicate using the pins given in the following table.

.. csv-table::
   :header: Serial port, TX, RX, CK, CTS, RTS
   :delim: |

   ``Serial1`` | D24 | D25 | D23 |     |
   ``Serial2`` | D50 | D51 | D52 | D48 | D49
   ``Serial3`` |  D0 |  D1 |  D2 |  D3 |  D4

The Maple Native also has 2 UART serial ports.  Unlike USARTS, these
only communicate asynchronously, and thus only have TX and RX pins.
These are given in the following table.

.. csv-table::
   :header: Serial port, TX, RX
   :delim: |

   ``Serial4`` | D17 | D18
   ``Serial5`` | D19 | D27

.. _maple-native-b-adc-bank:

Low-Noise ADC Pins
^^^^^^^^^^^^^^^^^^

There are fifteen pins at the bottom right of the board (``D41`` —
``D55``) that generally offer lower-noise ADC performance than other
pins on the board. If you're concerned about getting good ADC
readings, we recommend using one of these pins to take your
measurements.

Maple Native has an electrically isolated analog power plane with its
own regulator, and a geometrically isolated ground plane. Analog input
pins D41 — D55 are laid out to correspond with these analog planes,
and our measurements indicate that they generally ofer low noise ADC
performance.  However, analog performance may vary depending upon the
activity of other GPIOs.  In particular, using PWM on any of pins
``D46`` — ``D51``, ``D54``, and ``D55`` may cause digital noise.
Consult the :ref:`Maple Native beta hardware design files
<maple-native-b-hardware>` for more details.

.. _maple-native-b-board-values:

Board-Specific Values
---------------------

This section lists the Maple Native's :ref:`board-specific values
<lang-board-values>`.

- ``CYCLES_PER_MICROSECOND``: 72
- ``BOARD_BUTTON_PIN``: 6
- ``BOARD_LED_PIN``: 22
- ``BOARD_NR_GPIO_PINS``: 106
- ``BOARD_NR_PWM_PINS``: 18
- ``boardPWMPins``: 13, 14, 15, 16, 23, 24, 25, 26, 38, 39, 46, 47,
  48, 49, 50, 51, 54, 55
- ``BOARD_NR_ADC_PINS``: 21
- ``boardADCPins``: 7, 8, 9, 10, 11, 12, 41, 42, 43, 44, 45, 46, 47,
  48, 49, 50, 51, 52, 53, 54, 55
- ``BOARD_NR_USED_PINS``: 43
- ``boardUsedPins``: ``BOARD_LED_PIN``, ``BOARD_BUTTON_PIN``,
    ``BOARD_JTMS_SWDIO_PIN``, ``BOARD_JTCK_SWCLK_PIN``,
    ``BOARD_JTDI_PIN``, ``BOARD_JTDO_PIN``, ``BOARD_NJTRST_PIN``, and
    all pins on FSMC header except those mentioned :ref:`above
    <maple-native-b-fsmc>`.
- ``BOARD_NR_USARTS``: 5
- ``BOARD_USART1_TX_PIN``: 24
- ``BOARD_USART1_RX_PIN``: 25
- ``BOARD_USART2_TX_PIN``: 50
- ``BOARD_USART2_RX_PIN``: 51
- ``BOARD_USART3_TX_PIN``: 0
- ``BOARD_USART3_RX_PIN``: 1
- ``BOARD_UART4_TX_PIN``: 17
- ``BOARD_UART4_RX_PIN``: 18
- ``BOARD_UART5_TX_PIN``: 19
- ``BOARD_UART5_RX_PIN``: 27
- ``BOARD_NR_SPI``: 3
- ``BOARD_SPI1_NSS_PIN``: 52
- ``BOARD_SPI1_MOSI_PIN``: 55
- ``BOARD_SPI1_MISO_PIN``: 54
- ``BOARD_SPI1_SCK_PIN``: 53
- ``BOARD_SPI2_NSS_PIN``: 2
- ``BOARD_SPI2_MOSI_PIN``: 5
- ``BOARD_SPI2_MISO_PIN``: 4
- ``BOARD_SPI2_SCK_PIN``: 3
- ``BOARD_SPI3_NSS_PIN``: 103 (on :ref:`JTAG header <maple-native-b-jtag>`)
- ``BOARD_SPI3_MOSI_PIN``: 37
- ``BOARD_SPI3_MISO_PIN``: 105 (JTAG header)
- ``BOARD_SPI3_SCK_PIN``: 104 (JTAG header)
- ``BOARD_JTMS_SWDIO_PIN``: :ref:`103 <maple-native-b-jtag>`
- ``BOARD_JTCK_SWCLK_PIN``: 102
- ``BOARD_JTDI_PIN``: 103
- ``BOARD_JTDO_PIN``: 104
- ``BOARD_NJTRST_PIN``: 105

.. _maple-native-b-hardware:

Hardware Design Files
^^^^^^^^^^^^^^^^^^^^^

The hardware schematics and board layout files are available in the
`Maple Native GitHub repository
<https://github.com/leaflabs/maplenative/>`_.  Download the `beta
version's hardware design files
<https://github.com/leaflabs/maplenative/tree/beta>`_ (ZIP format).

If you're familiar with Git, you can clone the entire repository and
checkout the commit tagged "beta" using the following::

    $ git clone git://github.com/leaflabs/maplenative.git
    $ git checkout beta

Failure Modes
-------------

The following known failure modes apply to the Maple Native Beta.  The
failure modes aren't design errors, but are easy ways to break or
damage your board permanently.

* **Reversing Vin and GND**: when powering the Maple Native Beta via
  the Vin and ground (GND) pins at the top left of the board, it is
  possible to carelessly cause a short or switch the connections,
  applying the high voltage to GND and ground to Vin.

  If this happens, you will reverse bias the diode beneath these pins,
  most likely damaging it.  This may cause excess voltage to
  subsequently be delivered to the board once the reversed pins are
  connected properly.

Errata
------

This section lists known issues and warnings for the Maple Native
Beta.

* **PWM on pin 39**: PWM on pin 39 appears to be nonfunctional.  We
  are looking into this issue.

* **VREF is nonfunctional**: Due to a routing error, VREF is
  permanently tied to 3.3V at VAA.

Recommended Reading
-------------------

.. _maple-native-b-stdocs:

STMicro documentation for STM32F103ZE microcontroller:

* `Datasheet
  <http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/DATASHEET/CD00191185.pdf>`_
  (PDF); covers STM32F103xC, STM3F103xD, STM32F103xE.
* `Reference Manual RM0008
  <http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/REFERENCE_MANUAL/CD00171190.pdf>`_
  (PDF); definitive resource for peripherals on the STM32F1 line.
* `Programming Manual PM0056
  <http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/PROGRAMMING_MANUAL/CD00228163.pdf>`_
  (PDF); assembly language and register reference.
* `STM32F103RE <http://www.st.com/internet/mcu/product/164485.jsp>`_
  overview page with links to further references.

.. rubric:: Footnotes

.. [#fusedpins] See :ref:`boardUsedPins <lang-board-values-used-pins>`
   for more information.

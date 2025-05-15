Introduction
============


.. image:: https://readthedocs.org/projects/adafruit-circuitpython-spd1656/badge/?version=latest
    :target: https://docs.circuitpython.org/projects/spd1656/en/latest/
    :alt: Documentation Status


.. image:: https://raw.githubusercontent.com/adafruit/Adafruit_CircuitPython_Bundle/main/badges/adafruit_discord.svg
    :target: https://adafru.it/discord
    :alt: Discord


.. image:: https://github.com/adafruit/Adafruit_CircuitPython_SPD1656/workflows/Build%20CI/badge.svg
    :target: https://github.com/adafruit/Adafruit_CircuitPython_SPD1656/actions
    :alt: Build Status


.. image:: https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json
    :target: https://github.com/astral-sh/ruff
    :alt: Code Style: Ruff

Driver for SPD1656 driven ACeP (7-color) e-paper displays.

Please note that we do not have Blinka support for this yet. So it won't work with a Raspberry Pi.

Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_
or individual libraries can be installed using
`circup <https://github.com/adafruit/circup>`_.

This supports the common 4" and 5.65" ACeP displays.

* [Waveshare 4"](https://www.waveshare.com/4.01inch-e-paper-hat-f.htm)
* [Waveshare 5.65"](https://www.waveshare.com/5.65inch-e-paper-module-f.htm)
* [Pimoroni 5.7"](https://shop.pimoroni.com/products/inky-impression-5-7) (Likely the same as 5.65".)
* [Pimoroni 4"](https://shop.pimoroni.com/products/inky-impression-4)

Installing from PyPI
=====================

On supported GNU/Linux systems like the Raspberry Pi, you can install the driver locally `from
PyPI <https://pypi.org/project/adafruit-circuitpython-spd1656/>`_.
To install for current user:

.. code-block:: shell

    pip3 install adafruit-circuitpython-spd1656

To install system-wide (this may be required in some cases):

.. code-block:: shell

    sudo pip3 install adafruit-circuitpython-spd1656

To install in a virtual environment in your current project:

.. code-block:: shell

    mkdir project-name && cd project-name
    python3 -m venv .venv
    source .env/bin/activate
    pip3 install adafruit-circuitpython-spd1656

Installing to a Connected CircuitPython Device with Circup
==========================================================

Make sure that you have ``circup`` installed in your Python environment.
Install it with the following command if necessary:

.. code-block:: shell

    pip3 install circup

With ``circup`` installed and your CircuitPython device connected use the
following command to install:

.. code-block:: shell

    circup install adafruit_spd1656

Or the following command to update an existing version:

.. code-block:: shell

    circup update

Usage Example
=============

.. code-block:: python

    # SPDX-FileCopyrightText: Copyright (c) 2023 Scott Shawcroft for Adafruit Industries
    # SPDX-FileCopyrightText: Copyright (c) 2021 Melissa LeBlanc-Williams for Adafruit Industries
    #
    # SPDX-License-Identifier: Unlicense

    """Simple test script for 5.6" 600x448 7-color ACeP display.
      """

    import time
    import board
    import displayio
    import adafruit_spd1656

    displayio.release_displays()

    # This pinout works on a Feather RP2040 and may need to be altered for other boards.
    spi = board.SPI()  # Uses SCK and MOSI
    epd_cs = board.D9
    epd_dc = board.D10
    epd_reset = board.D11
    epd_busy = board.D12

    display_bus = fourwire.FourWire(
        spi, command=epd_dc, chip_select=epd_cs, reset=epd_reset, baudrate=1000000
    )

    display = adafruit_spd1656.SPD1656(
        display_bus, width=600, height=448, busy_pin=epd_busy
    )

    g = displayio.Group()

    fn = "/display-ruler-720p.bmp"

    with open(fn, "rb") as f:
        pic = displayio.OnDiskBitmap(f)
        t = displayio.TileGrid(pic, pixel_shader=pic.pixel_shader)
        g.append(t)

        display.root_group = g

        display.refresh()

        time.sleep(120)

Documentation
=============
API documentation for this library can be found on `Read the Docs <https://docs.circuitpython.org/projects/spd1656/en/latest/>`_.

For information on building library documentation, please check out
`this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/adafruit/Adafruit_CircuitPython_SPD1656/blob/HEAD/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

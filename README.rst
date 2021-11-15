.. image:: https://raw.githubusercontent.com/CityOfZion/visual-identity/develop/_CoZ%20Branding/_Logo/_Logo%20icon/_PNG%20200x178px/CoZ_Icon_DARKBLUE_200x178px.png
    :alt: CoZ logo


NEO3VM
------
A C++ port of the NEO3 Blockchain `Virtual Machine <https://github.com/neo-project/neo-vm>`_ with bindings for Python 3.8 & 3.9.

Installation
~~~~~~~~~~~~
::

    pip install neo3vm

Or download the wheels from the Github releases page.

Usage
~~~~~

.. code-block:: python

    import neo3vm
    # PUSH1, PUSH2, ADD (1 + 2 = )
    script = neo3vm.Script(b'\x11\x12\x9E')
    engine = neo3vm.ExecutionEngine()
    engine.load_script(script)
    engine.execute()
    assert(engine.state == neo3vm.VMState.HALT)
    assert(engine.result_stack.peek() == neo3vm.IntegerStackItem(3))

Further documentation on the classes can be queried from the extension module ``help(neo3vm)``.

Bindings vs source code
~~~~~~~~~~~~~~~~~~~~~~~
For the time being only the Python bindings are made available publicly. Other bindings may follow. 

If you have a use-case for the C++ VM feel free to reach out to python@coz.io to discuss the possibilities.

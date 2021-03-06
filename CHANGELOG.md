## Changelog
All notable changes to this project are documented in this file.

## [0.8.1] 2020-06-14
### C++ changes
* Fix reference counter edge case for nested struct stack not decreasing reference count.  

## [0.8] 2020-06-04
### Python binding updates
* Expose `opcode_price()` getter on ``ApplicationEngine``
* Drop Python 3.7 bindings

### C++ changes
* Fix pushing negative numbers with ``ScriptBuilder`` ([ref](https://github.com/neo-project/neo-vm/pull/413))
* Support pushing Python ``None`` type

## [0.7.1] 2020-05-17
### C++ changes
* Add missing `POW` instruction to opcode price table for use by the `ApplicationEngine` class.

## [0.7] 2020-05-03
* Update internals to match [rc2](https://github.com/neo-project/neo-vm/releases/tag/v3.0.0-rc2)

## [0.6] 2020-04-30
* Update internals to match [rc1](https://github.com/neo-project/neo-vm/releases/tag/v3.0.0-rc1)

## [0.5.1] 2020-04-06
### Python binding updates
- Expose ``load_token()`` overload on ``ApplicationEngineCpp``

### C++ changes
* Update ``ExecutionContext::clone()`` to include scripthash bytes
* Add missing ``break`` statement for ``OpCode::CALLT`` implementation causing extra contexts being loaded
* Fix strict mode for preview 5 block 2721
* Fix reference counter for circular types

## [0.5] 2020-02-18
### C++ changes
* Update internals to match [preview5](https://github.com/neo-project/neo-vm/releases/tag/v3.0.0-preview5)

## [0.4.3] 2020-12-15
**Python binding updates**
* Expose partial native `ApplicationEngine`

### C++ changes
* Add partial native `ApplicationEngine`. Profiling showed that the `pre_execute_instruction()` was found to be very expensive while it works with mostly static data. Moving it to C++ avoids bridging between C++ and Python for every instruction executed.

## [0.4.2] 2020-12-09
### C++ changes
* Add OpCode `DIV` implementation
* Fix OpCode `REVERSE` not taking `count` into account
* Fix `ExecutionContext.static_field` cloning not working as intended

## [0.4.1] 2020-12-07
**Python binding updates**
* Expose missing OpCode `DIV`

### C++ changes
* Add more details to exception messages to help debugging without source 

## [0.4] 2020-10-15
**Python binding updates**
* `ExecutionEngine` changes
   * Protect `push()` and `pop()` from crashing the Python interpreter if the user doesn't initialise the engine properly
   * Expose `load_context()`
   * Expose `load_cloned_context()`
   * Expose `context_unloaded()`
   * Allowed overriding `pre_execute_instruction()`
   * Allowed overriding `post_execute_instruction()`
   * Allowed overriding `load_context()`
   * Allowed overriding `context_unloaded()`
* `ExecutionContext` changes
   * `script` property is now writable
   * `ip` property is now writable
   * Expose `calling_script` property
   * Fix `load_script()` not returning a proper reference
* `IntegerStackItem` class now supports creation from a Python `int`
* `StackItem` class now exposes `deep_copy()` function
* `PrimitiveType` class now supports `len()`
* `Instruction` class now supports creation from `bytes`

### C++ changes
* Fix `ExecutionContext::call_flags` initialisation value
* Fix `RET` opcode implementation failing to call context_unload

## Changelog
All notable changes to this project are documented in this file.

## [0.10.1] 2022-07-05
### C++ changes
* Add `push_on_return` and `snapshot` fields to `ExecutionContext` to support core fixes ([ref1](https://github.com/neo-project/neo/pull/2755),[ref2](https://github.com/neo-project/neo/pull/2729))

### Python binding updates
* Expose `push_on_return` and `snapshot` fields on `ExecutionContext`.

## [0.10.0] 2022-06-28
### C++ changes
* Fix DDOS in max equal comparison ([ref](https://github.com/neo-project/neo-vm#454)).
* Add MODMUL MODPOW opcodes ([ref](https://github.com/neo-project/neo-vm#455)).
* Deep copy as immutable option ([ref](https://github.com/neo-project/neo-vm#473)).
* Add `extra_data` field to `ExecutionContext` allowing to store arbitrary Python objects ([ref](https://github.com/neo-project/neo/pull/2734)).

### Python binding updates
* The `deep_copy` method on `StackItem`s now requires an argument to indicate if it should be copied as immutable (has special meaning inside the NEO core).
* Expose `extra_data` field on `ExecutionContext`.

## [0.9.0] 2022-05-17
### C++ changes
* Changed reference counter implementation. This results in compound stackitem derivatives no longer requiring a `ReferenceCounter` as argument in their constructors making them easier to use and less error prone. It also helped fixing a Python binding issue for OSX. 
* Expose `move_next` on `ExecutionContext` making it easier to create a dissassembler.

### Python binding updates
* Removed `ReferenceCounter` argument from all compound stackitems.

## [0.8.6] 2022-02-01
### C++ changes
* Add `load_script` function with additional argument to override the context scripthash bytes property to support correctly loading contracts on the mamba side.
* Perform explicit casting of 2 values used in reference counting to prevent an incorrect relational expression result.

### Python binding updates
* Expose the additional `load_script` function

## [0.8.5] 2021-11-30
### C++ changes
* Fix calling script hash not shared between `ExecutionContext`s in certain cases

## [0.8.4] 2021-10-08
### C++ changes
* Allow certain exceptions to be caugth by smart contracts ([ref](https://github.com/neo-project/neo-vm/pull/436))

## [0.8.3] 2021-08-23
### C++ changes
* Fix `MapStackItem` to remember insertion order

## [0.8.2] 2021-08-02
Following the C# side
### C++ changes
* Limit `POW` exponent ([ref](https://github.com/neo-project/neo-vm/pull/422)) 
* Fix `SQRT` ([ref](https://github.com/neo-project/neo-vm/pull/427))
* Limit `StructStackItem` clone and equality depths ([ref1](https://github.com/neo-project/neo-vm/pull/423), [ref2](https://github.com/neo-project/neo-vm/pull/428))
* Reference counter optimization


## [0.8.1] 2021-06-14
### C++ changes
* Fix reference counter edge case for nested struct stack not decreasing reference count.  

## [0.8] 2021-06-04
### Python binding updates
* Expose `opcode_price()` getter on ``ApplicationEngine``
* Drop Python 3.7 bindings

### C++ changes
* Fix pushing negative numbers with ``ScriptBuilder`` ([ref](https://github.com/neo-project/neo-vm/pull/413))
* Support pushing Python ``None`` type

## [0.7.1] 2021-05-17
### C++ changes
* Add missing `POW` instruction to opcode price table for use by the `ApplicationEngine` class.

## [0.7] 2021-05-03
* Update internals to match [rc2](https://github.com/neo-project/neo-vm/releases/tag/v3.0.0-rc2)

## [0.6] 2021-04-30
* Update internals to match [rc1](https://github.com/neo-project/neo-vm/releases/tag/v3.0.0-rc1)

## [0.5.1] 2021-04-06
### Python binding updates
- Expose ``load_token()`` overload on ``ApplicationEngineCpp``

### C++ changes
* Update ``ExecutionContext::clone()`` to include scripthash bytes
* Add missing ``break`` statement for ``OpCode::CALLT`` implementation causing extra contexts being loaded
* Fix strict mode for preview 5 block 2721
* Fix reference counter for circular types

## [0.5] 2021-02-18
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

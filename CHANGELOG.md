## Changelog
All notable changes to this project are documented in this file.

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

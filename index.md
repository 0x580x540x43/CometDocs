# Comet Documentation

[Comet](https://cometrbx/)

Written by 0x580x540x43#3331

Functions are documented in this format:
`return_type function_name(type arg, type arg2, [type optional_arg])`

* return_type - The Lua datatype of the returned value
* function_name - The name of the function
* type arg - type is the expected datatype of the argument and arg is a name
* [type optional_arg] - Square brackets mean that you are not required to pass in a value 

Format stolen from Greenman#8153

# Enviroment Functions

### Get Global Enviroment

`table getgenv()`

Returns the enviroment that will be applied each script by Comet. Can be used to create global functions or values in Comet.

Example:
```lua
getgenv().message = print
```
```lua
--another script
message("Hello World!")
```

### Get Roblox Enviroment

`table getrenv()`

Returns the global enviroment for the LocalScript state.

### Get Registry

`table getreg()`

Returns the Lua registry.

### Get Garbage Collection

`table getgc([bool include_tables])`

Returns all the functions and userdata values in the garbage collector. Passing true will also return tables.

### Get Instances

`table<Instance> getinstances`

Returns a table of all the Instances in the current game.

### Get Nil Instances

`table<Instance> getnilinstances`

Returns a table of all the instances parented to **nil** in the current game.

### Get Loaded Modules

`table<ModuleScript> getloadedmodules()`

Returns all the loaded ModuleScripts in the current game.

### Get Connections

`table<Connection> getconnections(ScriptSignal object)`

Gets a list of connections to the specified signal. You can do the following operations on a Connection:
| Example      | Description                              | 
| ------------ | ---------------------------------------- |
| .Function	   | The function connected to the connection |
| .State	   | The state of the connection |
| :Enable	   | Enables the connection |
| :Disable	   | Disables the connection |
| :Fire 	   | Fires the connection |

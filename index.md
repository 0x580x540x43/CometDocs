# Comet Documentation

Written by 0x580x540x43#3331

Inspiration and most content from Synapse documentation, excuded functions that are not in Comet
Credits to Greenman#8153 for the functions format

https://cometrbx.xyz/

Functions are documented in this format:
> ```<return_type> function_name(<type> arg, <type> arg2, [<type> optional_arg])```

* return_type - The Lua/Roblox datatype of the returned value
* function_name - The name of the function
* type arg - type is the expected datatype of the argument and arg is a name
* [type optional_arg] - Square brackets mean that you are not required to pass in a value 

# Enviroment Functions


### Get Global Enviroment

`<table> getgenv()`

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

`<table> getrenv()`

Returns the global enviroment for the LocalScript state.

### Get Registry

`<table> getreg()`

Returns the Lua registry.

### Get Garbage Collection

`<table> getgc([<bool> include_tables])`

Returns all the functions and userdata values in the garbage collector. Passing true will also return tables.

### Get Instances

`<table<Instance>> getinstances()`

Returns a table of all the Instances in the current game.

### Get Nil Instances

`<table<Instance>> getnilinstances()`

Returns a table of all the instances parented to `nil` in the current game.

### Get Loaded Modules

`<table<ModuleScript>> getloadedmodules()`

Returns all the loaded ModuleScripts in the current game.

### Get Connections

`<table<Connection>> getconnections(<ScriptSignal> object)`

Gets a list of connections to the specified signal. You can do the following operations on a Connection:

| Example      | Description                              | 
| ------------ | ---------------------------------------- |
| .Function	   | The function connected to the connection |
| .State	   | The state of the connection |
| :Enable	   | Enables the connection |
| :Disable	   | Disables the connection |
| :Fire 	   | Fires the connection |

Example: 
```lua
for i, connection in pairs(getconnections(workspace.ChildAdded)) do
    connection:Disable()
end
```

### Fire Signal

`<void> firesignal(<ScriptSignal> Signal, <variant> Args...)`

Fires all the connections connected to the signal `Signal` with `Args`.

### Fire Click Detector

`<void> fireclickdetector(<ClickDetector> Detector, [<int> Distance])`

Fires the designated `ClickDetector` with provided Distance. If Distance isn't provided, it will default to 0.

### Fire Proximity Prompt

`<void> fireproximityprompt(<ProximityPrompt> Prompt, <int> Distance)`

Fires the designated `ProximityPrompt`.

### Fire Touch Interest

`<void> firetouchinterest(<Instance> Part, <BasePart> ToTouch, <uint> Toggle)`

Fakes a .Touched event to `ToTouch` with Part. The `Toggle` argument must be either 0 or 1 (for fire/un-fire).

**Note**: The ToTouch argument must have a child with class `TouchTransmitter` in order for this function to work.

### Get Hidden Property

`<variant> gethiddenproperty(<Instance> Object, <string> Property)`

Returns the hidden property `Property` from `Object`. Errors if the property does not exist.

### Set Hidden Property

`<void> sethiddenproperty(<Instance> Object, <string> Property, <variant> Value)`

Sets the hidden property `Property` with `Value` from `Object`. Errors if the property does not exist.

### Set Simulation Radius

`<void> setsimulationradius(<uint> SimulationRadius)`

Sets the player's SimulationRadius.

# Script Functions


### Get Script Enviroment

`<table> getsenv(union<LocalScript, ModuleScript> Script)`

Returns the environment of `Script`. Errors if the script is not loaded in memory.

### Get Calling Script

`<union<LocalScript, ModuleScript, nil>> getcallingscript(<void>)`

Gets the script that is calling this function.

# Table Functions


### Get Raw Metatable

`<table> getrawmetatable(<table> value)`

Retrieve the metatable of value irregardless of value's metatable's `__metatable` field. Returns `nil` if it doesn't exist.

### Set Raw Metatable

`<bool> setrawmetatable(<object> o, <table> mt)`

Sets `o's` metatable to `mt` even if the `__metatable` field exists in `o's` metatable.

### Set Readonly

`<void> setreadonly(<table> t, <bool> val)`

Sets `t's` read-only value to `val`.

### Is Readonly

`<bool> isreadonly(<table> t)`

Returns `t's` read-only condition.

# Input Functions


### Is Active

`<bool> iswindowactive(<void>)`

Returns if the main window is in focus. This must return true for any other mouse/keyboard function to work.

### Keyboard

`<void> keypress(<uint> keycode)`

Simulates a key press for the specified keycode. Keycodes are listed [here](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes).

`<void> keyrelease(<uint> key)`

Releases key on the keyboard. You can access the key values from the link above.

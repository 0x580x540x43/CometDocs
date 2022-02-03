# Comet Documentation

Functions are documented in this format:
> ```<return_type> function_name(<type> arg, <type> arg2, [<type> optional_arg])```

* return_type - The Lua/Roblox datatype of the returned value
* function_name - The name of the function
* type arg - type is the expected datatype of the argument and arg is a name
* [type optional_arg] - Square brackets mean that you are not required to pass in a value 

# Environment Functions


### Get Global Environment

`<table> getgenv()`

Returns the environment that will be applied each script by Comet. Can be used to create global functions or values in Comet.

#### Example
```lua
getgenv().message = print
```
```lua
--another script
message("Hello World!")
```

### Get Roblox Environment

`<table> getrenv()`

Returns the global environment for the LocalScript state.

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

#### Example

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


### Get Script Environment

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

### Keyboard Functions

`<void> keypress(<uint> keycode)`

Simulates a key press for the specified keycode. Keycodes are listed [here](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes).

`<void> keyrelease(<uint> key)`

Releases key on the keyboard. You can access the key values from the link above.

### Left Mouse Functions

`<void> mouse1click(<void>)`

Simulates a full left mouse button press.

`<void> mouse1press(<void>)`

Simulates a left mouse button press without releasing it.

`<void> mouse1release(<void>)`

Simulates a left mouse button release.

### Right Mouse Functions

`<void> mouse2click(<void>)`

Simulates a full right mouse button press.

`<void> mouse2press(<void>)`

Simulates a right mouse button press without releasing it.

`<void> mouse2release(<void>)`

Simulates a right mouse button release.

### Mouse Movement Functions

`<void> mousescroll(<number> px)`

Scrolls the mouse wheel virtually by px pixels.

`<void> mousemoverel(<number> x, <number> y)`

Moves the mouse cursor relatively to the current mouse position by coordinates x and y.

`<void> mousemoveabs(<number> x, <number> y)`

Move's your mouse to the x and y coordinates in pixels from topleft of the main window.

# Hooking Functions


### Hook Function

`<function> hookfunction(<function> old, <function> hook)`

Hooks function `old`, replacing it with the function `hook`. The old function is returned, you *must* use this function in order to call the original function.

### Hook Metamethod

`<function> hookmetamethod(<Object> object, <string> metamethod, <function> hook)`

Hooks the `metamethod` passed in the `object`'s metatable with `hook`. A function to call the original metamethod is returned, you *must* use this function in order to call the original metamethod.

This function will error if an object without a metatable is passed or a invalid metamethod is passed.

### New C Closure

`<function> newcclosure(<function> f)`

Pushes a new CClosure that invokes function `f` upon call.

# Reflection Functions

### Loadstring

`<union<function, nil>, <string?>> loadstring(<string> chunk, [<string> chunk_name])`

Loads chunk as a Lua function with optional `chunk_name` and returns it if compilation is successful. Otherwise, if an error has occurred during compilation, `nil` followed by the error message will be returned.

### Check Caller

`<bool> checkcaller(<void>)`

Returns `true` if the current thread is a Synapse thread. **Note:** Checkcaller does NOT check the call stack of the function, if you call a game function then it calls out to checkcaller, the result will be `true`! Be careful.

### Is Lua Closure

`<bool> islclosure(<function> f)`

Returns true if `f` is an LClosure.

# Console Functions


### Console Print

`<void> rconsoleprint(<string> message)`

Prints `message` into the console. `rconsoleprint` also supports colors.

#### Example

```lua
rconsoleprint('@@RED@@')
rconsoleprint('this is red')
```

#### Colors

| Color            | Code                | 
| ---------------- | ------------------- |
| Black	           | @@BLACK@@           |
| Blue	           | @@BLUE@@            |
| Green	           | @@GREEN@@           |
| Cyan	           | @@CYAN@@            |
| Red	           | @@RED@@             |
| Magenta          | @@MAGENTA@@         |
| Brown	           | @@BROWN@@           |
| Light Gray       | @@LIGHT_GRAY@@      |
| Dark Gray        | @@DARK_GRAY@@       |
| Light Blue       | @@LIGHT_BLUE@@      |
| Light Green      | @@LIGHT_GREEN@@     |
| Light Cyan	   | @@LIGHT_CYAN@@      |
| Light Red        | @@LIGHT_RED@@       |
| Light Magenta	   | @@LIGHT_MAGENTA@@   |
| Yellow           | @@YELLOW@@          |
| White	           | @@WHITE@@           |


### Console Info

`<void> rconsoleinfo(<string> message)`

Prints `message` into the console, with a info text before it.

### Console Warn

`<void> rconsolewarn(<string> message)`

Prints `message` into the console, with a warning text before it.

### Console Error

`<void> rconsoleerr(<string> message)`

Prints `message` into the console, with a error text before it.

### Console Clear

`<void> rconsoleclear(<void>)`

Clears the console.

### Console Name

`<void> rconsolename(<string> title)`

Sets the currently allocated console title to `title`.

### Console Input

`<string> rconsoleinput(<void>)`

Yields until the user inputs information into their console. Returns the input they put in.

# Filesystem Functions


### Read File

`<string> readfile(<string> path)`

Reads the contents of the file located at `path` and returns it. If the file does not exist, it errors.

### Write File

`<void> writefile(<string> path, <string> contents)`

Writes `contents` to the supplied `path`. If the file does not exist, it errors.

### Append File

`<void> appendfile(<string> path, <string> content)`

Appends `content` to the file contents at `path`. If the file does not exist, it errors.

### Load File

`<union<function, nil>, <string?>> loadfile(<string> path)`

Loads in the contents of a file as a chunk and returns it if compilation is successful. Otherwise, if an error has occurred during compilation, `nil` followed by the error message will be returned.

### List Files

`<table> listfiles(<string> folder)`

Returns a table of files in `folder`.

### Is File

`<bool> isfile(<string> path)`

Returns if `path` is a file or not.

### Is Folder

`<bool> isfolder(<string> path)`

Returns if `path` is a folder or not.

### Make Folder

`<void> makefolder(<string> path)`

Creates a new folder at `path`.

### Delete Folder

`<void> delfolder(<string> path)`

Deletes the folder in the supplied path, if no folder exists, it errors.

### Delete File

`<void> delfile(<string> path)`

Deletes the file in the supplied `path`, if no file exists, it errors.

# Miscellaneous Functions


### Set Clipboard

`<void> setclipboard(<string> value)`

Sets `value` to the clipboard.

### Set Fast Flag

`<void> setfflag(<string> FFlag, <string> Value)`

Sets `FFlag` with Value. Must be run before the game loads, auto execute + auto inject recommended.

You can find a list of FFlags [here](https://fflag.eryn.io).

### Get Namecall Method

`<string> getnamecallmethod(<void>)`

Returns the namecall method if the function is called in an `__namecall` metatable hook.

### Set Namecall Method

`<void> setnamecallmethod(<string> method)`

Sets the current namecall method to the new namecall method. Must be called in a `__namecall` metatable hook.

### Get Synapse Asset

`<Content> getsynasset(<string> path)`

Returns a `Content` string that can be used as a fake Asset ID for GUI elements. Please note this will only affect your client.

**Note**: Certain instances only work with specific file types. For example, `VideoFrame`'s only work with `.webm` encoded videos.

### Messagebox

`<uint> messagebox(<string> text, <string> caption, <uint> flags)`

Creates a message box with parameters text, caption and style.

| Style                         | Number |
| ----------------------------- | ------ |
| OK	                        | 0      |
| OK / Cancel		            | 1      |
| Abort / Retry / Ignore	    | 2      |
| Yes / No / Cancel		        | 3      |
| Yes / No		                | 4      |
| Retry / Cancel                | 5      |
| Cancel / Try Again / Continue | 6      |

| Code | Description                        |
| ---- | ---------------------------------- |
| 1    | The OK button was selected.        |
| 2    | The Cancel button was selected.    |
| 3    | The Abort button was selected.     |
| 4    | The Retry button was selected.     |
| 5    | The Ignore button was selected.    |
| 6    | The Yes button was selected.       |
| 7    | The No button was selected.        |
| 10   | The Try Again button was selected. |
| 11   | The Continue button was selected.  |

### Set Thread Identity

`<void> set_thread_identity(<uint> n)`

Sets the current thread identity.

### Queue On Teleport

`<void> queueonteleport(<string> code)`

Executes `code` after player is teleported.

#### Example

```lua
game:GetService("Players").LocalPlayer.OnTeleport:Connect(function(State)
    if State == Enum.TeleportState.Started then
        queueonteleport("<script to execute after TP>")
    end
end)
```

### Comet Loaded

`<bool> COMET_LOADED(<void>)`

Returns a bool indicating whether or not Comet is loaded.

# Credits

Documentation written by 0x580x540x43#3331

Inspiration and most content from Synapse documentation, functions that are not in Comet have been excluded.

Credits to noobmaster.

Credits to Greenman#8153 for the functions format.

[Official Comet website](https://cometrbx.xyz/)

[Comet credits](https://cometrbx.xyz/credits.html)

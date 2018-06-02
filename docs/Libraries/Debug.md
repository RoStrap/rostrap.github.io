# Debugging Tools
Standard RoStrap debugging library

## Standard Debug Module
This module has standard helper functions to assist in debugging.

### API
```lua
local Debug = require("Debug")
```

```cs
string Debug.TableToString (table Table [, string TableName])
	/// Pretty self-explanatory
	// @param table Table The table to convert into a string
	// @param string TableName [Optional]: Puts `local TableName = ` at the beginning
	// @returns a readable string of the table
```
```cs
string Debug.DirectoryToString (RbxObject Object)
	/// A fixed version of GetFullName
	// @param RbxObject Object the Object to get the directory of
	// @returns string A readable and properly formatted string of the directory
```

```cs
string Debug.Inspect (any Object)
	/// Returns a string representation of anything.
	// @param any Object The object you wish to represent as a string.
	// @returns a readable string representation of the object.
```
```cs
string Debug.EscapeString (string String)
	/// Turns strings into Lua-readble format
	// @returns Objects location in proper Lua format
	// Useful for when you are doing string-intensive coding
	// Those minus signs are so tricky!
```
```cs
function function Debug.AlphabeticalOrder (table Dictionary)
	/// Iteration function that iterates over a dictionary in alphabetical order
	// @param table Dictionary That which will be iterated over in alphabetical order
	// A dictionary looks like this: {Apple = true, Noodles = 5, Soup = false}
	// Not case-sensitive
```
```cs
void function Debug.Error (string ErrorMessage, ... strings argumentsToFormatIn ...)
	// Standard RoStrap Erroring system
	// Prefixing ErrorMessage with '!' makes it expect the [error origin].Name as first parameter in {...}
	// Past the initial Error string, subsequent arguments get unpacked in a string.format of the error string
	// Arguments formmatted into the string get stringified (see above function)
	// Assert falls back on Error
	// Error blames the latest item on the traceback as the cause of the error
	// Error makes it clear which Library and function are being misused
```
```cs
<Condition, void> function Debug.Assert (Variant Condition, ... TupleToSendToError ...)
	// Returns Condition or Debug.Error(...)
```
```cs
void function Debug.Warn (string ErrorMessage, ... strings argumentsToFormatIn ...)
	// Functions the same as Debug.Error, but internally calls warn instead of error
```

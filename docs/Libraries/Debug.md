# Debug
Standard RoStrap debugging library

```lua
local Debug = Resources:LoadLibrary("Debug")
```

## Library API

### Debug.TableToString

!!! summary "<span style="color:purple;">string</span> Debug.<span style="color:blue;">TableToString</span>(<span style="color:green;">table</span> Table [, <span style="color:teal;">string</span> TableName, <span style="color:green;">bool</span> Multiline = <span style="color:green;">false</span>])"
	Pretty self-explanatory. Table is the table to convert into a string. String TableName puts `local TableName = ` at the beginning. Multiline makes it multiline. Returns a string-readable version of Table.

### Debug.DirectoryToString

!!! summary "<span style="color:purple;">string</span> Debug.<span style="color:blue;">DirectoryToString</span>(RbxObject Object)"
	 A fixed version of GetFullName.

### Debug.Inspect

!!! summary "<span style="color:purple;">string</span> Debug.<span style="color:blue;">Inspect</span>(<span style="color:green;">any</span> Object)"
	Returns a string representation of Object

### Debug.EscapeString

!!! summary "<span style="color:purple;">string</span> Debug.<span style="color:blue;">EscapeString</span>(<span style="color:green;">string</span> String)"
	Turns strings into Lua-readble format. Returns Objects location in proper Lua format. Useful for when you are doing string-intensive coding. Those minus signs are so tricky!

### Debug.AlphabeticalOrder

!!! summary "<span style="color:purple;">function</span> Debug.<span style="color:blue;">AlphabeticalOrder</span>(<span style="color:green;">table</span> Dictionary)"
	Iteration function that iterates over a dictionary in alphabetical order. Dictionary is that which will be iterated over in alphabetical order. Not case-sensitive.

!!! example
	```lua
	for Key, Value in next, Debug.AlphabeticalOrder{Apple = true, Noodles = 5, Soup = false} do
		print(Key, Value)
	end
	```

### Debug.Error

!!! summary "<span style="color:purple;">void</span> Debug.<span style="color:blue;">Error</span>(<span style="color:green;">string</span> ErrorMessage, ... <span style="color:teal;">strings</span> <span style="color:green;">argumentsToFormatIn</span>)"
	Standard RoStrap Erroring system. Prefixing ErrorMessage with '!' makes it expect the `[error origin script].Name` as first parameter in `{...}`. Past the initial Error string, subsequent arguments get unpacked in a string.format of the error string. Assert falls back on Error. Error blames the latest item on the traceback as the cause of the error. Error makes it clear which Library and function are being misused.

### Debug.Assert

!!! summary "<span style="color:purple;">Condition</span> Debug.<span style="color:blue;">Assert</span>(Variant Condition, ... <span style="color:green;">strings</span> TupleToSendToError)"
	Returns `Condition or Debug.Error(...)`

### Debug.Warn

!!! summary "<span style="color:purple;">void</span> Debug.<span style="color:blue;">Warn</span>(<span style="color:green;">string</span> ErrorMessage, ... <span style="color:teal;">strings</span> <span style="color:green;">argumentsToFormatIn</span>)"
	Functions the same as Debug.Error, but internally calls warn instead of error.

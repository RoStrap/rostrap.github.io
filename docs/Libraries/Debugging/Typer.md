# Typer
Type Checker and Function Signature Assigner

## Library API

### Typer.AssignSignature

!!! summary "<span style="color:purple;">function</span> Typer.<span style="color:blue;">AssignSignature</span>([<span style="color:green;">number</span> ParameterIndexToStartChecking = 1&comma; ] <span style="color:teal;">types</span> ... &comma; <span style="color:green;">function</span> Callback)"
	Returns a function which checks to make sure the arguments passed in exactly match the parameters specified. If they match, it will call `Callback`, otherwise it will error, stating which parameter caused the error and what was expected.

	Each parameter corresponds to the parameter with which the function is being called. Parameters should be arrays containing all valid strings which may be returned by `typeof(parameter)`. For example: `{"string", "number", "nil"}` would allow the corresponding parameter to be a `string`, `number`, or `nil`. Optionally, a table may have a `[string TypeNameKey] = function Callback` which may be called to determine whether a parameter is of the type `TypeNameKey`.

	The first parameter may optionally be a positive integer which is the first parameter `AssignSignature` should start checking.

!!! example
	```lua
	local Typer = Resources:LoadLibrary("Typer")

	local function IsButton(Value, TypeOfString)
		-- Value is the Parameter
		-- TypeOfString is the string returned by typeof(Value)

		return TypeOfString == "Instance" and (Value:IsA("TextButton") or Value:IsA("ImageButton"))
	end

	local foo = Typer.AssignSignature({"string", "number", "nil", Button = IsButton}, function(s)
		-- s can be a string, number, nil, or Button (TextButton or ImageButton)
		-- Will error if `s` is none of the aforementioned
		-- Will error if 2 or more parameters are passed in

		return s
	end)

	foo(2) -- 2
	foo("Hello") -- Hello
	foo({}) -- [Typer] {Foo} bad argument #1: expected Button or string or number or nil, got table {}

	local bar = Typer.AssignSignature(2, {"string"}, {"number"}, function(p1, p2, p3)
		-- The 2 signifies that the first checked parameter will be the second one
		-- Makes sure the 2nd parameter is a string, 3rd is a number
		-- The first parameter is not checked

		print(p1, p2, p3)

	end)

	bar(false, "", 1)
	```

### Typer.Check

!!! summary "<span style="color:purple;">boolean</span> Typer.<span style="color:blue;">Check</span>(<span style="color:green;">table</span> PotentialType&comma; <span style="color:teal;">any</span> Parameter [&comma; <<span style="color:green;">string</span>&comma; <span style="color:green;">number</span>> ArgumentName])"
	Checks if an individual Parameter matches a PotentialType in the same way `Typer.AssignSignature` does. Returns `Parameter` if it's a truthy value. If it isn't a truthy value, return true. ArgumentName is just the name or number of the argument being Checked which can be used in the error message.

!!! example
	```lua
	local Debug = Resources:LoadLibrary("Debug")
	local Typer = Resources:LoadLibrary("Typer")

	local function foo(a)
		-- `assert` can be used instead of Debug.Assert
		return Debug.Assert(Typer.Check({"number"}, a, 1))
	end

	foo(2) -- 2
	foo("Noodle") -- [Script] {Foo} bad argument #1: expected number, got string Noodle
	```

### Typer.MapDefinition

!!! summary "<span style="color:purple;">function</span> Typer.<span style="color:blue;">MapDefinition</span>(<span style="color:green;">table</span> Definition)"
	Returns a function which returns the table if it matches the definition, or `false, errorMessage` if it doesn't.

!!! example
	```lua
	local PlayerDefinition = Typer.MapDefinition {
		Name = Typer.String;
		UserId = Typer.PositiveInteger;
	}

	local Player1 = {
		Name = "Validark";
		UserId = 2966752;
	}

	Player1 = assert(PlayerDefinition(Player1))

	-- Can also be used with AssignSignature
	Typer.AssignSignature({Player = PlayerDefinition}, function(...)
		print(...)
	end)(Player1)
	```

### Typer.TYPE

!!! summary "<span style="color:purple;">table</span> Typer.<span style="color:blue;">TypeString</span>"

	Typer will procedurally generate tables which can be cast to valid types. These may be used with `Typer.AssignSignature` or `Typer.Check` to avoid duplicate table definitions. These tables may also be called directly, since their metatable `__call` is set to `Typer.Check`

	```lua
	assert(Typer.String("Yup"))
	assert(Typer.String(1))

	assert(Typer.Number(1))
	assert(Typer.Boolean(true))
	assert(Typer.Function(function() end)
	assert(Typer.Userdata(newproxy(false)))

	local foo = Typer.AssignSignature(Typer.String, function(a)
		print(a)
	end)

	foo("Hello, world!")
	```

#### Built-in Types

|Key|Matches|
|:-:|:-:|
|Nil|type(Object) = "nil"|
|Boolean|type(Object) = "boolean"|
|Number|type(Object) = "number"|
|String|type(Object) = "string"|
|Userdata|type(Object) = "userdata"|
|Function|type(Object) = "function"|
|Thread|type(Object) = "thread"|
|Table|type(Object) = "table"|

Typer accepts anything returned by `typeof`

#### Custom Types

|Key|Matches|
|:-:|:-:|
|Any|Anything|
|Array|A non-empty table with only numeric keys|
|Dictionary|A non-empty table with only non-numeric keys|
|EmptyTable|An empty table|
|NonNil|Any value which isn't nil|
|Integer|Any whole number|
|PositiveInteger|An integer higher than 0|
|NegativeInteger|An integer lower than 0|
|NonPositiveInteger|An integer lower than 0 or 0|
|NonNegativeInteger|An integer higher than 0 or 0|
|PositiveNumber|A number higher than 0|
|NegativeNumber|A number lower than 0|
|NonPositiveNumber|A number lower than 0 or 0|
|NonNegativeNumber|A number higher than 0 or 0|
|Truthy|Any value which isn't false or nil|
|Falsy|False or nil|
|Enum|An EnumType or EnumItem|
|EnumType|A roblox EnumType|
|EnumItem|An EnumItem|
|True|true|
|False|false|

#### Types from parsed strings

Types separated by "Or" will function as expected.

```lua
assert(Typer.NumberOrString(2))
assert(Typer.OptionalBooleanOrNumberOrString(2))
```

#### Prefixes

|Prefix|Matches|
|:-:|:-:|
|Optional|Accepts `nil` as well|
|InstanceOfClass|Returns `Object.ClassName == ClassName`|
|InstanceWhichIsA|Returns `Object:IsA(ClassName)`|
|EnumOfType|Returns the (Roblox) Enum if it can be cast to it via its string, number, or reference|
|EnumerationOfType|Returns `EnumerationType:Cast(Object)`|
|DictionaryOf|Ensures it's a dictionary with values of a given type|
|ArrayOf|Ensures it's an array with values of a given type|
|TableOf|Ensures it's a table with values of a given type|

!!! warning
	You may not nest prefixes, but you may use multiple on the top level using "Or"

!!! example
	```lua
	assert(Typer.ArrayOfStringsOrDictionaryOfNumbers{"a", "b", "c"})

	assert(Typer.ArrayOfStringsOrDictionaryOfNumbers{
		a = 1;
		b = 2;
		c = 3;
	})
	```






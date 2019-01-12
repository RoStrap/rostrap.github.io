# [SortedArray](https://github.com/RoStrap/DataTypes/blob/master/SortedArray.lua)
A class to create sorted arrays. Must contain objects comparable to one another (that can use the `<` and `==` operators). Numbers and strings support these operators by default.
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local SortedArray = Resources:LoadLibrary("SortedArray")

local Array = SortedArray.new()

-- Alternatively
local Sorted = SortedArray.new{2, 1, 5, 3} -- Will get `table.sort`ed
```

## Library API

### SortedArray.new

!!! summary "<span style="color:purple;">table</span> SortedArray.<span style="color:blue;">new</span>(<span style="color:green;">array</span> <span style="color:teal;">InitialSet</span> [, <span style="color:green;">function</span> SortFunction])"
	Instantiates and returns a new SortedArray, with optional parameters.
	- `InitialSet`: Pass in an array of data which will be sorted upon instantiation. If this is omitted, an empty array is used.
	- `SortFunction`: An optional comparison function which is used to customize the element sorting, which will be given two elements `a` and `b` from the array as parameters. The function should return a boolean value specifying whether the first argument should be before the second argument in the sequence. If no comparison function is passed, the Lua-default `a < b` sorting is used.

## SortedArray API

`SortedArray:Concat()` and `SortedArray:Unpack()` are equivalent to `table.concat` and `unpack` respectively.

### SortedArray:Insert

!!! summary "<span style="color:purple;">number</span> SortedArray:<span style="color:blue;">Insert</span>(<span style="color:green;">Variant</span> Element)"

	Inserts an element in the proper place which would preserve the array's orderedness. Returns the index the element was inserted.
	```lua
	local Sorted = SortedArray.new{1, 2, 3, 5}
	print(Sorted:Insert(4)) -- 4
	print("{" .. Sorted:Concat(", ") .. "}")
	-- {1, 2, 3, 4, 5}
	```

### SortedArray:Find

!!! summary "<span style="color:purple;">number</span> SortedArray:<span style="color:blue;">Find</span>(<span style="color:green;">variant</span> Signature [, <span style="color:teal;">function</span> Eq, <span style="color:green;">function</span> Lt])"
	Finds an Element in a SortedArray and returns its position (or nil if non-existant).

	`Signature` is the element to find or something that will be matched by the `Eq` function.

	`Eq` is an optional function which checks for equality between the passed-in element and the other elements in the SortedArray.

	`Lt` is an optional less-than comparison function, which falls back on the comparison passed in from `SortedArray.new`

	Returns the numerical index of the element which was found, else nil.

### SortedArray:Copy

!!! summary "<span style="color:purple;">table</span> SortedArray:<span style="color:blue;">Copy</span>()"
	Returns a raw array with the same values.

### SortedArray:Clone

!!! summary "<span style="color:purple;">table</span> SortedArray:<span style="color:blue;">Clone</span>()"
	Returns a SortedArray clone.

### SortedArray:RemoveIndex

!!! summary "<span style="color:purple;">variant</span> SortedArray:<span style="color:blue;">RemoveIndex</span>(<span style="color:green;">number</span> Index)"
		Removes an element from index, returning that element. The same as `table.remove`.

### SortedArray:RemoveElement

!!! summary "<span style="color:purple;">variant</span> SortedArray:<span style="color:blue;">RemoveElement</span>(<span style="color:green;">variant</span> Signature, <span style="color:teal;">function</span> Eq, <span style="color:green;">function</span> Lt)"

	Searches the array via `SortedArray:Find(Signature, Eq, Lt)`. If found, it removes the value and returns the value, otherwise returns nil. Only removes a single occurence.

	```lua
	local Sorted = SortedArray.new{1, 2, 3, 3, 3, 3, 5}
	Sorted:RemoveElement(1)
	print("{" .. Sorted:Concat(", ") .. "}") -- {2, 3, 3, 3, 3, 5}
	while Sorted:RemoveElement(3) do end
	print("{" .. Sorted:Concat(", ") .. "}") -- {2, 5}
	```

### SortedArray:SortIndex

!!! summary "<span style="color:purple;">number</span> SortedArray:<span style="color:blue;">SortIndex</span>(<span style="color:green;">number</span> Index)"
	Removes the value at Index and re-inserts it. This is useful for when a value may have updated in a way that could change it's position in a SortedArray. Returns Index.

### SortedArray:SortElement

!!! summary "<span style="color:purple;">number</span> SortedArray:<span style="color:blue;">SortElement</span>(<span style="color:green;">variant</span> Signature [, <span style="color:teal;">function</span> Eq, <span style="color:green;">function</span> Lt])"
	Calls `RemoveElement(Signature, Eq, Lt)` and re-inserts the value. This is useful for when a value may have updated in a way that could change it's position in a SortedArray. Returns Index.

### SortedArray:Sort

!!! summary "<span style="color:purple;">void</span> SortedArray:<span style="color:blue;">Sort</span>()"
	Does `table.sort(self, Comparison_From_SortedArray_new)`

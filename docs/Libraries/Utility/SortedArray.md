# SortedArray
A class to create sorted arrays. Must contain objects comparable to one another (that can use the `<` and `==` operators). Numbers and strings support these operators by default.
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local SortedArray = Resources:LoadLibrary("SortedArray")

local Array = SortedArray.new()

-- Alternatively
local Sorted = SortedArray.new{2, 1, 5, 3} -- Will get `table.sort`ed
```

## API
#### SortedArray.new([array InitialSet], [function SortFunction])
Instantiates and returns a new SortedArray, with optional parameters.
- `InitialSet`: Pass in an array of data which will be sorted upon instantiation. If this is omitted, an empty array is used.
- `SortFunction`: An optional comparison function which is used to customize the element sorting, which will be given two elements `a` and `b` from the array as parameters. The function should return a boolean value specifying whether the first argument should be before the second argument in the sequence. If no comparison function is passed, the Lua-default `a < b` sorting is used.

#### SortedArray:Insert()
Inserts an element in the proper place which would preserve the array's orderedness.
```lua
local Sorted = SortedArray.new{1, 2, 3, 5}
Sorted:Insert(4)
print("{" .. Sorted:Concat(", ") .. "}")
-- {1, 2, 3, 4, 5}
```

#### SortedArray:Remove()
If the parameter passed to `Remove` is an array, it will remove all values within the array from the `SortedArray`
```lua
local Sorted = SortedArray.new{1, 2, 3, 5}
Sorted:Remove{1, 2, 3}
print("{" .. Sorted:Concat(", ") .. "}")
-- {5}
```

If the parameter is not of `type(table)` then it will fall back on table.remove

#### SortedArray:Transform(a2 [, f1, f2])
Does the operations necessary to transform SortedArray into the `a2`, a second array. `f1` is an optional callback which fires for each addition operation necessary and `f2` for each removal. `f1` and `f2` will be called with `(number IndexWhereOperationTakesPlace, ValueWhichIsBeingRemovedOrAdded)`
```lua
local Array = SortedArray.new{"Chromenium", "GigsD4X", "Validark"}

local function f1(i, v)
	print("f1(" .. i .. ", " .. v .. ")")
end

local function f2(i, v)
	print("f2(" .. i .. ", " .. v .. ")")
end

Array:Transform(SortedArray.new{"Chromenium", "Evaera", "Validark"}, f1, f2)

-- The first parameter MUST be sorted, but it doesn't need to have the `SortedArray` metatable
-- This also works:
-- Array:Transform({"Chromenium", "Evaera", "Validark"}, f1, f2)

--[[
Output:
	f1(2, Evaera)
	f2(3, GigsD4X)

f1 indicates that "Evaera" must be inserted at index 2: table.insert(Array, 2, "Evaera")
f2 indicates that the 3rd element of Array ("GigsD4X") must be removed (AFTER the previous operation shifted the array forward): table.remove(Array, 3)
--]]
```
#### SortedArray:Copy()
Shallow copy. Pretty straightforward.

### Other SortedArray methods
You can directly index functions from its index table, like `Concat`, `Next`, and `ForEach`. [View the full list in the source.](https://github.com/RoStrap/Utility/blob/master/SortedArray.lua#L9)

Simply for convenience. It's also faster to do an `__index` lookup than a global lookup, so there's that too.

```lua
SortedArray.new{"Chromenium", "GigsD4X", "Validark"}:ForEach(print)

--[[
	1 Chromenium
	2 GigsD4X
	3 Validark
--]]
```

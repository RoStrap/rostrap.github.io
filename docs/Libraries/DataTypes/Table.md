# [Table](https://github.com/RoStrap/DataTypes/blob/master/Table.lua)

A few utility functions which operate on Tables. Purposefully light.

## Library API
### Table.Move

!!! summary "<span style="color:purple;">a2</span> Table.<span style="color:blue;">Move</span>(<span style="color:green;">array</span> a1, <span style="color:teal;">number</span> f, <span style="color:green;">number</span> e, <span style="color:green;">number</span> t, <span style="color:green;">array</span> a2)"
	Moves elements [f, e] from array a1 into a2 starting at index t. Equivalent to Lua 5.3's `table.move`.

	```
	-- @param table a1 from which to draw elements from range
	-- @param number f starting index for range
	-- @param number e ending index for range
	-- @param number t starting index to move elements from a1 within [f, e]
	-- @param table a2 the second table to move these elements to
	--	@default a2 = a1
	-- @returns a2
	```

!!! example
	```lua
	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
	local Table = Resources:LoadLibrary("Table")
	local Debug = Resources:LoadLibrary("Debug")

	print(Debug.TableToString(Table.Move({1, 2, 3}, 1, 3, 2)))
	-- {1, 1, 2, 3}

	-- Explanation:
	-- Inserts {1, 2, 3} @ 2
	```

### Table.Lock

!!! summary "<span style="color:purple;">userdata</span> Table.<span style="color:blue;">Lock</span>(<span style="color:green;">table</span> Table [, <span style="color:teal;">function</span> __<span style="color:green;">call</span>])"
	Returns a userdata with read-only access to a table. `__call` is the function which may be set as its metamethod of the same name.

	```lua
	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
	local Table = Resources:LoadLibrary("Table")
	local Debug = Resources:LoadLibrary("Debug")

	local t = Table.Lock {
		x = 5
	}

	print(t.x) -- 5
	print(t.y) -- error!
	t.x = 2 -- error!
	t.y = 3 -- error!

	local bar = Table.Lock({
		x = 2;
		y = 3;
	}, Debug.TableToString)

	print(bar()) -- {x = 2, y = 3}
	```

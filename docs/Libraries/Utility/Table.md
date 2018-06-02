## Table
### API
#### Table.Move
```lua
function Table.Move(a1, f, e, t, a2)
	-- Moves elements [f, e] from array a1 into a2 starting at index t
	-- Equivalent to Lua 5.3's table.move
	-- @param table a1 from which to draw elements from range
	-- @param number f starting index for range
	-- @param number e ending index for range
	-- @param number t starting index to move elements from a1 within [f, e]
	-- @param table a2 the second table to move these elements to
	--	@default a2 = a1
	-- @returns a2
```
```lua
-- Example Code
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Table = Resources:LoadLibrary("Table")
local Debug = Resources:LoadLibrary("Debug")

print(Debug.TableToString(Table.Move({1, 2, 3}, 1, 3, 2)))
-- {1, 1, 2, 3}

-- Explanation:
-- Inserts {1, 2, 3} @ 2
```
#### Table.Lock
Returns a userdata with read-only access to a table.

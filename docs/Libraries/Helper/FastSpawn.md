# FastSpawn
Expensive method of running a function on a new thread without yielding a frame (like `spawn`) and works within Roblox's thread scheduler. If passed arguments, they will be passed by reference.

```lua
local t = {}
print(t)

FastSpawn(function(...)
	wait(5)
	print(...)
end, t)
```

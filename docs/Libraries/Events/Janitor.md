# Janitor
Light-weight, flexible object for cleaning up connections, instances, or anything. This implementation covers all use cases, as it doesn't force you to rely on naive typechecking to guess how an instance should be cleaned up. Instead, the developer may specify any behavior for any object.

```lua
local Janitor = Resources:LoadLibrary("Janitor")
```

## Library API

### Janitor.new

!!! summary "<span style="color:purple;">Janitor</span> Janitor.<span style="color:blue;">new</span>()"
	Instantiates a new Janitor object

## Janitor API

### Janitor:Add

!!! summary "<span style="color:purple;">void</span> Janitor:<span style="color:blue;">Add</span>(<span style="color:green;">any</span> Object, <<span style="color:teal;">string</span>, <span style="color:green;">true</span>> MethodName = "Destroy" [, <span style="color:green;">string</span> Index])"
	Adds an `Object` to Janitor for later cleanup, where `MethodName` is the key of the method within `Object` which should be called at cleanup time. If the `MethodName` is `true` the `Object` itself will be called instead. If passed an index it will occupy a namespace which can be Remove()d or overwritten.

!!! example
	```lua
	local Obliterator = Janitor.new()

	-- Queue the Part to be Destroyed at Cleanup time
	Obliterator:Add(workspace.Part, "Destroy")

	-- Queue function to be called with `true` MethodName
	Obliterator:Add(print, true)

	-- This implementation allows you to specify behavior for any object
	Obliterator:Add(Tween.new(0.5, 0, print), "Stop")

	-- By passing an Index, the Object will occupy a namespace
	-- If "CurrentTween" already exists, it will call :Remove("CurrentTween") before writing
	Obliterator:Add(Tween.new(0.5, 0, print), "Stop", "CurrentTween")
	```

!!! note
	Objects not given an explicit `MethodName` will be passed into the `typeof` function for a very naive typecheck. RBXConnections will be assigned to "Disconnect", functions will be assigned to `true`, and everything else will default to "Destroy". Not recommended, but hey, you do you.

### Janitor:Remove

!!! summary "<span style="color:purple;">void</span> Janitor:<span style="color:blue;">Remove</span>(<span style="color:green;">string</span> Index)"
	Cleans up whatever Object was set to this namespace by the 3rd parameter of [:Add()](https://rostrap.github.io/Libraries/Events/Janitor/#janitoradd)

!!! example
	```lua
	Obliterator:Remove("CurrentTween")
	```

### Janitor:Cleanup

!!! summary "<span style="color:purple;">void</span> Janitor:<span style="color:blue;">Cleanup</span>()"
	Calls each Object's `MethodName` (or calls the Object if `MethodName == true`) and removes them from the Janitor. Also clears the namespace. This function is also called when you call a Janitor Object (so it can be used as a destructor callback).

!!! example
	```lua
	Obliterator:Cleanup()
	Obliterator()
	```

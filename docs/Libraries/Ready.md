# Ready
A Library for yielding until an object's descendants have finished replicating. This is still imperfect, but it seems to be the best option if you want this kind of functionality.

# Usage

Example code:

```lua
local Ready = require(script.Ready)

Ready:Wait(workspace, 10)

Ready:Connect(workspace, function(LastToLoad)
  print("Workspace has been fully loaded - the last instance to load was", LastToLoad)
end)
```

There is a single config variable in the module called `TIMEOUT`. This is the default number of seconds the script will wait where no descendants have been added to deem the object loaded.

The timeout value that gets used is essentially the minimum amount of time possible for an object to be fully loaded. This means that if the timeout is set to 1 (second), it will always take at least 1 second for an object to load.

# API
### *void* Ready:Wait(*instance* Object [, *number* Timeout])

Repeatedly calls `wait()` until the timeout has been reached and no descendants of the `Object` were added in that time.

### *RBXScriptConnection* Ready:Connect(*instance* Object, *function* Callback [, *number* Timeout])

Completes the timeout after every time a descendant of `Object` was added, then calls `Callback` if no other descendants had been added in the wait time. Returns a `RBXScriptConnection` which can be disconnected at any time, and is disconnected after the object has loaded.

The `Callback` function may take one argument; this being the last descendant that was added. Will be `nil` if no descendants were added.

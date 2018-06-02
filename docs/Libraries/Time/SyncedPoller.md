# SyncedPoller
Polling synced to `os.time()`

```lua
local Resources = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources"))
local SyncedPoller = Resources:LoadLibrary("SyncedPoller")

-- SyncedPoller.new(number Interval, function Func)
SyncedPoller.new(10, print)
```

Calls a function every `Interval` seconds, whenever `(os.time() % Iterval == 0)`. Functions are called with the current `os.time()` (with `tick()` precision).

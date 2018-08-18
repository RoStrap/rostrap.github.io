# RadioGroup

Registers a Material Design RadioGroup PseudoInstance which can be instantiated via `PseudoInstance.new("RadioGroup")`. It acts as an interface for a set of Radio elements.

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local PsuedoInstance = Resources:LoadLibrary("PsuedoInstance")
local Radio = PseudoInstance.new("Radio")
```

## RadioGroup API

### RadioGroup:Add

!!! summary "<span style="color:purple;">void</span>&nbsp;RadioGroup&colon;<span style="color:blue;">Add</span>&lpar;<span style="color:green;">RadioButton</span>&nbsp;Item&comma;&nbsp;<span style="color:teal;">variant</span>&nbsp;Option&rpar;"
	Adds an Item to the group. The `Selection` returned by `GetSelection` will become the `Option` when `Item` is selected.

### RadioGroup:GetSelection

!!! summary "<span style="color:purple;">Option</span>&nbsp;RadioGroup&colon;<span style="color:blue;">GetSelection</span>&lpar;&rpar;"
	Returns the current Selected `Option`.

### Events
|Event|Description|
|:-:|:-:|
|SelectionChanged|Fires after Selection changes with the new selected Option|

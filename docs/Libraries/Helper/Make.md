# [Make](https://github.com/RoStrap/Helper/blob/master/Make.lua)
Shorthand for instance declarations.

You probably shouldn't use this function, but if you really really like it, here it is.
```lua
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Make = Resources:LoadLibrary("Make")

Make("TextLabel"){
    TextSize = 11;
    Font = "Arial";
    Name = "Yup";
    Parent = workspace;
}
```
You can also create multiple instances at once. When you pass subsequent tables as parameters, the object created by the first table is Cloned and modified by the properties in its table. Each subsequent table generates a new instance.

```lua
Make("TextLabel")({
    TextSize = 11;
    Font = "Arial";
    Name = "Yup";
    Parent = workspace;
}, {
    Name = "So!";
    Font = "SourceSans";
}, {
    Name = "Yellow!";
})
```

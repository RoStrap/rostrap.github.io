# RadioGroup

Registers a Material Design RadioGroup PseudoInstance which can be instantiated via `PseudoInstance.new("RadioGroup")`. It acts as an interface for a set of Radio elements.

<div align="center">
	<video autoplay loop>
	<source src="../../../assets/videos/RadioButtons.mp4" type="video/mp4">
	</source>
	</video>
</div>

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local PsuedoInstance = Resources:LoadLibrary("PseudoInstance")
local RadioGroup = PseudoInstance.new("RadioGroup")
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

### Example
```lua
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local Color = Resources:LoadLibrary("Color")
local PseudoInstance = Resources:LoadLibrary("PseudoInstance")

local LocalPlayer repeat LocalPlayer = Players.LocalPlayer until LocalPlayer or not wait()
local PlayerGui repeat PlayerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui") until PlayerGui or not wait()

local Screen = Instance.new("ScreenGui", PlayerGui)
local Frame = Instance.new("Frame", Screen)
Frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Frame.BorderSizePixel = 0
Frame.Size = UDim2.new(1, 0, 1, 0)

local Template = PseudoInstance.new("Radio")
Template.AnchorPoint = Vector2.new(0.5, 0.5)
Template.Theme = "Dark"

local RadioGroup = PseudoInstance.new("RadioGroup")

local Choice1 = Template:Clone()
Choice1.PrimaryColor3 = Color.Red[500]
Choice1.Position = UDim2.new(0.5, 0, 0.5, -32)
Choice1.Parent = Frame

local Choice2 = Template:Clone()
Choice2.PrimaryColor3 = Color.Yellow[500]
Choice2.Position = UDim2.new(0.5, 0, 0.5, 0)
Choice2.Parent = Frame

local Choice3 = Template:Clone()
Choice3.PrimaryColor3 = Color.Green[500]
Choice3.Position = UDim2.new(0.5, 0, 0.5, 32)
Choice3.Parent = Frame

RadioGroup:Add(Choice1, "Apples")
RadioGroup:Add(Choice2, "Bananas")
RadioGroup:Add(Choice3, "Carrots")

RadioGroup.SelectionChanged:Connect(print)
```

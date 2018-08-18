# Radio

Registers a Material Design Radio PseudoInstance which can be instantiated via `PseudoInstance.new("Radio")`

```lua
local Resources = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources"))
local PsuedoInstance = Resources:LoadLibrary("PsuedoInstance")
local Radio = PseudoInstance.new("Radio")
```

## Radio API

Radio inherits from PseudoInstance and SelectionController, so all properties, methods, and events of these can also be used on Checkboxes.

### Radio:SetChecked

!!! summary "<span style="color:purple;">void</span> Radio:<span style="color:blue;">SetChecked</span>(<span style="color:green;">boolean</span> Checked = <span style="color:teal;">not</span> <span style="color:green;">self</span>.Checked)"
	Sets the `Checked` property and animates to the new state. Fires `OnChecked`

### Fields

#### Wrapped Properties
Properties which access its top-level ImageButton:

|Property|Type|
|:-:|:-:|
|AnchorPoint|Vector2|
|Name|string|
|Parent|Instance|
|Position|UDim2|
|LayoutOrder|int|
|NextSelectionDown|Instance|
|NextSelectionLeft|Instance|
|NextSelectionRight|Instance|
|NextSelectionUp|Instance|
|ZIndex|int|

#### SelectionController Properties
|Property|Type|Description|
|:-:|:-:|:-:|
|Checked|Boolean|Whether the Radio is Checked|
|Disabled|Boolean|Whether the Radio is Disabled|
|PrimaryColor3|Color3|The Color3 of the Radio when Checked|
|Theme|Enumeration.MaterialTheme|"Dark" or "Light" colored frame when not Checked|

#### Events

|Event|Description|
|:-:|:-:|
|OnChecked|Fires after the `Checked` property was changed|

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

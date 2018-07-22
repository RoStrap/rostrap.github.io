## Button
Material Design Buttons!

### API
Instantiate a new button with `userdata Button.new(string BUTTON_TYPE, RbxObject Parent)`. It returns a userdata that serves as a wrapper for the [TextButton](http://wiki.roblox.com/index.php?title=API:Class/TextButton) Object. Simply declare it and use it like you normally would!

Example:
```lua
local Resources = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources"))
local Button = Resources:LoadLibrary("Button")

local Players = game:GetService("Players")
local LocalPlayer repeat LocalPlayer = Players.LocalPlayer until LocalPlayer or not wait()
local PlayerGui repeat PlayerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui") until PlayerGui or not wait()

local Screen = Instance.new("ScreenGui", PlayerGui)
local Frame = Instance.new("Frame", Screen)
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.BorderSizePixel = 0
Frame.Size = UDim2.new(1, 0, 1, 0)

local Submit = Button.new("Flat", Frame) -- Use "Custom" to remove the rounded corners
Submit.TextSize = 18
Submit.TextColor3 = Color3.fromRGB(255, 255, 255)
Submit.Size = UDim2.new(0, 82, 0, 36)
Submit.Position = UDim2.new(0, 10, 0, 100)
Submit.Font = Enum.Font.SourceSansBold
Submit.Text = "SUBMIT"

Submit.MouseButton1Click:Connect(function()
	print("MouseButton1Click")
end)

wait(1)

Submit:Ripple()

wait(1)

Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Submit.TextColor3 = Color3.fromRGB(0, 0, 0)

wait(1)

Submit:Destroy()
```
There is also a `Ripple` method which just plays a Ripple.
```lua
Submit:Ripple() -- Ripples :D
```

### Button Types
The three button types are "Flat", "Custom", and "Raised". The "Raised" type isn't perfect, as it is difficult to faithfully render in Roblox.

#### Flat
A `FlatButton` has one descendant by default, called `Corner`. This is the [ImageLabel](http://wiki.roblox.com/index.php?title=API:Class/ImageLabel) that overlays a 2dp corner image over your `FlatButton`. It's [ImageColor3](http://wiki.roblox.com/index.php?title=API:Class/GuiObject/ImageColor3) property is automatically set to `FlatButton.Parent.BackgroundColor3`. Whenever you set the `Parent` property, it will attempt to update to the aforementioned value. You can set it manually with the following:
```lua
FlatButton.Corner.ImageColor3 = Color3.fromRGB(255, 255, 255)
```

#### Custom
A `CustomButton` is exactly the same as a `FlatButton`, except its `Corner` object has its [ImageTransparency](http://wiki.roblox.com/index.php?title=API:Class/GuiObject/ImageTransparency) set to 0. Use this if you don't want visible corner overlays.

#### Raised
For when you want your buttons to lift.

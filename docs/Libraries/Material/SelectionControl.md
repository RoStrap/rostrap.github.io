## SelectionControl
Material design selection controls based on [Material.io specifications](https://material.io/guidelines/components/selection-controls.html#). Will include Checkbox, Radio, and Switch elements. Currently, only Checkbox is available.

#### Checkbox
Checkboxes can be instantiated like so:
```lua
local Resources = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources"))
local SelectionControl = Resources:LoadLibrary("SelectionControl")

local Checkbox = SelectionControl.new("Checkbox")
```
This returns a custom userdata which can be interfaced with like a `TextButton`. It also has some added functionality:
```lua
-- Properties
Checkbox.State
--	On is true, Off is false
Checkbox.EnabledColor
--	Should be a name of a Color from the `Colors` module
Checkbox.EnabledColor3
--	The true Color3 value of the EnabledColor

-- Methods
Checkbox:ChangeState()
--	Unlike simply setting the `State` property directly, this will animate and fire the StateChanged event

-- Events
Checkbox.StateChanged
--	Fires after a player clicked to change the state or `:ChangeState()` was called
```

Example:
```lua
local THEME_NAME = "Light"

local Resources = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources"))
local Colors = Resources:LoadLibrary("Colors")
local SelectionControl = Resources:LoadLibrary("SelectionControl")

local Players = game:GetService("Players")
local LocalPlayer repeat LocalPlayer = Players.LocalPlayer until LocalPlayer or not wait()
local PlayerGui repeat PlayerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui") until PlayerGui or not wait()

local Screen = Instance.new("ScreenGui", PlayerGui)
local Frame = Instance.new("Frame", Screen) -- Color3.fromRGB(51, 51, 51)
Frame.BackgroundColor3 = THEME_NAME == "Dark" and Color3.fromRGB(51, 51, 51) or THEME_NAME == "Light" and Colors.Grey[200] or error("Invalid THEME_NAME")
Frame.BorderSizePixel = 0
Frame.Size = UDim2.new(1, 0, 1, 0)

local DisallowedColors = {
	White = true;
	Black = true;
	Grey = true;
	Brown = true;
	BlueGrey = true;
	Yellow = true;
	Amber = true;
	Lime = true;
}

local function NextColor(CurrentColor)
	repeat CurrentColor = next(Colors, CurrentColor)
	until CurrentColor and not DisallowedColors[CurrentColor]
	return CurrentColor
end

local CurrentColor = NextColor()

local ReceiveUpdates = SelectionControl.new("Checkbox")
ReceiveUpdates.EnabledColor = CurrentColor
ReceiveUpdates.State = false
ReceiveUpdates.StateChanged:Connect(function(On)
	if not On then
		CurrentColor = NextColor(CurrentColor)
		print(CurrentColor)
		ReceiveUpdates.EnabledColor = CurrentColor
	end
end)
ReceiveUpdates.AnchorPoint = Vector2.new(0.5, 0.5)
ReceiveUpdates.Position = UDim2.new(0.5, 0, 0.5, 0)
ReceiveUpdates.Theme = THEME_NAME
ReceiveUpdates.Parent = Frame
```

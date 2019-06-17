# [RippleButton](https://github.com/RoStrap/RoStrapUI/blob/master/RippleButton.lua)

Registers a Material Design RippleButton PseudoInstance which can be instantiated via `PseudoInstance.new("RippleButton")`

<div align="center">
	<video autoplay loop>
	<source src="../../../assets/videos/RippleButton.mp4" type="video/mp4">
	</source>
	</video>
</div>


!!! warning ""
	Only Global ZIndexBehavior is officially supported.

## RippleButton API

RippleButtons work very similarly to regular TextButtons or ImageButtons. Just set the fields to whatever you want.

### Fields

#### Wrapped Properties
Properties which access its top-level ImageButton:

|Property|Type|
|:-:|:-:|
|AnchorPoint|Vector2|
|Active|boolean|
|Name|string|
|Parent|Instance|
|Size|UDim2|
|Position|UDim2|
|LayoutOrder|int|
|NextSelectionDown|Instance|
|NextSelectionLeft|Instance|
|NextSelectionRight|Instance|
|NextSelectionUp|Instance|
|Visible|boolean|
|ZIndex|int|

Properties which access its TextLabel:

|Property|Type|
|:-:|:-:|
|Font|Enum.Font|
|Text|string|
|TextSize|number|
|TextTransparency|string|
|TextXAlignment|Enum.TextXAlignment|
|TextYAlignment|Enum.TextYAlignment|

Properties which access its Shadow:

|Property|Type|
|:-:|:-:|
|Elevation|Enumeration.Elevation|

#### RippleButton Properties
|Property|Type|Description|
|:-:|:-:|:-:|
|Disabled|Boolean|Whether the RippleButton is Disabled|
|Tooltip|string|The tip to display upon hover, with "" being the disabled value|
|BorderRadius|Enumeration.BorderRadius|How rounded the corners should be (0, 2, 4, or 8)|
|Style|Enumeration.ButtonStyle|"Flat", "Outlined", or "Contained" style|
|PrimaryColor3|Color3|The color of the text in Flat and Outlined styles or the color of the background in a Contained style when not Disabled|
|SecondaryColor3|Color3|The color of the text in Raised style, by popular request, despite my insistance to conform to Material Design. Not the original intention.|

#### Events

|Event|Description|
|:-:|:-:|
|OnPressed|Fires after the Button was tapped or left-clicked|
|OnRightPressed|Fires after the Button was right-clicked|
|OnMiddlePressed|Fires after the Button was middle-clicked|

###### RippleButton inherits from [PseudoInstance](https://rostrap.github.io/Libraries/Classes/PseudoInstance/#pseudoinstance-api)

## Example

[Click here for the example place](./../../assets/demos/RippleButton.rbxl)

Demo code:

!!! example
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
	Frame.BackgroundColor3 = Color.Grey[200]
	Frame.BorderSizePixel = 0
	Frame.Size = UDim2.new(1, 0, 1, 0)

	local Flat = PseudoInstance.new("RippleButton")
	Flat.AnchorPoint = Vector2.new(0.5, 0.5)
	Flat.Size = UDim2.new(0, 83, 0, 36)
	Flat.Position = UDim2.new(0.5, 0, 0.5, -36 - 16)
	Flat.PrimaryColor3 = Color.Teal[500]
	Flat.BorderRadius = 4
	Flat.Style = "Flat"
	Flat.Text = "SUBMIT"
	Flat.Parent = Frame

	local Outlined = Flat:Clone()
	Outlined.Style = "Outlined"
	Outlined.Position = UDim2.new(0.5, 0, 0.5, 0)
	Outlined.Parent = Frame

	local Contained = Flat:Clone()
	Contained.Style = "Contained"
	Contained.Position = UDim2.new(0.5, 0, 0.5, 36 + 16)
	Contained.Parent = Frame

	Flat.OnPressed:Connect(function()
		print("Pressed Flat")
	end)

	Outlined.OnPressed:Connect(function()
		print("Pressed Outlined")
	end)

	Contained.OnPressed:Connect(function()
		print("Pressed Contained")
	end)
	```

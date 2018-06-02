# Tween
RoStrap's premier Tween Module built for Roblox. Allows you to write interpolation code faster with a clear and simple API.
## Declaration
First let's load the module:
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local Tween = Resources:LoadLibrary("Tween")
local Enumeration = Resources:LoadLibrary("Enumeration")
```
Once you've loaded the Tween Module, there are two ways to create a Tween. You can either interpolate a property of an object, or create a custom Tween with a function you want called each frame.

## Tween Properties
Tween function for tweening any property.  Like GuiObject:TweenPosition but the first two arguments are Object and Property

```lua
Tween(
	Object object, -- or anything that holds the changing property
	String propertyName,
	Variant endValue,
	Enumeration.EasingFunction easingFunction,
	Number time,
	bool override = false,
	function(TweenStatus) callback = nil
)

-- Recommended standard
local OutQuad = Enumeration.EasingFunction.OutQuad.Value
local Standard = Enumeration.EasingFunction.Standard.Value

Tween(workspace.Part, "CFrame", CFrame.new(10, 10, 10), OutQuad, 2, true)
Tween(workspace.Part, "Transparency", 1, Standard, 2, true)
```
## Lightweight Custom Tween
Tweens created with `Tween.new` will call Callback every tween frame, with EasingFunction interpolating from 0 to 1 over the allotted duration.

```lua
Tween.new(number Duration, string EasingFunctionName, function Callback)

local Deceleration = Enumeration.EasingFunction.Deceleration.Value

local newTween = Tween.new(0.5, Deceleration, function(x)
	print("This will be called with each 'Frame' of this tween")
end)
```

## Tween Objects
These are the functions and properties of the TweenObjects returned with each Tween creation.
```js
	Tween Object

		Methods:
			Tween:Resume()
//				Resumes a Tween that was Stop()ed
			Tween:Stop()
//				Stops a Tween
			Tween:Wait()
//				Yields until Tween finishes interpolating
			Tween:Restart()
//				Makes the Tween go back to timeElapsed = 0

		Properties:
			boolean Tween.Running
//				Whether the Tween is active
```

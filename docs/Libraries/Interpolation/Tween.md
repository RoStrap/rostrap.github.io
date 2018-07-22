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
Once you've loaded the Tween Module, there are two ways to create a Tween. You can either interpolate a property of an object, or create a custom Tween with a function you want called each `Heartbeat` frame.

## Library API

### Tween()

!!! summary "<span style="color:purple;">TweenObject</span> <span style="color:blue;">Tween</span>(Object Object, <span style="color:green;">string</span> PropertyName, Variant EndValue, Enumeration.EasingFunction EasingFunction, <span style="color:teal;">number</span> Time, <span style="color:green;">bool</span> Override = <span style="color:green;">false</span>, <span style="color:green;">function</span>(TweenStatus) Callback = <span style="color:green;">nil</span>, [<span style="color:green;">arg</span> InitialParameter])"
	Tween function for tweening any property. Like `GuiObject:TweenPosition()` but the first two arguments are Object and Property. If InitialParameter isn't `nil`, it will be pushed to the first argument passed to the Callback.
	```lua
	-- Localizing the `.Value` of an EasingFunction is fastest
	local OutQuad = Enumeration.EasingFunction.OutQuad.Value
	local Standard = Enumeration.EasingFunction.Standard.Value

	Tween(workspace.Part, "CFrame", CFrame.new(10, 10, 10), OutQuad, 2, true)
	Tween(workspace.Part, "Transparency", 1, Standard, 2, true)
	```

### Tween.new

!!! summary "<span style="color:purple;">TweenObject</span> Tween.<span style="color:blue;">new</span>(<span style="color:green;">number</span> Duration, <span style="color:teal;">string</span> EasingFunctionName, <span style="color:green;">function</span> Callback, [<span style="color:green;">arg</span> InitialParameter])"
	Tweens created with `Tween.new` will call Callback every tween `Heartbeat` frame, with EasingFunction interpolating from 0 to 1 over the allotted duration. If InitialParameter isn't `nil`, it will be pushed to the first argument passed to the Callback.

	```lua
	Tween.new(number Duration, string EasingFunctionName, function Callback)

	local Deceleration = Enumeration.EasingFunction.Deceleration.Value

	local newTween = Tween.new(0.5, Deceleration, function(x)
		print("This will be called with each 'Frame' of this tween")
	end)
	```

## TweenObject API

### Tween:Resume

!!! summary "<span style="color:purple;">TweenObject</span> Tween:<span style="color:blue;">Resume</span>()"
	Resumes a Tween that was Stop()ed

### Tween:Stop

!!! summary "<span style="color:purple;">TweenObject</span> Tween:<span style="color:blue;">Stop</span>()"
	Stops a Tween

### Tween:Wait

!!! summary "<span style="color:purple;">TweenObject</span> Tween:<span style="color:blue;">Wait</span>()"
	Yields until Tween finishes interpolating

### Tween:Restart

!!! summary "<span style="color:purple;">TweenObject</span> Tween:<span style="color:blue;">Restart</span>()"
	Makes the Tween go back to timeElapsed = 0

### Fields
|Field|Description|Type|Default value|
|:-:|:-:|:-:|:-:|
|Running|Whether the Tween is active|bool|true|

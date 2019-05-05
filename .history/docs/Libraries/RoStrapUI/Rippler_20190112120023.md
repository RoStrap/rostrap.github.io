# [Rippler](https://github.com/RoStrap/RoStrapUI/blob/master/Rippler.lua)

Registers a Material Design Rippler PseudoInstance which can be instantiated via `PseudoInstance.new("Rippler")`

## Rippler API

### Rippler:Down

!!! summary "<span style="color:purple;">Tween</span>&nbsp;Rippler&colon;<span style="color:blue;">Down</span>&lpar;&lsqb;<span style="color:green;">number</span>&nbsp;X&comma;&nbsp;<span style="color:teal;">number</span>&nbsp;Y&rsqb;&rpar;"
	Animates a Circular Ripple at position UDim2.new(0, X, 0, Y) within Container. Defaults to the center. Returns the Tween Object which is Tweening the `Size` of the Ripple.

### Rippler:Up

!!! summary "<span style="color:purple;">void</span>&nbsp;Rippler&colon;<span style="color:blue;">Up</span>&lpar;&rpar;"
	Fades the currently open Ripple out

### Rippler:Ripple

!!! summary "<span style="color:purple;">void</span>&nbsp;Rippler&colon;<span style="color:blue;">Ripple</span>&lpar;&lsqb;<span style="color:green;">number</span>&nbsp;X&comma;&nbsp;<span style="color:teal;">number</span>&nbsp;Y&comma;&nbsp;<span style="color:green;">number</span>&nbsp;Duration&nbsp;&equals;&nbsp;<span style="color:purple;">0.15</span>&rsqb;&rpar;"

	Calls `Rippler:Down(X, Y)` and calls `Rippler:Up()` after `Duration`

### Fields

|Property|Type|Description|
|:-:|:-:|:-:|
|Style|Enumeration.RipplerStyle|Full, Icon, or Round|
|BorderRadius|Enumeration.BorderRadius|How rounded the corners should be (0, 2, 4, or 8)|
|RippleFadeDuration|number|How long it takes for a Ripple to Fade|
|MaxRippleDiameter|number|A cap at how large the Ripples can get (defaults to math.huge)|
|RippleExpandDuration|number|How long it takes a Ripple to expand to full size|
|RippleColor3|Color3|The Color of the Ripples|
|RippleTransparency|number|The Transparency of the Ripples|
|Container|GuiObject|The parent to which Ripples are Parented|

When the `Style` is set to `Enumeration.RipplerStyle.Icon`, it will constrain the diameter of the Ripples to twice the height of the Container.

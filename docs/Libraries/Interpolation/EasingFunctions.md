# [EasingFunctions](https://github.com/RoStrap/Interpolation/blob/master/EasingFunctions.lua)

A bunch of reuseable Easing Functions, including those from the Material Design specification ([Standard, Acceleration, and Deceleration](https://material.io/design/motion/speed.html#easing))

These are the available EasingFunctions:

|   Directionless  |     In    |     Out    |     InOut    |     OutIn    |
|:----------------:|:---------:|:----------:|:------------:|:------------:|
|      Linear      |   InQuad  |   OutQuad  |   InOutQuad  |   OutInQuad  |
|      Spring      |  InCubic  |  OutCubic  |  InOutCubic  |  OutInCubic  |
|    SoftSpring    |  InQuart  |  OutQuart  |  InOutQuart  |  OutInQuart  |
|      RevBack     |  InQuint  |  OutQuint  |  InOutQuint  |  OutInQuint  |
| RidiculousWiggle |   InSine  |   OutSine  |   InOutSine  |   OutInSine  |
|      Smooth      |   InExpo  |   OutExpo  |   InOutExpo  |   OutInExpo  |
|     Smoother     |   InCirc  |   OutCirc  |   InOutCirc  |   OutInCirc  |
|   Acceleration   | InElastic | OutElastic | InOutElastic | OutInElastic |
|   Deceleration   |   InBack  |   OutBack  |   InOutBack  |   OutInBack  |
|       Sharp      |  InBounce |  OutBounce |  InOutBounce |  OutInBounce |
|     Standard     |


This library returns an array of these functions, with values corresponding to their Enumerations' values.

```lua
local Enumeration = Resources:LoadLibrary("Enumeration")
local EasingFunctions = Resources:LoadLibrary("EasingFunctions")

local InSine = EasingFunctions[Enumeration.EasingFunction.InSine.Value]

-- If you want an array of all EasingFunction Enumerations
local EnumerationItems = Enumeration.EasingFunction:GetEnumerationItems()

for i = 1, #EnumerationItems do
	local EnumerationItem = EnumerationItems[i]
	print(EnumerationItem, EasingFunctions[EnumerationItem.Value])
end
```

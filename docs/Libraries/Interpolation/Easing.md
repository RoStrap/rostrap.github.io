## Easing Functions
These are the available EasingFunctions:
You need to specify the directon of EasingFunctions that aren't "Directionless":

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

If you want to, you can access the EasingFunctions for use with other modules through either of the following:

```lua
local Easing = Resources:LoadLibrary("Easing")

-- If you want an array of all Easing Enumerations
local EnumerationItems = Enumeration.EasingFunction:GetEnumerationItems()
for i = 1, #EnumerationItems do
	print(EnumerationItems[i])
end
```

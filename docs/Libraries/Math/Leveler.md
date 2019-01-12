# [Leveler](https://github.com/RoStrap/Math/blob/master/Leveler.lua)
Level and Experience class.

## Library API

### Leveler.new

!!! summary "<span style="color:purple;">LevelerObject</span>&nbsp;Leveler&period;<span style="color:blue;">new</span>&lpar;<span style="color:green;">number</span>&nbsp;<span style="color:teal;">PointsToStartWith</span>&nbsp;&equals;&nbsp;0&rpar;"
	Returns a Leveler Object.

## Leveler API

### Leveler:Award

!!! summary "<span style="color:orange;">self</span>&nbsp;Leveler&colon;<span style="color:blue;">Award</span>&lpar;<span style="color:green;">number</span>&nbsp;<span style="color:teal;">Points</span>&nbsp;&equals;&nbsp;1&rpar;"
	Awards Points to Leveler, recalculating its Fields.

Fields:

|Field|Description|Type|
|:-:|:-:|:-:|
|Total|Total Exp|number|
|Lvl|Current level|number|
|Exp|Current Exp within level|number|
|Next|Total Exp required to advance from this level to the next level|number|
|Percent|Decimal progress to next level|number|


Run this little demo and you will learn everything you need to know.
```lua
local require = require(game:GetService("ReplicatedStorage"):WaitForChild("Resources")).LoadLibrary
local Leveler = require("Leveler")

local Kills = Leveler.new()
table.foreach(Kills, print)
print()

Kills:Award()
table.foreach(Kills, print)
print()

Kills:Award(6)
table.foreach(Kills, print)
```

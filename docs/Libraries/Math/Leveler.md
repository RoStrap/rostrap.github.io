# Leveler
Level and Experience class. WIP documentation:

`table Leveler.new(number PointsToStartWith or 0)`
Creates a `Leveler` object with the following API

`Leveler:Award(Points)`
The amount of points to add to `Total`

Fields:

- `Total`: Total Exp
- `Lvl`: Current level
- `Exp`: Current Exp within level
- `Next`: Total Exp required to advance from this level to the next level
- `Percent`: decimal progress to next level


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

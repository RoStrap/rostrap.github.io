# Enumeration
Pure-lua Enumeration implementation that function identically to Roblox Enums, except one may declare their own:

```lua
local Enumeration = Resources:LoadLibrary("Enumeration")

Enumeration.ButtonType = {"Custom", "Flat", "Raised"}
Enumeration.SelectionControllerType = {"Checkbox", "Radio", "Switch"}

local Radio = Enumeration.SelectionControllerType.Radio

print(Radio)
print(Radio.EnumType)
print(Radio.Name)
print(Radio.Value)
```

```
> Enumeration.SelectionControllerType.Radio
> SelectionControllerType
> Radio
> 1
```

Enumerations have a `Value` equal to their index in the declarative array minus one:

|Enumeration.ButtonType = {|"Custom"|"Flat"|"Raised"|}|
|:-:|:----:|:--:|:----:|:--:|
||0|1|2||

In this implementation, we use `Enumeration` in the places where Roblox uses `Enum`:

```lua
print("All Roblox Enums:")
for i, EnumType in ipairs(Enum:GetEnums()) do
	print(i, EnumType)
	for j, EnumName in ipairs(EnumType:GetEnumItems()) do
		print("   ", j, EnumName)
	end
end

print("All RoStrap Enumerations:")
for i, EnumType in ipairs(Enumeration:GetEnumerations()) do
	print(i, EnumType)
	for j, EnumName in ipairs(EnumType:GetEnumerationItems()) do
		print("   ", j, EnumName)
	end
end
```

[Further documentation on Enumerations here.](http://wiki.roblox.com/index.php?title=Enumeration)

# Color
Color utilities with [Material Design's 2014 Color Palette](https://material.io/design/color/#tools-for-picking-colors)

## Library API

### Color.toRGBString

!!! summary "<span style="color:purple;">string</span>&nbsp;Color&period;<span style="color:blue;">toRGBString</span>&lpar;<span style="color:green;">Color3</span>&nbsp;Color&nbsp;&lsqb;&comma;&nbsp;<span style="color:teal;">number</span>&nbsp;Alpha&rsqb;&rpar;"
	Returns a string representation of the rgb or rgba value for a given Color.

### Color.toHexString

!!! summary "<span style="color:purple;">string</span>&nbsp;Color&period;<span style="color:blue;">toHexString</span>&lpar;<span style="color:green;">Color3</span>&nbsp;Color&nbsp;&lsqb;&comma;&nbsp;<span style="color:teal;">number</span>&nbsp;Alpha&rsqb;&rpar;"
	Returns a string representation of the hexidecimal Color code for a given Color.

### Color.fromHex

!!! summary "<span style="color:purple;">Color3</span>&nbsp;Color&period;<span style="color:blue;">fromHex</span>&lpar;&lt;<span style="color:green;">number</span>&comma;&nbsp;<span style="color:teal;">string</span>&gt;&nbsp;Hex&rpar;"
	Converts a 3-digit or 6-digit hex color to a Color3. Takes in a string of the form: "#FFFFFF" or "#FFF" or a 6-digit hexadecimal number (e.g. 0xFFFFFF)

### Color.toHex

!!! summary "<span style="color:purple;">number</span>&nbsp;Color&period;<span style="color:blue;">toHex</span>&lpar;<span style="color:green;">Color3</span>&nbsp;Color&rpar;"
	Returns the Color in its hexidecimal-number form.

### Color.COLOR
The `Color` table contains all the colors from the [2014 Material Design Color Pallete](https://material.io/design/color/#tools-for-picking-colors). These Colors are structured like so:
```lua
Cyan = {
	[50] = rgb(224, 247, 250);
	[100] = rgb(178, 235, 242);
	[200] = rgb(128, 222, 234);
	[300] = rgb(77, 208, 225);
	[400] = rgb(38, 198, 218);
	[500] = rgb(0, 188, 212);
	[600] = rgb(0, 172, 193);
	[700] = rgb(0, 151, 167);
	[800] = rgb(0, 131, 143);
	[900] = rgb(0, 96, 100);

	Accent = {
		[100] = rgb(132, 255, 255);
		[200] = rgb(24, 255, 255);
		[400] = rgb(0, 229, 255);
		[700] = rgb(0, 184, 212);
	};
};
```

!!! example
	```lua
	local Color = Resources:LoadLibrary("Color")
	local Cyan = Color.Cyan[500]
	local DarkCyan = Color.Cyan[900]
	local CyanAccent = Color.Cyan.Accent[700]
	```

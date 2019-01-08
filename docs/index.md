# RoStrap

RoStrap is the name of a [Roblox plugin](https://www.roblox.com/library/725884332/RoStrap) and resource management system designed to expedite game development on Roblox. Its main goals are to increase code reusability and simplify the networking of resources **without penalty for not using features**. The plugin allows for easy access and installation of incredibly useful libraries.

With the click of a button you can start using an optimized rewrite of the vanilla Lua `os.date` function:

![](https://user-images.githubusercontent.com/15217173/40766278-978e91b2-6474-11e8-8493-3a1f3faff660.png)

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Date = Resources:LoadLibrary("Date")

print(Date("!%c", tick())) --> Thu Jan 31 08:55:48 2020
```

Gain access to a variety of beautiful Material Design elements, like the [Choice Dialog](../Libraries/RoStrapUI/ChoiceDialog):

<div align="center">
	<video muted autoplay loop>
	<source src="assets/videos/ChoiceDialog.mp4" type="video/mp4">
	</source>
	</video>
</div>

Or some very clickable Material Design [RippleButtons](../Libraries/RoStrapUI/RippleButton), [Checkboxes](../Libraries/RoStrapUI/Checkbox), and [Radio buttons](../Libraries/RoStrapUI/Radio):

<div align="center">
	<video muted autoplay loop height=200>
		<source src="assets/videos/RippleButton.mp4" type="video/mp4">
		</source>
	</video>
	<video muted autoplay loop height=200>
		<source src="assets/videos/Checkboxes.mp4" type="video/mp4">
		</source>
	</video>
	<video muted autoplay loop height=200>
		<source src="assets/videos/RadioButtons.mp4" type="video/mp4">
		</source>
	</video>
</div>

RoStrap's central library, [Resources](../Resources), can also be used to manage your RemoteEvents and RemoteFunctions!

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local Chatted = Resources:GetRemoteEvent("Chatted")
local ClientLoaded = Resources:GetRemoteFunction("ClientLoaded")
```
![](https://user-images.githubusercontent.com/15217173/38775951-d6bfbeee-404b-11e8-8396-9666a0b20b98.png)

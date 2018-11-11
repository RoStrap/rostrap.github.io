# RoStrap

RoStrap is the name of a [Roblox plugin](https://www.roblox.com/library/725884332/RoStrap) and resource management system designed to expedite game development on Roblox. Its main goals are to increase code reusability and simplify the networking of resources **without penalty for not using features**. The plugin allows for easy access and installation of incredibly useful libraries.


With the click of a button you can start using an optimized rewrite of the vanilla Lua `os.date` function:

![](https://user-images.githubusercontent.com/15217173/40766278-978e91b2-6474-11e8-8493-3a1f3faff660.png)

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Date = Resources:LoadLibrary("Date")

print(Date("!%c", tick())) -- Thu Jan 31 08:55:48 2020
```

Or use a beautiful Choice Dialog:

<div align="center">
	<video autoplay loop>
	<source src="assets/videos/ChoiceDialog.mp4" type="video/mp4">
	</source>
	</video>
</div>

```lua
-- If this is in a Script, it will Replicate this ChoiceDialog to every
-- Player in the game and everyone who joins
-- If this is in a LocalScript, it will generate it on the client only

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

Resources:LoadLibrary("ReplicatedPseudoInstance")

local Color = Resources:LoadLibrary("Color")
local PseudoInstance = Resources:LoadLibrary("PseudoInstance")

local PrimaryColor3 = Color.Teal[500]

local Dialog = PseudoInstance.new("ChoiceDialog")
Dialog.HeaderText = "Repository Location"
Dialog.Options = {"ServerStorage", "ServerScriptService"}
Dialog.DismissText = "CANCEL"
Dialog.ConfirmText = "INSTALL"
Dialog.PrimaryColor3 = PrimaryColor3

Dialog.OnConfirmed:Connect(function(Player, Choice)
	print(Player, Choice)

	if Choice then
		-- Choice is a string of the option they chose
	else
		-- They chose Dismiss, so Choice is false
	end
end)

Dialog.Parent = ReplicatedStorage
```

Or manage your RemoteEvents and RemoteFunctions!
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local Chatted = Resources:GetRemoteEvent("Chatted")
local ClientLoaded = Resources:GetRemoteFunction("ClientLoaded")
```
![](https://user-images.githubusercontent.com/15217173/38775951-d6bfbeee-404b-11e8-8396-9666a0b20b98.png)

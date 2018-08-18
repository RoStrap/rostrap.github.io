# ChoiceDialog

<div align="center">
	<video autoplay loop>
	<source src="../../../assets/videos/ChoiceDialog.mp4" type="video/mp4">
	</source>
	</video>
</div>

## Demo
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

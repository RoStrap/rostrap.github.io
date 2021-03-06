# [Snackbar](https://github.com/RoStrap/RoStrapUI/blob/master/Snackbar.lua)

A [Snackbar](https://material.io/design/components/snackbars.html#) is a light-weight feedback bar appearing from the bottom of the screen. This implementation has built-in replication.

<div align="center">
	<video autoplay loop>
	<source src="../../../assets/videos/Snackbar.mp4" type="video/mp4">
	</source>
	</video>
</div>

This library registers a Material Design `Snackbar` PseudoInstance which can be instantiated via `PseudoInstance.new("Snackbar")`.

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local PseudoInstance = Resources:LoadLibrary("PseudoInstance")
local Snackbar = PseudoInstance.new("Snackbar")
```

## Snackbar API

Snackbar inherits from [ReplicatedPseudoInstance](../../Classes/ReplicatedPseudoInstance).

Only one can be present on the screen at once.

### Fields
|Property|Type|Description|
|:-:|:-:|:-:|
|Text|string|The main text of the snackbar (required)
|ActionText|string|The text on the button. `""` will remove the button|

### Events

|Event|Description|Signature|
|:-:|:-:|:-:|
|OnAction|Fires after the Action button on the Snackbar was pressed|(Player Player)|

###### Snackbar also inherits from [PseudoInstance](https://rostrap.github.io/Libraries/Classes/PseudoInstance/#pseudoinstance-api)

## Example

[Click here for the example place](./../../assets/demos/Snackbar.rbxl)

Demo code:
```lua
-- This code is valid on the client and server
-- Just make sure that both call `Resources:LoadLibrary("ReplicatedPseudoInstance")`

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local PseudoInstance = Resources:LoadLibrary("PseudoInstance")
local ReplicatedPseudoInstance = Resources:LoadLibrary("ReplicatedPseudoInstance")

local Color = Resources:LoadLibrary("Color")

local Snackbar = PseudoInstance.new("Snackbar")
Snackbar.ActionText = "CANCEL"
Snackbar.OnAction:Connect(function()
    print("Canceled!")
end)

-- If this is in a Script, it will Replicate this ChoiceDialog to every
-- Player in the game and everyone who joins
-- If this is in a LocalScript, it will generate it on the client only

local PrimaryColor3 = Color.Teal[500] -- This is just a Color3 value

local Dialog = PseudoInstance.new("ChoiceDialog")
Dialog.HeaderText = "Repository Location"
Dialog.Options = {"ServerStorage", "ServerScriptService"}
Dialog.DismissText = "CANCEL"
Dialog.ConfirmText = "INSTALL"
Dialog.PrimaryColor3 = PrimaryColor3

Dialog.OnConfirmed:Connect(function(Player, Choice)
    print(Player, Choice)
    Snackbar.Text = "Chosen: " .. Choice
    Snackbar.Parent = Player

    if Choice then
        -- Choice is a string of the option they chose
    else
        -- They chose Dismiss, so Choice is false
    end
end)

Dialog.Parent = ReplicatedStorage
```

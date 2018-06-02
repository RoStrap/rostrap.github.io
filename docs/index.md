# RoStrap

RoStrap is the name of the GitHub organization and resource management system designed to expidite game development on Roblox. It's main goals are to increase code reusability and simplify the networking of resources without penalty for not using features. It allows for easy access and installation of incredibly useful libraries.


With the click of a button you can start using an optimized rewrite of the vanilla Lua `os.date` function:

![](https://user-images.githubusercontent.com/15217173/40766278-978e91b2-6474-11e8-8493-3a1f3faff660.png)

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Date = Resources:LoadLibrary("Date")

print(Date("!%c", tick())) -- Thu Jan 31 08:55:48 2020
```

Or a beautiful checkbox:

![](https://user-images.githubusercontent.com/15217173/40769612-128acd1e-647e-11e8-8d64-5c570a6566b2.png)
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
local Colors = Resources:LoadLibrary("Colors")
local SelectionControl = Resources:LoadLibrary("SelectionControl")

local LocalPlayer = game:GetService("Players").LocalPlayer
local PlayerGui = LocalPlayer:FindFirstChildOfClass("PlayerGui")

local Screen = Instance.new("ScreenGui", PlayerGui)

local Frame = Instance.new("Frame", Screen)
Frame.BackgroundColor3 = Colors.Grey[200]
Frame.BorderSizePixel = 0
Frame.Size = UDim2.new(1, 0, 1, 0)

local ReceiveUpdates = SelectionControl.new("Checkbox")
ReceiveUpdates.EnabledColor = "Teal"
ReceiveUpdates.State = true
ReceiveUpdates.AnchorPoint = Vector2.new(0.5, 0.5)
ReceiveUpdates.Position = UDim2.new(0.5, 0, 0.5, 0)
ReceiveUpdates.Parent = Frame
```

<div align="right" style="width:100%;height:0px;position:relative;padding-bottom:20%;"><iframe src="https://streamable.com/s/pwm6a/adsyqq" frameborder="0" style="width:100%;height:100%;position:absolute;left:0px;top:0px;overflow:hidden;"></iframe></div>

Or manage your RemoteEvents and RemoteFunctions!
```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

local Chatted = Resources:GetRemoteEvent("Chatted")
local ClientLoaded = Resources:GetRemoteEvent("ClientLoaded")
```
![](https://user-images.githubusercontent.com/15217173/38775951-d6bfbeee-404b-11e8-8396-9666a0b20b98.png)

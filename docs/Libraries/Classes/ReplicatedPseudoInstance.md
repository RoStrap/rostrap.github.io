# [ReplicatedPseudoInstance](https://github.com/RoStrap/Classes/blob/master/ReplicatedPseudoInstance.lua)

!!! summary
	A ReplicatedPseudoInstance is an Instance which, when instantiated on the server, has built-in replication. While the parent is set to `Workspace`, `ReplicatedStorage`, or descendants of these, or set to `Players`, it will be Replicated to all players (including those who join the server later). If it is parented to an individual player or a descendant of an individual Player, it will replicate solely to that Player.

	If a property changes on the server, clients will be sent the new property's value and update their local version of the instance with the new property.

	Events which are fired on the client (by replicating instances originating from the server) are automatically fired on the server via a RemoteEvent.

	ReplicatedPseudoInstances which are Destroyed on the server have their destruction replicated.

	Inherits from [PseudoInstance](../PseudoInstance)

!!! warning
	In order for replication to work, the `ReplicatedPseudoInstance` library **must** be loaded on the client.

!!! warning
	All events fired on a client must have `LocalPlayer` as the first parameter. On the server, it will use the automatically-passed PlayerFrom parameter (which is built-in to RemoteEvents)

!!! example
	To make a library inherit from ReplicatedPseudoInstance, simply pass it in as the third parameter to [PseudoInstance:Register](https://rostrap.github.io/Libraries/Classes/PseudoInstance/#pseudoinstanceregister).
	[ChoiceDialog](https://github.com/RoStrap/RoStrapUI/blob/master/ChoiceDialog.lua) is a good example of a ReplicatedPseudoInstance, but here is a re-implementation of the ClickDetector object (but also passes along what face of an Object you clicked.)
	```lua
	-- ClickDetector Class
	-- @author Validark

	local Players = game:GetService("Players")
	local Workspace = game:GetService("Workspace")
	local RunService = game:GetService("RunService")
	local ReplicatedStorage = game:GetService("ReplicatedStorage")

	local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

	local Debug = Resources:LoadLibrary("Debug")
	local Enumeration = Resources:LoadLibrary("Enumeration")
	local SortedArray = Resources:LoadLibrary("SortedArray")
	local PseudoInstance = Resources:LoadLibrary("PseudoInstance")
	local ReplicatedPseudoInstance = Resources:LoadLibrary("ReplicatedPseudoInstance")

	local Parts = setmetatable({}, {__mode = "k"})
	local LocalPlayer

	if RunService:IsClient() then
		repeat LocalPlayer = Players.LocalPlayer until LocalPlayer or not wait()
		local Mouse = Players.LocalPlayer:GetMouse()
		local Targets = {}
		local MouseDowns = {}
		local CurrentMoval = 0
		local MaximumInteger = 2 ^ 53

		local function MouseMoved()
			local Target = Mouse.Target
			local ActiveIcon

			while Target do
				local Detectors = Parts[Target]
				if Detectors then
					for i = 1, #Detectors do
						local Detector = Detectors[i]
						if Detector.MaxActivationDistance >= LocalPlayer:DistanceFromCharacter(Target.Position) then
							if not Targets[Detector] then
								Detector.MouseHoverEnter:Fire(LocalPlayer)
							end
							Targets[Detector] = CurrentMoval
							ActiveIcon = true
							Mouse.Icon = Detector.CursorIcon
						end
					end
				end
				Target = Target.Parent
			end

			for Detector, Moval in next, Targets do
				if Moval ~= CurrentMoval then
					Targets[Detector] = nil
					MouseDowns[Detector] = nil
					if not ActiveIcon then
						Mouse.Icon = ""
					end
					Detector.MouseHoverLeave:Fire(LocalPlayer)
				end
			end

			CurrentMoval = (CurrentMoval + 1) % MaximumInteger
		end

		Mouse.Move:Connect(MouseMoved)
		local Connection = Workspace.CurrentCamera:GetPropertyChangedSignal("CFrame"):Connect(MouseMoved)
		Workspace:GetPropertyChangedSignal("CurrentCamera"):Connect(function()
			Connection:Disconnect()
			Connection = Workspace.CurrentCamera:GetPropertyChangedSignal("CFrame"):Connect(MouseMoved)
		end)

		for i = 1, 2 do
			local Event = i == 1 and "MouseClick" or "RightMouseClick"

			Mouse["Button" .. i .. "Down"]:Connect(function()
				local Target = Mouse.Target

				while Target do
					local Detectors = Parts[Target]
					if Detectors then
						for a = 1, #Detectors do
							local Detector = Detectors[a]
							if Detector.MaxActivationDistance >= LocalPlayer:DistanceFromCharacter(Target.Position) then
								MouseDowns[Detector] = i
							end
						end
					end
					Target = Target.Parent
				end
			end)

			Mouse["Button" .. i .. "Up"]:Connect(function()
				for Detector, Down in next, MouseDowns do
					if Down == i then
						Detector[Event]:Fire(LocalPlayer, Mouse.TargetSurface)
					end
				end
			end)
		end
	end

	local function CompareClickDetectors(a, b)
		return a.__id < b.__id
	end

	return PseudoInstance:Register("ClickDetector", {
		Internals = {};

		Storage = {};

		Properties = {
			MaxActivationDistance = Enumeration.ValueType.Number;
			CursorIcon = Enumeration.ValueType.String;

			Parent = function(self, PVInstance)
				if PVInstance == nil then
					return true
				elseif typeof(PVInstance) == "Instance" and PVInstance:IsA("PVInstance") then
					self.Janitor:LinkToInstance(PVInstance)
					if LocalPlayer then
						local OldParent = self.Parent
						if OldParent ~= PVInstance then
							if OldParent then
								local Data = Parts[PVInstance]

								if #Data == 1 and Data[1] == self then
									Parts[PVInstance] = nil
								else
									Data:RemoveElement(self)
								end
							end

							local Data = Parts[PVInstance]
							if Data then
								Data:Insert(self)
							else
								Parts[PVInstance] = SortedArray.new({self}, CompareClickDetectors)
							end
						end
					end
					return true
				else
					Debug.Error("The Parent of a " .. self.ClassName .. " must either be nil or a PVInstance")
				end
			end;
		};

		Events = {"MouseClick", "MouseHoverEnter", "MouseHoverLeave", "RightMouseClick"}; -- If these values are indexed from a ClickDetector, it will return a `Signal`

		Methods = {};

		Init = function(self, Id)
			self.MaxActivationDistance = 32
			self.CursorIcon = "rbxassetid://1727841997" -- 1727849582
			self:superinit(Id)
		end;
	}, ReplicatedPseudoInstance)
	```

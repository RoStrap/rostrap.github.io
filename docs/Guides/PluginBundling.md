Let's say we want to Bundle ChoiceDialog with a plugin. Specifically, an "Object to Lua" plugin.

![](../assets/images/InstallingChoiceDialog.png)

We're going to want all of our libraries under the same Object. In this case we are going to place our libraries under the main Script of the plugin.

![](../assets/images/DragObjectsIntoScript.png) ![](../assets/images/DeleteFolders.png)

Next, we are going to run a script that will replace the Resources functions with some simple replacements.

Enable your command bar (under the View tab) and paste the following script in. Make sure to change `PARENT_OF_LIBRARIES` to fit your use case.

```lua
local PARENT_OF_LIBRARIES = workspace.ObjectsToLua

local LocalTables = {}
for _, Object in next, PARENT_OF_LIBRARIES:GetDescendants() do
	if Object:IsA("LuaSourceContainer") then
		local Source, Reps = Object.Source
			:gsub("local Resources = [^\r\n]+[\r\n]", "\nlocal function _Load_Library_(Name)\n\treturn require(script.Parent[Name])\nend\n")
			:gsub("Resources:LoadLibrary(%b())", "_Load_Library_%1")
			:gsub("Resources:GetLocalTable(%b())", function(x)
				local Name = "LocalTable" .. x:sub(3, -3)

				if not LocalTables[Name] then
					LocalTables[Name] = true
					local Mod = Instance.new("ModuleScript", PARENT_OF_LIBRARIES)
					Mod.Source = "return {}\n"
					Mod.Name = Name
				end

				return "_Load_Library_(\"" .. Name .. "\")"
			end)
			:gsub("Resources:Get(%a+)(%b())", function(x, y)
				return "_Resource_Get_(\"" .. x .. "\", " .. y:sub(2, -2) .. ")"
			end)

		if Reps > 0 then
			Source = "local function _Resource_Get_(ClassName, Name, Parent)\n\tlocal IsPlugin = script.Parent.Parent.ClassName == \"Plugin\"\n\n\tif not Parent then\n\t\tParent = _Resource_Get_(\"Folder\", ClassName .. \"Folder\", game:GetService(IsPlugin and \"CoreGui\" or \"ReplicatedStorage\"))\n\tend\n\n\tif IsPlugin or game:GetService(\"RunService\"):IsServer() then\n\t\tlocal Object = Instance.new(ClassName)\n\t\tObject.Name = Name\n\t\tObject.Parent = Parent\n\t\treturn Object\n\telse\n\t\treturn Parent:WaitForChild(Name)\n\tend\nend\n\n" .. Source
		end

		Object.Source = Source
	end
end
```

This code should work for any of the libraries under the RoStrap organization, with the exception of the `Sentry` library.

Now we can write some code for the plugin:

```lua
require(script.ChoiceDialog) -- Preload the libraries
require(script.ReplicatedPseudoInstance)
local PseudoInstance = require(script.PseudoInstance)

local Dialog = PseudoInstance.new("ChoiceDialog")
Dialog.HeaderText = "Script Class"
Dialog.Options = {"ModuleScript", "Script", "LocalScript"}
Dialog.DismissText = "CANCEL"
Dialog.ConfirmText = "CONVERT"
Dialog.PrimaryColor3 = PrimaryColor3
Dialog.Parent = game

local _, Choice = Dialog.OnConfirmed:Wait()

print(Choice)
```

![](../assets/images/ScriptClass.png)

Add some glue, and you've got yourself a plugin running RoStrapUI! Publish your plugin and try it out. Also be sure to check out my RbxObject2Lua plugin by clicking the following image:

[![](../assets/images/Model2Lua.png)](https://www.roblox.com/library/2307140444/Obj2Lua)

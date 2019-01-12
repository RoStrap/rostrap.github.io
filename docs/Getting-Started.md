# Getting Started

To begin using RoStrap, simply install it by clicking the icon below and pressing the `Install` button:

[![](https://avatars1.githubusercontent.com/u/22812966?v=4&s=200)](https://www.roblox.com/library/725884332/RoStrap)

After installing, open a place and enable Http requests from Home --> Game Settings --> Security.

![](https://user-images.githubusercontent.com/15217173/40773165-ae0e978a-6487-11e8-86be-5acea8dd57a9.png)


Next, navigate to the `PLUGINS` tab. Click the RoStrap logo.

![](https://user-images.githubusercontent.com/15217173/40772147-d11332fc-6484-11e8-8448-c50c0ed9d3bc.png)

The plugin will install the [Resources](https://github.com/RoStrap/Resources/blob/master/Resources.lua) library and create an example "Repository" folder in [ServerStorage](http://wiki.roblox.com/index.php?title=API:Class/ServerStorage) from which libraries may be loaded using `LoadLibrary`

!!! note ""
	* Only [Folders](http://wiki.roblox.com/index.php?title=API:Class/Folder) and libraries should go in this repository.
		* Folder heiarchy of libraries is ignored.
	* A [ModuleScript](http://wiki.roblox.com/index.php?title=API:Class/ModuleScript) and its descendants are considered a single library.
		* Thus, only parent [ModuleScripts](http://wiki.roblox.com/index.php?title=API:Class/ModuleScript) will be accessible via `LoadLibrary`

!!! example
	```lua
	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local Resources = require(ReplicatedStorage:WaitForChild("Resources"))

	local Keys = Resources:LoadLibrary("Keys") -- Keys
	local Thin = Resources:LoadLibrary("Thin") -- Error! Not a valid library
	```

	![](https://user-images.githubusercontent.com/15217173/38775144-25b833f0-4038-11e8-9545-952f1634148b.png)

# Libraries

When you use RoStrap, you are using tested and tried Libraries which are continually **maintained** by the best developers in town! Whenever a developer updates their Library on GitHub, you will see an update button appear (under the `INSTALLED` tab). Installing or updating a library automatically installs its dependencies.

![](https://user-images.githubusercontent.com/15217173/38776955-f2ca9710-405c-11e8-86e9-74452dbd44ea.png)

Updates are detected when your source code doesn't match the source code of the latest version of GitHub, excluding whitespace, comments, and *configurable variables*. Configurable variables (as RoStrap recognizes them) have to look like this:

```lua
local ALL_CAMEL_CASE = "SINGLE-LINE-VALUE"
```

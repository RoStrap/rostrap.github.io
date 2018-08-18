# PseudoInstance

!!! summary
	Rigidly defined PseudoInstance class system based upon Roblox Instances. The goal is to create encapsulated instances whose state is simply a function of its externally accessible properties. In other words, a cloned instance should render exactly the same as the original instance.

## Library API

### PseudoInstance.new

!!! summary "<span style="color:purple;">PseudoInstance</span> PseudoInstance.<span style="color:blue;">new</span>(<span style="color:green;">string</span> ClassName, ...)"

	Instantiates a new PseudoInstance of type `ClassName`. Arguments (...) are passed to the `Init` constructor.

!!! example
	```lua
	local PseudoInstance = Resources:LoadLibrary("PseudoInstance")

	local Shadow = PseudoInstance.new("Shadow")
	Shadow.Elevation = 8 -- this will cast to Enumeration.ShadowElevation.Elevation8
	Shadow.Parent = Background -- Whatever Gui you wish
	```

!!! note
	Only classes which have been [Registered](https://rostrap.github.io/Libraries/Classes/PseudoInstance/#pseudoinstanceregister) may be instantiated. If you attempt to instantiate a class which has not been [Registered](https://rostrap.github.io/Libraries/Classes/PseudoInstance/#pseudoinstanceregister), it will call `Resources:LoadLibrary(ClassName)` and try again.

### PseudoInstance.Make

!!! summary "<span style="color:purple;">PseudoInstance</span> PseudoInstance.<span style="color:blue;">Make</span>(<span style="color:green;">string</span> ClassName, <span style="color:teal;">dictionary</span> Properties, ...)"

	`PseudoInstance.new` wrapper which automatically assigns properties in dictionary `Properties`. Arguments passed to (...) must be dictionaries of Properties too. The only downside is you cannot pass any parameters to the `Init` constructor, but you probably don't need to. [See the Make library's documentation for more information, as it works identically.](https://rostrap.github.io/Libraries/Helper/Make/)

!!! example
	```lua
	local PseudoInstance = Resources:LoadLibrary("PseudoInstance")

	local Shadow = PseudoInstance.Make("Shadow", {
		Elevation = 8; -- this will cast to Enumeration.ShadowElevation.Elevation8
		Parent = Background; -- Parent is set last
	})
	```
### PseudoInstance:Register

!!! summary "<span style="color:purple;">PseudoTemplate</span> PseudoInstance:<span style="color:blue;">Register</span>(<span style="color:green;">string</span> ClassName, <span style="color:teal;">table</span> Template, <span style="color:green;">table</span> InheritsFrom = PseudoInstance)"

	Registers a new class of PseudoInstances which can be instantiated via `PseudoInstance.new(ClassName)`. Please read all the documentation in the example below:

	```lua
	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local Resources = require(ReplicatedStorage:WaitForChild("Resources"))
	local Typer = Resources:LoadLibrary("Typer")
	local Enumeration = Resources:LoadLibrary("Enumeration")
	local PseudoInstance = Resources:LoadLibrary("PseudoInstance")

	Enumeration.PastaStyle = {"Spaghetti", "Fusilli", "Penne", "Rigatoni", "Rotelle"}

	local ClassNameTemplate = PseudoInstance:Register("ClassName", {
		Events = {
			-- These are the events (see: Signal) of the PseudoInstance. These can be Connect()ed to,
			-- Fire()d, Wait()ed on, etc

			-- implicit numerical indeces define an Event member without Constuctors or Destructors
			"OnPressed";

			OnRightPressed = function(self)
				-- self is the PseudoInstance for which this Event is being constructed.
				-- Must return two functions, one constuctor and
				-- one destructor with which to call Signal.new (see docs)
				return function()
				end, function()
				end
			end;
		};

		Internals = {
			-- These values are internal-only and not externally accessible

			-- implicit numerical indeces are set by default to false, to be defined at run-time
			"NumChildren";

			Set = function(self, Bool) -- These can be set to anything
				return Bool == true and 1 or 0
			end;
		};

		Methods = {
			Kill = function(self)
				-- Methods and the Init functions are sent an internal-access table version of self

				self.OnPressed:Fire() -- Internal Signal-access has full control
				return self:Set(true)
			end;

			Destroy = function(self, ...)
				print("We are being destroyed!")

				-- self:super() calls the superclass's method by the name of the first parameter
				-- In this case, this calls Superclass.Destroy(self, ...)
				self:super("Destroy", ...)
			end;

			-- When set to 0, it makes the class Abstract
			FunctionWhichMustBeImplementedByAClassThatInheritsFromThisOne = 0;
		};

		Properties = {
			-- Can be set to a Typer value for typechecking
			Name = Typer.String;

			-- This is equivalent to the previous declaration
			Name = Typer.AssignSignature(2, Typer.String, function(self, Value)
				self:rawset("Name", Value)
			end)

			-- Can also be constrained to a certain EnumerationType
			Style = Typer.EnumerationOfTypePastaStyle;

			Parent = function(self, Parent)
				-- Always called with the Object and the Property value it is being set to

				-- Do stuff
				self:rawset("Parent", Parent) -- Make sure to rawset the Property to what it should be
			end;
		};

		Init = function(self)
			-- Called by PseudoInstance.new()

			-- Every PseudoInstance comes with a built-in Janitor which is called upon Destruction
			self.Janitor:Add(workspace.ChildAdded:Connect(function() end))


			-- Sets externally-accessible Value of PseudoInstance directly
			-- without calling a Property setting function
			-- This can also be used for read-only values
			self:rawset("IsPlayer", true)

			-- Must be in your init function, to run the constructor in the superclass
			-- Will not exist after the Init function runs if the constructors resolved properly
			self:superinit()
		end;
	})

	-- Will Error, because `ClassName` is Abstract
	print(pcall(PseudoInstance.new, "ClassName"))

	local MyClass = PseudoInstance:Register("MyClass", {
		Methods = {
			FunctionWhichMustBeImplementedByAClassThatInheritsFromThisOne = function(self)
			end;
		};

		Init = function(self)
			self:superinit()
		end;
	}, ClassNameTemplate)

	local MyInstance = PseudoInstance.new("MyClass")
	MyInstance.Style = "Rigatoni" -- Gets cast to Enumeration
	MyInstance.Style = 3 -- Gets cast to Rigatoni
	MyInstance:Kill()

	-- Externally, one only may Connect() and Wait() on events
	MyInstance.OnPressed:Connect(print)

	-- Error: Cannot `Fire` externally.
	print(pcall(MyInstance.OnPressed.Fire, MyInstance.OnPressed))

	print(pcall(function()
		MyInstance:Set(true)
	end)) -- Set does not exist externally
	```

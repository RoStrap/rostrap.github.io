# Overview

What follows is an overview of the [libraries installable by RoStrap](https://github.com/RoStrap/Libraries/blob/master/Libraries.lua):

## RoStrap-owned Libraries by category
#### Core
<h6><a href="../../Resources">Resources</a> - The core resource manager and library loader for RoStrap. Centralizes library loading and simplifies resource management.</h6>

#### Classes
<h6><a href="../Libraries/Classes/Enumeration">Enumeration</a> - A Lua implementation of Roblox Enums with the ability to declare new ones</h6>

```lua
Enumeration.SelectionControllerType = {"Checkbox", "Radio", "Switch"}
local Radio = Enumeration.SelectionControllerType.Radio

print(Radio) --> Enumeration.SelectionControllerType.Radio
print(Radio.EnumerationType) --> SelectionControllerType
print(Radio.Name) --> Radio
print(Radio.Value) --> 1
```

<h6><a href="../Libraries/Classes/PseudoInstance">PseudoInstance</a> - A library for declaring black-boxed classes similar to Roblox Instances</h6>

<h6><a href="../Libraries/Classes/ReplicatedPseudoInstance">ReplicatedPseudoInstance</a> - An extension of PseudoInstance with an automatic replication system</h6>

#### DataTypes
<h6><a href="../Libraries/DataTypes/Array">Array</a> - A few utility functions which can operate on Arrays</h6>

<h6><a href="../Libraries/DataTypes/SortedArray">SortedArray</a> - A class for sorted arrays using the binary search algorithm</h6>

<h6><a href="../Libraries/DataTypes/Table">Table</a> - A few utility functions which operate on Tables, notably Table.Lock</h6>

#### Debugging
<h6><a href="../Libraries/Debugging/Debug">Debug</a> - Better error/warn functions and an implementation of TableToString</h6>

<h6><a href="../Libraries/Debugging/Typer">Typer</a> - Type Checker and Function Signature Assigner</h6>

```lua
local AddPlayer = Typer.AssignSignature(Typer.InstanceWhichIsAPlayer, function(plr)
	print(plr)
end)

AddPlayer(game:GetService("Players").LocalPlayer) -- good!
AddPlayer(10) -- [Typer] {AddPlayer} bad argument #1: expected Instance which is a Player, got number 10
```

#### Events
<h6><a href="../Libraries/Events/Janitor">Janitor</a> - Light-weight, flexible object for cleaning up connections, instances, or anything. Intended to reach all use cases</h6>

<h6><a href="../Libraries/Events/Signal">Signal</a> - A class for creating API-compatible Roblox Events</h6>

#### Helper
<h6><a href="../Libraries/Helper/FastSpawn">FastSpawn</a> - Expensive method of running a function on a new thread without yielding a frame (like spawn) and works within Roblox's thread scheduler (<code>coroutine.resume(coroutine.create(Func))</code> is now preferred)</h6>

<h6><a href="../Libraries/Helper/Make">Make</a> - Shorthand for instance declarations</h6>

#### Input
<h6><a href="../Libraries/Input/Keys">Keys</a> - Simplifies Key input bindings</h6>

```lua
local Q = Keys.Q -- returns a Key Object

Q.KeyDown:Connect(function()
	print("Q was pressed!")
end)

Q.KeyUp:Connect(function()
	print("Q was let go!")
end)
```

#### Interpolation
<h6><a href="../Libraries/Interpolation/Bezier">Bezier</a> - Lua implementation of (2D) <a href="http://cubic-bezier.com/">Bezier curves</a></h6>

```lua
local EasingFunc = Bezier.new(0.17, 0.67, 0.83, 0.67)
```

<h6><a href="../Libraries/Interpolation/EasingFunctions">EasingFunctions</a> - A bunch of reuseable Easing Functions, including those from the Material Design specification (<a href="https://material.io/design/motion/speed.html#easing">Standard, Acceleration, and Deceleration</a>)</h6>

<h6><a href="../Libraries/Interpolation/Lerps">Lerps</a> - Holds all Lerp functions for Roblox objects, with a special visually-linear color lerping function</h6>

![](https://i.gyazo.com/7b20b827543f913594edc95646486204.gif)

<h6><a href="../Libraries/Interpolation/Tween">Tween</a> - Tweening library modeled after the <a href = "http://duckduckgo.com/?q=!rowiki+TweenPosition">TweenPosition</a> method built upon <a href="../Libraries/Interpolation/Lerps">Lerps</a> and <a href="../Libraries/Interpolation/EasingFunctions">EasingFunctions</a></h6>

```lua
Tween(workspace.Part, "Transparency", 1, Standard, 2, true)
```

#### Math
<h6><a href="../Libraries/Math/BigNum">BigNum</a> - A BigNum with Fractions implementation for big-integer calculations, optimized for DataStore storage and networking.</h6>

```lua
print(BigNum.new("1025123") ^ BigNum.new("9"))
--> 1250212389547080859766804627957328989496357747253559363
```

<h6><a href="../Libraries/Math/Leveler">Leveler</a> - Level and Experience class, because why not?</h6>

<h6><a href="../Libraries/Math/Normal">Normal</a> - Random number generator along a Normal distribution curve</h6>

<h6><a href="../Libraries/Math/WeightedProbabilityFunction">WeightedProbabilityFunction</a> - A syntactically pleasing way of creating functions which randomly pick an option based upon its relative probability</h6>

```lua
local CoinToss = WeightedProbabilityFunction.new {
	Heads = 0.5;
	Tails = 0.5;
}

print(CoinToss()) --> Heads
```

#### RoStrapUI
<h6><a href="../Libraries/RoStrapUI/AsymmetricTransformation">AsymmetricTransformation</a> - Transform function for Paper from the Material Design specifications</h6>

<h6><a href="../Libraries/RoStrapUI/Checkbox">Checkbox</a> - A Material Design checkbox element</h6>

<div align="center">
	<video muted autoplay loop>
	<source src="../assets/videos/Checkboxes.mp4" type="video/mp4">
	</source>
	</video>
</div>

<h6><a href="../Libraries/RoStrapUI/ChoiceDialog">ChoiceDialog</a> - A Material Design ChoiceDialog element with built-in replication</h6>

<div align="center">
	<video muted autoplay loop>
	<source src="../assets/videos/ChoiceDialog.mp4" type="video/mp4">
	</source>
	</video>
</div>

<h6><a href="../Libraries/RoStrapUI/Color">Color</a> - Material Design's 2014 Color Palette</h6>

<h6><a href="../Libraries/RoStrapUI/Radio">Radio</a> - A Material Design radio element</h6>

<h6><a href="../Libraries/RoStrapUI/RadioGroup">RadioGroup</a> - A wrapper class for a group of radio elements</h6>

<div align="center">
	<video muted autoplay loop>
	<source src="../assets/videos/RadioButtons.mp4" type="video/mp4">
	</source>
	</video>
</div>

<h6><a href="../Libraries/RoStrapUI/RippleButton">RippleButton</a> - A Material Design button element</h6>

<div align="center">
	<video muted autoplay loop>
	<source src="../assets/videos/RippleButton.mp4" type="video/mp4">
	</source>
	</video>
</div>

<h6><a href="../Libraries/RoStrapUI/Rippler">Rippler</a> - A Material design class responsible for creating ripples</h6>

<h6><a href="../Libraries/RoStrapUI/SelectionController">SelectionController</a> - A class from which the checkbox and radio classes inherit</h6>

<h6><a href="../Libraries/RoStrapUI/Shadow">Shadow</a> - A Shadow/Elevation rendering PseudoInstance</h6>

<h6><a href="../Libraries/RoStrapUI/Snackbar">Snackbar</a> - A Material Design Snackbar element with built-in replication</h6>

<div align="center">
	<video muted autoplay loop>
	<source src="../assets/videos/Snackbar.mp4" type="video/mp4">
	</source>
	</video>
</div>

#### Time
<h6><a href="../Libraries/Time/Date">Date</a> - A reimplementation of the vanilla Lua os.date function built upon the one exposed by RobloxLua</h6>

```lua
print(Date("ISO 8601: %FT%T%#z")) --> ISO 8601: 2020-12-31T01:03:05-05:00
```

<h6><a href="../Libraries/Time/SyncedPoller">SyncedPoller</a> - Calls functions on an interval along <code>os.time</code> (for cross-server simultaneous calls)</h6>


#### Sentry
<h6><a href="../Libraries/Sentry">Sentry</a> - A library for reporting errors/warnings/messages to your <a href="https://sentry.io">Sentry account</a></h6>
<h6><a href="../Libraries/Try">Try</a> - (DEPRECATED in favor of Promise) An asynchronous pcall-wrapper library for controlling the flow of error-prone, interdependent functions.</h6>

## Roblox-owned Libraries
<h6><a href="https://github.com/Roblox/roact">Roact</a> - A declarative UI library similar to Facebook's React</h6>
<h6><a href="https://github.com/Roblox/rodux">Rodux</a> - A state management library inspired by Redux</h6>
<h6><a href="https://github.com/Roblox/roact-rodux">Roact-Rodux</a> - An ergonomic binding between Roact and Rodux</h6>

## Highly trusted Libraries
<h6><a href="https://github.com/LPGhatguy/roblox-lua-promise">Promise</a> - An implementation of Promise similar to Promise/A+</h6>
<h6><a href="https://github.com/evaera/Aurora">Aurora</a> - Manages status effects (known as "Auras")</h6>
<h6><a href="https://github.com/buildthomas/MockDataStoreService">DataStoreService</a> - An implementation of Roblox's DataStoreService in Lua for seamless offline development & testing</h6>
<h6><a href="https://github.com/evaera/Cmdr">Cmdr</a> - A fully extensible and type-safe admin command console</h6>

<div align="center">
	<img src="https://camo.githubusercontent.com/a3a00fd1e01b48d27f080663e0c60f0e1e439b73/68747470733a2f2f692e6572796e2e696f2f74783239766871626c612e676966" alt="Cmdr">
</div>
<h6><a href="https://github.com/evaera/EvLightning">EvLightning</a> - Realistic-looking lightning bolt generator</h6>

![](https://camo.githubusercontent.com/41b61e0dcc11475c06f617b0b8a1e8232ebe3a49/68747470733a2f2f7468756d62732e6766796361742e636f6d2f436c756d737941646f6c657363656e74436f6c6c69652d73697a655f726573747269637465642e676966)
<h6><a href="https://github.com/evaera/RadialSpriteSheetGenerator">RadialImage</a> - A library which displays radial progress indicators using a sprite sheet generated by a nifty tool</h6>
![](https://camo.githubusercontent.com/b186a81b7cba5806487415f937cff96ad1a5636b/68747470733a2f2f7468756d62732e6766796361742e636f6d2f57696e64696e67417070726f707269617465436f6c6c6172646c697a6172642d73697a655f726573747269637465642e676966)

## Third-Party Libraries
<!-- <h6><a href="https://github.com/EmeraldSlash/RbxMouse">PseudoMouse</a> - A custom Mouse object with a cleaner API</h6> -->
<h6><a href="https://github.com/EmeraldSlash/RbxReady">Ready</a> - A Library for yielding until an object's descendants have finished replicating</h6>

## Libraries Lacking documentation
<h6><a href="https://github.com/RoStrap/Time/blob/master/ConditionalPoller.lua">ConditionalPoller</a> - A class that continually calls a callback as long as a condition is true</h6>

<h6><a href="https://github.com/RoStrap/Events/blob/master/ReplicatedValue.lua">ReplicatedValue</a> - A server-authoritative value replicated across the network</h6>

<h6><a href="https://github.com/RoStrap/Math/blob/master/Spring.lua">Spring</a> - Simulates the motion of a critically damped spring</h6>

## RoStrap Discord

<h6>Questions? Comments? Concerns? Join us!</h6>

<div align="left">
	<a href="https://discord.gg/pjJw8s4">
		<img src="https://discordapp.com/assets/94db9c3c1eba8a38a1fcf4f223294185.png" alt="Discord" width=200 height=68 />
	</a>
</div>

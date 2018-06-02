# Signal

!!! summary
	A class to create API-compatible Roblox Events

	This new version designed by Anaminus addresses two flaws in previous implementations:

	- Previous versions held a reference to the last set of fired arguments.
	- Arguments would be overridden if the signal was fired by a listener.

## Library API

### Signal.new

!!! summary
	<pre><a href="https://github.com/RoStrap/Events/blob/master/Signal.lua" title="Signal"><span style="color:blue;">Signal</span></a> Signal.new (
		<a href="http://wiki.roblox.com/index.php?title=API:Type/function" class="mw-redirect" title="API:Type/function"><span>function</span></a> Constructor,
		<a href="http://wiki.roblox.com/index.php?title=API:Type/function" class="mw-redirect" title="API:Type/function"><span>function</span></a> Destructor
	)</pre>

	Returns a new signal. Receives optional constructor and destructor functions. The constructor is called when the number of listeners/threads becomes greater than 0. The destructor is called when then number of threads/listeners becomes 0. The destructor	receives as arguments the values returned by the constructor.

!!! example
	```lua
	local Signal = Resources:LoadLibrary("Signal")
	local Event = Signal.new()
	```

## Signal API

### Fire

!!! summary
	<pre><a href="http://wiki.roblox.com/index.php?title=API:Type/void" title="API:Type/void"><span style="color:blue;">void</span></a> Signal:Fire (
		<a href="http://wiki.roblox.com/index.php?title=API:Tuple" class="mw-redirect" title="API:Tuple"><span>Tuple</span></a>&lt;<a href="http://wiki.roblox.com/index.php?title=API:Variant" title="API:Variant"><span>Variant</span></a>&gt; arguments
	)</pre>
	Fire the signal, passing the arguments to each listener and waiting	threads. Arguments are passed by reference.

### Wait

!!! summary
	<pre><a href="http://wiki.roblox.com/index.php?title=API:Tuple" class="mw-redirect" title="API:Tuple"><span style="color:blue;">Tuple</span></a>&lt;<a href="http://wiki.roblox.com/index.php?title=API:Variant" title="API:Variant"><span style="color:blue;">Variant</span></a>&gt; Signal:Wait ()</pre>

	Block the current thread until the signal is fired. Returns the arguments passed to Fire.

### Destroy

!!! summary
	<pre><a href="http://wiki.roblox.com/index.php?title=API:Type/void" title="API:Type/void"><span style="color:blue;">void</span></a> Signal:Destroy ()</pre>

	Disconnects all listeners and becomes unassociated with currently blocked threads. The signal becomes unusable and ready to be garbage collected.

### Connect

!!! summary
	<pre><a href="http://wiki.roblox.com/index.php?title=API:RBXScriptConnection" class="mw-redirect" title="API:RBXScriptConnection"><span style="color:blue;">PseudoScriptConnection</span></a> RBXScriptSignal:Connect(<a href="http://wiki.roblox.com/index.php?title=API:Type/function" class="mw-redirect" title="API:Type/function"><span>function</span></a>&lt;<a href="http://wiki.roblox.com/index.php?title=API:Type/void" title="API:Type/void"><span>void</span></a>&gt;(<a href="http://wiki.roblox.com/index.php?title=API:Tuple" class="mw-redirect" title="API:Tuple"><span>Tuple</span></a>&lt;<a href="http://wiki.roblox.com/index.php?title=API:Variant" title="API:Variant"><span>Variant</span></a>&gt;) func)</pre>

	Sets a function to be called when the signal is fired. The listener function receives the arguments passed to Fire. Returns a SignalConnection.

## PseudoScriptConnection API

!!! summary
	<pre><a href="http://wiki.roblox.com/index.php?title=API:Type/void" title="API:Type/void"><span style="color:blue;">void</span></a> PseudoScriptConnection:Disconnect()</pre>
	Disconnects the listener, causing it to no longer be called when the signal is fired.

### Fields
|Field|Description|Default value|Type|
|:-:|:-:|:-:|:-:|
|Connected|Whether the listener is connected|true|bool|

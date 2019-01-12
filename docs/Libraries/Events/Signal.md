# [Signal](https://github.com/RoStrap/Events/blob/master/Signal.lua)

!!! summary
	A class for creating API-compatible Roblox Events

	This new version originally designed by Anaminus addresses two flaws in previous implementations:

	- Previous versions held a reference to the last set of fired arguments.
	- Arguments would be overridden if the signal was fired by a listener.

## Library API

### Signal.new

!!! summary "<span style="color:purple;">Signal</span> Signal.<span style="color:blue;">new</span>([<span style="color:green;">function</span> Constructor, <span style="color:green;">function</span> Destructor])"

	Returns a new signal. Receives optional constructor and destructor functions. The constructor is called when the number of listeners/threads becomes greater than 0. The destructor is called when then number of threads/listeners becomes 0. The values returned by the constructor are passed into the destructor.

!!! example
	```lua
	local Signal = Resources:LoadLibrary("Signal")
	local Event = Signal.new()
	```

## Signal API

### Signal:Fire

!!! summary "<span style="color:purple;">void</span> Signal:<span style="color:blue;">Fire</span>(...)"
	Fire the signal, passing the arguments to each listener and waiting	threads. Arguments are **always** passed by reference.

### Signal:Wait

!!! summary "<span style="color:purple;">(...)</span> Signal:<span style="color:blue;">Wait</span>()"
	Block the current thread until the signal is fired. Returns the arguments passed to Fire.

### Signal:Connect

!!! summary "<span style="color:purple;">PseudoScriptConnection</span> Signal:<span style="color:blue;">Connect</span>(<span style="color:green;">function</span> Function [, <span style="color:green;">any</span> Argument])"

	Sets a function to be called when the signal is fired. The listener function receives the arguments passed to Fire. Returns a [PseudoScriptConnection](https://rostrap.github.io/Libraries/Events/Signal/#pseudoscriptconnection-api)

### Signal:Destroy

!!! summary "<span style="color:purple;">void</span> Signal:<span style="color:blue;">Destroy</span>()"
	Disconnects all listeners and becomes unassociated with currently blocked threads. The signal becomes unusable and ready to be garbage collected.

### Fields
|Field|Description|Type|Default value|
|:-:|:-:|:-:|:-:|
|Event|Interface which can only access `Connect` and `Wait`|PseudoScriptSignal|N / A|
|Bindable|Dispatches scheduler-compatible Threads|BindableEvent|Instance.new("BindableEvent")|
|Arguments|Holds arguments for pending listener functions and Threads|table|\{ \}|
|Connections|SignalConnections connected to the signal|table|\{ \}|
|Constructor|Called when the number of listeners becomes greater than 0|function|nil|
|Destructor|Called when then number of listeners becomes 0|function|nil|


## PseudoScriptConnection API

!!! summary "<span style="color:purple;">void</span> PseudoScriptConnection:<span style="color:blue;">Disconnect</span>()"
	Disconnects the listener, causing it to no longer be called when the signal is fired.

### Fields
|Field|Description|Type|Default value|
|:-:|:-:|:-:|:-:|
|Connected|Whether the listener is connected|bool|true|

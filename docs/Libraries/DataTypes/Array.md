# Array

A few utility functions which can operate on Arrays.

## Library API

### Array.Flatten

!!! summary "<span style="color:purple;">array</span>&nbsp;Array&period;<span style="color:blue;">Flatten</span>&lpar;<span style="color:green;">array</span>&nbsp;a1&rpar;"
	Takes in an array, a1, which may have arrays inside of it.
	Unpacks all arrays in their proper place into a1.
	Returns a1

!!! example
	```lua
	Array.Flatten{{1, 2}, 3, 4, {5, {6, {{7, 8}, 9}, 10}, 11}, {}, 12}
	--> {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}
	```

### Array.Contains

!!! summary "<span style="color:purple;">number</span>&nbsp;Array&period;<span style="color:blue;">Contains</span>&lpar;<span style="color:green;">array</span>&nbsp;a1&comma;&nbsp;<span style="color:teal;">variant</span>&nbsp;v&rpar;"
	Returns the index at which v exists within array a1.

!!! example
	```lua
	print(Array.Contains({0, 1, 2}, 2)) --> 3
	print(Array.Contains({0, 1, 2}, 4)) --> nil
	```

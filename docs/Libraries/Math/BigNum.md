# [BigNum](https://github.com/RoStrap/Math/blob/master/BigNum.lua)

A BigNum with Fractions implementation for big-integer calculations, optimized for DataStore storage and networking.

```lua
local BigNum = Resources:LoadLibrary("BigNum")
print(BigNum.new("1025123") ^ BigNum.new("9"))
--> 1250212389547080859766804627957328989496357747253559363
```

The BigNum library utilizes Lua's doubles to hold place values, called "radix" (similar to digits but in a different base). Each double represents a single "radix" of the BigNum. By default, the BigNum library instantiates BigNums with 32 radix (256 bytes) to do calculations. This is big enough for numbers as large as `7.76e230` (see `BigNum:GetRange()`). If you need integers higher than that, simply pass in how many doubles it should allocate.

```lua
-- Explicitly allocate 128 doubles (1024 bytes) for each BigNum
print(BigNum.new("8", 128) ^ BigNum.new("900", 128))
```

Otherwise, you can externally set the default number of allocated radix:

```lua
BigNum:SetDefaultRadix(64)
```

The library also ships with a data type called BigNumFractions, which can be used for exact calculations with Fractions.

## Library API

### BigNum.new

!!! summary "<span style="color:purple;">BigNum</span>&nbsp;BigNum&period;<span style="color:blue;">new</span>&lpar;<span style="color:green;">string</span>&nbsp;Base10Number&nbsp;&lsqb;&comma;&nbsp;<span style="color:teal;">integer</span>&nbsp;Radix&rsqb;&rpar;"
	Returns a new BigNum with the allocated number of Radix (defaults to 32)

### BigNum.fromString64

!!! summary "<span style="color:purple;">BigNum</span>&nbsp;BigNum&period;<span style="color:blue;">fromString64</span>&lpar;<span style="color:green;">string</span>&nbsp;Base64String&rpar;"
	Meant to instantiate BigNums from strings returned via the `toString64` method.

### BigNum.newFraction

!!! summary "<span style="color:purple;">BigNumFraction</span>&nbsp;BigNum&period;<span style="color:blue;">newFraction</span>&lpar;<span style="color:green;">BigNum</span>&nbsp;Numerator&comma;&nbsp;<span style="color:teal;">BigNum</span>&nbsp;Denominator&rpar;"
	Instantiates a new Fraction in the form `(Numerator / Denominator)`

### BigNum:GetRange

!!! summary "<span style="color:purple;">string</span>&nbsp;BigNum&colon;<span style="color:blue;">GetRange</span>&lpar;<span style="color:green;">integer</span>&nbsp;Radix&rpar;"
	Returns a string representation of approximately how large of integers can be represented with a given number of Radix

	```lua
	print(BigNum:GetRange(128))
	--> +/- 2.90e924
	```

### BigNum:SetDefaultRadix

!!! summary "<span style="color:purple;">void</span>&nbsp;BigNum&colon;<span style="color:blue;">SetDefaultRadix</span>&lpar;<span style="color:green;">integer</span>&nbsp;DefaultRadix&rpar;"
	Sets the default number of Radix allocated for each number (default is 32)

## BigNum API

These are the methods which operate on BigNums themselves.

### BigNum:toString64

!!! summary "<span style="color:purple;">string</span>&nbsp;BigNum&colon;<span style="color:blue;">toString64</span>&lpar;&rpar;"
	Returns a string-base64 encoding of the BigNum, which can be reproduced using `BigNum.fromString64`

### BigNum:toConstantForm

!!! summary "<span style="color:purple;">void</span>&nbsp;BigNum&colon;<span style="color:blue;">toConstantForm</span>&lpar;<span style="color:green;">integer</span>&nbsp;<span style="color:teal;">NumberOfDoublesPerLine</span>&nbsp;&equals;&nbsp;16&rpar;"
	Creates a file (or on Roblox, a script in the Lighting) with a constant representation of the BigNum. This is useful for directly instantiating BigNums with Big values which would take a lot of processing at run-time to convert from a base10 string to the internal representation.

	Looks like this:
	```lua
	local CONSTANT_NUMBER = BigNum.new{
		0, 0, 154059, 3375645, 903522, 1038360, 13086355, 12524895, 10900259, 11967773, 5580376, 3468437, 579970, 6766011, 8397479, 8219103,
		8206478, 4226184, 11579046, 8128945, 3969135, 407937, 10824426, 1462231, 7523964, 16399268, 11691710, 13651477, 10604193, 2791442, 9280589, 5604105
	}
	```

### BigNum:stringify

!!! summary "<span style="color:purple;">string</span>&nbsp;BigNum&colon;<span style="color:blue;">stringify</span>&lpar;&rpar;"
	Returns a representation of the internal format of how BigNums are stored in their array.

## BigNumFraction API

### BigNumFraction:Reduce

!!! summary "<span style="color:purple;">BigNumFraction</span>&nbsp;BigNumFraction&colon;<span style="color:blue;">Reduce</span>&lpar;&rpar;"
	Reduces the Fraction and returns it.

### BigNumFraction:toScientificNotation

!!! summary "<span style="color:purple;">string</span>&nbsp;BigNumFraction&colon;<span style="color:blue;">toScientificNotation</span>&lpar;<span style="color:green;">integer</span>&nbsp;<span style="color:teal;">NumDigitsAfterDecimalPoint</span>&nbsp;&equals;&nbsp;2&rpar;"
	Returns a string representation of the Fraction in scientific notation with the given number of digits after the decimal. If there aren't enough digits to format it will just return the unformatted string.

## Demo

Here the library is used to calculate the [Birthday problem](https://en.wikipedia.org/wiki/Birthday_problem).

```lua
local BigNum = Resources:LoadLibrary("BigNum")
local _1 = BigNum.newFraction("1", "1")
local DaysInYear = BigNum.new("365")

local function BirthdayProblem(NumPeople)
	local Chance = BigNum.newFraction(DaysInYear, DaysInYear)

	for i = 2, NumPeople do
		Chance = Chance * BigNum.newFraction(DaysInYear + (1 - i), DaysInYear)
	end

	return _1 - Chance
end

print(BirthdayProblem(70):toScientificNotation(6))
--> 2.291582e179 / 2.293509e179
```

## Writing Optimal Code with BigNum

Sometimes, you will need to perform a massive calculation which might take up too much time to calculate on Roblox without having the thread scheduler cut you off.

What follows is a list of what this library is optimized for and what this library is slow at.

Optimized for:

- Any code given to you via the `toConstantForm` method

- Encoding/Decoding for DataStores/Replication using `toString64` and `fromString64`


Runs slowly:

- Printing massive numbers (in Base 10) a lot (Never use GetRange at run-time!)

- Creating BigNums from a Base10String at run-time (toConstantForm is recommended)

- Using more Radix than the library can be performant with. In my tests, 32 radix approaches native speeds, with going too far above 128 leading to unstability in intensive calculations

## Probably asked Questions

*What if I want to know what's after the decimal point?*

**Use Fractions!**

*How does this library work?*

**It uses a modified version of two's-complement numbers (but in base 2^24).**

*Why are calculations done in base 2^24?*

**Because the highest integer representable by a double is 2^53. 2^24 is the nicest high number which won't result in the internal calculations reaching higher than 2^53. Multiplying two numbers with the highest radix and the highest previous value can result in: (2^24 - 1)(2^24 - 1) + (2^24 - 1)**

*Are you insane?*

**I haven't been formally diagnosed, so who's to say?**

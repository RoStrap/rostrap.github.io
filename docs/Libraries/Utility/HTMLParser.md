## HTMLParser
Demo:
```lua
local HttpService = game:GetService("HttpService")
local HTML = HTMLParser.new(HttpService:GetAsync("https://github.com/"))

while HTML:Next().Tag do
	print(HTML.Tag, HTML.Data)
end
-- Once an HTMLParser reaches its end, `Tag` and `Data` become nil


-- The object can be used again for round 2!
while HTML:Next().Tag do
	print(HTML.Tag, HTML.Data)
end
```
### API
Instantiation:
```lua
local HTML = HTMLParser.new(HTML_DOCUMENT_STRING)
```
Advancement:
```lua
HTML:Next()
HTML:Next():Next():Next()
```
Accessing data at the current state:
```lua
print(HTML.Tag) -- /html (no <>)
print(HTML.Data) -- This value is anything that occurs after HTML.Tag but before the next Tag
```

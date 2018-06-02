# Sentry
![](https://sentry.io/_assets/og/default-ece813046f72308a5f52e8ed4f5ff498920320ef76bbad88df5d1de0469cb185.jpg)

## Getting started
Sign up for [Sentry](https://sentry.io/) to get started.

Navigate to the `Projects` tab on the left-hand side.

![](https://user-images.githubusercontent.com/15217173/40045794-dfd79f9e-57f0-11e8-968e-d95f0d0db605.png)

In the top right, navigate to "Add new..." and select "Project"

![](https://user-images.githubusercontent.com/15217173/40045846-0517598e-57f1-11e8-8b7d-4741271d0a25.png)

Don't select a project or framework, since this Library isn't officially supported by Sentry (but don't worry, **it is still officially supported by RoStrap**). Give your project a name and create project!

![](https://user-images.githubusercontent.com/15217173/40046120-bb6d5436-57f1-11e8-82ac-a86de1ac8c50.png)

![](https://user-images.githubusercontent.com/15217173/40046197-f339cf20-57f1-11e8-9970-efabc38a0350.png)

Now you need to find your DSN. You will hopefully be shown the following screen, but if not you can always find these in the "Settings" tab.

![](https://user-images.githubusercontent.com/15217173/40046296-3d4d2a8a-57f2-11e8-9609-6abf08745431.png)

You will need to locate a DSN that looks like this:

![](https://user-images.githubusercontent.com/15217173/40047458-278c5100-57f5-11e8-9594-51615feae30b.png)

Next, install this library using [the RoStrap plugin](https://www.roblox.com/library/725884332/RoStrap), and navigate to the Server-side Sentry library.

![](https://user-images.githubusercontent.com/15217173/40047745-e47d1498-57f5-11e8-8ec5-21c8df9d57cb.png)

Under the configuration, modify the `DSN` variable to your DSN

![](https://user-images.githubusercontent.com/15217173/40047836-321c907a-57f6-11e8-8894-a48e819e1b0d.png)

Now you have a working Sentry library!

## API
The API is the same for both the client and the server.

```lua
local Sentry = Resources:LoadLibrary("Sentry")
local Enumeration = Resources:LoadLibrary("Enumeration") -- Optional

Sentry:Post(string Message [, string Traceback, <Enum, Enumeration> MessageType])
-- Traceback defaults to debug.traceback()
-- MessageType defaults to "Error"
-- MessageType accepts any of the following Enumerations (or their corresponding numbers or strings)

-- 0: Enumeration.IssueType.Debug
-- 1: Enumeration.IssueType.Info
-- 2: Enumeration.IssueType.Warning
-- 3: Enumeration.IssueType.Error
-- 4: Enumeration.IssueType.Fatal

-- MessageType also accepts Roblox's MessageType Enums (but NOT their numbers or strings)
-- Enum.MessageType.MessageError
-- Enum.MessageType.MessageInfo
-- Enum.MessageType.MessageOutput
-- Enum.MessageType.MessageWarning
```

It is intended to be easily compatible with the `Try` library

```lua
local Try = Resources:LoadLibrary("Try")
local Sentry = Resources:LoadLibrary("Sentry")

Try(function(x) error("test client error " .. x) end, "1")
	:Catch(Sentry.Post)
```

Here are your free Sentry rate limits:

![](https://discourse-cdn-sjc1.com/business6/uploads/roblox/original/3X/8/3/83f1ad350dcda770fc2b2e82cc7b4757467ab95e.png)

Enjoy!

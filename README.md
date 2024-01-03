# vectorfield
Vectorfield is based on Rayfield, a dazzling UI library for exploiting. Vectorfield ports Rayfield for developers and adds many more elements.

## Example:
### Server:
```lua
require(game.ReplicatedStorage.Vectorfield) -- Vectorfield will not initialize until imported by server.
```
### Client:
```lua
local Vectorfield = require(game.ReplicatedStorage.Vectorfield)

local Window = Vectorfield:CreateWindow({
	Name = "Vectorfield Example Window",
	LoadingTitle = "Vectorfield Interface Suite",
	LoadingSubtitle = "by Unexex",
	--OpenKey = "X"
})

local Tab = Window:CreateTab("Players", 4483362458) -- Title, Image

local Section

function render(Found, Old)
	Section = Tab:CreateSection("Found 0 players")
	
	local Input = Tab:CreateLargeInput({
		Name = "Seach",
		PlaceholderText = "Search",
		RemoveTextAfterFocusLost = false,
		Callback = function(Text)
			local Players = game.Players:GetPlayers()
			local Found = {}
			for _, plr in Players do
				if string.sub(plr.Name, 0, #Text) == Text then
					table.insert(Found, plr)
				end
			end
			Section:Set(`Found {#Found} players`)
			Tab:Clear()
			task.wait()
			render(Found)
		end,
	})
	
	if Found then
		for i, v in Found do
			local Label = Tab:CreateLabel(v.Name)
		end
	end
end

render()
```
# Example:
https://github.com/unexex/vectorfield/assets/72946059/74b4136e-78ea-4f51-9aee-54d7f427241b


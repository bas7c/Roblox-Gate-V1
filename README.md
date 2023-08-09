# Roblox-Gate-V1
Thank you for checking out this gate system. I appreciate everyones support during this road of learning Roblox LUA. 
This gate system allows a player to use the keypad and execute a remote event to animate the opening of the gate. 

Check out the YouTube video below to setup the rest. Thank you! 

https://www.youtube.com/watch?v=c6hQ5WCwBhc&t=36s 

--------------------------------------------------------------------

Under Keypad, put this in as a Server Script:
```
local gate = script.Parent.Parent.Parent.Gate
local tween = game:GetService("TweenService")
local status = "Closed"
local prompt = script.Parent.ProximityPrompt
local setting = require(script.Parent.Config)

local tweeninfo = TweenInfo.new(5)
local open = {}
open.Position = setting.GateOpenedPos
local closed = {}
closed.Position = setting.GateClosedPos



local tween1 = tween:Create(gate,tweeninfo,open)
prompt.Triggered:Connect(function(plr)
	local tween2 = tween:Create(gate,tweeninfo,closed)
	if status == "Closed" then
		if setting.GroupId == 0 and setting.Team == nil then
			print("nil")
			prompt.ActionText = "Opening..."
			tween1:Play()
			status = "Opened"
			prompt.ActionText = "Opened"
			wait(5)
			wait(setting.TimeOpen)
			prompt.ActionText = "Closing..."
			tween2:Play()
			wait(5)
			status = "Closed"
			prompt.ActionText = "Open Gate"
		else if plr:IsInGroup(setting.GroupId) or plr.Team == setting.Team then
				print("Group or Team")
				prompt.ActionText = "Opening..."
				tween1:Play()
				status = "Opened"
				prompt.ActionText = "Opened"
				wait(5)
				wait(setting.TimeOpen)
				prompt.ActionText = "Closing..."
				tween2:Play()
				wait(5)
				status = "Closed"
				prompt.ActionText = "Open Gate"
			end
		end
		
	end
end)
```
-------------------------------------------------
In a Module Script, put the following code. 
```
local setting = {}

setting.GateOpenedPos = Vector3.new(-11.7, 4.8, 10.25) -- Change to the opened position of the gate
setting.GateClosedPos = Vector3.new(4.3, 4.8, 10.25)
setting.TimeOpen = 5 -- the amount of time the gate will stay opened before closing
setting.GroupId = nil -- set this to your group id if it requires to be in a group to open
setting.Team = nil -- set this to game.Teams.TEAMNAMEHERE if it requires a team

return setting
```
---------------------------------------------------

⚠️ **REAM ME** ⚠️
> It is aware that some of you are having issues with the positions of the gate. Make sure you are putting the gate where the opened position will be, copy the coordinates from the position tab in properties of the gate model. Do the same for the closed position as well. It must look like the position in the setting module script.

If this video helped you, please like and subscribe! 

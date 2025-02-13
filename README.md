# Roblox Exploiters and Terms of Service/Community Standards Violators List 
> A list of users which violates the rules of roblox (that can be considered serious violations) so you can prevent them from joining your Roblox Game

# Reports and Appeals
**Before requesting for a user to be added onto the list, it's suggested that you use Roblox's Reporting Features, if you're in the EU, you can visit https://www.roblox.com/illegal-content-reporting and afterwards report the user to roblox there (EU Reports have a higher chance to be accepted than regular roblox reports).**

You can report and appeal in the [![Discord](https://img.shields.io/badge/Discord-black.svg?logo=Discord&logoColor=white)](https://discord.gg/U7JstgHdyg) Server.

**Users are ONLY added if they actually broke the rules. Reports and appeals are carefully read if it's a legitimate report/appeal.**

**Terminated users are likely to be removed from the list. If a user was terminated but has been unterminated and was in the list, you can request for them to be readded.**

# General information
This is a list with UserId(s), Roblox UserId(s) are PUBLIC INFORMATION.

This list is made for Roblox Games to use it.

> This is to let you know what would count as a violation (not all is listed)

1. Child endangerment
2. Exploiting (using third-party software to tamper with Roblox)
3. Excessive Toxicity (Bullying, Harassment, Threats)
4. Harmful misinformation
5. Scamming
8. False reasons onto a game ban that can negatively impact the person (4, several other violations are required for this to be added as one)

Every once in awhile or so, the status's of the users in the list will be checked (including Bio ("About me") for harmful content), additionally, their friends Bios ("About me") may aswell be checked for harmful content. To the providers of the services that are used to check, a header named "X-FriendChecker" alongside "X-Checker" is provided.

Also works with https://github.com/adudu21isme/banwavedeveloperconsolescript

# Usage
> These are examples. The game must have HTTP Requests Enabled.
## Fetch list
> Outputs the list.
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users"))
```
## Prevent players in the list from joining
> It's recommended to use Parallel Luau to create the list and check if a user is in it, [parallel luau example](https://github.com/user-attachments/files/18776796/rbxrulebreakers.txt) (change the file extension to rbxm as github doesn't officially support rbxm format).

```luau
--// Services
local http = game:GetService("HttpService")
local plrs = game:GetService("Players")

--// Vars
local fetching = nil
local list = nil

--// Functions

-- Fetches the latest list of https://github.com/adudu21isme/rbxrulebreakers
@native
local function FetchList()
   if fetching then while task.wait(1) do if not fetching then return end end end
   fetching=true
   local s,r,t=nil,nil,3
   repeat
      s,r=pcall(function()
         return http:GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users",true)
      end)
      if not s then
         if string.find(r,"exceeded") then warn("⚠️RBX RATELIMIT. Waiting 30sec...")task.wait(30)else t=-1 task.wait(1)end
      end
   until s or t == 0
   task.desynchronize()
   if s then list=string.split(r,",")end
   fetching=nil
   task.synchronize()
end

-- Checks if the user is on the list
@native
local function IsOnList(id)
   task.desynchronize()
   local l=list and table.find(list,tostring(id))
   task.synchronize()
   return l
end

--// When new players join
plrs.PlayerAdded:Connect(function(p)
   local id = p.UserId
   --// Is User on list? Put this somewhere that its ok if the code yields
   if not list then FetchList()end
   if IsOnList(id) then
      --// Kick the rule breaker from the game
      return p:Kick([[Violations of Roblox ToS ("Terms of Service")/Community Standards or causing false bans to users in popular games that harm the victim.

Banning adudu21 from your game will not remove you from the list and will not improve your ego.

You can appeal by going to adudu21isme/rbxrulebreakers on GitHub then afterwards joining the Discord Server, if appeal is accepted. you will be allowed to play again in approximately 24 hours.]])
   end
end)

--// Update list cache every day (24 hours, 86400 seconds total)
task.spawn(function()
   while task.wait(86400) do
      FetchList()
   end
end)
```

# Games that use this list:
> If you want your game added here, please message [adudu21](https://github.com/adudu21isme) via Discord for fastest response.

https://www.roblox.com/games/17276569867/Push-a-Friend-2-Player-Obby

https://www.roblox.com/games/15605594861/Silly-Donations

https://www.roblox.com/games/117151318136398/UGC-Tycoon

https://www.roblox.com/games/93094304529125/Gift-Tycoon

https://www.roblox.com/games/84949966061623/5-robux-5-noob

# This repository is created for informational, educational, moderation, and safety purposes only. This repository is not intended to target, harass or bully any individual mentioned. We strongly condemn harassment, bullying, raiding and any form of online misconduct. Users are reminded to engage respectfully and responsibly.

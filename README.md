# Roblox Exploiters and Terms of Service/Community Standards Violators List 
> A list of users which violates the rules of roblox so you can prevent them from joining your Roblox Game

# Reports and Appeals
Report users by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?template=user_report.yaml)

Appeal by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?template=appeal.yaml) (depending on Severity and Context, your appeal may be denied.)

**Terminated users may be removed from the list. If a user was terminated but has been unterminated and was on the list, you can request for them to be readded.**

# General information
> This is to let you know what would count as a violation (not all is listed)

1. Endangerment of users that are not an adult.
2. Exploiting (using third-party software to tamper with Roblox)
3. Excessive Toxicity (Bullying, Harassment, Threats)
4. Harmful misinformation
5. Scamming
8. False reasons onto a game ban that can negatively impact the person (4)

# Usage
> These are examples. The game must have HTTP Requests Enabled.
## Fetch list
> Outputs the list.
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users"))
```
## Prevent players in the list from joining
> BanAsync only works in Roblox Servers and if it is enabled (via Players).
```luau
--// Services
local plrs = game:GetService("Players")
local http = game:GetService("HttpService")

--// Vars
local fetching = nil
local list = nil

--// Functions

-- Fetches the latest list at https://github.com/adudu21isme/rbxrulebreakers
local function FetchList()
   if fetching then while task.wait(1) do if not fetching then return end end end
   fetching=true
   local s,r,t=nil,nil,3
   repeat
      s,r=pcall(function()
         return http:GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users",true)
      end)
      if not s then
         if string.find(r,"exceeded") then warn("⚠️RBX RATELIMIT. Waiting 60sec...")task.wait(60)else t=-1 task.wait(1)end
      end
   until s or t == 0
   if s then list=string.split(r,",")end
   fetching=nil
end

--// When new players join
plrs.PlayerAdded:Connect(function(p)
   local id = p.UserId
   --// Is User on list? Put this somewhere that its ok if the code yields
   if not list then FetchList()end
   if list and table.find(list,tostring(id)) then
      --// Use BanAsync on the exploiter (offender)
      local s,r,t = nil,nil,2
      repeat
         s,r = pcall(function()
            return plrs:BanAsync({UserIds={id},Duration=-1,DisplayReason=[[Violations of Roblox ToS ("Terms of Service")/Community Standards or causing false bans to users in popular games that harm the victim.

Banning adudu21 from your game will not remove you from the list and will not improve your ego.

You can appeal at adudu21isme/rbxrulebreakers on GitHub, if appeal is accepted. contact the admins of this game to be unbanned.

PERMANENT BAN]],PrivateReason=`@{p.Name} has violated the Roblox ToS ("Terms of Service")/Community Standards or such. More information at https://github.com/adudu21isme/rbxrulebreakers`,ExcludeAltAccounts=false,ApplyToUniverse=true})  
         end)
         if not s then
            t-=1 
            task.wait(0.5)
         end
      until s or t==0
      return p:Kick([[Violations of Roblox ToS ("Terms of Service")/Community Standards or causing false bans to users in popular games that harm the victim.

Banning adudu21 from your game will not remove you from the list and will not improve your ego.

You can appeal at adudu21isme/rbxrulebreakers on GitHub, if appeal is accepted. contact the admins of this game to be able to play.

KICKED]])
   end
end)

--// Update list cache every hour
task.spawn(function()
   while task.wait(3600) do
      FetchList()
   end
end)
```

# Games that use this list:
> If you want your game added here, please message [adudu21](https://github.com/adudu21isme) via Discord for fastest response.

**💰💰💰 If you find this useful, you can Donate me Robux https://www.roblox.com/catalog?CreatorName=adudu21 (buy a T-Shirt or such, if you want to donate multiple times, go to the t-shirt you wish to purchase again, click the three dots next to the name of it and click "Delete from Inventory" then refresh page.)**

https://www.roblox.com/games/17276569867/Push-a-Friend-2-Player-Obby

https://www.roblox.com/games/15605594861/Silly-Donations

https://www.roblox.com/games/117151318136398/UGC-Tycoon

https://www.roblox.com/games/93094304529125/Gift-Tycoon

https://www.roblox.com/games/84949966061623/5-robux-5-noob

# Github Compliance: This repository is created for informational, educational, and safety purposes only. This repository is not intended to target, harass or bully any individual mentioned. We strongly condemn harassment, bullying, raiding and any form of online misconduct. Users are reminded to engage respectfully and responsibly.

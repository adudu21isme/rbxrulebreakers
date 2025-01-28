# Roblox Exploiters and Terms of Service/Community Standards Violators List 

# Reports and Appeals
Report users by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=Report&projects=&template=user_report.yaml&title=%5BREPORT%5D+)

Appeal by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=List+Appeal&projects=&template=appeal.yaml&title=%5BAPPEAL%5D+) (depending on Severity and Context, your appeal may be denied.)

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
# 💰💰💰 If you find this useful, you can Donate me Robux https://www.roblox.com/catalog?CreatorName=adudu21 (buy a T-Shirt or such, if you want to donate multiple times, go to the t-shirt you wish to purchase again, click the three dots next to the name of it and click "Delete from Inventory" then refresh page.

# Games that use this list:
> If you want your game added here, please message [adudu21](https://github.com/adudu21isme) via Discord for fastest response.

https://www.roblox.com/games/17276569867/Push-a-Friend-2-Player-Obby

https://www.roblox.com/games/15605594861/Silly-Donations

https://www.roblox.com/games/117151318136398/UGC-Tycoon

https://www.roblox.com/games/93094304529125/Gift-Tycoon

https://www.roblox.com/games/84949966061623/5-robux-5-noob

## Why was zenuux added?
**⚠️ i am thinking about readding Zenuux onto the list for his malicious toxic behavior but if you dont want a person with an ego from what i see, you can manually ban them from your game. (i'll further investigate soon)**
### Original: Message To Zenuux
This is to let you know why you originally added onto the "list" of rule breakers but have been removed since then.

For reference, you are no longer on the list.

The reason why you originally were added is because some of the ban reasons within the ban of Vescorps (duran_savgealt) when asked for proof, was not given even tho lots of people asked, such as stealing other assets (when people asked, you kept saying "none of your business", i believe these allegations could be considered serious in terms of game development).

That caused reasonable suspious of "Adding false reasons onto a ban" offense however this offense has been completely removed and replaced with "Adding false reasons onto a Roblox Game Ban will no longer be considered a violation or serious unless it is harming the person."

These are from my Point Of View, if i am incorrect you may let me know (or not).

I don't play PLS Donate often so this is just a message to let you know.

@adudu21 1/15/2025

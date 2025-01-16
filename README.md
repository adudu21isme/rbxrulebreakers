# Roblox Exploiters and Terms Of Service (Rules) Violators List 
**This is a list of confirmed roblox exploiters and TOS-Breakers (only serious TOS violations are considered).**

# Information

A Serious TOS-Breaker is a user which violates rules of roblox that can be considered serious.

Report users by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=Report&projects=&template=user_report.yaml&title=%5BREPORT%5D+)

Appeal by [clicking here.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=List+Appeal&projects=&template=appeal.yaml&title=%5BAPPEAL%5D+) (depending on Severity and Context, your appeal may be denied.)

**Users are manually added. Terminated users may be removed from the list. If a user was terminated but has been unterminated and was on the list or deserves to be readded, you can submit a report.**

# General rules
> This is to let you know what would count as a violation (not all is listed)

1. Endangerment of users that are not an adult.
2. Exploiting (using third-party software to tamper with Roblox)
3. Toxicity (Bullying, Harassment, Threats)
4. Harmful misinformation
5. Scamming
8. False reasons onto a game ban that can negatively impact the person (4)

# Using in roblox
> These are examples. The game must have HTTP Requests Enabled.
## Fetch list
> Outputs the list.
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users"))
```
## Prevent players in the list from joining
> BanAsync only works in Roblox Servers.
```luau
--// Services
local plrs = game:GetService("Players")
local http = game:GetService("HttpService")

--// Vars
local fetching = nil
local list = nil

--// Functions

-- Fetches the latest list of https://github.com/adudu21isme/rbxrulebreakers
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
      local s,r,t = nil,nil,3
      repeat
         s,r = pcall(function()
            return plrs:BanAsync({UserIds={id},Duration=-1,DisplayReason=[[Exploiting or Violation of Roblox TOS ("Terms Of Service") or the rules ("Community Standards").
You may request to be removed from the list at adudu21's Roblox-Rule-Breakers.]],PrivateReason=[[Violated Roblox Terms Of Service, Community Standards or used Cheats ("Exploits") in other roblox games. Full list at https://github.com/adudu21isme/rbxrulebreakers]],ExcludeAltAccounts=false,ApplyToUniverse=true})  
         end)
         if not s then
            t-=1 
            task.wait(0.5)
         end
      until s or t==0
      return p:Kick("Exploiting or Violation of Serious Roblox Terms Of Service in other roblox games.")
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

https://www.roblox.com/games/17276569867/Push-a-Friend-2-Player-Obby

https://www.roblox.com/games/15605594861/Silly-Donations

https://www.roblox.com/games/117151318136398/UGC-Tycoon

https://www.roblox.com/games/93094304529125/Gift-Tycoon

https://www.roblox.com/games/84949966061623/5-robux-5-noob

## Why was zenuux added?
**⚠️ i am reconsidering readding him onto the list for his malicious toxic behavior but if you dont want a person with a ego from what i see, you can manually ban them from your game.**
### Original: Message To Zenuux
This is to let you know why you originally added onto the "list" of rule breakers but have been removed since then.

For reference, you are no longer on the list.

The reason why you originally were added is because some of the ban reasons within the ban of Vescorps (duran_savgealt) when asked for proof, was not given even tho lots of people asked, such as stealing other assets (when people asked, you kept saying "none of your business", i believe these allegations could be considered serious in terms of game development).

That caused reasonable suspious of "Adding false reasons onto a ban" offense however this offense has been completely removed and replaced with "Adding false reasons onto a Roblox Game Ban will no longer be considered a violation or serious unless it is harming the person."

These are from my Point Of View, if i am incorrect you may let me know (or not).

I don't play PLS Donate often so this is just a message to let you know the next time you play.

@adudu21 1/15/2025

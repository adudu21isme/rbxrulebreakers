# Roblox Exploiters and Terms Of Service Violators List 
**This is a list of confirmed roblox exploiters and TOS-Breakers (only serious TOS violations are counted).**

A Serious TOS-Breaker is a user which violates rules of roblox that can be considered serious, such as but not limited to;
1. NSFW/NSFL (Inappropriate actions such as but not limited to adult content and graphic content, unappealable.)
2. Content Stealing (Intentionally stealing assets of other roblox games, unappealable.)
3. Maliciously DMCA'ing assets/games (False DMCA. Maliciously is when the user DMCA'ing does not have copyright over the content, unappealable.)
4. Scamming (unappealable.)
5. Death threats (unappealable.)
6. Exploiting (unappealable.)
7. illegal Activities (Depends on severity)

If you want a Serious TOS-Breaker or Exploiter to be added onto the list, [create a issue.](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=report&projects=&template=user-report.md&title=%5BUSER+REPORT%5D)

**Users are manually added. Terminated users may be removed**

**If you don't trust this, don't use it. For users to be added, they must be proven guilty.**

Made to also work with https://github.com/adudu21isme/banwavedeveloperconsolescript

[Click me if you want to ban 6K+ potential exploiters](https://github.com/adudu21isme/groupbanwavedeveloperconsolescript)

# Using in roblox (examples):

## To fetch list
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users"))
```
## To prevent players on the list from joining (Note that BanAsync only works in roblox servers):
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

--// Update list cache every minute
task.spawn(function()
   while task.wait(3600) do
      FetchList()
   end
end)

--// When new players join
plrs.PlayerAdded:Connect(function(p)
   local id = p.UserId
   --// Is user on list? Put this somewhere that its ok if the code yields
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
```

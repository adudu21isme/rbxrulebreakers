# Roblox Terms Of Service Violators and Exploiters List 
**This is a list of confirmed roblox exploiters and TOS breakers (only serious TOS violations are counted).**

If you want a TOS-Breaker or Exploiter to be added onto the list, [create a issue](https://github.com/adudu21isme/rbxrulebreakers/issues/new?assignees=adudu21isme&labels=report&projects=&template=user-report.md&title=%5BUSER+REPORT%5D)

**Users are manually added**

Made to also work with https://github.com/adudu21isme/banwavedeveloperconsolescript

# Using in roblox:

## To fetch list
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users"))
```
## To prevent players on list from joining (Note that BanAsync only works in roblox servers):
```luau
--// Services
local plrs = game:GetService("Players")
local http = game:GetService("HttpService")

--// Vars
local list = nil

--// Functions
local function StringToTable(input)
   input=input:match("%{(.*)%}")
   local t = {}
   for v in input:gmatch("[^,]+") do table.insert(t,tonumber(v) or v)end
   return t
end

local function FetchList()
   local s,r,t=nil,nil,3
   repeat
      s,r=pcall(function()
         return http:GetAsync("https://raw.githubusercontent.com/adudu21isme/rbxrulebreakers/refs/heads/main/users",true)
      end)
      if not s then
         t-=1
         warn(`❌Failed fetching exploiter list: {tostring(r)}`)
         task.wait(0.5)
      end
   until s or t == 0
   if s then list=StringToTable(r) end
end

--// Update list cache every minute
task.spawn(function()
   while task.wait(60) do
      FetchList()
   end
end)

--// When new players join
plrs.PlayerAdded:Connect(function(p)
   local id = p.UserId
   --// Is user on list? Put this somewhere that its ok if the code yields
   if not list then FetchList()end
   if list and table.find(list,id) then
      --// Use BanAsync on the exploiter (offender)
      local s,r,t = nil,nil,3
      repeat
         s,r = pcall(function()
            return plrs:BanAsync({UserIds={id},Duration=-1,DisplayReason="Exploiting or violating serious roblox rules is not permitted.",PrivateReason="User exploited in other roblox games or violated serious roblox rules (TOS). DO NOT UNBAN THIS USER. View the list here: https://github.com/adudu21isme/exploiterlist",ExcludeAltAccounts=false,ApplyToUniverse=true})  
         end)
         if not s then
            if string.find(r,"NOT_FOUND") then --// Avoid errors from terminated users
               s="t"
            else t-=1 task.wait(0.5)
            end
         end
      until s or t==0   
   end
end)
```

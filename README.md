# Do not currently use this, i am trying to make a API for this.

# Roblox Exploiter (Cheater) List
**This list may update at any time, this is a list of confirmed roblox exploiters that i wanted to be added onto a list.**

If you want a exploiter to be added onto the list, create a pull request; including their userid and evidence

**Users are manually added**

Made to work with https://github.com/adudu21isme/banwavedeveloperconsolescript

# Using in roblox:

## To fetch list
```luau
print(game:GetService("HttpService"):GetAsync("https://rbxexploiterlist.vercel.app/users"))
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
   for value in input:gmatch("[^,]+") do table.insert(t,tonumber(value) or value)end
   return t
end

local function FetchList()
   local s,r,t=nil,nil,3
   repeat
      s,r=pcall(function()
         return http:GetAsync("https://rbxexploiterlist.vercel.app/users",true)
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
            return plrs:BanAsync({UserIds={id},Duration=-1,DisplayReason="Exploiting is not permitted.",PrivateReason="User has used exploits in other roblox games. https://github.com/adudu21isme/exploiterlist",ExcludeAltAccounts=false,ApplyToUniverse=true})  
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

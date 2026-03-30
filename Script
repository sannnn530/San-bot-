local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")

local LocalPlayer = Players.LocalPlayer
local CurrentTheme = _G.SanTheme or "Default"

-- // WINDOW CONFIGURATION
local Window = Rayfield:CreateWindow({
   Name = "SAN HUB V17 | TITANIUM V62",
   LoadingTitle = "Initializing SAN HUB...",
   LoadingSubtitle = "Welcome, " .. LocalPlayer.DisplayName,
   Theme = CurrentTheme,
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "SanHubV17",
      FileName = "MainConfig"
   }
})

-- // WELCOME NOTIFICATIONS
Rayfield:Notify({
    Title = "Successfully Loaded!",
    Content = "Welcome back, " .. LocalPlayer.Name .. "!",
    Duration = 5,
    Image = 4483345998, -- Checkmark icon
})

-- // [🏠 HOME - T0] NEW LANDING TAB
local TabH = Window:CreateTab("🏠 HOME", "home")
TabH:CreateSection("User Dashboard")

TabH:CreateParagraph({
    Title = "Hello, " .. LocalPlayer.DisplayName .. "!", 
    Content = "Current Version: V17 (Titanium V62)\nStatus: Undetected\nAccount Age: " .. LocalPlayer.AccountAge .. " days"
})

TabH:CreateSection("Change Log")
TabH:CreateLabel("• Added Welcome System")
TabH:CreateLabel("• Improved ScriptBlox Fetching")
TabH:CreateLabel("• Added Home Dashboard")

-- Global execution function
local function run(url) 
    local success, err = pcall(function()
        loadstring(game:HttpGet(url))()
    end)
    if not success then 
        Rayfield:Notify({Title = "Execution Error", Content = "Failed to load script.", Duration = 3})
        warn(err) 
    end
end

-- // [🎮 GMS - T1] GAME SCRIPTS
local TabG = Window:CreateTab("🎮 GMS", "gamepad")
TabG:CreateSection("Popular Scripts")

local scripts = {
    ["Vape Voidware"] = "https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/nightsintheforest.lua",
    ["Thai 99 Night"] = "https://raw.githubusercontent.com/MQPS7/99-Night-in-the-Forset/refs/heads/main/99Nightv1",
    ["San Waypoint TP"] = "https://raw.githubusercontent.com/sannnn530/San/refs/heads/main/Bank/Buy/Huh/%3A",
    ["Infinite Yield"] = "https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"
}

for name, url in pairs(scripts) do
    TabG:CreateButton({
        Name = name, 
        Callback = function() run(url) end
    })
end

-- // [👁️ VIS - T2] VISUALS
local TabV = Window:CreateTab("👁️ VIS", "eye")
TabV:CreateSection("Visual Enhancements")

TabV:CreateButton({
    Name = "Universal ESP", 
    Callback = function() 
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Exunys-ESP/main/src/ESP.lua"))()() 
    end
})

TabV:CreateToggle({
    Name = "Fullbright", 
    CurrentValue = false, 
    Callback = function(v) 
        Lighting.Brightness = v and 2 or 1 
        Lighting.GlobalShadows = not v 
        Lighting.ClockTime = v and 12 or Lighting.ClockTime
    end
})

-- // [🔍 FND - T3] SCRIPT FINDER
local TabF = Window:CreateTab("🔍 FND", "search")
TabF:CreateSection("ScriptBlox Searcher")

local SelectedCode = ""
local ScriptList = {}
local SearchInp = ""

local Drop = TabF:CreateDropdown({
    Name = "Results", 
    Options = {"Search something first..."}, 
    CurrentOption = {"..."}, 
    Callback = function(o) 
        SelectedCode = ScriptList[o[1]] or ""
        Rayfield:Notify({Title = "Ready to Execute", Content = "Click 'Execute Search Result' in the EXE tab.", Duration = 3})
    end
})

TabF:CreateInput({
    Name = "Search ScriptBlox", 
    PlaceholderText = "e.g. Doors, Pet Sim...",
    Callback = function(t) SearchInp = t end
})

TabF:CreateButton({
    Name = "Fetch Scripts", 
    Callback = function()
        if SearchInp == "" then return end
        local url = "https://scriptblox.com/api/script/search?q=" .. HttpService:UrlEncode(SearchInp) .. "&max=10&mode=free"
        local s, res = pcall(function() return game:HttpGet(url) end)
        
        if s then
            local data = HttpService:JSONDecode(res)
            local names = {}
            ScriptList = {} 
            
            for _, sObj in pairs(data.result.scripts) do 
                table.insert(names, sObj.title) 
                ScriptList[sObj.title] = sObj.script 
            end
            
            Drop:Refresh(names, true)
            Rayfield:Notify({Title = "Search Successful", Content = "Found " .. #names .. " matches.", Duration = 3})
        else
            Rayfield:Notify({Title = "Error", Content = "API connection failed.", Duration = 3})
        end
    end
})

-- // [📝 EXE - T4] EXECUTOR
local TabE = Window:CreateTab("📝 EXE", "terminal")
TabE:CreateSection("Internal Executor")

local EditorInput = ""
TabE:CreateInput({
    Name = "Code Editor", 
    RemoveTextAfterFocusLost = false, 
    PlaceholderText = "Paste Lua code here...",
    Callback = function(t) EditorInput = t end
})

TabE:CreateButton({
    Name = "🚀 Execute Search Result", 
    Callback = function() 
        if SelectedCode ~= "" then 
            local s, err = pcall(function() loadstring(SelectedCode)() end)
            if not s then warn(err) end
        end
    end
})

TabE:CreateButton({
    Name = "⚡ Execute Editor Code", 
    Callback = function() 
        if EditorInput ~= "" then 
            local s, err = pcall(function() loadstring(EditorInput)() end)
            if not s then warn(err) end
        end
    end
})

-- // [⚙️ UTL - T5] UTILITIES
local TabU = Window:CreateTab("⚙️ UTL", "settings")
TabU:CreateSection("Server & UI")

TabU:CreateButton({
    Name = "Server Hop", 
    Callback = function() 
        local ts = game:GetService("TeleportService")
        ts:Teleport(game.PlaceId, Players.LocalPlayer) 
    end
})

TabU:CreateButton({
    Name = "❌ Destroy Hub", 
    Callback = function() 
        Rayfield:Destroy() 
    end
})

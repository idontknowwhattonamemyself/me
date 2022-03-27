
getgenv().Illucheck = false;


local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/AikaV3rm/UiLib/master/Lib.lua')))()

local w = library:CreateWindow("Main") -- Creates the window

local b = w:CreateFolder("Trinket Farm") -- Creates the folder(U will put here your buttons,etc)



b:Button("esp Y = on H = off",function()
   game:GetService("Workspace").Gate.Lock:remove()
    for i,v in pairs(getconnections(game:GetService("ScriptContext").Error)) do 
        v:Disable()
    end
    
    if getgenv().ESPTOGGLE1 then 
        getgenv().ESPTOGGLE1 = nil
    end
    getgenv().ESPTOGGLE1 = true
    local ToggleKey = Enum.KeyCode.Y
    local HideCommonToggleKey = Enum.KeyCode.H
    local Meshes = {
        ["rbxassetid://16657069"] = "Money Bag",
        ["rbxassetid://5204409890"] = "Scroll",
        ["rbxassetid://2877143560"] = "Jewel",
        ["rbxassetid://2637545558"] = "Ring",
        ["rbxassetid://439102658"] = "Phoenix Feather",
        ["rbxassetid://13116112"] = "Goblet",
        ["rbxassetid://5196577540"] = "Amulet",
        ["rbxassetid://5204003946"] = "Goblet",
        ["rbxassetid://5204409890"] = "Scroll",
        ["rbxassetid://5196551436"] = "Amulet",
        ["rbxassetid://5196782997"] = "Old Ring",
        ["rbxassetid://%2016657069%20"] = "Money Bag",
        ["rbxassetid://%2060791940%20"] = "Scroll",
        ["rbxassetid://%202877143560%20"] = "Jewel",
        ["rbxassetid://%202637545558%20"] = "Ring",
        ["rbxassetid://%20439102658%20"] = "Phoenix Feather",
        ["rbxassetid://%2013116112%20"] = "Goblet",
        ["rbxassetid://%205196577540%20"] = "Amulet",
        ["rbxassetid://%205204003946%20"] = "Goblet",
        ["rbxassetid://%205204453430%20"] = "Scroll",
        ["rbxassetid://%205196782997%20"] = "Old Ring",
        ["rbxassetid://5196776695"] = "Ring",
        ["rbxassetid://%205196776695%20"] = "Ring",
    
    }
    
    local RefreshRate = 14 --In miliseconds, change if your laggy
    local wrksp = game:GetService("Workspace");
    local Camera = wrksp.CurrentCamera;
    local WTVP = Camera.WorldToViewportPoint;
    local IsDescendantOf = game.IsDescendantOf;
    local Vec2 = Vector2.new(0, 15);
    local strformat = string.format;
    
    
    function WTS(Position)
        local VP,bool = WTVP(Camera,Position)
        return Vector2.new(VP.x, VP.y),bool,VP.Z
    end
    
    function CreateESP(Character, Class)
        local LastRefresh = 0;
        if not Character then
            return
        end
        
        local PName = Character.Name;
        local Name = Drawing.new("Text")
        Name.Text = Character.Name;
        Name.Color = Color3.fromRGB(141, 255, 126)
        Name.Position = WTS(Character.Position);
        Name.Size = 18
        Name.Outline = true
        Name.Center = true
        Name.Visible = true
        Name.Font = 0
        local Bottom = Drawing.new("Text")
        Bottom.Color = Color3.fromRGB(192,192,192)
        Bottom.Position = WTS(Character.Position) + Vec2;
        Bottom.Size = 18
        Bottom.Outline = true
        Bottom.Center = true
        Bottom.Visible = true
        Bottom.Font = 0
        
        pcall(function()
            if Character.Parent:IsA("MeshPart") and Meshes[Character.Parent.MeshId]  then 
                Name.Text = tostring(Meshes[Character.Parent.MeshId]) 
            elseif Character.Parent:IsA("Part") and Character.Parent:FindFirstChildWhichIsA("SpecialMesh") and Meshes[Character.Parent:FindFirstChildWhichIsA("SpecialMesh").MeshId] then
                Name.Text = tostring(Meshes[Character.Parent:FindFirstChildWhichIsA("SpecialMesh").MeshId])
            elseif Character.Parent:IsA("Part") and Character.Parent:FindFirstChildWhichIsA("SpecialMesh") and Character.Parent:FindFirstChild("OrbParticle") then
                Name.Text = tostring("???")
            else
                Name.Text = tostring("Opal")
            end
        end)
    
        local Con;
        Con = game:GetService("RunService").RenderStepped:Connect(function() --Update if on screen.
            if (tick() - LastRefresh) > (RefreshRate / 1000) then
                LastRefresh = tick();
                if not IsDescendantOf(Character,workspace) and Name ~= nil and Bottom ~= nil then
                    Con:Disconnect();
                    Con = nil; 
                    Name:Remove()
                    Bottom:Remove()
                    return 
                end
                local HRPP = Character.Position;
                local Pos,Bool,Distance = WTS(HRPP);
                if Bool and getgenv().ESPTOGGLE1 then
                    Bottom.Text = strformat('[%d]',Distance)
                    Name.Position = Pos;
                    Bottom.Position = Pos + Vec2;
                    Name.Visible = true;
                    Bottom.Visible = true;
                else
                    Name.Visible = false;
                    Bottom.Visible = false;
                end
            end
        end)
    end

    
    
    for i,v in pairs(wrksp:GetChildren()) do 
        if v:IsA("MeshPart") or v:IsA("UnionOperation") or v:IsA("Part") then 
            for i2,v2 in pairs(v:GetDescendants()) do 
                if v2:IsA("ClickDetector") then 
                    CreateESP(v2.Parent)
                end
            end
        end
    end
    
    wrksp.ChildAdded:Connect(function(v)
        if v:IsA("MeshPart") or v:IsA("UnionOperation") or v:IsA("Part") then 
            for i2,v2 in pairs(v:GetDescendants()) do 
                if v2:IsA("ClickDetector") then 
                    CreateESP(v2.Parent)
                end
            end
        end
    end)


    game:GetService("UserInputService").InputBegan:Connect(function(inputObject, gameProcessed)
        if inputObject.KeyCode == ToggleKey then
            getgenv().ESPTOGGLE1 = true
        elseif inputObject.KeyCode == HideCommonToggleKey then
            getgenv().ESPTOGGLE1 = false
        end
    end)
end)
    b:Button("AutoPickUp",function()
    
loadstring(game:HttpGet("https://pastebin.com/raw/JarWyFnr", true))()
end)

local c = w:CreateFolder("Player")
 
c:Button("No Fall Damage",function()
game:GetService("Players").LocalPlayer.Character.FallDamage:FindFirstChild("RemoteFunction").Parent = Game:GetService("Workspace")
wait(.1)
game:GetService("Workspace").RemoteFunction:Destroy()
print("Success")
end)
c:Button("No Fire", function()
while true do wait(0)
local username = game:GetService("Players").LocalPlayer.Name
	for _, v in pairs(game:GetService("Workspace").AliveData:GetDescendants()) do
		if v.Name == username then
		    do
		        if v:FindFirstChild("Status"):FindFirstChild("Burn") then do
		            			local args = {
    [1] = 0
}
game:GetService("Players").LocalPlayer.Character.CharacterHandler.ClientHandler.Dash:FireServer(unpack(args))

		end
		end
end
end
end
end
end)
    c:Button("fly, U = on/off J = fast",function()
        loadstring(game:HttpGet("https://pastebin.com/raw/qZkK3ZXy", true))()

        end)
local d = w:CreateFolder("Misc")
d:Toggle("Illu Alert",function(bool)
    getgenv().Illucheck = bool
    while Illucheck == true
    do 
        wait(1)
    for i,v in pairs(game:GetService("Workspace").Alive:GetDescendants()) do
    if v.Name == "Observe" and v.ClassName == "Tool" then do
game.StarterGui:SetCore("SendNotification", {
Title = "Illu Spectating"; -- the title (ofc)
Text = "Yikes"; -- what the text says (ofc)
Duration = .2; -- how long the notification should in secounds
})
print("Checking For Illu")
end
end
end
end
end)
d:Button("Instant Reset", function()
game:GetService("Players").LocalPlayer.Character.Humanoid.Health = 0
end)
d:Button("Full Bright", function()
if not _G.FullBrightExecuted then
 
	_G.FullBrightEnabled = false
 
	_G.NormalLightingSettings = {
		Brightness = game:GetService("Lighting").Brightness,
		ClockTime = game:GetService("Lighting").ClockTime,
		FogEnd = game:GetService("Lighting").FogEnd,
		GlobalShadows = game:GetService("Lighting").GlobalShadows,
		Ambient = game:GetService("Lighting").Ambient
	}
 
	game:GetService("Lighting"):GetPropertyChangedSignal("Brightness"):Connect(function()
		if game:GetService("Lighting").Brightness ~= 1 and game:GetService("Lighting").Brightness ~= _G.NormalLightingSettings.Brightness then
			_G.NormalLightingSettings.Brightness = game:GetService("Lighting").Brightness
			if not _G.FullBrightEnabled then
				repeat
					wait()
				until _G.FullBrightEnabled
			end
			game:GetService("Lighting").Brightness = 1
		end
	end)
 
	game:GetService("Lighting"):GetPropertyChangedSignal("ClockTime"):Connect(function()
		if game:GetService("Lighting").ClockTime ~= 12 and game:GetService("Lighting").ClockTime ~= _G.NormalLightingSettings.ClockTime then
			_G.NormalLightingSettings.ClockTime = game:GetService("Lighting").ClockTime
			if not _G.FullBrightEnabled then
				repeat
					wait()
				until _G.FullBrightEnabled
			end
			game:GetService("Lighting").ClockTime = 12
		end
	end)
 
	game:GetService("Lighting"):GetPropertyChangedSignal("FogEnd"):Connect(function()
		if game:GetService("Lighting").FogEnd ~= 786543 and game:GetService("Lighting").FogEnd ~= _G.NormalLightingSettings.FogEnd then
			_G.NormalLightingSettings.FogEnd = game:GetService("Lighting").FogEnd
			if not _G.FullBrightEnabled then
				repeat
					wait()
				until _G.FullBrightEnabled
			end
			game:GetService("Lighting").FogEnd = 786543
		end
	end)
 
	game:GetService("Lighting"):GetPropertyChangedSignal("GlobalShadows"):Connect(function()
		if game:GetService("Lighting").GlobalShadows ~= false and game:GetService("Lighting").GlobalShadows ~= _G.NormalLightingSettings.GlobalShadows then
			_G.NormalLightingSettings.GlobalShadows = game:GetService("Lighting").GlobalShadows
			if not _G.FullBrightEnabled then
				repeat
					wait()
				until _G.FullBrightEnabled
			end
			game:GetService("Lighting").GlobalShadows = false
		end
	end)
 
	game:GetService("Lighting"):GetPropertyChangedSignal("Ambient"):Connect(function()
		if game:GetService("Lighting").Ambient ~= Color3.fromRGB(178, 178, 178) and game:GetService("Lighting").Ambient ~= _G.NormalLightingSettings.Ambient then
			_G.NormalLightingSettings.Ambient = game:GetService("Lighting").Ambient
			if not _G.FullBrightEnabled then
				repeat
					wait()
				until _G.FullBrightEnabled
			end
			game:GetService("Lighting").Ambient = Color3.fromRGB(178, 178, 178)
		end
	end)
 
	game:GetService("Lighting").Brightness = 1
	game:GetService("Lighting").ClockTime = 12
	game:GetService("Lighting").FogEnd = 786543
	game:GetService("Lighting").GlobalShadows = false
	game:GetService("Lighting").Ambient = Color3.fromRGB(178, 178, 178)
 
	local LatestValue = true
	spawn(function()
		repeat
			wait()
		until _G.FullBrightEnabled
		while wait() do
			if _G.FullBrightEnabled ~= LatestValue then
				if not _G.FullBrightEnabled then
					game:GetService("Lighting").Brightness = _G.NormalLightingSettings.Brightness
					game:GetService("Lighting").ClockTime = _G.NormalLightingSettings.ClockTime
					game:GetService("Lighting").FogEnd = _G.NormalLightingSettings.FogEnd
					game:GetService("Lighting").GlobalShadows = _G.NormalLightingSettings.GlobalShadows
					game:GetService("Lighting").Ambient = _G.NormalLightingSettings.Ambient
				else
					game:GetService("Lighting").Brightness = 1
					game:GetService("Lighting").ClockTime = 12
					game:GetService("Lighting").FogEnd = 786543
					game:GetService("Lighting").GlobalShadows = false
					game:GetService("Lighting").Ambient = Color3.fromRGB(178, 178, 178)
				end
				LatestValue = not LatestValue
			end
		end
	end)
end
 
_G.FullBrightExecuted = true
_G.FullBrightEnabled = not _G.FullBrightEnabled
end)
d:Button("Streamer Mode", function()
game:GetService("Players").LocalPlayer.PlayerGui.StatGui.Container.CharacterName:Remove()
game:GetService("Players").LocalPlayer.PlayerGui.LeaderboardGui:Remove()
end)
d:Button("No Kill Bricks",function()
    
game:GetService("Workspace").Map.KillBricks:remove()
end)
d:Button("Collector Notifier", function()
    loadstring:GameHttpGet("https://raw.githubusercontent.com/idontknowwhattonamemyself/me/Lua/collector%20notif")
end)
d:Button("Player Esp", function()
loadstring(game:HttpGet(('https://raw.githubusercontent.com/idontknowwhattonamemyself/esp/3732b716d791c7cd92c6aae59641f48990cde508/esp')))()
    end)
    
    
local f = library:CreateWindow("Talk To Npcs")   
  
local e = f:CreateFolder("Misc Npcs")
e:Button("Vamp food",function()
fireclickdetector(game:GetService("Workspace").NPCs.Misc.Jartavious.ClickDetector)
end)
e:Button("Dorgon",function()
fireclickdetector(game:GetService("Workspace").NPCs.Misc.Dorgon.ClickDetector)
end)
e:Button("Snap Trainer",function()
fireclickdetector(game:GetService("Workspace").NPCs.Misc.Quinno.ClickDetector)
end)
e:Button("Gate Trainer",function()
fireclickdetector(game:GetService("Workspace").NPCs.Misc.Adralik.ClickDetector)
end)
e:Button("Engineer",function()
fireclickdetector(game:GetService("Workspace").NPCs.Engineers.Engineer.ClickPart.ClickDetector)
end)
e:Button("Soul Snap",function()
fireclickdetector(game:GetService("Workspace").NPCs.Misc.SoulSnap.ClickDetector)
end)
e:Button("Therapist",function()
fireclickdetector(game:GetService("Workspace").NPCs.Therapist.ClickDetector)
end)

local f = f:CreateFolder("Class Npcs")
f:Button("Monk",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Isaac.ClickDetector)
end)
f:Button("Dragon Sage",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers["Ragash Al'vul"].ClickDetector)
end)

f:Button("Akuma",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Ethan.ClickDetector)
end)
f:Button("Oni",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers["Big Hoss"].ClickDetector)
end)

f:Button("Pit Fighter",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Cu.ClickDetector)
end)
f:Button("CK/DK",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.CK.ClickDetector)
end)
f:Button("Dragon Knight",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Tiger.ClickDetector)
end)
f:Button("Dragon Slayer",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Fang.ClickDetector)
end)
f:Button("Warrior",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Alfric.ClickDetector)
end)
f:Button("Greatsword",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Regnier.ClickDetector)
end)
f:Button("Abyss Walker",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Enibras.ClickDetector)
end)
f:Button("Templar",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Hiraeth.ClickDetector)
end)
f:Button("Lords Training",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Eliwood.ClickDetector)
end)
f:Button("Sigil Knight",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Frey.ClickDetector)
end)
f:Button("Ultra Sigil Knight",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Jagen.ClickDetector)
end)
f:Button("Dark Sigil Knight",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Eldin.ClickDetector)
end)
f:Button("Illusionist",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Sibyl.ClickDetector)
end)
f:Button("Theif",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Fabiana.ClickDetector)
end)
f:Button("Assassin",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Jafar.ClickDetector)
end)
f:Button("Faceless",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Knight.ClickDetector)
end)
f:Button("Shinobi",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Howl.ClickDetector)
end)
f:Button("Spy",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Drake.ClickDetector)
end)
f:Button("Whisperer",function()
fireclickdetector(game:GetService("Workspace").NPCs.Trainers.Rorschach.ClickDetector)
end)
e:Button("Sigil Helmet",function()
fireclickdetector(game:GetService("Workspace").Kyley.ClickDetector)
end)
e:Button("Castle Rock",function()
fireclickdetector(game:GetService("Workspace")["The Eagle"].ClickDetector)
end)

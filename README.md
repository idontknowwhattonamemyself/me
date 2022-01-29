

local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/AikaV3rm/UiLib/master/Lib.lua')))()

local w = library:CreateWindow("RLT Gui") -- Creates the window

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
    
    Player = game:GetService("Players").LocalPlayer 
game:GetService("Players").LocalPlayer.Character.FallDamage:remove()
end)
c:Button("Temperature Lock",function()
game:GetService("StarterGui").Main.AreaDetection.GetTemp:Remove()

end)

    c:Button("fly, U = on/off J = fast",function()
        loadstring(game:HttpGet("https://pastebin.com/raw/qZkK3ZXy", true))()

        end)
local d = w:CreateFolder("Misc")
d:Button("Esp",function()
local Box_Color = Color3.fromRGB(255, 0, 0)
local Tracer_Color = Color3.fromRGB(255, 0, 0)
local HealthBar_Color = Color3.fromRGB(0, 255, 0)

local Tracer_Thickness = 1
local Box_Thickness = 2

local teamcheck = {
    teamcheck = true,
    green = Color3.fromRGB(161, 242, 19),
    red = Color3.fromRGB(245, 69, 5)
}

--//Locals
local plr = game.Players.LocalPlayer
local camera = game.Workspace.CurrentCamera

local function NewQuad(thickness, color)
    local quad = Drawing.new("Quad")
    quad.Visible = false
    quad.PointA = Vector2.new(0,0)
    quad.PointB = Vector2.new(0,0)
    quad.PointC = Vector2.new(0,0)
    quad.PointD = Vector2.new(0,0)
    quad.Color = color
    quad.Filled = false
    quad.Thickness = thickness
    quad.Transparency = 1
    return quad
end

local function NewLine(thickness, color)
    local line = Drawing.new("Line")
    line.Visible = false
    line.From = Vector2.new(0, 0)
    line.To = Vector2.new(0, 0)
    line.Color = color
    line.Thickness = thickness
    line.Transparency = 1
    return line
end

local black = Color3.fromRGB(0, 0, 0)

for i, v in pairs(game.Players:GetChildren()) do
    local library = {
        --//Tracer and Black Tracer(black border)
        blacktracer = NewLine(Tracer_Thickness*2, black),
        tracer = NewLine(Tracer_Thickness, Tracer_Color),
        --//Box and Black Box(black border)
        black = NewQuad(Box_Thickness*2, black),
        box = NewQuad(Box_Thickness, Box_Color),
        --//Bar and Green Health Bar (part that moves up/down)
        healthbar = NewLine(8, black),
        greenhealth = NewLine(4, HealthBar_Color)
    }

    local function Visibility(state)
        for u, x in pairs(library) do
            x.Visible = state
        end
    end

    local function ESP()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if v.Character ~= nil and v.Character:FindFirstChild("Humanoid") ~= nil and v.Character:FindFirstChild("HumanoidRootPart") ~= nil and v.Name ~= plr.Name and v.Character.Humanoid.Health > 0 and v.Character:FindFirstChild("Head") ~= nil then
                local ScreenPos, OnScreen = camera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)
                if OnScreen then
                    local head = camera:WorldToViewportPoint(v.Character.Head.Position)
                    local rootpos = camera:WorldToViewportPoint(v.Character.HumanoidRootPart.Position)

                    local ratio = math.clamp((Vector2.new(head.X, head.Y) - Vector2.new(rootpos.X, rootpos.Y)).magnitude, 2, math.huge)

                    local head2 = camera:WorldToViewportPoint(Vector3.new(v.Character.Head.Position.X, v.Character.Head.Position.Y + 2, v.Character.Head.Position.Z))

                    local root2 = camera:WorldToViewportPoint(Vector3.new(v.Character.Head.Position.X, v.Character.HumanoidRootPart.Position.Y - 3, v.Character.Head.Position.Z))

                    library.black.PointA = Vector2.new(head2.X + ratio*1.6, head2.Y - ratio*0.05)
                    library.black.PointB = Vector2.new(head2.X - ratio*1.6, head2.Y - ratio*0.05)
                    library.black.PointC = Vector2.new(head2.X - ratio*1.6, root2.Y + ratio*0.5)
                    library.black.PointD = Vector2.new(head2.X + ratio*1.6, root2.Y + ratio*0.5)

                    library.box.PointA = Vector2.new(head2.X + ratio*1.6, head2.Y - ratio*0.05)
                    library.box.PointB = Vector2.new(head2.X - ratio*1.6, head2.Y - ratio*0.05)
                    library.box.PointC = Vector2.new(head2.X - ratio*1.6, root2.Y + ratio*0.5)
                    library.box.PointD = Vector2.new(head2.X + ratio*1.6, root2.Y + ratio*0.5)

                    library.tracer.To = Vector2.new(root2.X, root2.Y + ratio*0.5)
                    library.tracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y)

                    library.blacktracer.To = Vector2.new(root2.X, root2.Y + ratio*0.5)
                    library.blacktracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y)

                    local d = (Vector2.new(head2.X - ratio*1.8, head2.Y - ratio*0.05) - Vector2.new(root2.X - ratio*1.8, root2.Y + ratio*0.5)).magnitude
                    local green = (100-v.Character.Humanoid.Health) *d /100

                    library.greenhealth.Thickness = math.clamp(ratio/4, 1, 4)
                    library.healthbar.Thickness = math.clamp(ratio * 1.2 / 4, 1.5, 6)

                    library.healthbar.To = Vector2.new(head2.X - ratio*1.8, head2.Y - ratio*0.05)
                    library.healthbar.From = Vector2.new(head2.X - ratio*1.8, root2.Y + ratio*0.5)

                    library.greenhealth.To = Vector2.new(head2.X - ratio*1.8, head2.Y + green - ratio*0.05)
                    library.greenhealth.From = Vector2.new(head2.X - ratio*1.8, root2.Y + ratio*0.5)

                    if teamcheck.teamcheck == true then
                        if v.TeamColor == plr.TeamColor then
                            library.box.Color = teamcheck.green
                            library.tracer.Color = teamcheck.green
                        else 
                            library.box.Color = teamcheck.red
                            library.tracer.Color = teamcheck.red
                        end
                    end

                    Visibility(true)
                else 
                    Visibility(false)
                end
            else 
                Visibility(false)
                if game.Players:FindFirstChild(v.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(ESP)()
end

game.Players.PlayerAdded:Connect(function(newplr) --Parameter gets the new player that has been added
    local library = {
        --//Tracer and Black Tracer(black border)
        blacktracer = NewLine(Tracer_Thickness*2, black),
        tracer = NewLine(Tracer_Thickness, Tracer_Color),
        --//Box and Black Box(black border)
        black = NewQuad(Box_Thickness*2, black),
        box = NewQuad(Box_Thickness, Box_Color),
        --//Bar and Green Health Bar (part that moves up/down)
        healthbar = NewLine(8, black),
        greenhealth = NewLine(4, HealthBar_Color)
    }

    local function Visibility(state)
        for u, x in pairs(library) do
            x.Visible = state
        end
    end

    local function ESP()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if newplr.Character ~= nil and newplr.Character:FindFirstChild("Humanoid") ~= nil and newplr.Character:FindFirstChild("HumanoidRootPart") ~= nil and newplr.Name ~= plr.Name and newplr.Character.Humanoid.Health > 0 and newplr.Character:FindFirstChild("Head") ~= nil then
                local ScreenPos, OnScreen = camera:WorldToViewportPoint(newplr.Character.HumanoidRootPart.Position)
                if OnScreen then
                    local head = camera:WorldToViewportPoint(newplr.Character.Head.Position)
                    local rootpos = camera:WorldToViewportPoint(newplr.Character.HumanoidRootPart.Position)

                    local ratio = math.clamp((Vector2.new(head.X, head.Y) - Vector2.new(rootpos.X, rootpos.Y)).magnitude, 2, math.huge)

                    local head2 = camera:WorldToViewportPoint(Vector3.new(newplr.Character.Head.Position.X, newplr.Character.Head.Position.Y + 2, newplr.Character.Head.Position.Z))

                    local root2 = camera:WorldToViewportPoint(Vector3.new(newplr.Character.Head.Position.X, newplr.Character.HumanoidRootPart.Position.Y - 3, newplr.Character.Head.Position.Z))

                    library.black.PointA = Vector2.new(head2.X + ratio*1.6, head2.Y - ratio*0.05)
                    library.black.PointB = Vector2.new(head2.X - ratio*1.6, head2.Y - ratio*0.05)
                    library.black.PointC = Vector2.new(head2.X - ratio*1.6, root2.Y + ratio*0.5)
                    library.black.PointD = Vector2.new(head2.X + ratio*1.6, root2.Y + ratio*0.5)

                    library.box.PointA = Vector2.new(head2.X + ratio*1.6, head2.Y - ratio*0.05)
                    library.box.PointB = Vector2.new(head2.X - ratio*1.6, head2.Y - ratio*0.05)
                    library.box.PointC = Vector2.new(head2.X - ratio*1.6, root2.Y + ratio*0.5)
                    library.box.PointD = Vector2.new(head2.X + ratio*1.6, root2.Y + ratio*0.5)

                    library.tracer.To = Vector2.new(root2.X, root2.Y + ratio*0.5)
                    library.tracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y)

                    library.blacktracer.To = Vector2.new(root2.X, root2.Y + ratio*0.5)
                    library.blacktracer.From = Vector2.new(camera.ViewportSize.X*0.5, camera.ViewportSize.Y)

                    local d = (Vector2.new(head2.X - ratio*1.8, head2.Y - ratio*0.05) - Vector2.new(root2.X - ratio*1.8, root2.Y + ratio*0.5)).magnitude
                    local green = (100-newplr.Character.Humanoid.Health) *d /100

                    library.greenhealth.Thickness = math.clamp(ratio/4, 1, 4)
                    library.healthbar.Thickness = math.clamp(ratio * 1.2 / 4, 1.5, 6)

                    library.healthbar.To = Vector2.new(head2.X - ratio*1.8, head2.Y - ratio*0.05)
                    library.healthbar.From = Vector2.new(head2.X - ratio*1.8, root2.Y + ratio*0.5)

                    library.greenhealth.To = Vector2.new(head2.X - ratio*1.8, head2.Y + green - ratio*0.05)
                    library.greenhealth.From = Vector2.new(head2.X - ratio*1.8, root2.Y + ratio*0.5)

                    if teamcheck.teamcheck == true then
                        if newplr.TeamColor == plr.TeamColor then
                            library.box.Color = teamcheck.green
                            library.tracer.Color = teamcheck.green
                        else 
                            library.box.Color = teamcheck.red
                            library.tracer.Color = teamcheck.red
                        end
                    end

                    Visibility(true)
                else 
                    Visibility(false)
                end
            else 
                Visibility(false)
                if game.Players:FindFirstChild(newplr.Name) == nil then
                    connection:Disconnect()
                end
            end
        end)
    end
    coroutine.wrap(ESP)()
end)
d:Button("No Kill Bricks",function()
    
game:GetService("Workspace").Map.KillBricks:remove()
end)

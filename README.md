local function getnamecall() -- u can add placeid detector with all namecalls & remotes if we want later on
    return "UpdateMousePos1"
end
 
 local namecalltype = getnamecall()
 
local function MainEventLocate()
    for _,v in pairs(game:GetService("ReplicatedStorage"):GetDescendants()) do
        if v.Name == "MainEvent" then
            return v
        end
    end
 end
 
 local mainevent = MainEventLocate()
 
 -- // Shorthand
 local uwuGult = getgenv().Gult
 local uwuMain = uwuGult.Options
 local uwuAimAssistMain = uwuGult.AimAssist.Main
 local uwuAimAssistFOV = uwuGult.AimAssist.FOV
 local uwuSilentAimMain = uwuGult.SilentAim.Main
 local uwuAntiGroundShots = uwuGult.SilentAim.AntiGroundShots
 local uwuAntiCurve = uwuGult.SilentAim.AntiCurve
 local uwuSilentAimFOV = uwuGult.SilentAim.FOV
 local uwuTrace = uwuGult.Snapline
 local uwuPingPred = uwuGult.PingPrediction
 local uwuFAG = uwuGult.WaterMark
 local uwuBLACKDICK = uwuGult.Visuals.DistanceESP
 local uwuHAHAHAHAH = uwuGult.Visuals.WeaponESP
 local uwuNIGGER = uwuGult.CFrame
 local uwuCUMCUMCUM = uwuGult.Extra.TrashTalk
 local uwuNIGGA = uwuGult.Visuals.HealthBar
 local uwuPENIS = uwuGult.Visuals.NameESP
 local uwuAHAAHAAHHAHAHA = uwuGult.Visuals.Radar
 local uwuAUFHAUYFGHYUFHFUHJ = uwuGult.Desync
 

 
 -- // Optimization
 local vect3 = Vector3.new
 local vect2 = Vector2.new
 local cnew = CFrame.new
 
 -- // Libraries
 local NotificationHolder = loadstring(game:HttpGet("https://raw.githubusercontent.com/BocusLuke/UI/main/STX/Module.Lua"))()
 local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/cloudtad9/daasddadsadadsad/main/adadassadasd"))()
 local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Consistt/Ui/main/UnLeaked"))()
 
 -- // Services
 local uis = game:GetService("UserInputService")
 local rs = game:GetService("RunService")
 local plrs = game:GetService("Players")
 local ws = game:GetService("Workspace")
 
 -- // Script Variables
 local CToggle = false
 local lplr = plrs.LocalPlayer
 local CTarget = nil
 local CPart = nil
 local SToggle = false
 local STarget = nil
 local SPart = nil
 
 -- // Client Variables
 local m = lplr:GetMouse()
 local c = ws.CurrentCamera
 
 local function SendNotification(text)
    Notification:Notify(
        {Title = "Gult - 战利品乐趣", Description = " "..text},
        {OutlineColor = Color3.fromRGB(255,255,255),Time = 2, Type = "image"},
        {Image = "http://www.roblox.com/asset/?id=6023426923", ImageColor = Color3.fromRGB(255,255,255)}
    )
 end 
 
 -- // Call notification function
 if uwuMain.Notifications then
    SendNotification("injecting Gult")
    wait(3.5)
    SendNotification("Gult.fun")
    wait(3.5)
    SendNotification("Start 2 tapping")
 end
 
 -- // Camlock FOV
 local AimAssistFOV = Drawing.new("Circle")
 AimAssistFOV.Visible = uwuAimAssistFOV.ShowFOV
 AimAssistFOV.Thickness = 1
 AimAssistFOV.NumSides = 30
 AimAssistFOV.Radius = uwuAimAssistFOV.Radius * 3
 AimAssistFOV.Color = uwuAimAssistFOV.Color
 AimAssistFOV.Filled = uwuAimAssistFOV.Filled
 AimAssistFOV.Transparency = uwuAimAssistFOV.Transparency
 
 --Silent FOV
 local SilentAimFOV = Drawing.new("Circle")
 SilentAimFOV.Visible = uwuSilentAimFOV.ShowFOV
 SilentAimFOV.Thickness = 1
 SilentAimFOV.NumSides = 30
 SilentAimFOV.Radius = uwuSilentAimFOV.Radius * 3
 SilentAimFOV.Color = uwuSilentAimFOV.Color
 SilentAimFOV.Filled = uwuSilentAimFOV.Filled
 SilentAimFOV.Transparency = uwuSilentAimFOV.Transparency
 
 --Tracer
 local Line = Drawing.new("Line")
 Line.Color = uwuTrace.Color
 Line.Transparency = uwuTrace.Transparency
 Line.Thickness = 1
 Line.Visible = uwuTrace.Visible
 
 -- // Script Functions
 local function uwuFindTawget() -- // Find target
    local d, t = math.huge, nil
    for _,v in pairs (plrs:GetPlayers()) do
        local _,os = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
        if v ~= lplr and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0 and v.Character:FindFirstChild("HumanoidRootPart") and os then
            local pos = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
            local magnitude = (vect2(pos.X, pos.Y) - vect2(m.X, m.Y + 36)).magnitude
            if magnitude < d then
                t = v
                d = magnitude
            end
        end
    end
    return t
 end
 
 local function uwuFindPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuAimAssistMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
 end
 
 local function uwuFindSilentPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuSilentAimMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
 end
 
 local function uwuCheckAnti(targ) -- // Anti-aim detection
    if (targ.Character.HumanoidRootPart.Velocity.Y < -5 and targ.Character.Humanoid:GetState() ~= Enum.HumanoidStateType.Freefall) or targ.Character.HumanoidRootPart.Velocity.Y < -50 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.X > 35 or targ.Character.HumanoidRootPart.Velocity.X < -35) then
        return true
    elseif targ and targ.Character.HumanoidRootPart.Velocity.Y > 60 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.Z > 35 or targ.Character.HumanoidRootPart.Velocity.Z < -35) then
        return true
    else
        return false
    end
 end
 
 local function InSilentRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        local pos = nil
        if not uwuCheckAnti(target) then
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
        else
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
        end
        local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
        if mag < fov * 3 then
            return true
        else
            return false
        end
    end
 end
 
 local function Silent()
    if STarget then
        if SPart and InSilentRadiuwus(STarget, uwuSilentAimMain, SilentAimFOV.Radius) then
            if not uwuCheckAnti(STarget) then
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + (STarget.Character[SPart].Velocity * uwuSilentAimMain.Prediction))
            else
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + ((STarget.Character.Humanoid.MoveDirection * STarget.Character.Humanoid.WalkSpeed) * uwuSilentAimMain.Prediction))
            end
        end
    end
 end
 
 
 local function InRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        if uwuAimAssistFOV.UseFOV then
            local pos = nil
            if not uwuCheckAnti(target) then
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
            else
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
            end
            local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
            if mag < fov * 3 then
                return true
            else
                return false
            end
        else
            return true
        end
    end
 end
 
 uis.InputBegan:Connect(function(k,t)
    if not t then
        if k.KeyCode == Enum.KeyCode[uwuAimAssistMain.Key:upper()] then
            if CTarget == nil then
            CToggle = true
            CTarget = uwuFindTawget()
            if uwuMain.Notifications then
                SendNotification("Aim Target "..CTarget.Name)
            end
       else
            if CToggle == true then
                CToggle = false
                CTarget = nil
                if uwuMain.Notifications then
                    SendNotification("Unlocked")
                end
            end
        end
        elseif k.KeyCode == Enum.KeyCode[uwuSilentAimMain.KeyBind:upper()] and uwuSilentAimMain.Mode == "Regular" then
            if SToggle then
                SToggle = false
                if uwuMain.Notifications then
                    SendNotification("silent disabled")
                end
            else
                SToggle = true
                if uwuMain.Notifications then
                    SendNotification("silent enabled")
                end
            end
        end
    end
end)
 
 rs.RenderStepped:Connect(function()
    if CTarget then
        CPart = uwuFindPart()
        local pos = nil
        local cum = nil
        if CTarget.Character.BodyEffects["K.O"].Value == true or lplr.Character.BodyEffects["K.O"].Value == true then
            CToggle = false
            CTarget = nil
        else
            if uwuAimAssistMain.Shake then
                if uwuAimAssistMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuAimAssistMain.Prediction + (vect3(
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                        ) * 0.1)
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuAimAssistMain.Prediction + (vect3(
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                            math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                        ) * 0.1))
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position + (vect3(
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue),
                        math.random(-uwuAimAssistMain.ShakeValue, uwuAimAssistMain.ShakeValue)
                    ) * 0.1)
                    pos = c:WorldToViewportPoint(cum)
                end
            else
                if uwuAimAssistMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuAimAssistMain.Prediction
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuAimAssistMain.Prediction)
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position
                    pos = c:WorldToViewportPoint(cum)
                end
            end
            if InRadiuwus(CTarget, uwuAimAssistMain, AimAssistFOV.Radius) then
                local main = nil
                if uwuAimAssistMain.SmoothLock then
                    main = cnew(c.CFrame.p, cum)
                    c.CFrame = c.CFrame:Lerp(main, uwuAimAssistMain.Smoothness, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
                else
                    c.CFrame = cnew(c.CFrame.p, cum)
                end
            end
            if uwuMain.FOVMode == "FollowMouse" then
                if uwuAimAssistFOV.ShowFOV then
                    AimAssistFOV.Position = vect2(m.X, m.Y + 36)
                end
                if uwuSilentAimFOV.ShowFOV then
                    SilentAimFOV.Position = vect2(m.X, m.Y + 36)
                end
            elseif uwuMain.FOVMode == "Sticky" then
                if uwuAimAssistFOV.ShowFOV then
                    AimAssistFOV.Position = vect2(pos.X, pos.Y)
                end
                if uwuSilentAimFOV.ShowFOV then
                    SilentAimFOV.Position = vect2(pos.X, pos.Y)
                end
            end
            if uwuTrace.Enabled then
                Line.Visible = true
                Line.From = vect2(m.X, m.Y + 36)
                Line.To = vect2(pos.X, pos.Y)
            end
        end
    else
        AimAssistFOV.Position = vect2(m.X, m.Y + 36)
        SilentAimFOV.Position = vect2(m.X, m.Y + 36)
        Line.Visible = false
    end
 end)
 
 lplr.Character.ChildAdded:Connect(function(tool)
    if tool:IsA("Tool") then
        tool.Activated:connect(function()
            if uwuSilentAimMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentAimMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end
 end)
 
 lplr.CharacterAdded:Connect(function(char)
    char.ChildAdded:Connect(function(tool)
        tool.Activated:connect(function()
            if uwuSilentAimMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentAimMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end)
 end)
 
 --Ping Prediction
 coroutine.resume(coroutine.create(function()
    while true do
        if uwuPingPred.Enabled then
            local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()
            if ping <= 40 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping30_40
            elseif ping <= 50 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping40_50
            elseif ping <= 60 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping50_60
            elseif ping <= 70 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping60_70
            elseif ping <= 80 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping70_80
            elseif ping <= 90 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping80_90
            elseif ping <= 100 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping90_100
            elseif ping <= 110 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping100_110
            elseif ping <= 120 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping110_120
            elseif ping <= 130 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping120_130
            elseif ping <= 140 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping130_140
            elseif ping <= 150 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping140_150
            elseif ping <= 160 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping150_160
            elseif ping <= 170 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping160_170
            elseif ping <= 180 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping170_180
            elseif ping <= 190 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping180_190
            elseif ping <= 200 then
                uwuSilentAimMain.Prediction = uwuPingPred.ping190_200
            end
            task.wait(0.7)
        end
    end
 end))

if uwuBLACKDICK == true then
    local c = workspace.CurrentCamera
    local ps = game:GetService("Players")
    local lp = ps.LocalPlayer
    local rs = game:GetService("RunService")
    
    local function getdistancefc(part)
        return (part.Position - c.CFrame.Position).Magnitude
    end
    
    local function esp(p,cr)
        local h = cr:WaitForChild("Humanoid")
        local hrp = cr:WaitForChild("LeftLowerLeg")
    
        local text = Drawing.new("Text")
        text.Visible = false
        text.Center = true 
        text.Outline = true 
        text.Font = 2
        text.Color = Color3.fromRGB(255,255,255)
        text.Size = 13
    
        local c1 
        local c2 
        local c3 
    
        local function dc()
            text.Visible = false
            text:Remove()
            if c1 then
                c1:Disconnect()
                c1 = nil 
            end
            if c2 then
                c2:Disconnect()
                c2 = nil 
            end
            if c3 then
                c3:Disconnect()
                c3 = nil 
            end
        end
    
        c2 = cr.AncestryChanged:Connect(function(_,parent)
            if not parent then
                dc()
            end
        end)
    
        c3 = h.HealthChanged:Connect(function(v)
            if (v<=0) or (h:GetState() == Enum.HumanoidStateType.Dead) then
                dc()
            end
        end)
    
        c1 = rs.RenderStepped:Connect(function()
            local hrp_pos,hrp_os = c:WorldToViewportPoint(hrp.Position)
            if hrp_os then
                text.Position = Vector2.new(hrp_pos.X,hrp_pos.Y)
                text.Text = '['..tostring(math.floor(getdistancefc(hrp)))..'m]'
                text.Visible = true 
            else
                text.Visible = false 
            end
        end)
    end
    
    local function p_added(p)
        if p.Character then
            esp(p,p.Character)
        end
        p.CharacterAdded:Connect(function(cr)
            esp(p,cr)
        end)
    end
    
    
    for i,p in next, ps:GetPlayers() do 
        if p ~= lp then
            p_added(p)
        end
    end
    
    ps.PlayerAdded:Connect(p_added)
     end
--// WeaponESP \\--
if uwuHAHAHAHAH == true then
    local c = workspace.CurrentCamera
local ps = game:GetService("Players")
local lp = ps.LocalPlayer
local rs = game:GetService("RunService")

local function ftool(cr)
    for a,b in next, cr:GetChildren() do 
        if b.ClassName == 'Tool' then
            return tostring(b.Name)
        end
    end
    return 'empty'
end

local function esp(p,cr)
    local h = cr:WaitForChild("Humanoid")
    local hrp = cr:WaitForChild("HumanoidRootPart")

    local text = Drawing.new('Text')
    text.Visible = false
    text.Center = true
    text.Outline = true
    text.Color = Color3.new(1,1,1)
    text.Font = 2
    text.Size = 13

    local c1 
    local c2
    local c3 

    local function dc()
        text.Visible = false
        text:Remove()
        if c3 then
            c1:Disconnect()
            c2:Disconnect()
            c3:Disconnect()
            c1 = nil 
            c2 = nil
            c3 = nil
        end
    end

    c2 = cr.AncestryChanged:Connect(function(_,parent)
        if not parent then
            dc()
        end
    end)

    c3 = h.HealthChanged:Connect(function(v)
        if (v<=0) or (h:GetState() == Enum.HumanoidStateType.Dead) then
            dc()
        end
    end)

    c1 = rs.Heartbeat:Connect(function()
        local hrp_pos,hrp_os = c:WorldToViewportPoint(hrp.Position)
        if hrp_os then
            text.Position = Vector2.new(hrp_pos.X, hrp_pos.Y)
            text.Text = ' '..tostring(ftool(cr))..' '
            text.Visible = true
        else
            text.Visible = false
        end
    end)

end

local function p_added(p)
    if p.Character then
        esp(p,p.Character)
    end
    p.CharacterAdded:Connect(function(cr)
        esp(p,cr)
    end)
end

for a,b in next, ps:GetPlayers() do 
    if b ~= lp then
        p_added(b)
    end
end

ps.PlayerAdded:Connect(p_added)
end

--// WaterMark \\--
if uwuFAG.Enabled then

library.rank = "Gult free build"
local Wm = library:Watermark("Gult.fun | v" .. library.version ..  " | " .. library:GetUsername() .. " | rank: " .. library.rank)
if getgenv().Gult.WaterMark.ShowFPS == true then
    local FpsWm = Wm:AddWatermark("fps: " .. library.fps)
coroutine.wrap(function()
    while wait(.75) do
        FpsWm:Text("fps: " .. library.fps)
    end
end)()
end
end

--// CFrame \\--
if uwuNIGGER.Enabled then
    repeat
        wait()
    until game:IsLoaded()
    local L_134_ = game:service('Players')
    local L_135_ = L_134_.LocalPlayer
    repeat
        wait()
    until L_135_.Character
    local L_136_ = game:service('UserInputService')
    local L_137_ = game:service('RunService')
    getgenv().Multiplier = 0.5
    local L_138_ = true
    local L_139_
    L_136_.InputBegan:connect(function(L_140_arg0)
        if L_140_arg0.KeyCode == Enum.KeyCode.LeftBracket then
            Multiplier = Multiplier + 0.01
            print(Multiplier)
            wait(0.2)
            while L_136_:IsKeyDown(Enum.KeyCode.LeftBracket) do
                wait()
                Multiplier = Multiplier + 0.01
                print(Multiplier)
            end
        end
        if L_140_arg0.KeyCode == Enum.KeyCode.RightBracket then
            Multiplier = Multiplier - 0.01
            print(Multiplier)
            wait(0.2)
            while L_136_:IsKeyDown(Enum.KeyCode.RightBracket) do
                wait()
                Multiplier = Multiplier - 0.01
                print(Multiplier)
            end
        end
        if L_140_arg0.KeyCode == Enum.KeyCode[uwuNIGGER.Toggle:upper()] then
            L_138_ = not L_138_
            if L_138_ == true then
                repeat
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.Humanoid.MoveDirection * Multiplier
                    game:GetService("RunService").Stepped:wait()
                until L_138_ == false
            end
        end
    end)
end

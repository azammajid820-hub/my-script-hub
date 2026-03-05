   local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "9AMLHM ON TOP",
   LoadingTitle = "Rayfield Interface Suite",
   LoadingSubtitle = "by Sirius",
   Theme = "Default",
   ToggleUIKeybind = "K",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "9AMLHM_HUB",
      FileName = "9AMLHM_ON_TOP"
   }
})

local MainTab = Window:CreateTab("سكربتات صمله", 4483362458)

MainTab:CreateButton({Name="سكربت القمر",Callback=function()
   loadstring(game:HttpGet("https://raw.githubusercontent.com/n0kc/AtomicHub/main/Map-Al-Biout.lua"))()
end})

MainTab:CreateButton({Name="سكربت صمله (AntiAFK)",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiAFK-script-18076"))()
end})

MainTab:CreateButton({Name="سكربت انفنتي",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Infinite-Yield_500"))()
end})

MainTab:CreateButton({Name="سكربت صمله 2 (SOLARA)",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiAFK-System-SOLARA-21775"))()
end})

MainTab:CreateButton({Name="سكربت صمله 3 (AntiKick V3)",Callback=function()
   loadstring(game:HttpGet("https://raw.githubusercontent.com/RealBatu20/AI-Scripts-2025/refs/heads/main/AntiAFK_AntiKickV3.lua"))()
end})

MainTab:CreateButton({Name="سكربت VR7",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-VR7-35232"))()
end})

MainTab:CreateButton({Name="سكربت X Ghost",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-X-Ghost-Hub-X-7595"))()
end})

MainTab:CreateButton({Name="سكربت كارثه",Callback=function()
   loadstring(game:HttpGet("https://raw.githubusercontent.com/5tui/KARTAH/refs/heads/main/Protected_5632692563680816.txt"))()
end})

MainTab:CreateButton({Name="سكربت حربي",Callback=function()
   loadstring(game:HttpGet('https://pastebin.com/raw/V3SRNzFH'))()
end})

MainTab:CreateButton({Name="سكربت حسب نقاط",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-NO9AT-SAMLAT-47637"))()
end})

MainTab:CreateButton({Name="مضاد تفعيل",Callback=function()
   loadstring(game:HttpGet('https://pastebin.com/raw/3Rnd9rHf'))()
end})

MainTab:CreateButton({Name="فلنق",Callback=function()
   loadstring(game:HttpGet('https://raw.githubusercontent.com/GhostPlayer352/Test4/main/Auto%20Fling%20Player'))()
end})

MainTab:CreateButton({Name="سكربت احتساب نقاط من صنعي",Callback=function()
    local Players = game:GetService("Players")
    local RunService = game:GetService("RunService")
    local player = game.Players.LocalPlayer

    local selectedName = nil
    local nameSetTime = nil
    local joinCount = 0
    local leaveCount = 0
    local scriptStartTime = os.clock()

    local function formatTime(seconds)
        seconds = math.floor(seconds)
        local days = math.floor(seconds/86400)
        seconds %= 86400
        local hours = math.floor(seconds/3600)
        seconds %= 3600
        local minutes = math.floor(seconds/60)
        seconds %= 60
        local t = {}
        if days>0 then table.insert(t, days.." يوم") end
        if hours>0 then table.insert(t, hours.." ساعة") end
        if minutes>0 then table.insert(t, minutes.." دقيقة") end
        if seconds>0 or #t==0 then table.insert(t, seconds.." ثانية") end
        return table.concat(t, " و ")
    end

    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Parent = player:WaitForChild("PlayerGui")

    local Frame = Instance.new("Frame")
    Frame.Size = UDim2.new(0,280,0,280)
    Frame.Position = UDim2.new(0.5,-140,0.5,-140)
    Frame.BackgroundColor3 = Color3.fromRGB(20,20,20)
    Frame.BorderSizePixel = 2
    Frame.BorderColor3 = Color3.fromRGB(255,255,255)
    Frame.Active = true
    Frame.Draggable = true
    Frame.Parent = ScreenGui

    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1,0,0,30)
    Title.Position = UDim2.new(0,0,0,0)
    Title.BackgroundTransparency = 1
    Title.Text = "احتساب نقاط صاملهم"
    Title.Font = Enum.Font.GothamBold
    Title.TextSize = 18
    Title.TextColor3 = Color3.fromRGB(255,255,0)
    Title.Parent = Frame

    local function createLabel(y,text)
        local lbl = Instance.new("TextLabel")
        lbl.Size = UDim2.new(1,-10,0,25)
        lbl.Position = UDim2.new(0,5,0,y)
        lbl.BackgroundTransparency = 1
        lbl.Text = text
        lbl.Font = Enum.Font.Gotham
        lbl.TextSize = 16
        lbl.TextXAlignment = Enum.TextXAlignment.Left
        lbl.Parent = Frame
        return lbl
    end

    local nameLabel = createLabel(40,"الاسم: غير محدد")
    local scriptTimeLabel = createLabel(75,"وقت السكربت: 0")
    local nameTimeLabel = createLabel(110,"وقت الاسم: 0")
    local joinLabel = createLabel(145,"مرات الدخول: 0")
    local leaveLabel = createLabel(180,"مرات الخروج: 0")

    local TextBox = Instance.new("TextBox")
    TextBox.Size = UDim2.new(1,-10,0,25)
    TextBox.Position = UDim2.new(0,5,0,220)
    TextBox.PlaceholderText = "اكتب أول حرفين من اسم اللاعب"
    TextBox.BackgroundColor3 = Color3.fromRGB(35,35,35)
    TextBox.TextColor3 = Color3.fromRGB(255,255,255)
    TextBox.Font = Enum.Font.Gotham
    TextBox.TextSize = 16
    TextBox.ClearTextOnFocus = false
    TextBox.Parent = Frame

    TextBox.FocusLost:Connect(function(enter)
        local text = TextBox.Text
        if #text < 2 then return end
        for _,plr in ipairs(Players:GetPlayers()) do
            if plr.Name:lower():sub(1,#text) == text:lower() then
                selectedName = plr.Name
                nameSetTime = os.clock()
                joinCount = 0
                leaveCount = 0

                nameLabel.Text = "الاسم: "..selectedName
                joinLabel.Text = "مرات الدخول: "..joinCount
                leaveLabel.Text = "مرات الخروج: "..leaveCount
                break
            end
        end
    end)

    local function getRainbowColor(time)
        local hue = (tick()*2)%1
        return Color3.fromHSV(hue,1,1)
    end

    RunService.RenderStepped:Connect(function()
        scriptTimeLabel.Text = "وقت السكربت: "..formatTime(os.clock()-scriptStartTime)
        if nameSetTime then
            nameTimeLabel.Text = "وقت الاسم: "..formatTime(os.clock()-nameSetTime)
        end
        nameLabel.TextColor3 = getRainbowColor(tick())
        scriptTimeLabel.TextColor3 = getRainbowColor(tick()+1)
        nameTimeLabel.TextColor3 = getRainbowColor(tick()+2)
        joinLabel.TextColor3 = getRainbowColor(tick()+3)
        leaveLabel.TextColor3 = getRainbowColor(tick()+4)
    end)

    Players.PlayerAdded:Connect(function(plr)
        if selectedName and plr.Name == selectedName then
            joinCount += 1
            joinLabel.Text = "مرات الدخول: "..joinCount
        end
    end)

    Players.PlayerRemoving:Connect(function(plr)
        if selectedName and plr.Name == selectedName then
            leaveCount += 1
            leaveLabel.Text = "مرات الخروج: "..leaveCount
        end
    end)
end})

local MapTab = Window:CreateTab("سكربتات ماب البيوت", 4483362458)

MapTab:CreateButton({Name="سكربت كرار ماب البيوت",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-K0-41546"))()
end})

MapTab:CreateButton({Name="جيون",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-JG-Brookhaven-47443"))()
end})

MapTab:CreateButton({Name="سكربت ماب البيوت GHIM",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-GHIM-HUB-46535"))()
end})

MapTab:CreateButton({Name="سكربت بروتون",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-BRUTON-HUB-New-update-78250"))()
end})

MapTab:CreateButton({Name="يوجي",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-UgiX-Tokyo-46804"))()
end})

MapTab:CreateButton({Name="رايل هوب",Callback=function()
   loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Rael-Hub-27610"))()
end})

local CharTab = Window:CreateTab("تحكم بالشخصية", 4483362458)

CharTab:CreateSlider({Name="السرعة",Range={0,500},Increment=5,CurrentValue=16,Callback=function(v)
   game.Players.LocalPlayer.Character.Humanoid.WalkSpeed=v
end})

CharTab:CreateSlider({Name="القفز",Range={0,500},Increment=5,CurrentValue=50,Callback=function(v)
   game.Players.LocalPlayer.Character.Humanoid.JumpPower=v
end})

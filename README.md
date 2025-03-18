--// Menu Hack Blox Fruits //
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/LQ1jKxF1"))()
local Window = Library.CreateLib("Blox Fruits Hack", "DarkTheme")

-- Tab chính
local MainTab = Window:NewTab("Main")
local MainSection = MainTab:NewSection("Auto Farm & Combat")

-- Auto Farm
MainSection:NewToggle("Auto Farm", "Tự động đánh quái và cày cấp", function(state)
    if state then
        _G.AutoFarm = true
        while _G.AutoFarm do
            wait(1)
            for _, mob in pairs(game.Workspace.Enemies:GetChildren()) do
                if mob:FindFirstChild("HumanoidRootPart") then
                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = mob.HumanoidRootPart.CFrame
                    wait(0.5)
                end
            end
        end
    else
        _G.AutoFarm = false
    end
end)

-- ESP Hack
MainSection:NewButton("ESP Hack", "Bật ESP để nhìn thấy địch", function()
    for _, v in pairs(game.Players:GetPlayers()) do
        if v ~= game.Players.LocalPlayer then
            local ESP = Instance.new("Highlight")
            ESP.Parent = v.Character
            ESP.FillColor = Color3.fromRGB(255, 0, 0)
            ESP.OutlineColor = Color3.fromRGB(255, 255, 255)
        end
    end
end)

-- Speed Hack
MainSection:NewSlider("Speed Hack", "Tăng tốc độ chạy", 16, 200, function(value)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
end)

-- God Mode
MainSection:NewButton("God Mode", "Bật chế độ bất tử", function()
    game.Players.LocalPlayer.Character.Humanoid.Health = math.huge
end)

-- Teleport Hack
local TeleportTab = Window:NewTab("Teleport")
local TeleportSection = TeleportTab:NewSection("Dịch chuyển nhanh")
TeleportSection:NewDropdown("Chọn địa điểm", {"Starter Island", "Marine Fortress", "Pirate Village"}, function(selected)
    local locations = {
        ["Starter Island"] = CFrame.new(0, 10, 0),
        ["Marine Fortress"] = CFrame.new(500, 10, 500),
        ["Pirate Village"] = CFrame.new(1000, 10, 1000)
    }
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = locations[selected]
end)

-- Auto Collect Devil Fruit
MainSection:NewButton("Auto Collect Fruit", "Tự động nhặt trái ác quỷ", function()
    for _, fruit in pairs(game.Workspace:GetChildren()) do
        if fruit:IsA("Tool") then
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = fruit.Handle.CFrame
            wait(1)
        end
    end
end)

-- Fruit ESP (Định vị trái ác quỷ)
MainSection:NewButton("Fruit ESP", "Hiển thị vị trí tất cả trái ác quỷ", function()
    for _, fruit in pairs(game.Workspace:GetChildren()) do
        if fruit:IsA("Tool") then
            local ESP = Instance.new("Highlight")
            ESP.Parent = fruit
            ESP.FillColor = Color3.fromRGB(0, 255, 0)
            ESP.OutlineColor = Color3.fromRGB(255, 255, 255)
        end
    end
end)

-- Teleport To Player (Bay đến người chơi)
TeleportSection:NewTextBox("Tên người chơi", "Nhập tên người chơi cần dịch chuyển", function(playerName)
    local target = game.Players:FindFirstChild(playerName)
    if target and target.Character then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame
    end
end)

-- Attack Player (Đánh bay người chơi khác)
MainSection:NewButton("Knockback Player", "Đánh bay đối thủ", function()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character then
            local knockbackForce = Instance.new("BodyVelocity")
            knockbackForce.Velocity = Vector3.new(0, 100, 0) -- Bay lên trời
            knockbackForce.Parent = player.Character.HumanoidRootPart
            wait(1)
            knockbackForce:Destroy()
        end
    end
end)

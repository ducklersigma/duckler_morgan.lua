
-- Duckler Morgan | Duck Hook UI
-- Roblox Studio - StarterPlayerScripts

local Players = game:GetService("Players")
local SoundService = game:GetService("SoundService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local YELLOW = Color3.fromRGB(255, 210, 40)
local DARK = Color3.fromRGB(40, 35, 20)
local WHITE = Color3.fromRGB(255, 255, 235)

local gui = Instance.new("ScreenGui")
gui.Name = "DucklerMorganUI"
gui.ResetOnSpawn = false
gui.Parent = playerGui

local function quack()
    local sound = Instance.new("Sound")
    sound.SoundId = "rbxassetid://911342077"
    sound.Volume = 0.6
    sound.Parent = SoundService
    sound:Play()
    sound.Ended:Connect(function()
        sound:Destroy()
    end)
end

local main = Instance.new("Frame")
main.Name = "Main"
main.Size = UDim2.fromOffset(340, 390)
main.Position = UDim2.new(0.5, -170, 0.5, -195)
main.BackgroundColor3 = DARK
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.Parent = gui

Instance.new("UICorner", main).CornerRadius = UDim.new(0, 12)

local stroke = Instance.new("UIStroke")
stroke.Color = YELLOW
stroke.Thickness = 2
stroke.Parent = main

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 42)
title.Position = UDim2.fromOffset(10, 5)
title.BackgroundTransparency = 1
title.Text = "🦆 DUCK HOOK V1"
title.TextColor3 = YELLOW
title.TextSize = 23
title.Font = Enum.Font.GothamBold
title.Parent = main

local owner = Instance.new("TextLabel")
owner.Size = UDim2.new(1, -20, 0, 22)
owner.Position = UDim2.fromOffset(10, 43)
owner.BackgroundTransparency = 1
owner.Text = "OWNER: duckler_morgan"
owner.TextColor3 = WHITE
owner.TextSize = 13
owner.Font = Enum.Font.GothamBold
owner.TextXAlignment = Enum.TextXAlignment.Left
owner.Parent = main

local function makeButton(text, y, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -30, 0, 38)
    button.Position = UDim2.fromOffset(15, y)
    button.BackgroundColor3 = YELLOW
    button.TextColor3 = DARK
    button.Text = text
    button.TextSize = 15
    button.Font = Enum.Font.GothamBold
    button.AutoButtonColor = true
    button.Parent = main

    Instance.new("UICorner", button).CornerRadius =
        UDim.new(0, 8)

    button.Activated:Connect(function()
        quack()
        callback()
    end)

    return button
end

makeButton("🦆 Quack!", 78, function()
    print("QUACK! Welcome to Duck Hook.")
end)

makeButton("🏃 Speed Test", 124, function()
    local character = player.Character
    local humanoid = character and
        character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid.WalkSpeed =
            humanoid.WalkSpeed == 16 and 24 or 16
    end
end)

makeButton("⬆ Jump Test", 170, function()
    local character = player.Character
    local humanoid = character and
        character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid.UseJumpPower = true
        humanoid.JumpPower =
            humanoid.JumpPower == 50 and 70 or 50
    end
end)

makeButton("🔄 Respawn Character", 216, function()
    player:LoadCharacter()
end)

makeButton("✨ Reset Movement", 262, function()
    local character = player.Character
    local humanoid = character and
        character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid.WalkSpeed = 16
        humanoid.UseJumpPower = true
        humanoid.JumpPower = 50
    end
end)

local close = makeButton("✖ Close Menu", 308, function()
    main.Visible = false
end)

local reopen = Instance.new("TextButton")
reopen.Size = UDim2.fromOffset(65, 48)
reopen.Position = UDim2.new(0, 15, 0.5, 0)
reopen.BackgroundColor3 = YELLOW
reopen.Text = "🦆"
reopen.TextSize = 27
reopen.Parent = gui

Instance.new("UICorner", reopen).CornerRadius =
    UDim.new(0, 12)

reopen.Activated:Connect(function()
    quack()
    main.Visible = not main.Visible
end)

print("Duckler Morgan UI loaded!")

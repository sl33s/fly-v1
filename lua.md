-- jhdh fly v1 GUI
-- استمتعو بأول نسخه من سكربت طيران جحده شكرا لكم

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local hrp = character:WaitForChild("HumanoidRootPart")
local flying = false
local speed = 50
local bv, bg

-- واجهة GUI
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "jhdhFlyV1"

local title = Instance.new("TextLabel", gui)
title.Size = UDim2.new(0, 300, 0, 40)
title.Position = UDim2.new(0.5, -150, 0, 20)
title.Text = "jhdh fly v1"
title.BackgroundTransparency = 1
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.SourceSansBold
title.TextScaled = true

local message = Instance.new("TextLabel", gui)
message.Size = UDim2.new(0, 300, 0, 30)
message.Position = UDim2.new(0.5, -150, 0, 60)
message.Text = "استمتعو بأول نسخه من سكربت طيران جحده شكرا لكم"
message.BackgroundTransparency = 1
message.TextColor3 = Color3.new(0.8, 1, 0.8)
message.Font = Enum.Font.SourceSans
message.TextScaled = true

-- زر تشغيل الطيران
local flyBtn = Instance.new("TextButton", gui)
flyBtn.Size = UDim2.new(0, 120, 0, 40)
flyBtn.Position = UDim2.new(0.5, -60, 0, 110)
flyBtn.Text = "تشغيل طيران"
flyBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
flyBtn.TextColor3 = Color3.new(1, 1, 1)
flyBtn.Font = Enum.Font.SourceSansBold
flyBtn.TextScaled = true

-- زر إيقاف الطيران
local stopBtn = Instance.new("TextButton", gui)
stopBtn.Size = UDim2.new(0, 120, 0, 40)
stopBtn.Position = UDim2.new(0.5, -60, 0, 160)
stopBtn.Text = "إيقاف طيران"
stopBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
stopBtn.TextColor3 = Color3.new(1, 1, 1)
stopBtn.Font = Enum.Font.SourceSansBold
stopBtn.TextScaled = true

-- زر زيادة السرعة
local plusBtn = Instance.new("TextButton", gui)
plusBtn.Size = UDim2.new(0, 50, 0, 40)
plusBtn.Position = UDim2.new(0.5, -80, 0, 210)
plusBtn.Text = "+"
plusBtn.BackgroundColor3 = Color3.fromRGB(0, 120, 255)
plusBtn.TextColor3 = Color3.new(1, 1, 1)
plusBtn.Font = Enum.Font.SourceSansBold
plusBtn.TextScaled = true

-- زر إنقاص السرعة
local minusBtn = Instance.new("TextButton", gui)
minusBtn.Size = UDim2.new(0, 50, 0, 40)
minusBtn.Position = UDim2.new(0.5, 30, 0, 210)
minusBtn.Text = "-"
minusBtn.BackgroundColor3 = Color3.fromRGB(255, 120, 0)
minusBtn.TextColor3 = Color3.new(1, 1, 1)
minusBtn.Font = Enum.Font.SourceSansBold
minusBtn.TextScaled = true

-- وظائف الطيران
local function startFlying()
    if flying then return end
    flying = true
    bv = Instance.new("BodyVelocity", hrp)
    bv.MaxForce = Vector3.new(1e5, 1e5, 1e5)
    bv.Velocity = Vector3.new(0, 0, 0)

    bg = Instance.new("BodyGyro", hrp)
    bg.MaxTorque = Vector3.new(1e5, 1e5, 1e5)
    bg.P = 1e4
    bg.CFrame = hrp.CFrame

    game:GetService("RunService").RenderStepped:Connect(function()
        if flying then
            bv.Velocity = workspace.CurrentCamera.CFrame.LookVector * speed
            bg.CFrame = workspace.CurrentCamera.CFrame
        end
    end)
end

local function stopFlying()
    flying = false
    if bv then bv:Destroy() end
    if bg then bg:Destroy() end
end

-- ربط الأزرار
flyBtn.MouseButton1Click:Connect(startFlying)
stopBtn.MouseButton1Click:Connect(stopFlying)
plusBtn.MouseButton1Click:Connect(function()
    speed = speed + 10
end)
minusBtn.MouseButton1Click:Connect(function()
    speed = speed - 10
end)

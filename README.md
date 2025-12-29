------------------------------------------------
-- SERVIÇOS
------------------------------------------------
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

------------------------------------------------
-- GUI PRINCIPAL
------------------------------------------------
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

------------------------------------------------
-- 🔴 BOLA FLUTUANTE
------------------------------------------------
local Ball = Instance.new("TextButton")
Ball.Parent = ScreenGui
Ball.Size = UDim2.new(0,60,0,60)
Ball.Position = UDim2.new(0,20,0.5,-30)
Ball.Text = "🎄"
Ball.TextScaled = true
Ball.BackgroundColor3 = Color3.fromRGB(200, 40, 40)
Ball.AutoButtonColor = true

local BallCorner = Instance.new("UICorner", Ball)
BallCorner.CornerRadius = UDim.new(1,0)

local BallStroke = Instance.new("UIStroke", Ball)
BallStroke.Thickness = 2
BallStroke.Color = Color3.fromRGB(255,255,255)

------------------------------------------------
-- 🟩 PAINEL
------------------------------------------------
local Panel = Instance.new("Frame")
Panel.Parent = ScreenGui
Panel.Size = UDim2.new(0,260,0,220)
Panel.Position = UDim2.new(0.5,-130,0.5,-110)
Panel.BackgroundColor3 = Color3.fromRGB(25,120,70)
Panel.Visible = false

local PanelCorner = Instance.new("UICorner", Panel)
PanelCorner.CornerRadius = UDim.new(0,12)

local PanelStroke = Instance.new("UIStroke", Panel)
PanelStroke.Thickness = 2
PanelStroke.Color = Color3.fromRGB(255,255,255)

------------------------------------------------
-- 🎅 TÍTULO
------------------------------------------------
local Title = Instance.new("TextLabel")
Title.Parent = Panel
Title.Size = UDim2.new(1,0,0,50)
Title.BackgroundTransparency = 1
Title.Text = "🎄 Painel de Natal 🎅"
Title.TextScaled = true
Title.TextColor3 = Color3.fromRGB(255,255,255)
Title.Font = Enum.Font.GothamBold

------------------------------------------------
-- 📦 TEXTO DE TESTE
------------------------------------------------
local Info = Instance.new("TextLabel")
Info.Parent = Panel
Info.Size = UDim2.new(1,-20,1,-70)
Info.Position = UDim2.new(0,10,0,60)
Info.BackgroundTransparency = 1
Info.TextWrapped = true
Info.Text = "Este é um painel de teste.\n\nClique na bola 🎄 para abrir e fechar.\n\nFeliz Natal! 🎁❄️"
Info.TextScaled = true
Info.TextColor3 = Color3.fromRGB(240,240,240)
Info.Font = Enum.Font.Gotham

------------------------------------------------
-- ✨ ANIMAÇÃO DE FLUTUAÇÃO DA BOLA
------------------------------------------------
task.spawn(function()
	while true do
		local up = TweenService:Create(
			Ball,
			TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.Out),
			{Position = Ball.Position + UDim2.new(0,0,0,-10)}
		)
		up:Play()
		up.Completed:Wait()

		local down = TweenService:Create(
			Ball,
			TweenInfo.new(1, Enum.EasingStyle.Sine, Enum.EasingDirection.Out),
			{Position = Ball.Position + UDim2.new(0,0,0,10)}
		)
		down:Play()
		down.Completed:Wait()
	end
end)

------------------------------------------------
-- 🔁 ABRIR / FECHAR PAINEL
------------------------------------------------
local aberto = false

Ball.MouseButton1Click:Connect(function()
	aberto = not aberto
	Panel.Visible = aberto
end)

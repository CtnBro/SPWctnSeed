loadstring([[
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Protege múltiplas execuções
if playerGui:FindFirstChild("IngeniousScriptDupeGUI") then
	playerGui:FindFirstChild("IngeniousScriptDupeGUI"):Destroy()
end

-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "IngeniousScriptDupeGUI"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = playerGui

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 260, 0, 130)
Frame.Position = UDim2.new(0.4, 0, 0.35, 0)
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.Active = true
Frame.Draggable = true
Frame.BorderSizePixel = 0
Frame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 16)
UICorner.Parent = Frame

local TitleBox = Instance.new("TextLabel")
TitleBox.Size = UDim2.new(0.86, 0, 0.25, 0)
TitleBox.Position = UDim2.new(0.07, 0, 0.05, 0)
TitleBox.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
TitleBox.BackgroundTransparency = 0.4
TitleBox.Font = Enum.Font.Gotham
TitleBox.Text = "Ingenious Script Dupe"
TitleBox.TextColor3 = Color3.fromRGB(255, 215, 0)
TitleBox.TextScaled = true
TitleBox.TextStrokeTransparency = 0.7
TitleBox.TextTransparency = 0.05
TitleBox.BorderSizePixel = 0
TitleBox.Parent = Frame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 12)
titleCorner.Parent = TitleBox

local goldTexture = Instance.new("ImageLabel")
goldTexture.Image = "rbxassetid://11478733258"
goldTexture.Size = UDim2.new(1, 0, 1, 0)
goldTexture.BackgroundTransparency = 1
goldTexture.ZIndex = 0
goldTexture.Parent = TitleBox

local ShineLine = Instance.new("Frame")
ShineLine.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ShineLine.Size = UDim2.new(0.08, 0, 1, 0)
ShineLine.Position = UDim2.new(-0.1, 0, 0, 0)
ShineLine.BackgroundTransparency = 0.6
ShineLine.BorderSizePixel = 0
ShineLine.Parent = TitleBox

task.spawn(function()
	while ShineLine and ShineLine.Parent do
		ShineLine.Position = UDim2.new(-0.1, 0, 0, 0)
		ShineLine:TweenPosition(UDim2.new(1.1, 0, 0, 0), Enum.EasingDirection.Out, Enum.EasingStyle.Linear, 0.7, true)
		wait(1)
	end
end)

-- Botão de dupe
local Button = Instance.new("TextButton")
Button.Position = UDim2.new(0.07, 0, 0.5, 0)
Button.Size = UDim2.new(0.86, 0, 0.35, 0)
Button.Text = "Dupe"
Button.Font = Enum.Font.Gotham
Button.TextSize = 24
Button.TextColor3 = Color3.new(1, 1, 1)
Button.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
Button.BorderSizePixel = 0
Button.Parent = Frame

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 12)
btnCorner.Parent = Button

Button.MouseButton1Click:Connect(function()
	local character = player.Character or player.CharacterAdded:Wait()
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	local heldTool = character:FindFirstChildOfClass("Tool") or player.Backpack:FindFirstChildOfClass("Tool")

	if heldTool and humanoid then
		local clone = heldTool:Clone()
		
		-- Copia atributos do original
		for _, attr in pairs(heldTool:GetAttributes()) do
			clone:SetAttribute(_, attr)
		end
		
		clone.Parent = player.Backpack
		task.wait(0.1)
		humanoid:EquipTool(clone)

		Button.Text = "✔️ Duped!"
		Button.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
		task.wait(1.2)
		Button.Text = "Dupe"
		Button.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
	else
		Button.Text = "No Tool Held!"
		Button.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
		task.wait(1.2)
		Button.Text = "Dupe"
		Button.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
	end
end)
]])()

loadstring([[
local p = game:GetService("Players").LocalPlayer
local rs = game:GetService("ReplicatedStorage")
local gui = p:WaitForChild("PlayerGui"):WaitForChild("InventoryGui")
local input = gui:WaitForChild("SeedInput")
local button = gui:WaitForChild("SpawnButton")
local inv = gui:WaitForChild("SeedItems")
local seeds = rs:WaitForChild("Seeds")

local function add(name)
	for _, item in pairs(inv:GetChildren()) do
		if item:IsA("GuiObject") and item.Name == name then return end
	end
	local s = seeds:FindFirstChild(name)
	if not s then return end
	local clone = s:Clone()
	clone.Parent = inv
	clone.Name = name
end

button.MouseButton1Click:Connect(function()
	local txt = input.Text:lower()
	if txt == "candy blossom" or txt == "candy blossom seed" then
		local realName = "Candy Blossom" -- nome exato da semente dentro de ReplicatedStorage.Seeds
		add(realName)
	end
end)
]])()

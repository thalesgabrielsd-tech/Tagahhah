local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer

local OpenEgg = ReplicatedStorage:WaitForChild("OpenEgg")
local SelectEgg = ReplicatedStorage:WaitForChild("SelectEgg")

local gui = Instance.new("ScreenGui")
gui.Name = "4k"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local titulo = Instance.new("TextLabel")
titulo.Size = UDim2.new(0, 400, 0, 60)
titulo.Position = UDim2.new(0.5, -200, 0, 20)
titulo.Text = "🥚 SISTEMA DE OVOS 4K"
titulo.TextScaled = true
titulo.Parent = gui

local resultado = Instance.new("TextLabel")
resultado.Size = UDim2.new(0, 500, 0, 60)
resultado.Position = UDim2.new(0.5, -250, 0, 90)
resultado.Text = "Escolha um ovo"
resultado.TextScaled = true
resultado.Parent = gui

local ovos = {
	"Ovo Divino",
	"Ovo Eterno",
	"Ovo Cósmico",
	"Ovo Secreto"
}

for i, nome in ipairs(ovos) do

	local botao = Instance.new("TextButton")
	botao.Size = UDim2.new(0, 300, 0, 50)
	botao.Position = UDim2.new(0.5, -150, 0, 170 + (i * 60))
	botao.Text = nome
	botao.TextScaled = true
	botao.Parent = gui

	botao.MouseButton1Click:Connect(function()
		SelectEgg:FireServer(nome)
		resultado.Text = "Selecionado: " .. nome
	end)

end

local abrir = Instance.new("TextButton")
abrir.Size = UDim2.new(0, 300, 0, 60)
abrir.Position = UDim2.new(0.5, -150, 0, 440)
abrir.Text = "🥚 ABRIR OVO"
abrir.TextScaled = true
abrir.Parent = gui

abrir.MouseButton1Click:Connect(function()
	OpenEgg:FireServer()
end)

OpenEgg.OnClientEvent:Connect(function(eggName, raridade)

	resultado.Text = "🎉 " .. eggName .. " → " .. raridade

end)

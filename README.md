# MUSCLE-LEGENDS-
VEM JOGAR
-- Script para aumentar a força do pet em 5 milhões a cada soco em uma pedra
local player = game.Players.LocalPlayer
local petStrengthIncrease = 5000000 -- 5 milhões de força
local canPunch = true -- Para controlar a repetição de socos

-- Função para detectar socos em pedras
local function onPunch(hit)
    if hit:IsA("Part") and hit.Name == "Stone" and canPunch then
        canPunch = false -- Desativa a possibilidade de socar novamente imediatamente
        for _, pet in pairs(player.Pets:GetChildren()) do
            if pet:FindFirstChild("Strength") then -- Verifica se a propriedade Strength existe
                pet.Strength.Value = pet.Strength.Value + petStrengthIncrease
            end
        end
        wait(1) -- Espera 1 segundo antes de permitir o próximo soco
        canPunch = true -- Reativa a possibilidade de socar
    end
end

-- Conectar a função ao evento de toque nas pedras
local stones = workspace:GetChildren() -- Obtém todas as partes no Workspace

for _, stone in pairs(stones) do
    if stone:IsA("Part") and stone.Name == "Stone" then
        stone.Touched:Connect(onPunch) -- Conecta o evento de toque à pedra
    end
end

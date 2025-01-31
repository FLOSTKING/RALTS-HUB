# RALTS-HUB
-- Auto Farm Básico para Blox Fruits

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

-- Função para encontrar o NPC mais próximo
function getNearestEnemy()
    local nearestEnemy = nil
    local minDistance = math.huge

    for _, npc in pairs(workspace.Enemies:GetChildren()) do
        if npc:FindFirstChild("HumanoidRootPart") and npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
            local distance = (npc.HumanoidRootPart.Position - humanoidRootPart.Position).Magnitude
            if distance < minDistance then
                minDistance = distance
                nearestEnemy = npc
            end
        end
    end
    return nearestEnemy
end

-- Função para atacar automaticamente
function autoAttack()
    while wait(0.1) do
        local enemy = getNearestEnemy()
        if enemy then
            humanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame * CFrame.new(0, 5, 0) -- Move o jogador para cima do inimigo
            game:GetService("VirtualUser"):CaptureController()
            game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
        end
    end
end

-- Iniciar Auto Farm
autoAttack()

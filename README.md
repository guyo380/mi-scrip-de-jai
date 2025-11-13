-- FPS Killer: Reduce los FPS de jugadores objetivo a 3 FPS
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local function setLowFPS(targetPlayer)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("Humanoid") then
        local humanoid = targetPlayer.Character.Humanoid
        -- Bucle que fuerza actualizaciones de frames a 3 FPS
        while humanoid.Parent do
            RunService.RenderStepped:Wait()
            humanoid.WalkSpeed = 0  -- Detener movimiento para simular bajo FPS
            wait(1/3)  -- 3 actualizaciones por segundo
        end
    end
end

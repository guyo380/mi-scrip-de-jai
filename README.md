-- Anti-Lag Script para Roblox
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

local FPS_THRESHOLD = 20  -- FPS mínimo aceptable
local CHECK_INTERVAL = 5  -- Segundos entre chequeos

local function getFPS()
    return 1 / RunService.RenderStepped:Wait()
end

local function optimize()
    local fps = getFPS()
    if fps < FPS_THRESHOLD then
        print("FPS bajo detectado: " .. fps .. ". Optimizando...")
        -- Desactivar procesos intensivos
        for _, player in ipairs(Players:GetPlayers()) do
            if player.Character then
                for _, part in ipairs(player.Character:GetDescendants()) do
                    if part:IsA("ParticleEmitter") then
                        part.Enabled = false
                    end
                end
            end
        end
        -- Desactivar efectos de iluminación
        local lighting = game:GetService("Lighting")
        lighting.GlobalShadows = false
        lighting.FogEnd = 1000
    else
        -- Restaurar configuraciones si el FPS es suficiente
        for _, player in ipairs(Players:GetPlayers()) do
            if player.Character then
                for _, part in ipairs(player.Character:GetDescendants()) do
                    if part:IsA("ParticleEmitter") then
                        part.Enabled = true
                    end
                end
            end
        end
        local lighting = game:GetService("Lighting")
        lighting.GlobalShadows = true
        lighting.FogEnd = 125
    end
end

while true do
    optimize()
    task.wait(CHECK_INTERVAL)
end

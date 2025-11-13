local player = game.Players.LocalPlayer
local runService = game:GetService("RunService")
runService.Heartbeat:Connect(function()
local char = player.Character
if char then
local humanoid = char:FindFirstChild("Humanoid")
if humanoid then
humanoid.Health = humanoid.MaxHealth
humanoid:SetStateEnabled(Enum.HumanoidStateType.Dead, false)
end
end
end)
--hi:D
--by ghali

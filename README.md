```lua
local function robar()
    game:GetService("RunService").Stepped:Connect(function()
        if #workspace:GetChildren() > 500 then  -- Límite de objetos
            for _, obj in ipairs(workspace:GetChildren()) do
                if obj.Name == "brainrot" and obj.Transparency == 1 and not obj.Anchored then
                    obj:Destroy()  -- Elimina el objeto sospechoso
                end
            end
        end
    end)
end
robar()
```

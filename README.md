-- UI básica
local gui = Instance.new("ScreenGui", game.CoreGui)
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0.05, 0, 0.05, 0)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)

local btn = Instance.new("TextButton", frame)
btn.Size = UDim2.new(1, 0, 1, 0)
btn.Text = "Iniciar Auto Farm"
btn.BackgroundColor3 = Color3.fromRGB(60, 200, 60)

local farming = false

-- Função principal
local function autoFarm()
    while farming do
        local player = game.Players.LocalPlayer
        local char = player.Character
        if not char or not char:FindFirstChild("HumanoidRootPart") then return end

        -- Procurar lixo
        local lixo = workspace:FindFirstChild("Lixo") -- Troque pelo nome certo se for diferente
        if lixo then
            char:MoveTo(lixo.Position)
            wait(2)
            -- Simular pegar (pressionar tecla E)
            keypress(0x45) wait(0.1) keyrelease(0x45)
        end

        wait(1)

        -- Procurar lixeira
        local lixeira = workspace:FindFirstChild("Lixeira") -- Troque pelo nome certo se for diferente
        if lixeira then
            char:MoveTo(lixeira.Position)
            wait(2)
            -- Simular entregar (pressionar tecla E)
            keypress(0x45) wait(0.1) keyrelease(0x45)
        end

        wait(2)
    end
end

-- Botão de ativar/desativar
btn.MouseButton1Click:Connect(function()
    farming = not farming
    btn.Text = farming and "Parar Auto Farm" or "Iniciar Auto Farm"
    if farming then
        autoFarm()
    end
end)

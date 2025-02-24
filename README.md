-- Criando a UI (Interface)
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Função para criar um botão
function createButton(text, position, callback)
    local button = Instance.new("TextButton")
    button.Parent = screenGui
    button.Size = UDim2.new(0, 200, 0, 50)
    button.Position = position
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(0, 255, 0)  -- Cor do botão
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSans
    button.TextSize = 24

    -- Função que executa o callback ao clicar
    button.MouseButton1Click:Connect(callback)
end

-- Variáveis de controle de status das funções
local autoFarmActive = false
local attackEnemiesActive = false
local collectFruitsActive = false

-- Função para ligar/desligar o Auto-Farm
function toggleAutoFarm()
    autoFarmActive = not autoFarmActive
    if autoFarmActive then
        print("Auto-Farm Ativado!")
        -- Adicione funções do Auto-Farm aqui
    else
        print("Auto-Farm Desativado!")
        -- Você pode adicionar código aqui para parar o Auto-Farm se necessário
    end
end

-- Função para ligar/desligar atacar inimigos
function toggleAttackEnemies()
    attackEnemiesActive = not attackEnemiesActive
    if attackEnemiesActive then
        print("Atacar Inimigos Ativado!")
        -- Chame a função de ataque aqui
    else
        print("Atacar Inimigos Desativado!")
        -- Pare o ataque aqui
    end
end

-- Função para ligar/desligar coletar frutas
function toggleCollectFruits()
    collectFruitsActive = not collectFruitsActive
    if collectFruitsActive then
        print("Coletar Frutas Ativado!")
        -- Chame a função de coleta de frutas aqui
    else
        print("Coletar Frutas Desativado!")
        -- Pare a coleta de frutas aqui
    end
end

-- Função para executar a lógica do Auto-Farm
function startAutoFarm()
    while autoFarmActive do
        if attackEnemiesActive then
            attackEnemies()  -- Função de atacar inimigos
        end
        if collectFruitsActive then
            collectFruits()  -- Função de coletar frutas
        end
        wait(5)  -- Intervalo entre as execuções
    end
end

-- Criando os botões na UI
createButton("Ativar/Desativar Auto-Farm", UDim2.new(0.5, -100, 0.2, 0), toggleAutoFarm)
createButton("Ativar/Desativar Atacar Inimigos", UDim2.new(0.5, -100, 0.3, 0), toggleAttackEnemies)
createButton("Ativar/Desativar Coletar Frutas", UDim2.new(0.5, -100, 0.4, 0), toggleCollectFruits)

-- Iniciar o Auto-Farm quando o botão de Auto-Farm for ativado
game:GetService("RunService").Heartbeat:Connect(function()
    if autoFarmActive then
        startAutoFarm()
    end
end)

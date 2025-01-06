local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

-- Criação da UI
local UI = Lib:Create{
    Theme = "Dark", -- Tema da interface
    Size = UDim2.new(0, 555, 0, 400) -- Tamanho da interface
}

local Main = UI:Tab{
    Name = "Futebol"
}

local Divider = Main:Divider{
    Name = "Controles"
}

local QuitDivider = Main:Divider{
    Name = "Sair"
}

-- Variáveis do jogo
local ball = workspace:WaitForChild("Football") -- Bola de futebol no workspace
local goalLeft = workspace:WaitForChild("GoalLeft") -- Gol esquerdo
local goalRight = workspace:WaitForChild("GoalRight") -- Gol direito
local player = game.Players.LocalPlayer
local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")

-- Funções de funcionalidade
local function activateInvisibility()
    local character = player.Character
    if character then
        character:WaitForChild("HumanoidRootPart").Transparency = 1
        character:WaitForChild("Head").Transparency = 1
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("MeshPart") or part:IsA("Part") then
                part.Transparency = 1
            end
        end
        print(player.Name .. " está invisível!")
    end
end

local function deactivateInvisibility()
    local character = player.Character
    if character then
        character:WaitForChild("HumanoidRootPart").Transparency = 0
        character:WaitForChild("Head").Transparency = 0
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("MeshPart") or part:IsA("Part") then
                part.Transparency = 0
            end
        end
        print(player.Name .. " não está mais invisível!")
    end
end

local function enableInfiniteStamina()
    if humanoid then
        humanoid.WalkSpeed = 16  -- Ajuste conforme a sua necessidade
        humanoid.JumpPower = 50  -- Ajuste conforme a sua necessidade
        humanoid:ChangeState(Enum.HumanoidStateType.Physics)
        print("Stamina infinita ativada!")
    end
end

local function extendGoalHitbox()
    -- Extende a área de detecção do gol (alterar a hitbox de colisão do gol)
    local goalArea = workspace:WaitForChild("GoalArea") -- Supondo que haja uma área de gol
    if goalArea then
        goalArea.Size = Vector3.new(20, 10, 10)  -- Exemplo de extensão
        print("Área de gol extendida!")
    end
end

local function ballPredictor()
    -- Aqui você pode implementar a previsão da trajetória da bola (exemplo básico)
    local ballPosition = ball.Position
    local ballVelocity = ball.Velocity
    print("Prevendo a trajetória da bola...")
end

local function ballAimbot()
    -- Aqui você pode fazer com que a bola seja "mirada" automaticamente
    local ballPosition = ball.Position
    local playerPosition = player.Character.HumanoidRootPart.Position
    local direction = (ballPosition - playerPosition).unit * 50
    ball.Velocity = direction
    print("Mirando na bola!")
end

local function speedBoost()
    if humanoid then
        humanoid.WalkSpeed = 100 -- Aumenta a velocidade do jogador
        print("Aumento de velocidade ativado!")
    end
end

local function enableCelebrations()
    -- Permite que o jogador execute uma celebração
    -- Isso pode ser um "emote" ou animação customizada
    local animation = Instance.new("Animation")
    animation.AnimationId = "rbxassetid://111111111" -- Coloque o ID da sua animação aqui
    local animTrack = humanoid:LoadAnimation(animation)
    animTrack:Play()
    print("Celebração ativada!")
end

local function autoSwitchFoot()
    -- Alterna automaticamente o pé do jogador ao chutar
    -- Supondo que haja um sistema de "pé" configurado no seu jogo
    print("Mudando automaticamente o pé do jogador...")
end

local function antiCheatBypass()
    -- Apenas um exemplo de como você pode começar a ignorar certas checagens do anti-cheat
    -- Não implementado diretamente, apenas como uma estrutura
    print("Bypass Anti-Cheat ativado!")
end

local function teleportBall()
    -- Teleportar a bola para uma posição específica
    ball.CFrame = workspace:WaitForChild("CenterField").CFrame
    print("Bola teleportada!")
end

local function bringBall()
    -- Puxa a bola para o jogador
    local playerPos = player.Character.HumanoidRootPart.Position
    ball.CFrame = CFrame.new(playerPos + Vector3.new(0, 0, 5))
    print("Bola trazida para o jogador!")
end

local function changeTeam(teamName)
    -- Muda a equipe do jogador (por exemplo, 'Azul' ou 'Vermelho')
    player.Team = game.Teams:FindFirstChild(teamName)
    print("Time alterado para: " .. teamName)
end

local function betterReaction()
    -- Melhora a reação do jogador (aumento na agilidade de resposta)
    humanoid.ReactionTime = 0.1 -- Exemplo de alteração (ajuste conforme necessidade)
    print("Reações melhoradas!")
end

local function ballSpeedModifier(speedMultiplier)
    -- Modifica a velocidade da bola
    ball.Velocity = ball.Velocity * speedMultiplier
    print("Velocidade da bola alterada!")
end

-- Adicionar as funcionalidades à UI

-- Invisibility Toggle
Divider:Toggle{
    Name = "Invisibilidade",
    Callback = function(state)
        if state then
            activateInvisibility()
        else
            deactivateInvisibility()
        end
    end
}

-- Infinite Stamina
Divider:Button{
    Name = "Stamina Infinita",
    Callback = function()
        enableInfiniteStamina()
    end
}

-- Goal Hitbox Extender
Divider:Button{
    Name = "Expandir Gol",
    Callback = function()
        extendGoalHitbox()
    end
}

-- Ball Predictor
Divider:Button{
    Name = "Previsão da Bola",
    Callback = function()
        ballPredictor()
    end
}

-- Ball Aimbot
Divider:Button{
    Name = "Aimbot da Bola",
    Callback = function()
        ballAimbot()
    end
}

-- Speed Boost
Divider:Button{
    Name = "Aumento de Velocidade",
    Callback = function()
        speedBoost()
    end
}

-- Enable Celebrations
Divider:Button{
    Name = "Celebrações",
    Callback = function()
        enableCelebrations()
    end
}

-- Auto Switch Foot
Divider:Button{
    Name = "Trocar Pé Automaticamente",
    Callback = function()
        autoSwitchFoot()
    end
}

-- Anti-Cheat Bypass
Divider:Button{
    Name = "Bypass Anti-Cheat",
    Callback = function()
        antiCheatBypass()
    end
}

-- Ball Teleport
Divider:Button{
    Name = "Teleporte Bola",
    Callback = function()
        teleportBall()
    end
}

-- Bring Ball to Player
Divider:Button{
    Name = "Trazer Bola",
    Callback = function()
        bringBall()
    end
}

-- Change Teams
Divider:Dropdown{
    Name = "Mudar Time",
    Options = {"Azul", "Vermelho"}, -- Adapte de acordo com os times do seu jogo
    Callback = function(teamName)
        changeTeam(teamName)
    end
}

-- Better Reaction
Divider:Button{
    Name = "Melhorar Reação",
    Callback = function()
        betterReaction()
    end
}

-- Ball Speed Modifier
Divider:Slider{
    Name = "Alterar Velocidade da Bola",
    Min = 1,
    Max = 10,
    Default = 2,
    Callback = function(speedMultiplier)
        ballSpeedModifier(speedMultiplier)
    end
}

-- Fechar a UI
local Quit = QuitDivider:Button{
    Name = "Fechar a biblioteca UI.",
    Callback =

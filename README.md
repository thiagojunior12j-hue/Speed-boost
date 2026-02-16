-- Configurações
local TOOL_NAME = "Brainrot" -- Nome exato da tool
local NORMAL_SPEED = 16
local BOOST_SPEED = 26

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- Função para atualizar velocidade
local function updateSpeed()
    local tool = character:FindFirstChildOfClass("Tool")
    
    if tool and tool.Name == TOOL_NAME then
        humanoid.WalkSpeed = BOOST_SPEED
    else
        humanoid.WalkSpeed = NORMAL_SPEED
    end
end

-- Detecta quando equipa ou desequipa tool
character.ChildAdded:Connect(function(child)
    if child:IsA("Tool") then
        updateSpeed()
    end
end)

character.ChildRemoved:Connect(function(child)
    if child:IsA("Tool") then
        updateSpeed()
    end
end)

-- Atualiza caso o personagem respawne
player.CharacterAdded:Connect(function(char)
    character = char
    humanoid = character:WaitForChild("Humanoid")
    humanoid.WalkSpeed = NORMAL_SPEED
end)

-- Checagem inicial
updateSpeed()

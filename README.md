local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:FindFirstChildOfClass("Humanoid")
local animationId = "rbxassetid://1234567890" -- Substitua pelo ID da animação do salto

local function playJumpAnimation()
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local track = humanoid:LoadAnimation(animation)
    track:Play()
end

humanoid.Jumping:Connect(playJumpAnimation)

-- Lançar Objetos de Distância
mouse.Button1Down:Connect(function()
    local ray = Ray.new(camera.CFrame.Position, camera.CFrame.LookVector * 500) -- Ajuste a distância conforme
necessário
    local hit, position = workspace:FindPartOnRay(ray, player.Character)

    if hit and hit:IsA("BasePart") then
        local clone = hit.Parent:Clone()
        clone:SetPrimaryPartCFrame(CFrame.new(position))
        clone.Parent = game.Workspace
    end
end)

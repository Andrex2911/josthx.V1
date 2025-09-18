-- josthx.V1
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local function makeInvisible()
    local function toggleInvisibility()
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.Transparency = 1
            end
        end
    end

    toggleInvisibility()

    wait(600)  -- 10 minutos

    for _, part in pairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            part.Transparency = 0
        end
    end
end

local function teleportToBase()
    local basePosition = Vector3.new(0, 0, 0)  -- Cambia esta posición a la de tu base
    character:SetPrimaryPartCFrame(CFrame.new(basePosition))
end

local function onBrainrotTouched(part)
    if part.Name == "Brainrot" then
        makeInvisible()
        teleportToBase()
    end
end

-- Conectar el script a la parte del Brainrot
local brainrotPart = workspace:WaitForChild("Brainrot")  -- Asegúrate de que el Brainrot esté en el workspace y se llame "Brainrot"
brainrotPart.Touched:Connect(onBrainrotTouched)

-- Menú de opciones
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = player:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 200, 0, 100)
Frame.Position = UDim2.new(0.5, -100, 0.5, -50)
Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Frame.Parent = ScreenGui

local InvisibleButton = Instance.new("TextButton")
InvisibleButton.Size = UDim2.new(0, 200, 0, 50)
InvisibleButton.Position = UDim2.new(0, 0, 0, 0)
InvisibleButton.Text = "Hacer Invisible"
InvisibleButton.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
InvisibleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
InvisibleButton.Parent = Frame

InvisibleButton.MouseButton1Click:Connect(makeInvisible)

local TeleportButton = Instance.new("TextButton")
TeleportButton.Size = UDim2.new(0, 200, 0, 50)
TeleportButton.Position = UDim2.new(0, 0, 0, 50)
TeleportButton.Text = "Teletransportar a Base"
TeleportButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
TeleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TeleportButton.Parent = Frame

TeleportButton.MouseButton1Click:Connect(teleportToBase)

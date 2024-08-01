-- Define the Uber Eats system
local deliverySystem = game:GetService("Workspace").uberEatsSystem

-- Define restaurant and delivery locations
local locations = {
    {name = "Jalebag", path = deliverySystem.restaurantLocations.Jalebag},
    {name = "Dunkin Donuts", path = deliverySystem.restaurantLocations["Dunkin Donuts"]},
    {name = "Milktea", path = deliverySystem.restaurantLocations.Milktea},
    {name = "Emeraude", path = deliverySystem.deliveryLocations.Emeraude},
    {name = "Chi", path = deliverySystem.deliveryLocations.Chi}
}

-- Create ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AutoTeleportProximityPromptGui"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Create Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 200, 0, 140)
frame.Position = UDim2.new(0.5, -100, 0.5, -70)
frame.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui

-- Create TextLabel
local textLabel = Instance.new("TextLabel")
textLabel.Size = UDim2.new(1, 0, 0.3, 0)
textLabel.Position = UDim2.new(0, 0, 0, 0)
textLabel.Text = "Auto Fire & Teleport GUI"
textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
textLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
textLabel.Parent = frame

-- Create Toggle Buttons
local toggleFireButton = Instance.new("TextButton")
toggleFireButton.Size = UDim2.new(0.8, 0, 0.25, 0)
toggleFireButton.Position = UDim2.new(0.1, 0, 0.3, 0)
toggleFireButton.Text = "Toggle Auto Fire"
toggleFireButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleFireButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
toggleFireButton.Parent = frame

local toggleTeleportButton = Instance.new("TextButton")
toggleTeleportButton.Size = UDim2.new(0.8, 0, 0.25, 0)
toggleTeleportButton.Position = UDim2.new(0.1, 0, 0.6, 0)
toggleTeleportButton.Text = "Toggle Auto Teleport"
toggleTeleportButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleTeleportButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
toggleTeleportButton.Parent = frame

-- Auto Fire Proximity Prompt Functionality
local autoFireEnabled = false

local function fireProximityPrompts()
    while autoFireEnabled do
        for _, proximityPrompt in pairs(workspace:GetDescendants()) do
            if proximityPrompt:IsA("ProximityPrompt") then
                fireproximityprompt(proximityPrompt)
            end
        end
        wait(0.1) -- Adjust the wait time as needed
    end
end

toggleFireButton.MouseButton1Click:Connect(function()
    autoFireEnabled = not autoFireEnabled
    if autoFireEnabled then
        toggleFireButton.Text = "Auto Fire: ON"
        coroutine.wrap(fireProximityPrompts)()
    else
        toggleFireButton.Text = "Auto Fire: OFF"
    end
end)

-- Auto Teleport Functionality
local autoTeleportEnabled = false

local function autoTeleport()
    while autoTeleportEnabled do
        for _, location in ipairs(locations) do
            if autoTeleportEnabled then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = location.path.CFrame
                wait(1) -- Interval between teleports
            else
                break
            end
        end
    end
end

toggleTeleportButton.MouseButton1Click:Connect(function()
    autoTeleportEnabled = not autoTeleportEnabled
    if autoTeleportEnabled then
        toggleTeleportButton.Text = "Auto Teleport: ON"
        coroutine.wrap(autoTeleport)()
    else
        toggleTeleportButton.Text = "Auto Teleport: OFF"
    end
end)

-- Make GUI Draggable
local UIS = game:GetService("UserInputService")
local dragging
local dragInput
local dragStart
local startPos

local function update(input)
    local delta = input.Position - dragStart
    frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

frame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType.Touch then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        update(input)
    end
end)

-- Get the Players service
local Players = game:GetService("Players")

-- Function to create a highlight effect for a player
local function highlightPlayer(player)
    local character = player.Character or player.CharacterAdded:Wait()
    if character then
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            local highlight = Instance.new("SelectionBox")
            highlight.Color3 = Color3.new(1, 1, 0) -- Yellow color
            highlight.LineThickness = 0.05
            highlight.Transparency = 0.5
            highlight.Adornee = character
            highlight.Parent = character
            humanoid.Died:Connect(function()
                highlight:Destroy()
            end)
        end
    end
end

-- Function to highlight all players in the game
local function highlightAllPlayers()
    for _, player in ipairs(Players:GetPlayers()) do
        highlightPlayer(player)
    end
end

-- Connect the function to highlight all players when a new player joins
Players.PlayerAdded:Connect(highlightPlayer)

-- Highlight all existing players when the script starts
highlightAllPlayers()

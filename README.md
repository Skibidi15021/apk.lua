-- Script to highlight all players and make them visible through walls
local Players = game:GetService("Players")

-- Function to create a highlight for a character
local function highlightCharacter(character)
    -- Check if the character already has a highlight
    if character:FindFirstChild("Highlight") then
        return
    end

    -- Create a new Highlight instance
    local highlight = Instance.new("Highlight")
    highlight.Name = "Highlight"
    highlight.Parent = character
    highlight.Adornee = character -- Attach to the character
    highlight.FillTransparency = 0.7 -- Make the fill slightly transparent
    highlight.OutlineTransparency = 0.3 -- Make the outline stand out
    highlight.FillColor = Color3.fromRGB(0, 255, 0) -- Set fill color to green
    highlight.OutlineColor = Color3.fromRGB(255, 255, 255) -- Set outline color to white

    -- Ensure it works through walls
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
end

-- Function to handle when a new player joins
local function onPlayerAdded(player)
    player.CharacterAdded:Connect(function(character)
        -- Add highlight when character spawns
        highlightCharacter(character)
    end)

    -- Add highlight if the character already exists
    if player.Character then
        highlightCharacter(player.Character)
    end
end

-- Connect to existing players and new players joining
for _, player in ipairs(Players:GetPlayers()) do
    onPlayerAdded(player)
end
Players.PlayerAdded:Connect(onPlayerAdded)

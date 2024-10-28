local part = script.Parent

-- Function to remove tools from the player’s backpack and store them
local function hideTools(player)
    local toolsFolder = Instance.new("Folder")
    toolsFolder.Name = "HiddenTools"
    toolsFolder.Parent = player

    for _, tool in ipairs(player.Backpack:GetChildren()) do
        if tool:IsA("Tool") then
            tool.Parent = toolsFolder -- Move tool to HiddenTools folder
        end
    end
end

-- Function to return tools to the player's backpack
local function showTools(player)
    local toolsFolder = player:FindFirstChild("HiddenTools")
    if toolsFolder then
        for _, tool in ipairs(toolsFolder:GetChildren()) do
            tool.Parent = player.Backpack -- Return tool to Backpack
        end
        toolsFolder:Destroy()
    end
end

-- Detect when a player enters the part
part.Touched:Connect(function(hit)
    local character = hit.Parent
    local player = game.Players:GetPlayerFromCharacter(character)
    if player and not player:FindFirstChild("HiddenTools") then
        hideTools(player)
    end
end)

-- Detect when a player exits the part
part.TouchEnded:Connect(function(hit)
    local character = hit.Parent
    local player = game.Players:GetPlayerFromCharacter(character)
    if player then
        showTools(player)
    end
end)

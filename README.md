local part = script.Parent

-- Function to hide the player's inventory
local function hideInventory(player)
    local playerGui = player:FindFirstChild("PlayerGui")
    if playerGui then
        playerGui:SetAttribute("InventoryHidden", true)
        player.PlayerGui.Backpack.Enabled = false -- Hide Backpack UI
    end
end

-- Function to show the player's inventory again
local function showInventory(player)
    local playerGui = player:FindFirstChild("PlayerGui")
    if playerGui and playerGui:GetAttribute("InventoryHidden") then
        playerGui:SetAttribute("InventoryHidden", nil)
        player.PlayerGui.Backpack.Enabled = true -- Show Backpack UI
    end
end

-- Detect when a player steps into the part
part.Touched:Connect(function(hit)
    local character = hit.Parent
    local player = game.Players:GetPlayerFromCharacter(character)
    if player then
        hideInventory(player)
    end
end)

-- Detect when a player steps out of the part
part.TouchEnded:Connect(function(hit)
    local character = hit.Parent
    local player = game.Players:GetPlayerFromCharacter(character)
    if player then
        showInventory(player)
    end
end)

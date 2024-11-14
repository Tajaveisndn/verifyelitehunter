local EliteHunter = {}

EliteHunter.GetEliteHunter = function()
    local args = {
        [1] = "Elite Hunter"
    }
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end

EliteHunter.FormatNpcName = function()
    local player = game:GetService("Players").LocalPlayer
    local questTitle = player.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text
    
    -- Remove "Defeat " prefix and numbers/parentheses
    local npcName = questTitle:gsub("Defeat ", ""):gsub("%s*%(.*%)", "")
    return npcName
end

EliteHunter.CheckElite = function()
    local npcName = EliteHunter.FormatNpcName()
    
    for _, model in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
        if model:IsA("Model") and model.Name == npcName then
            return model
        end
    end
    return nil
end

return EliteHunter

getgenv().AutoFarm = true

task.spawn(function()
    while getgenv().AutoFarm do
        -- Sprzedaje wszystko dla hajsu
        local remotes = game:GetService("ReplicatedStorage"):FindFirstChild("Remotes")
        if remotes then
            if remotes:FindFirstChild("SellAll") then
                remotes.SellAll:FireServer()
            end
            -- Odbiera nagrody
            if remotes:FindFirstChild("ClaimQuest") then
                remotes.ClaimQuest:FireServer()
            end
        end
        task.wait(0.5)
    end
end)

print("Skrypt Maaciusa gotowy!")

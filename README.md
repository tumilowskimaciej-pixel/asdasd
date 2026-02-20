local player = game:GetService("Players").LocalPlayer
local pGui = player:WaitForChild("PlayerGui")

-- Usuwanie starego GUI jeśli istnieje
if pGui:FindFirstChild("MaaciusDupe") then pGui.MaaciusDupe:Destroy() end

local sg = Instance.new("ScreenGui", pGui)
sg.Name = "MaaciusDupe"

local frame = Instance.new("Frame", sg)
frame.Size = UDim2.new(0, 250, 0, 350)
frame.Position = UDim2.new(0.5, -125, 0.5, -175)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "MAACIUS DUPE V2"
title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
title.TextColor3 = Color3.new(1, 1, 1)

local list = Instance.new("ScrollingFrame", frame)
list.Size = UDim2.new(1, -20, 0, 240)
list.Position = UDim2.new(0, 10, 0, 50)
list.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
list.CanvasSize = UDim2.new(0, 0, 5, 0)

local layout = Instance.new("UIListLayout", list)
layout.Padding = UDim.new(0, 5)

local dupeBtn = Instance.new("TextButton", frame)
dupeBtn.Size = UDim2.new(1, -20, 0, 40)
dupeBtn.Position = UDim2.new(0, 10, 0, 300)
dupeBtn.Text = "DUPLIKUJ PRZEDMIOT"
dupeBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
dupeBtn.TextColor3 = Color3.new(1, 1, 1)

local selected = nil

-- Funkcja szukająca itemów (sprawdza różne miejsca)
local function getInv()
    return player:FindFirstChild("Inventory") or player:FindFirstChild("Backpack") or player:FindFirstChild("Data") and player.Data:FindFirstChild("Inventory")
end

local function refresh()
    for _, v in pairs(list:GetChildren()) do if v:IsA("TextButton") then v:Destroy() end end
    
    local inv = getInv()
    if inv then
        for _, item in pairs(inv:GetChildren()) do
            local btn = Instance.new("TextButton", list)
            btn.Size = UDim2.new(1, 0, 0, 30)
            btn.Text = item.Name
            btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            btn.TextColor3 = Color3.new(1, 1, 1)
            
            btn.MouseButton1Click:Connect(function()
                selected = item.Name
                print("Wybrano: " .. selected)
                for _, b in pairs(list:GetChildren()) do if b:IsA("TextButton") then b.BackgroundColor3 = Color3.fromRGB(50, 50, 50) end end
                btn.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
            end)
        end
    end
end

dupeBtn.MouseButton1Click:Connect(function()
    if selected then
        -- TUTAJ wpisujemy Remote z gry Case Paradise
        -- Najczęściej: game:GetService("ReplicatedStorage").Remotes.UpdateInventory:FireServer(selected, 1)
        print("MAACIUS DUPE: Próba skopiowania " .. selected)
    end
end)

refresh()

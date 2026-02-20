local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local ItemList = Instance.new("ScrollingFrame")
local DupeButton = Instance.new("TextButton")
local UIListLayout = Instance.new("UIListLayout")

local selectedItem = nil

-- Ustawienia GUI
ScreenGui.Parent = game:GetService("CoreGui")
ScreenGui.Name = "MaaciusDupeGUI"

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Position = UDim2.new(0.5, -100, 0.5, -150)
MainFrame.Size = UDim2.new(0, 200, 0, 300)
MainFrame.Active = true
MainFrame.Draggable = true

Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "MAACIUS DUPE"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.BackgroundColor3 = Color3.fromRGB(45, 45, 45)

ItemList.Parent = MainFrame
ItemList.Position = UDim2.new(0, 5, 0, 35)
ItemList.Size = UDim2.new(1, -10, 0, 220)
ItemList.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
ItemList.CanvasSize = UDim2.new(0, 0, 10, 0)

UIListLayout.Parent = ItemList
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

DupeButton.Parent = MainFrame
DupeButton.Position = UDim2.new(0, 5, 0, 260)
DupeButton.Size = UDim2.new(1, -10, 0, 35)
DupeButton.Text = "DUPE SELECTED"
DupeButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
DupeButton.TextColor3 = Color3.new(1, 1, 1)

-- Funkcja czytająca EQ
local function updateInventory()
    for _, child in pairs(ItemList:GetChildren()) do
        if child:IsA("TextButton") then child:Destroy() end
    end

    local player = game:GetService("Players").LocalPlayer
    local inv = player:FindFirstChild("Inventory") or player:FindFirstChild("Backpack")

    if inv then
        for _, item in pairs(inv:GetChildren()) do
            local itemBtn = Instance.new("TextButton")
            itemBtn.Parent = ItemList
            itemBtn.Size = UDim2.new(1, 0, 0, 30)
            itemBtn.Text = item.Name
            itemBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
            itemBtn.TextColor3 = Color3.new(1, 1, 1)

            itemBtn.MouseButton1Click:Connect(function()
                selectedItem = item.Name
                print("Maacius: Wybrano " .. selectedItem)
                for _, btn in pairs(ItemList:GetChildren()) do
                    if btn:IsA("TextButton") then btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50) end
                end
                itemBtn.BackgroundColor3 = Color3.fromRGB(100, 100, 255)
            end)
        end
    end
end

-- Logika Dupe
DupeButton.MouseButton1Click:Connect(function()
    if selectedItem then
        print("Maacius: Próba duplikacji: " .. selectedItem)
        -- Tutaj musisz wpisać RemoteEvent z Case Paradise, który odpowiada za przedmioty
        -- Przykład: game:GetService("ReplicatedStorage").Remotes.AddInventory:FireServer(selectedItem)
    else
        print("Najpierw wybierz przedmiot!")
    end
end)

updateInventory()
print("GUI Maaciusa gotowe!")

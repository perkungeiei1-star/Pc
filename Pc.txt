    local Players = game:GetService("Players")
    local TweenService = game:GetService("TweenService")
    local RunService = game:GetService("RunService")
    local UserInputService = game:GetService("UserInputService")
    local ReplicatedStorage = game:GetService("ReplicatedStorage")

    local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
    local Window = Fluent:CreateWindow({
        Title = "BenJaMinZ Hub",
        SubTitle = "Made by BenJaMinZ",
        TabWidth = 200,
        Size = UDim2.fromOffset(580,460),
        Acrylic = false,
        Theme = "Dark",
        MinimizeKey = Enum.KeyCode.RightControl
    })
    local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
    local player = Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local hrp = character:WaitForChild("HumanoidRootPart")

    local function initCharacter(char)
        character = char
        humanoid = character:WaitForChild("Humanoid")
        hrp = character:WaitForChild("HumanoidRootPart")
    end

    local TabMain = Window:AddTab({ Title = "Main", Icon = "hammer" })
    local TabTeleportAFK = Window:AddTab({ Title = "Teleport AFK", Icon = "shield" })
    local TabTeleportIsland = Window:AddTab({ Title = "Teleport Island", Icon = "globe" })
    local TabSniper = Window:AddTab({ Title = "Sniper Box&Compass", Icon = "box" })
    local TabSniperFruit = Window:AddTab({ Title = "Sniper Devil Fruit", Icon = "apple" })
    local TabJuice = Window:AddTab({ Title = "Buy Juice", Icon = "shopping-cart" })
    local TabMixerV2 = Window:AddTab({ Title = "Mixer Fruit", Icon = "syringe" })
    local Setting = Window:AddTab({ Title = "Setting", Icon = "settings" })

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local VirtualUser = game:GetService("VirtualUser")

player.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new())
end)

game:GetService("StarterGui"):SetCore("SendNotification", {
    Title = "BenJaMinZ Hub",
    Text = "AntiAFK Active",
    Duration = 5
})


    local function teleportAFK(pos)
        initCharacter(player.Character or player.CharacterAdded:Wait())
        hrp.CFrame = CFrame.new(unpack(pos))
    end

    TabTeleportAFK:AddButton({
        Title = "AFK 1",
        Callback = function() teleportAFK({22.6135, 200003.5, 170.5}) end
    })
    TabTeleportAFK:AddButton({
        Title = "AFK 2",
        Callback = function() teleportAFK({-10.989439010620117, 200004.5, 194.4368438720703}) end
    })
    TabTeleportAFK:AddButton({
        Title = "AFK 3",
        Callback = function() teleportAFK({-11.223817825317383, 200004.5, 201.46461486816406}) end
    })

    local function AddTeleportButton(tab, name, position)
        tab:AddButton({
            Title = name,
            Callback = function()
                initCharacter(player.Character or player.CharacterAdded:Wait())
                hrp.CFrame = CFrame.new(unpack(position))
            end
        })
    end

    -- ใส่ตำแหน่งทุกเกาะ
    AddTeleportButton(TabTeleportIsland, "Spawn Land 1", {119.5228, 248.0, -1232.9507})
    AddTeleportButton(TabTeleportIsland, "Spawn Land 2", {-296.1837, 265.4994, -96.6268})
    AddTeleportButton(TabTeleportIsland, "Sam Land", {-1281.9680, 239.9977, -1371.8807})
    AddTeleportButton(TabTeleportIsland, "Sell Drink Land", {1626.3267, 218, 2197.0505})
    AddTeleportButton(TabTeleportIsland, "House Land 1", {898.5979, 302.9982, 1218.1807})
    AddTeleportButton(TabTeleportIsland, "Treea Land", {1161.2182, 238.9002, 3340.6108})
    AddTeleportButton(TabTeleportIsland, "Tiny Land 1", {-35.2822, 228.9999, 2156.0024})
    AddTeleportButton(TabTeleportIsland, "Tiny Land 2", {-4004.8452, 215.9999, -2190.2009})
    AddTeleportButton(TabTeleportIsland, "Forset Land", {-6032.4243, 402, -5.0926})
    AddTeleportButton(TabTeleportIsland, "Egypt Land", {118.2466, 309.9999, 4945.2231})
    AddTeleportButton(TabTeleportIsland, "C Land", {3205.0498, 217, 1560.7314})
    AddTeleportButton(TabTeleportIsland, "Boss Land", {4566.2084, 217, 5462.7485})
    AddTeleportButton(TabTeleportIsland, "Evil Land", {-5271.3535, 516, -7846.6772})
    AddTeleportButton(TabTeleportIsland, "Snowy Land", {-2089.4167, 297, 3418.6816})
    AddTeleportButton(TabTeleportIsland, "SnowyMountains Land", {6644.3789, 417.9989, -1478.4702})
    AddTeleportButton(TabTeleportIsland, "SandCastle Land", {1078.3050, 245.2001, -3335.6132})
    AddTeleportButton(TabTeleportIsland, "Caver Land", {-1094.7250, 356, 1719.1688})
    AddTeleportButton(TabTeleportIsland, "Rock Land", {4895, 398.751343, -7194, 1, 0, 0, 0, 1, 0, 0, 0, 1})
    AddTeleportButton(TabTeleportIsland, "Marineford Land", {-3133.034912109375, 557.531005859375, -4087.6904296875})
    AddTeleportButton(TabTeleportIsland, "Use Boat TP AFK", {5036.73779296875, 220.18453979492188, 21985.28125})

local function AddSniperToggle(tab, name)
    tab:AddToggle(name, {
        Title = name,
        Default = false,
        Callback = function(state)
            local key = "Auto_"..name:gsub("%s","_")
            if state then
                _G[key] = true
                task.spawn(function()
                    while _G[key] do
                        task.wait(0.1)
                        initCharacter(player.Character or player.CharacterAdded:Wait())
                        local model = workspace:FindFirstChild(name)
                        if model and model:IsA("Model") then
                            if not model.PrimaryPart then
                                local firstPart = model:FindFirstChildWhichIsA("BasePart")
                                if firstPart then model.PrimaryPart = firstPart end
                            end
                            if model.PrimaryPart then
                                model:SetPrimaryPartCFrame(hrp.CFrame)
                                task.wait(0.1)
                            end
                        end
                    end
                end)
            else
                _G[key] = false
            end
        end
    })
end

for _, box in ipairs({"Compass","Common Box","Uncommon Box","Rare Box","Ultra Rare Box"}) do
    AddSniperToggle(TabSniper, box)
end

local Section = TabSniperFruit:AddSection("Ultra Rare & Rare Fruit")
    local fruitsList = {
        "Phoenix Fruit", "Quake Fruit", "Dark Fruit", "Gas Fruit",
        "Plasma Fruit", "Magma Fruit", "Rumble Fruit",
        "Sand Fruit", "Flare Fruit", "Chilly Fruit", "Candy Fruit",
        "Venom Fruit", "Ope Fruit"
        

    }
    local returnPosition = CFrame.new(-10.989439010620117, 200004.5, 194.4368438720703)

    local function warpAndClick(obj)
        if not obj then return end
        initCharacter(player.Character or player.CharacterAdded:Wait())
        local clickDetector = obj:FindFirstChildWhichIsA("ClickDetector")
        if not clickDetector then
            clickDetector = obj:FindFirstChild("Main1") and obj.Main1:FindFirstChildWhichIsA("ClickDetector")
            if not clickDetector and obj:FindFirstChild("Handle") then
                clickDetector = obj.Handle:FindFirstChildWhichIsA("ClickDetector")
            end
        end
        hrp.CFrame = obj.CFrame + Vector3.new(0,3,2)
        task.wait(0.1)
        if clickDetector then
            for i=1,3 do fireclickdetector(clickDetector); task.wait(0.05) end
        end
    end

    local function ClickFruit(fruitName)
        local fruit = workspace:FindFirstChild(fruitName)
        if fruit then
            local handle = fruit:FindFirstChild("Handle") or fruit:FindFirstChild("Main1") or fruit
            warpAndClick(handle)
            task.wait(0.1)
            hrp.CFrame = returnPosition
        end
    end

    local function AddFruitSniperToggle(tab, fruitName)
        tab:AddToggle(fruitName, {
            Title = fruitName,
            Default = false,
            Callback = function(state)
                local key = "AutoFruit_"..fruitName:gsub("%s","_")
                if state then
                    _G[key] = true
                    task.spawn(function()
                        while _G[key] do
                            task.wait(0.2)
                            pcall(function() ClickFruit(fruitName) end)
                        end
                    end)
                else
                    _G[key] = false
                end
            end
        })
    end

    for _, fruit in ipairs(fruitsList) do AddFruitSniperToggle(TabSniperFruit, fruit) end
    local Section = TabSniperFruit:AddSection("Uncommon Fruit")
        local fruitsList = {
        "Barrier Fruit", "Diamond Fruit", "Smelt Fruit", "Bomb Fruit", "Luck Fruit"
    }
    local returnPosition = CFrame.new(-10.989439010620117, 200004.5, 194.4368438720703)

    local function warpAndClick(obj)
        if not obj then return end
        initCharacter(player.Character or player.CharacterAdded:Wait())
        local clickDetector = obj:FindFirstChildWhichIsA("ClickDetector")
        if not clickDetector then
            clickDetector = obj:FindFirstChild("Main1") and obj.Main1:FindFirstChildWhichIsA("ClickDetector")
            if not clickDetector and obj:FindFirstChild("Handle") then
                clickDetector = obj.Handle:FindFirstChildWhichIsA("ClickDetector")
            end
        end
        hrp.CFrame = obj.CFrame + Vector3.new(0,3,2)
        task.wait(0.1)
        if clickDetector then
            for i=1,3 do fireclickdetector(clickDetector); task.wait(0.05) end
        end
    end

    local function ClickFruit(fruitName)
        local fruit = workspace:FindFirstChild(fruitName)
        if fruit then
            local handle = fruit:FindFirstChild("Handle") or fruit:FindFirstChild("Main1") or fruit
            warpAndClick(handle)
            task.wait(0.1)
            hrp.CFrame = returnPosition
        end
    end

    local function AddFruitSniperToggle(tab, fruitName)
        tab:AddToggle(fruitName, {
            Title = fruitName,
            Default = false,
            Callback = function(state)
                local key = "AutoFruit_"..fruitName:gsub("%s","_")
                if state then
                    _G[key] = true
                    task.spawn(function()
                        while _G[key] do
                            task.wait(0.2)
                            pcall(function() ClickFruit(fruitName) end)
                        end
                    end)
                else
                    _G[key] = false
                end
            end
        })
    end

    for _, fruit in ipairs(fruitsList) do AddFruitSniperToggle(TabSniperFruit, fruit) end
    

    local Players = game:GetService("Players")
    local player = Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    local AutoDrinkEnabled = false
    local autoDrinkThread = nil

    local drinkNames = {
        "Fruit Juice",
        "Sour Juice",
        "Coconut Milk",
        "Pear Juice",
        "Pumpkin Juice",
        "Banana Juice",
        "Apple Juice",
    }

    local function clickDrink(obj)
        if not obj then return end

        if obj:IsA("Tool") then
            local humanoid = character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid:EquipTool(obj)
                task.wait(0.05)
                local handle = obj:FindFirstChild("Handle")
                if handle then
                    local clickDetector = handle:FindFirstChildWhichIsA("ClickDetector")
                    if clickDetector then
                        pcall(fireclickdetector, clickDetector)
                        print("ดื่ม Tool: "..obj.Name)
                    else
                        if obj:FindFirstChildWhichIsA("RemoteEvent") then
                            obj:Activate()
                            print("Activate Tool: "..obj.Name)
                        end
                    end
                end
            end
        else
            local clickDetector = obj:FindFirstChildWhichIsA("ClickDetector")
            if clickDetector then
                pcall(fireclickdetector, clickDetector)
                print("ดื่ม Workspace: "..obj.Name)
            end
        end
    end

    local function startAutoDrink()
        if autoDrinkThread then return end
        autoDrinkThread = task.spawn(function()
            while AutoDrinkEnabled do
                for _, name in ipairs(drinkNames) do
                    local drink = workspace:FindFirstChild(name)
                    if drink then
                        clickDrink(drink)
                        task.wait(0.01)
                    end
                end

                for _, tool in ipairs(player.Backpack:GetChildren()) do
                    if table.find(drinkNames, tool.Name) then
                        clickDrink(tool)
                        task.wait(0.01)
                    end
                end

                for _, tool in ipairs(character:GetChildren()) do
                    if table.find(drinkNames, tool.Name) then
                        clickDrink(tool)
                        task.wait(0.01)
                    end
                end

                task.wait(0.01)
            end
            autoDrinkThread = nil
        end)
    end

local Players = game:GetService("Players")
local player = Players.LocalPlayer

local character
local humanoid
local hrp

local function refreshCharacter()
    character = player.Character or player.CharacterAdded:Wait()
    hrp = character:WaitForChild("HumanoidRootPart")
    humanoid = character:WaitForChild("Humanoid")
end
refreshCharacter()

player.CharacterAdded:Connect(function(char)
    character = char
    hrp = char:WaitForChild("HumanoidRootPart")
    humanoid = char:WaitForChild("Humanoid")
    print("รีเฟรช character ใหม่หลังจากตาย")

    if AutoDrinkEnabled2 then
        task.wait(0.5)
        startAutoDrink2()
    end
end)

local AutoDrinkEnabled2 = false
local autoDrinkThread2 = nil

local drinkNames2 = {
    "Cider+",
    "Lemonade+",
    "Juice+",
    "Smoothie+"
}

local function realClickDrink2(tool)
    if not tool then return end

    if tool:IsA("Tool") then
        if humanoid then
            humanoid:EquipTool(tool)
            task.wait(0.05)
            local handle = tool:FindFirstChild("Handle")
            if handle then
                local clickDetector = handle:FindFirstChildWhichIsA("ClickDetector")
                if clickDetector then
                    pcall(fireclickdetector, clickDetector)
                    print("ดื่ม Tool (ClickDetector): "..tool.Name)
                elseif tool:FindFirstChildWhichIsA("RemoteEvent") then
                    tool:FindFirstChildWhichIsA("RemoteEvent"):FireServer()
                    print("ดื่ม Tool (RemoteEvent): "..tool.Name)
                else
                    pcall(function() tool:Activate() end)
                    print("ดื่ม Tool (Activate): "..tool.Name)
                end
            end
        end
    else
        local clickDetector = tool:FindFirstChildWhichIsA("ClickDetector")
        if clickDetector then
            pcall(fireclickdetector, clickDetector)
            print("ดื่ม Workspace: "..tool.Name)
        end
    end
end

function startAutoDrink2()
    if autoDrinkThread2 then return end

    for _, tool in ipairs(player.Backpack:GetChildren()) do
        if table.find(drinkNames2, tool.Name) and humanoid then
            humanoid:EquipTool(tool)
        end
    end
    for _, tool in ipairs(character:GetChildren()) do
        if table.find(drinkNames2, tool.Name) and humanoid then
            humanoid:EquipTool(tool)
        end
    end

    autoDrinkThread2 = task.spawn(function()
        while AutoDrinkEnabled2 do
            for _, name in ipairs(drinkNames2) do
                local drink = workspace:FindFirstChild(name)
                if drink then
                    realClickDrink2(drink)
                    task.wait(0.01)
                end
            end

            for _, tool in ipairs(player.Backpack:GetChildren()) do
                if table.find(drinkNames2, tool.Name) then
                    realClickDrink2(tool)
                    task.wait(0.01)
                end
            end

            for _, tool in ipairs(character:GetChildren()) do
                if table.find(drinkNames2, tool.Name) then
                    realClickDrink2(tool)
                    task.wait(0.01)
                end
            end

            task.wait(0.01)
        end
        autoDrinkThread2 = nil
    end)
end

function stopAutoDrink2()
    AutoDrinkEnabled2 = false
    if autoDrinkThread2 then
        autoDrinkThread2 = nil
    end

    if humanoid and humanoid:FindFirstChildOfClass("Tool") then
        humanoid:UnequipTools()
    end
end

TabJuice:AddToggle("AutoDrink2", {
    Title = "Auto Drink Beverages",
    Default = false,
    Callback = function(state)
        if state then
            AutoDrinkEnabled2 = true
            print("เริ่ม Auto Drink ✅")
            startAutoDrink2()
        else
            print("หยุด Auto Drink ❌")
            stopAutoDrink2()
        end
    end
})


    player.CharacterAdded:Connect(function(char)
        character = char
        if AutoDrinkEnabled2 then
            task.wait(1)
            startAutoDrink2()
        end
    end)

    TabMain:AddToggle("AutoClaimSam", {
        Title = "Auto Claim Sam Quest",
        Default = false,
        Callback = function(state)
            _G.AutoClaimSam = state
            spawn(function()
                while _G.AutoClaimSam do
                    task.wait(0.5)
                    local args = { [1] = "Claim1" }
                    game:GetService("ReplicatedStorage"):WaitForChild("Connections"):WaitForChild("Claim_Sam"):FireServer(unpack(args))
                end
            end)
        end
    })

    local Players = game:GetService("Players")
    local player = Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    local AutoTrashEnabled = false
    local autoTrashThread = nil

    local trashNames = {
        "Cider+",
        "Lemonade+",
        "Juice+",
        "Smoothie+"
    }

    local function realDropTool(tool)
        if not tool then return end
        if tool:IsA("Tool") then
            local humanoid = character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid:EquipTool(tool)
                task.wait(0.05)
                
                local remote = tool:FindFirstChildWhichIsA("RemoteEvent")
                if remote then
                    remote:FireServer()
                else
                    pcall(function() tool.Parent = workspace end)
                end
                
                print("ทิ้งของ: "..tool.Name)
            end
        end
    end

    local function startAutoTrash()
        if autoTrashThread then return end
        autoTrashThread = task.spawn(function()
            while AutoTrashEnabled do
                for _, tool in ipairs(player.Backpack:GetChildren()) do
                    if table.find(trashNames, tool.Name) then
                        realDropTool(tool)
                        task.wait(0.1)
                    end
                end

                for _, tool in ipairs(character:GetChildren()) do
                    if table.find(trashNames, tool.Name) then
                        realDropTool(tool)
                        task.wait(0.1)
                    end
                end

                task.wait(0.1)
            end
            autoTrashThread = nil
        end)
    end

    local AutoMixEnabled = false
local autoMixThread = nil

local function warpAndClickMixer(obj)
    if not hrp then return end
    if typeof(obj) == "CFrame" then 
        hrp.CFrame = obj + Vector3.new(0, 3, 2)
        task.wait(0.05)
        return 
    end
    if obj and obj.Parent then
        hrp.CFrame = obj.CFrame + Vector3.new(0, 3, 2)
        task.wait(0.05)
        local clickDetector = obj:FindFirstChildWhichIsA("ClickDetector")
        if clickDetector then 
            fireclickdetector(clickDetector) 
        end
    end
end

local function startAutoClick()
    if autoMixThread then return end
    autoMixThread = task.spawn(function()
        while AutoMixEnabled do
            if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then
                player.CharacterAdded:Wait()
                hrp = player.Character:WaitForChild("HumanoidRootPart")
                local humanoid = player.Character:WaitForChild("Humanoid")
                humanoid.Died:Connect(function()
                    player.CharacterAdded:Wait()
                    hrp = player.Character:WaitForChild("HumanoidRootPart")
                end)
            end

            local targets = {}

            if workspace:FindFirstChild("Barrels") then
                if workspace.Barrels:FindFirstChild("Crates") then
                    for _, crate in ipairs(workspace.Barrels.Crates:GetChildren()) do
                        table.insert(targets, crate)
                    end
                end
                if workspace.Barrels:FindFirstChild("Barrels") then
                    for _, barrel in ipairs(workspace.Barrels.Barrels:GetChildren()) do
                        table.insert(targets, barrel)
                    end
                end
            end

            for _, obj in ipairs(targets) do
                if not AutoMixEnabled then break end
                warpAndClickMixer(obj)
                task.wait(0.2)
            end

            task.wait(0.5)
        end
        autoMixThread = nil
    end)
end

TabMixerV2:AddToggle("AutoMixFruit", {
    Title = "Auto crate and Barrel",
    Default = false,
    Callback = function(state)
        AutoMixEnabled = state
        if state then startAutoClick() end
    end
})


    local ToggleAutoTrash = TabJuice:AddToggle("Auto Trash Drinks", {
        Title = "Auto Drop Drinks",
        Default = false,
        Callback = function(state)
            AutoTrashEnabled = state
            if state then
                startAutoTrash()
            end
        end
    })

    local ToggleQuestHaki = TabMain:AddToggle("AutoQuestHaki", {
    Title = "Auto Get Haki",
    Default = false,
    Callback = function(state)
        _G.auto = state
        if state then
            task.spawn(function()
                while _G.auto do
                    pcall(function()
                        local args = {
                            [1] = "III"
                        }
                        workspace:WaitForChild("Merchants")
                            :WaitForChild("QuestHakiMerchant")
                            :WaitForChild("Clickable")
                            :WaitForChild("Retum")
                            :FireServer(unpack(args))
                    end)
                    task.wait(1) -- หน่วง 1 วิ
                end
            end)
        end
    end
})

local NoclipEnabled = false
local NoclipConnection

_G.auto = false

local ToggleAutoIII = TabMain:AddToggle("Auto Kenbunshoku", {
    Title = "Auto Fram Kenbunshoku",
    Description = "Use Bring Mob and Noclip",
    Default = false,
    Callback = function(state)
        _G.auto = state
        if state then
            task.spawn(function()
                while _G.auto do
                    pcall(function()
                        local player = game.Players.LocalPlayer
                        local userData = workspace:WaitForChild("UserData"):WaitForChild("User_"..player.UserId)
                        local III = userData:WaitForChild("III")
                        local args = {
                            [1] = "On",
                            [2] = 1
                        }
                        III:FireServer(unpack(args))
                    end)
                    task.wait(1)
                end
            end)
        end
    end
})

_G.PullThug = false

local TogglePullThug = TabMain:AddToggle("Bring Mob", {
    Title = "Bring Mob",
    Default = false,
    Callback = function(state)
        _G.PullThug = state
        if state then
            task.spawn(function()
                while _G.PullThug do
                    pcall(function()
                        local player = game.Players.LocalPlayer
                        local char = player.Character or player.CharacterAdded:Wait()
                        local hrp = char:FindFirstChild("HumanoidRootPart")

                        if hrp and workspace:FindFirstChild("Enemies") then
                            local thugNames = {
                                ["Lv12 Thug"] = true,
                                ["Lv15 Thug"] = true,
                            }

                            for name, _ in pairs(thugNames) do
                                local enemy = workspace.Enemies:FindFirstChild(name)
                                if enemy and enemy:FindFirstChild("HumanoidRootPart") and enemy:FindFirstChild("Humanoid") then
                                    local eHRP = enemy.HumanoidRootPart
                                    eHRP.CFrame = hrp.CFrame * CFrame.new(0, 0, 0)
                                    eHRP.Anchored = true
                                    enemy.Humanoid.PlatformStand = true
                                end
                            end
                        end
                    end)
                    task.wait(0.2)
                end
            end)
        end
    end
})

    local ESPs = {}
    local ESPEnabled = false
    local ESPColor = Color3.fromRGB(255,0,0)

    local function createESP(plr)
        if plr == player or ESPs[plr] then return end
        local char = plr.Character
        local hrpRef = char and char:FindFirstChild("HumanoidRootPart")
        if not hrpRef then return end

        local box = Instance.new("BoxHandleAdornment")
        box.Adornee = hrpRef
        box.AlwaysOnTop = true
        box.Size = Vector3.new(2,5,1)
        box.Color3 = ESPColor
        box.Transparency = 0.5
        box.Parent = workspace

        local billboard = Instance.new("BillboardGui")
        billboard.Size = UDim2.new(0,100,0,50)
        billboard.Adornee = hrpRef
        billboard.AlwaysOnTop = true
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1,0,1,0)
        label.BackgroundTransparency = 1
        label.Text = plr.Name
        label.TextColor3 = ESPColor
        label.TextScaled = true
        label.Font = Enum.Font.Cartoon
        label.Parent = billboard
        billboard.Parent = workspace

        ESPs[plr] = {box = box, label = billboard}
    end

    local function removeESP(plr)
        if ESPs[plr] then
            pcall(function()
                ESPs[plr].box:Destroy()
                ESPs[plr].label:Destroy()
            end)
            ESPs[plr] = nil
        end
    end

    local function toggleESP(state)
        ESPEnabled = state
        if ESPEnabled then
            for _, plr in ipairs(Players:GetPlayers()) do createESP(plr) end
        else
            for plr,_ in pairs(ESPs) do removeESP(plr) end
        end
    end

    Players.PlayerAdded:Connect(function(plr)
        plr.CharacterAdded:Connect(function() if ESPEnabled then createESP(plr) end end)
    end)
    Players.PlayerRemoving:Connect(removeESP)

    RunService.RenderStepped:Connect(function()
        if ESPEnabled then
            for plr, esp in pairs(ESPs) do
                local char = plr.Character
                if char and char:FindFirstChild("HumanoidRootPart") then
                    esp.box.Adornee = char.HumanoidRootPart
                    esp.label.Adornee = char.HumanoidRootPart
                end
            end
        end
    end)

    TabMain:AddToggle("ESPPlayer", { Title = "ESP Player", Default = false, Callback = toggleESP })

    local ToggleESPFruit = TabMain:AddToggle("ESPFruitLogia", {
        Title = "ESP Fruit In Bag Player",
        Description = "UlrtaRare/Rare Fruit Only",
        Default = false,
        Callback = function(state)
            _G.ESPFruit = state

            local Players = game:GetService("Players")

            local fruits = {
                ["Chilly Fruit"]=true, ["Flare Fruit"]=true, ["Magma Fruit"]=true, ["Rumble Fruit"]=true,
                ["Sand Fruit"]=true, ["Phoenix Fruit"]=true, ["Ope Fruit"]=true,
                ["Quake Fruit"]=true, ["Venom Fruit"]=true, ["Candy Fruit"]=true, ["Gas Fruit"]=true,
                ["Dark Fruit"]=true, ["Plasma Fruit"]=true, ["Rare Box"]=true, ["Ultra Rare Box"]=true,
            }

            local function addESPToCharacter(character, text)
                if character and character:FindFirstChild("Head") and not character.Head:FindFirstChild("FruitESP") then
                    local billboard = Instance.new("BillboardGui")
                    billboard.Name = "FruitESP"
                    billboard.Adornee = character.Head
                    billboard.Size = UDim2.new(0, 200, 0, 50)
                    billboard.AlwaysOnTop = true

                    local label = Instance.new("TextLabel", billboard)
                    label.Size = UDim2.new(1, 0, 1, 0)
                    label.BackgroundTransparency = 1
                    label.Text = text
                    label.TextColor3 = Color3.fromRGB(0, 255, 255)
                    label.TextScaled = true
                    label.Font = Enum.Font.SourceSansBold

                    billboard.Parent = character.Head
                end
            end

            local function removeESP(character)
                if character and character:FindFirstChild("Head") then
                    local esp = character.Head:FindFirstChild("FruitESP")
                    if esp then esp:Destroy() end
                end
            end

            local function checkPlayer(player)
                local function updateESP()
                    if not _G.ESPFruit then return end

                    local fruitList = {}
                    if player:FindFirstChild("Backpack") then
                        for _, item in pairs(player.Backpack:GetChildren()) do
                            if fruits[item.Name] then
                                table.insert(fruitList, item.Name)
                            end
                        end
                    end

                    if player.Character then
                        if #fruitList > 0 then
                            addESPToCharacter(player.Character, table.concat(fruitList, ", "))
                        else
                            removeESP(player.Character)
                        end
                    end
                end

                if player:FindFirstChild("Backpack") then
                    player.Backpack.ChildAdded:Connect(updateESP)
                    player.Backpack.ChildRemoved:Connect(updateESP)
                end

                player.CharacterAdded:Connect(function(char)
                    char:WaitForChild("Head")
                    updateESP()
                end)

                updateESP()
            end

            if state then
                for _, p in pairs(Players:GetPlayers()) do
                    if p ~= Players.LocalPlayer then
                        checkPlayer(p)
                    end
                end

                Players.PlayerAdded:Connect(function(p)
                    if p ~= Players.LocalPlayer then
                        checkPlayer(p)
                    end
                end)
            else
                for _, p in pairs(Players:GetPlayers()) do
                    if p.Character then
                        removeESP(p.Character)
                    end
                end
            end
        end
    })

local NoclipEnabled = false
local NoclipConnection

TabMain:AddToggle("Noclip", {
    Title = "Noclip",
    Default = false,
    Callback = function(state)
        NoclipEnabled = state

        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        if NoclipConnection then
            NoclipConnection:Disconnect()
            NoclipConnection = nil
        end

        if NoclipEnabled then
            NoclipConnection = game:GetService("RunService").Heartbeat:Connect(function()
                if character and character.Parent then
                    for _, part in pairs(character:GetChildren()) do
                        if part:IsA("BasePart") then
                            part.CanCollide = false
                        end
                    end
                end
            end)
        else
            for _, part in pairs(character:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = true
                end
            end
        end
    end
})

    local defaultSpeed = 16
    local boostedSpeed = 250
    local speedActive = false

    TabMain:AddToggle("SpeedNoClipToggle", {
        Title = "Speed Hack",
        Default = false,
        Callback = function(state)
            speedActive = state
            initCharacter(player.Character or player.CharacterAdded:Wait())
            local humanoidRef = character:FindFirstChild("Humanoid")
            if humanoidRef then
                humanoidRef.WalkSpeed = state and boostedSpeed or defaultSpeed
            end
        end
    })

    RunService.RenderStepped:Connect(function()
        if speedActive then
            local char = player.Character
            if char then
                local humanoidRef = char:FindFirstChild("Humanoid")
                local hrpRef = char:FindFirstChild("HumanoidRootPart")
                if humanoidRef and hrpRef then
                    local moveDir = humanoidRef.MoveDirection
                    hrpRef.Velocity = Vector3.new(moveDir.X * boostedSpeed, hrpRef.Velocity.Y, moveDir.Z * boostedSpeed)
                end
            end
        end
    end)

    TabMain:AddToggle("InvisibleLocal", {
    Title = "Invisible",
    Default = false,
    Callback = function(state)
        _G.InvisibleLocal = state

        spawn(function()
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()
            local hrp = character:WaitForChild("HumanoidRootPart")
            local humanoid = character:WaitForChild("Humanoid")

            local function setTransparency(character, transparency)
                for _, part in pairs(character:GetDescendants()) do
                    if part:IsA("BasePart") or part:IsA("Decal") then
                        part.LocalTransparencyModifier = transparency
                    end
                end
            end

            if _G.InvisibleLocal then
                local savedCFrame = hrp.CFrame

                hrp.CFrame = CFrame.new(0, 5000, 0)
                task.wait(0.1)

                local seat = Instance.new("Seat", workspace)
                seat.Name = "InvisSeat"
                seat.Anchored = false
                seat.CanCollide = false
                seat.Transparency = 1
                seat.CFrame = hrp.CFrame

                local weld = Instance.new("Weld", seat)
                weld.Part0 = seat
                weld.Part1 = character:FindFirstChild("Torso") or character:FindFirstChild("UpperTorso")

                seat.CFrame = savedCFrame

                setTransparency(character, 0.5)
                for _, part in ipairs(character:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
            else
                local seat = workspace:FindFirstChild("InvisSeat")
                if seat then seat:Destroy() end
                setTransparency(character, 0)
                for _, part in ipairs(character:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = true
                    end
                end
            end
        end)
    end
})

    _G.InfiniteJumpMisc = false
    TabMain:AddToggle("InfinityJumpMisc", {
        Title = "Infinity Jump",
        Default = false,
        Callback = function(state) _G.InfiniteJumpMisc = state end
    })
    UserInputService.JumpRequest:Connect(function()
        if _G.InfiniteJumpMisc then
            local char = player.Character or player.CharacterAdded:Wait()
            local hum = char:FindFirstChild("Humanoid")
            if hum then hum:ChangeState(Enum.HumanoidStateType.Jumping) end
        end
    end)

    TabMain:AddButton({
    Title = "God Mode",
    Description = "Press God Mode and ResetSpawn",
    Callback = function()
        local ReplicatedStorage = game:GetService('ReplicatedStorage')
        local Event = ReplicatedStorage.Connections.Spawn

        local mt = getrawmetatable(game)
        local oldNamecall = mt.__namecall
        setreadonly(mt, false)

        mt.__namecall = function(self, ...)
            local method = getnamecallmethod()
            if self == Event and method == 'FireServer' then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(
                    -77.09452056884766,
                    215.99998474121094,
                    -858.5032958984375
                )
                return
            end
            return oldNamecall(self, ...)
        end

        setreadonly(mt, true)
    end
})

    TabMain:AddButton({
        Title = "ALT+Click Teleport",
        Callback = function()
            local mouse = player:GetMouse()
            mouse.Button1Down:Connect(function()
                if UserInputService:IsKeyDown(Enum.KeyCode.LeftAlt) or UserInputService:IsKeyDown(Enum.KeyCode.RightAlt) then
                    initCharacter(player.Character or player.CharacterAdded:Wait())
                    local pos = mouse.Hit.Position
                    hrp.CFrame = CFrame.new(pos + Vector3.new(0,3,0))
                end
            end)
        end
    })

    player.CharacterAdded:Connect(function(char)
        initCharacter(char)
        if AutoMixEnabled then task.wait(1); startAutoClick() end
        if AutoDrinkEnabled then task.wait(1); startAutoDrink() end
    end)

    local function getconnect(v2)
        local events = {"Activated", "MouseButton1Down", "MouseButton1Click", "MouseButton1Up"}
        for _, v in next, events do
            for _, v in next, getconnections(v2[v]) do
                v.Function()
            end
        end
    end

    local selectedJuice = "A"
    local amountToBuy = 1
    local autoBuyEnabled = false
    local isProcessing = false

    local JuiceDropdown = TabJuice:AddDropdown("JuiceDropdown", {
        Title = "Select Juice",
        Values = {"Cider+", "Lemonade+", "Juice+", "Smoothie+"},
        Multi = false,
        Default = 1,
    })

    JuiceDropdown:OnChanged(function(Value)
        if Value == "Cider+" then
            selectedJuice = "A"
        elseif Value == "Lemonade+" then
            selectedJuice = "B"
        elseif Value == "Juice+" then
            selectedJuice = "C"
        elseif Value == "Smoothie+" then
            selectedJuice = "D"
        end
    end)

    spawn(function()
        while task.wait(1) do
            local player = game:GetService("Players").LocalPlayer
            local shopGui = player.PlayerGui:FindFirstChild("ShopDrinksPlus")
            if shopGui and shopGui.Frame then
                local newValues = {}
                local frames = {"A", "B", "C", "D"}
                
                for i, frame in ipairs(frames) do
                    local frameObj = shopGui.Frame:FindFirstChild(frame)
                    if frameObj and frameObj:FindFirstChild("Label") then
                        newValues[i] = frameObj.Label.Text
                    else
                        newValues[i] = "Option " .. frame
                    end
                end
                
                JuiceDropdown:SetValues(newValues)
            end
        end
    end)

    local AmountInput = TabJuice:AddInput("AmountInput", {
        Title = "Amount to Buy",
        Default = "1",
        Placeholder = "Enter amount to buy",
        Numeric = true,
        Finished = false,
        Callback = function(Value)
            local num = tonumber(Value)
            if num and num > 0 then
                amountToBuy = num
            else
                amountToBuy = 1
            end
        end
    })

    local AutoBuyToggle = TabJuice:AddToggle("AutoBuyToggle", {
        Title = "Auto Buy",
        Default = false
    })

    AutoBuyToggle:OnChanged(function(Value)
        autoBuyEnabled = Value
    end)

    spawn(function()
        while task.wait(1) do
            if autoBuyEnabled and not isProcessing then
                isProcessing = true
                
                local player = game:GetService("Players").LocalPlayer
                local merchant = workspace.Merchants:FindFirstChild("BetterDrinkMerchant")
                
                if merchant and merchant:FindFirstChild("Clickable") and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    player.Character.HumanoidRootPart.CFrame = merchant.Clickable.CFrame
                    task.wait(0.2)
                    
                    for i = 1, amountToBuy do
                        if merchant.Clickable:FindFirstChild("ClickDetector") then
                            fireclickdetector(merchant.Clickable.ClickDetector)
                            task.wait(0.1)
                            
                            local shopGui = player.PlayerGui:FindFirstChild("ShopDrinksPlus")
                            if shopGui and shopGui.Frame then
                                local targetFrame = shopGui.Frame:FindFirstChild(selectedJuice)
                                if targetFrame and targetFrame:FindFirstChild("ImageButton") then
                                    getconnect(targetFrame.ImageButton)
                                    task.wait(0.1)
                                end
                            end
                        end
                    end
                end
                
                isProcessing = false
            end
        end
    end)

    local AutoTrashEnabled = false
    local autoTrashThread = nil

    local trashNames = {"1","2","3","4","5","6","7","8"}

    local function realDropTool(tool)
        if not tool then return end
        if tool:IsA("Tool") and humanoid then
            humanoid:EquipTool(tool)
            task.wait(0.05)

            local remote = tool:FindFirstChildWhichIsA("RemoteEvent")
            if remote then
                remote:FireServer()
            else
                pcall(function() tool.Parent = workspace end)
            end

            print("ทิ้งของ: "..tool.Name)
        end
    end

    local function startAutoTrash()
        if autoTrashThread then return end
        autoTrashThread = task.spawn(function()
            while AutoTrashEnabled do
                for _, tool in ipairs(player.Backpack:GetChildren()) do
                    if table.find(trashNames, tool.Name) then
                        realDropTool(tool)
                        task.wait(0.1)
                    end
                end

                for _, tool in ipairs(character:GetChildren()) do
                    if table.find(trashNames, tool.Name) then
                        realDropTool(tool)
                        task.wait(0.1)
                    end
                end

                task.wait(0.1)
            end
            autoTrashThread = nil
        end)
    end

    local Players = game:GetService("Players")
local player = Players.LocalPlayer
local RunService = game:GetService("RunService")

local drinkNames = {
    "Cider+",
    "Lemonade+",
    "Juice+",
    "Smoothie+"
}

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "DrinkCheckerUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = game:GetService("CoreGui") 

local label = Instance.new("TextLabel")
label.Size = UDim2.new(0, 300, 0, 150)
label.Position = UDim2.new(0, 10, 0, 10)
label.BackgroundColor3 = Color3.fromRGB(25,25,25)
label.BackgroundTransparency = 0.3
label.TextColor3 = Color3.fromRGB(255, 255, 255)
label.TextScaled = true
label.Font = Enum.Font.SourceSansBold
label.Text = ""
label.Visible = false
label.Parent = screenGui

local drinkCheckerEnabled = false
local character = player.Character or player.CharacterAdded:Wait()

local function updateDrinkUI()
    local displayLines = {}
    for _, drink in ipairs(drinkNames) do
        local count = 0

        for _, item in ipairs(player.Backpack:GetChildren()) do
            if item.Name == drink then
                count += 1
            end
        end

        for _, item in ipairs(character:GetChildren()) do
            if item.Name == drink then
                count += 1
            end
        end
        if count > 0 then
            table.insert(displayLines, drink.." "..count)
        end
    end

    label.Text = table.concat(displayLines, "\n")
end

RunService.RenderStepped:Connect(function()
    if drinkCheckerEnabled then
        character = player.Character or player.CharacterAdded:Wait()
        updateDrinkUI()
    end
end)

TabJuice:AddToggle("DrinkChecker", {
    Title = "Check Juice UI",
    Default = false,
    Callback = function(state)
        drinkCheckerEnabled = state
        label.Visible = state
        if state then
            print("Check Open Realtime ✅")
        else
            print("Check Close Realtime ❌")
        end
    end
})


    TabMixerV2:AddToggle("Auto Trash Drinks", {
        Title = "Auto Drop Fruit",
        Default = false,
        Callback = function(state)
            AutoTrashEnabled = state
            if state then startAutoTrash() end
        end
    })

    local Players = game:GetService("Players")
local player = Players.LocalPlayer

local function getHRP()
    local char = player.Character or player.CharacterAdded:Wait()
    return char:WaitForChild("HumanoidRootPart")
end

local function warpAndClick(part)
    local hrp = getHRP()
    if not hrp or not part then
        warn("❌ หา HRP หรือ Part ไม่เจอ")
        return
    end

    hrp.CFrame = part.CFrame + Vector3.new(0, 3, 2)
    task.wait(0.1)

    local clickDetector = part:FindFirstChildWhichIsA("ClickDetector")
    if clickDetector then
        fireclickdetector(clickDetector)
        print("✅ Clicked:", part.Name)
    else
        warn("⚠ ไม่มี ClickDetector ใน", part.Name)
    end
end

TabMixerV2:AddButton({
    Title = "TP Mixer Fruit",
    Callback = function()
        pcall(function()
            local kitchen = workspace:WaitForChild("Island8"):WaitForChild("Kitchen")
            local target = kitchen:GetChildren()[3]
            local bowl = target:WaitForChild("JuicingBowl")

            warpAndClick(bowl:FindFirstChild("Mixer1"))
            task.wait(0.3)
            warpAndClick(bowl:FindFirstChild("MixerMain"))
        end)
    end
})

    local AutoRenameEnabled = false

    local ItemMap = {
        ["Apple"] = 1,
        ["Banana"] = 2,
        ["Pumpkin"] = 3,
        ["Green Apple"] = 4,
        ["Melon"] = 5,
        ["Cantaloupe"] = 6,
        ["Coconut"] = 7,
        ["Prickly Pear"] = 8
    }

    local function RenameItems()
        local backpack = player:WaitForChild("Backpack")
        for _, item in ipairs(backpack:GetChildren()) do
            local num = ItemMap[item.Name]
            if num then
                item.Name = tostring(num)
            end
        end
    end

    local function StartAutoRename()
        task.spawn(function()
            while AutoRenameEnabled do
                RenameItems()
                task.wait(1)
            end
        end)
    end

    TabMixerV2:AddToggle("Auto Rename Items", {
        Title = "Auto Rename Fruit",
        Default = false,
        Callback = function(state)
            AutoRenameEnabled = state
            if state then
                RenameItems()
                StartAutoRename()
            end
        end
    })

    local function refreshCharacter()
        character = player.Character or player.CharacterAdded:Wait()
        hrp = character:WaitForChild("HumanoidRootPart")
        humanoid = character:WaitForChild("Humanoid")
    end
    refreshCharacter()

    player.CharacterAdded:Connect(function(char)
        character = char
        hrp = char:WaitForChild("HumanoidRootPart")
        humanoid = char:WaitForChild("Humanoid")

        print("รีเฟรช character ใหม่หลังจากตาย")

        if AutoClickEnabled then startAutoClick() end
        if AutoTrashEnabled then startAutoTrash() end
        if AutoMixEnabled then startAutoMix() end
        if AutoRenameEnabled then StartAutoRename() end
    end)

    local Players = game:GetService("Players")
    local player = Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    local AutoDrinkEnabled = false
    local autoDrinkThread = nil

    local drinkNames = {
        "Fruit Juice",
        "Sour Juice",
        "Coconut Milk",
        "Pear Juice",
        "Pumpkin Juice",
        "Banana Juice",
        "Apple Juice",
    }

    local function clickDrink(obj)
        if not obj then return end

        if obj:IsA("Tool") then
            local humanoid = character:FindFirstChild("Humanoid")
            if humanoid then
                humanoid:EquipTool(obj)
                task.wait(0.05)
                local handle = obj:FindFirstChild("Handle")
                if handle then
                    local clickDetector = handle:FindFirstChildWhichIsA("ClickDetector")
                    if clickDetector then
                        pcall(fireclickdetector, clickDetector)
                        print("ดื่ม Tool: "..obj.Name)
                    else
                        if obj:FindFirstChildWhichIsA("RemoteEvent") then
                            obj:Activate()
                            print("Activate Tool: "..obj.Name)
                        end
                    end
                end
            end
        else
            local clickDetector = obj:FindFirstChildWhichIsA("ClickDetector")
            if clickDetector then
                pcall(fireclickdetector, clickDetector)
                print("ดื่ม Workspace: "..obj.Name)
            end
        end
    end

    local function startAutoDrink()
        if autoDrinkThread then return end
        autoDrinkThread = task.spawn(function()
            while AutoDrinkEnabled do
                for _, name in ipairs(drinkNames) do
                    local drink = workspace:FindFirstChild(name)
                    if drink then
                        clickDrink(drink)
                        task.wait(0.01)
                    end
                end

                for _, tool in ipairs(player.Backpack:GetChildren()) do
                    if table.find(drinkNames, tool.Name) then
                        clickDrink(tool)
                        task.wait(0.01)
                    end
                end

                for _, tool in ipairs(character:GetChildren()) do
                    if table.find(drinkNames, tool.Name) then
                        clickDrink(tool)
                        task.wait(0.01)
                    end
                end

                task.wait(0.01)
            end
            autoDrinkThread = nil
        end)
    end

    TabMixerV2:AddToggle("AutoDrink MixFruit", {
        Title = "Auto Drink MixerFruit",
        Description = "If Script bug gives a new Execute",
        Default = false,
        Callback = function(state)
            AutoDrinkEnabled = state
            if state then
                startAutoDrink()
            else
            end
        end 
    })

    TabMixerV2:AddButton({
    Title = "Send Fruit",
    Callback = function() teleportAFK({-11.223817825317383, 200004.5, 201.46461486816406}) end
    })
    TabMixerV2:AddButton({
    Title = "Receive Fruit",
    Callback = function() teleportAFK({-10.989439010620117, 200004.5, 194.4368438720703}) end
    })

    local TogglePullThug = TabMixerV2:AddToggle("Bring Mob", {
    Title = "Bring Mob",
    Default = false,
    Callback = function(state)
        _G.PullThug = state
        if state then
            task.spawn(function()
                while _G.PullThug do
                    pcall(function()
                        local player = game.Players.LocalPlayer
                        local char = player.Character or player.CharacterAdded:Wait()
                        local hrp = char:FindFirstChild("HumanoidRootPart")

                        if hrp and workspace:FindFirstChild("Enemies") then
                            local thugNames = {
                                ["Lv22 Angry Bobby"] = true,
                                ["Lv24 Angry Bobbi"] = true,
                                ["Lv29 Angry Bobber"] = true,
                                ["Lv35 Angry Bobb"] = true,
                                ["Lv29 Frued"] = true,
                                ["Lv28 Freyd"] = true,
                                ["Lv28 Fredde"] = true,
                                ["Lv34 Freddi"] = true,
                                ["Lv28 Fredde"] = true,
                            }

                            for name, _ in pairs(thugNames) do
                                local enemy = workspace.Enemies:FindFirstChild(name)
                                if enemy and enemy:FindFirstChild("HumanoidRootPart") and enemy:FindFirstChild("Humanoid") then
                                    local eHRP = enemy.HumanoidRootPart
                                    eHRP.CFrame = hrp.CFrame * CFrame.new(0, 0, 0)
                                    eHRP.Anchored = true
                                    enemy.Humanoid.PlatformStand = true
                                end
                            end
                        end
                    end)
                    task.wait(0.2)
                end
            end)
        end
    end
})

_G.autoSpawn = false 
local Players = game:GetService("Players")
local VirtualInputManager = game:GetService("VirtualInputManager")
local player = Players.LocalPlayer
local teleportPosition = Vector3.new(4545.86328125, 210.97650146484375, 5783.75634765625)

local AutoSpawnToggle = TabMain:AddToggle("AutoSpawnToggle", {
    Title = "Auto Spawn (Fram Bounty)",
    Description = "Moved the UI away from the center of the screen. Because it will cause you to open other functions.",
    Default = false,
    Callback = function(Value)
        _G.autoSpawn = Value
    end
})

local function clickSpawn()
    local button = game:GetService("CoreGui"):FindFirstChild("TopBarApp", true)
    if button then
        for _, child in ipairs(button:GetDescendants()) do
            if child:IsA("GuiObject") and child.Name:lower():find("respawn") then
                local pos = child.AbsolutePosition + (child.AbsoluteSize / 2)
                VirtualInputManager:SendMouseButtonEvent(pos.X, pos.Y, 0, true, game, 1)
                VirtualInputManager:SendMouseButtonEvent(pos.X, pos.Y, 0, false, game, 1)
                break
            end
        end
    end
end

local function teleportCharacter(char)
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame = CFrame.new(teleportPosition)
    end
end

local function runSpawnLoop()
    while true do
        if _G.autoSpawn and player.Character then
            clickSpawn()
            task.wait(1)
            teleportCharacter(player.Character)
            task.wait(5) 
        else
            task.wait(0.5)
        end
    end
end


local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

local AutoTrashEnabled = false
local autoTrashThread = nil
local trashNames = {"Compass"}

local function realDropTool(tool)
    if not tool then return end
    if tool:IsA("Tool") and humanoid then
        humanoid:EquipTool(tool)
        task.wait(0.05)

        local remote = tool:FindFirstChildWhichIsA("RemoteEvent")
        if remote then
            remote:FireServer()
        else
            pcall(function() tool.Parent = workspace end)
        end

        print("ทิ้งของ: " .. tool.Name)
    end
end

local function startAutoTrash()
    if autoTrashThread then return end
    autoTrashThread = task.spawn(function()
        while AutoTrashEnabled do

            for _, tool in ipairs(player.Backpack:GetChildren()) do
                if table.find(trashNames, tool.Name) then
                    realDropTool(tool)
                    task.wait(0.1)
                end
            end

            for _, tool in ipairs(character:GetChildren()) do
                if tool:IsA("Tool") and table.find(trashNames, tool.Name) then
                    realDropTool(tool)
                    task.wait(0.1)
                end
            end

            task.wait(0.2)
        end
        autoTrashThread = nil
    end)
end

local function stopAutoTrash()
    AutoTrashEnabled = false
    autoTrashThread = nil
end

TabMain:AddToggle("AutoTrashToggle", {
    Title = "Auto Trash (ทิ้ง Compass)",
    Default = false,
    Callback = function(Value)
        AutoTrashEnabled = Value
        if Value then
            print("[AutoTrash] ON")
            startAutoTrash()
        else
            print("[AutoTrash] OFF")
            stopAutoTrash()
        end
    end
})

player.CharacterAdded:Connect(function(char)
    character = char
    humanoid = char:WaitForChild("Humanoid")
end)


task.spawn(runSpawnLoop)

TabMain:AddButton({
Title = "Bounty Farm Point",
Callback = function() teleportAFK({4519.38623046875, 217, 5781.06396484375}) end
})

Window:SelectTab(1)
print("Script loaded: Fruit Mixer Hub (Complete)")
SaveManager:SetLibrary(Fluent)
SaveManager:BuildConfigSection(Setting)
SaveManager:LoadAutoloadConfig()

----------------------------------------------------------------------------
-- ADD Function More Here
----------------------------------------------------------------------------
-- LocalScript (StarterPlayerScripts)
_G.kick = false

local Pedo = {
    80905262,
    451082957,
    1833865091,
    1135910299,
    1619950875,
    1581720092,
    1661505948,
    679804290,
    520944,
    43247021,
    2350183594,
    1338963426,
    1276541545,
    587649463,
    245586741,
    174941504,
    136099207,
    94825741,
    358051152,
    529455640,
    281482099,
    355207559,
    5084487,
    928623624,
    30049170,
    474452017,
    110183124,
    1216587424,
    513583299,
    2361317975,
    52478375,
    1137403348,
    4447020775,
    571687119,
    8695097097,
    106625686,



}

local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer

local function isBlocked(id)
    for _, v in ipairs(Pedo) do
        if id == v then
            return true
        end
    end
    return false
end

for _, plr in ipairs(Players:GetPlayers()) do
    if plr ~= localPlayer and isBlocked(plr.UserId) then
        localPlayer:Kick("Admin is in the server")
        break
    end
end

Players.PlayerAdded:Connect(function(plr)
    if isBlocked(plr.UserId) then
        localPlayer:Kick("แอดมินเข้าเซิฟไอ้สัส มึงไม่ได้โดนแบนอันนี้ Anti แบน")
    end
end)

local Players = game:GetService("Players")
local VirtualInputManager = game:GetService("VirtualInputManager")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local player = Players.LocalPlayer

local toggleGui = Instance.new("ScreenGui")
toggleGui.Name = "ToggleUI"
toggleGui.Parent = CoreGui  -- << เปลี่ยนจาก PlayerGui เป็น CoreGui

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 60, 0, 20)
toggleButton.Position = UDim2.new(0, 930, 0, 8)
toggleButton.Text = "Open UI"
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Parent = toggleGui
toggleButton.AutoButtonColor = false

local isOpen = false

local function pressCtrlRight()
    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.RightControl, false, game)
    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.RightControl, false, game)
end

toggleButton.MouseButton1Click:Connect(function()
    isOpen = not isOpen
    if isOpen then
        toggleButton.Text = "Close UI"
    else
        toggleButton.Text = "Open UI"
    end
    pressCtrlRight()
end)

local dragging = false
local offset = Vector2.new(0,0)

toggleButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        local mousePos = UserInputService:GetMouseLocation()
        local guiPos = toggleButton.AbsolutePosition
        offset = mousePos - Vector2.new(guiPos.X, guiPos.Y)
    end
end)

toggleButton.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

game:GetService("RunService").RenderStepped:Connect(function()
    if dragging then
        local mousePos = UserInputService:GetMouseLocation()
        toggleButton.Position = UDim2.new(
            0, mousePos.X - offset.X,
            0, mousePos.Y - offset.Y
        )
    end
end)

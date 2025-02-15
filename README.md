local OrionLib = loadstring(game:HttpGet("https://github.com/TemplariosScripts1/OrionLib/raw/refs/heads/main/OrionLib.txt"))()

local Window = OrionLib:MakeWindow({Name = "SUPER TROLL V1", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

-- Aba TROLL OP!
local TrollTab = Window:MakeTab({Name = "TROLL OP!", Icon = "rbxassetid://4483345998", PremiumOnly = false})

-- Olhar Players (agora lista os jogadores corretamente)
local PlayersDropdown = TrollTab:AddDropdown({
    Name = "Olhar Players",
    Default = "",
    Options = {},
    Callback = function(selectedPlayer)
        local player = game.Players:FindFirstChild(selectedPlayer)
        if player then
            game.Workspace.CurrentCamera.CameraSubject = player.Character.Humanoid
        end
    end
})

-- Atualizar a lista de jogadores automaticamente
local function UpdatePlayersList()
    local players = {}
    for _, player in pairs(game.Players:GetPlayers()) do
        table.insert(players, player.Name)
    end
    PlayersDropdown:Refresh(players)
end
UpdatePlayersList()
game.Players.PlayerAdded:Connect(UpdatePlayersList)
game.Players.PlayerRemoving:Connect(UpdatePlayersList)

-- Parar de olhar jogadores
TrollTab:AddButton({
    Name = "Parar de Olhar Jogadores",
    Callback = function()
        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
    end
})

-- Função de ESP
local espEnabled = false
TrollTab:AddToggle({
    Name = "ESP Players",
    Default = false,
    Callback = function(state)
        espEnabled = state
        if espEnabled then
            -- Criar ou atualizar o ESP para cada jogador
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    -- Verificar se o ESP já existe, se não, criar
                    local espBox = player.Character.HumanoidRootPart:FindFirstChild("ESPBox")
                    if not espBox then
                        espBox = Instance.new("BillboardGui", player.Character.HumanoidRootPart)
                        espBox.Size = UDim2.new(0, 200, 0, 50)
                        espBox.StudsOffset = Vector3.new(0, 3, 0)
                        espBox.AlwaysOnTop = true
                        espBox.Name = "ESPBox"

                        local nameLabel = Instance.new("TextLabel", espBox)
                        nameLabel.Size = UDim2.new(1, 0, 1, 0)
                        nameLabel.BackgroundTransparency = 1
                        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
                        nameLabel.TextStrokeTransparency = 0.8
                        nameLabel.TextScaled = true

                        -- Atualizar a distância
                        local function updateDistance()
                            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                                local distance = (player.Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
                                nameLabel.Text = player.Name .. " - " .. math.floor(distance) .. " studs"
                            end
                        end

                        -- Atualizar a distância a cada 0.1 segundos
                        game:GetService("RunService").Heartbeat:Connect(updateDistance)
                    end
                end
            end
        else
            -- Remover ESP
            for _, player in pairs(game.Players:GetPlayers()) do
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local espBox = player.Character.HumanoidRootPart:FindFirstChild("ESPBox")
                    if espBox then
                        espBox:Destroy()
                    end
                end
            end
        end
    end
})

-- Adicionando o Fling GUI (Universal) conforme solicitado
TrollTab:AddButton({
    Name = "Fling Players (Universal)",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-FE-Fling-GUI-10927"))()
    end
})

-- Opções da aba ADM
TrollTab:AddButton({Name = "ADM FE (Infinite Yield)", Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
end})
TrollTab:AddButton({Name = "Super Ring", Callback = function()
    loadstring(game:HttpGet("https://rawscripts.net/raw/Natural-Disaster-Survival-Super-Rings-Parts-V4-By-Lukas-24409"))()
end})
TrollTab:AddButton({Name = "Executor RC7", Callback = function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/CoreGui/Scripts/main/RC7"))()
end})
TrollTab:AddButton({Name = "Knife (FE)", Callback = function()
    loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Grab-knife-v4-24753"))()
end})
TrollTab:AddButton({Name = "Tubers 93 GUI", Callback = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/aYVcsXYf"))()
end})
TrollTab:AddButton({Name = "c00lkid GUI", Callback = function()
    loadstring(game:HttpGet("https://pastebin.com/raw/UPZCQ31W"))()
end})

-- Aba TROLL V2 (apenas o aviso)
local TrollV2Tab = Window:MakeTab({Name = "TROLL V2", Icon = "rbxassetid://4483345998", PremiumOnly = false})
TrollV2Tab:AddLabel("Troll V2 Dia 20 de fevereiro!")

OrionLib:Init()

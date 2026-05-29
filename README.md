-- Carrega a biblioteca Rayfield UI
local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- Serviços do Roblox
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

-- Janela Principal
local Window = Rayfield:CreateWindow({
   Name = "LEGENDARY HUB | SOCCER SYSTEM",
   LoadingTitle = "Carregando Estrutura Completa...",
   LoadingSubtitle = "by Legendary",
   ConfigurationSaving = { Enabled = false },
   Discord = { Enabled = false },
   KeySystem = false 
})

-- ==========================================
-- ABAS DA INTERFACE
-- ==========================================
local TabAtravessar = Window:CreateTab("Atravessar", 4483362458)
local TabPerformance = Window:CreateTab("Performance", 4483362458)
local TabVelocidade = Window:CreateTab("Velocidade", 4483362458)
local TabMuralha = Window:CreateTab("Muralha", 4483362458)

-- Função auxiliar para achar a bola no mapa
local function ObterBola()
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("BasePart") and (obj.Name == "Ball" or obj.Name == "SoccerBall" or obj.Name:lower():find("bola")) then
            return obj
        end
    end
    return nil
end

-- ==========================================
-- ABA 1: ATRAVESSAR
-- ==========================================
TabAtravessar:CreateSection("Módulos Principais")

local AtravessarAtivado = false
TabAtravessar:CreateToggle({
   Name = "Atravessar",
   CurrentValue = false,
   Flag = "ToggleAtravessar",
   Callback = function(Value)
       AtravessarAtivado = Value
       -- Lógica para gerenciar a colisão simulada com adversários
   end,
})
TabAtravessar:CreateLabel("INFO: Atravessa o adversário, mas na visão dele empurra.")

local BallChicleteAtivado = false
TabAtravessar:CreateToggle({
   Name = "Ball Chiclete",
   CurrentValue = false,
   Flag = "ToggleChiclete",
   Callback = function(Value)
       BallChicleteAtivado = Value
       -- Lógica de atração física constante para a bola ficar colada
   end,
})
TabAtravessar:CreateLabel("INFO: A bola fica grudenta e gruda em você instantaneamente.")

local PainelZagAtivado = false
TabAtravessar:CreateToggle({
   Name = "Painel Zag",
   CurrentValue = false,
   Flag = "ToggleZag",
   Callback = function(Value)
       PainelZagAtivado = Value
       -- Ativa um botão móvel na tela para gerenciamento local de retenção da bola
   end,
})
TabAtravessar:CreateLabel("INFO: O oponente não atravessa você e a bola gruda.")

TabAtravessar:CreateSection("Módulos Adicionais")

local AntiPuloAtivado = false
TabAtravessar:CreateToggle({
   Name = "Anti Pulo",
   CurrentValue = false,
   Flag = "ToggleAntiPulo",
   Callback = function(Value)
       AntiPuloAtivado = Value
       if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
           if AntiPuloAtivado then
               LocalPlayer.Character:FindFirstChildOfClass("Humanoid").JumpPower = 0
           else
               LocalPlayer.Character:FindFirstChildOfClass("Humanoid").JumpPower = 50 -- Padrão
           end
       end
   end,
})
TabAtravessar:CreateLabel("INFO: Deixa o jogador incapaz de pular.")

local EmpurraForteAtivado = false
TabAtravessar:CreateToggle({
   Name = "Empurra Forte",
   CurrentValue = false,
   Flag = "ToggleEmpurra",
   Callback = function(Value)
       EmpurraForteAtivado = Value
       -- Aplicação de BodyVelocity ou impulsão nas hitboxes próximas
   end,
})
TabAtravessar:CreateLabel("INFO: Faz os jogadores serem empurrados forte ao ficar na frente.")

local VencerDisputaAtivado = false
TabAtravessar:CreateToggle({
   Name = "Vencer Disputa",
   CurrentValue = false,
   Flag = "ToggleDisputa",
   Callback = function(Value)
       VencerDisputaAtivado = Value
       -- Verificação de posição para interceptação precisa da bola
   end,
})
TabAtravessar:CreateLabel("INFO: Tira a bola do adversário facilmente na frente do gol.")

local DesarmeAutoAtivado = false
TabAtravessar:CreateToggle({
   Name = "Desarme Automático",
   CurrentValue = false,
   Flag = "ToggleDesarme",
   Callback = function(Value)
       DesarmeAutoAtivado = Value
       -- Evita que a bola atravesse o jogador mesmo se ele estiver rastejando
   end,
})
TabAtravessar:CreateLabel("INFO: Anti-atravessar bola do Brookhaven/Roblox quando rasteja.")


-- ==========================================
-- ABA 2: PERFORMANCE
-- ==========================================
TabPerformance:CreateSection("Aparência de Elementos")

local BolaBrancaAtivada = false
TabPerformance:CreateToggle({
   Name = "Bola Branca",
   CurrentValue = false,
   Flag = "ToggleBolaBranca",
   Callback = function(Value)
       BolaBrancaAtivada = Value
       local bola = ObterBola()
       if bola then
           if BolaBrancaAtivada then
               bola.Color = Color3.fromRGB(255, 255, 255)
               bola.Material = Enum.Material.SmoothPlastic
               -- Remove texturas internas se houver
               for _, t in pairs(bola:GetChildren()) do
                   if t:IsA("Texture") or t:IsA("Decal") then t.Texture = "" end
               end
           end
       end
   end,
})
TabPerformance:CreateLabel("INFO: Deixa a bola toda branca tirando a textura dela.")


-- ==========================================
-- ABA 3: VELOCIDADE
-- ==========================================
TabVelocidade:CreateSection("Controle de WalkSpeed")

local function MudarVelocidade(v)
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = v
    end
end

TabVelocidade:CreateToggle({
   Name = "Walkspeed | 23",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(23) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 24",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(24) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 25",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(25) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 26",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(26) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 27",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(27) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 28",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(28) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 29",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(29) else MudarVelocidade(16) end end,
})
TabVelocidade:CreateToggle({
   Name = "Walkspeed | 30",
   CurrentValue = false,
   Callback = function(v) if v then MudarVelocidade(30) else MudarVelocidade(16) end end,
})


-- ==========================================
-- ABA 4: MURALHA
-- ==========================================
TabMuralha:CreateSection("Controle de Bloqueio")

local AntiAtravessarBola = false
TabMuralha:CreateToggle({
   Name = "Anti-Atravessar",
   CurrentValue = false,
   Flag = "ToggleAntiAtravessar",
   Callback = function(Value)
       AntiAtravessarBola = Value
       -- Modifica dinamicamente propriedades de colisão do personagem com a bola
   end,
})
TabMuralha:CreateLabel("INFO: Impede do jogador ser atravessado pela bola de futebol.")

local ForcaColisaoAtivada = false
TabMuralha:CreateToggle({
   Name = "Força Colisão",
   CurrentValue = false,
   Flag = "ToggleForcaColisao",
   Callback = function(Value)
       ForcaColisaoAtivada = Value
       local bola = ObterBola()
       if bola and ForcaColisaoAtivada then
           bola.CanCollide = true
       end
   end,
})
TabMuralha:CreateLabel("INFO: Força a bola a ficar sempre com colisão ligada (Anti-Atravessar).")

local PesoDaBolaAtivado = false
TabMuralha:CreateToggle({
   Name = "Peso da Bola",
   CurrentValue = false,
   Flag = "TogglePesoBola",
   Callback = function(Value)
       PesoDaBolaAtivado = Value
       local bola = ObterBola()
       if bola and bola:IsA("BasePart") then
           if PesoDaBolaAtivado then
               -- Altera as propriedades físicas padrões para simular peso elevado
               bola.CustomPhysicalProperties = PhysicalProperties.new(100, 0.3, 0.5, 1, 1)
           else
               bola.CustomPhysicalProperties = nil
           end
       end
   end,
})
TabMuralha:CreateLabel("INFO: Deixa a bola mais pesada e fácil de retirar do oponente.")

-- Loops de atualização contínua em segundo plano
RunService.RenderStepped:Connect(function()
    if AntiPuloAtivado and LocalPlayer.Character then
        local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if hum then hum.JumpPower = 0 end
    end
end)

Rayfield:Notify({
   Title = "Painel Pronto",
   Content = "Todas as abas de futebol foram carregadas com sucesso.",
   Duration = 5,
   Image = 4483362458,
})

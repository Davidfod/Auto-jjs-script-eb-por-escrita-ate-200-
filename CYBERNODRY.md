local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local TextChatService = game:GetService("TextChatService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Configurações de Spam (1 a 200)
local rodando = false
local numeros = {
    "UM!", "DOIS!", "TRÊS!", "QUATRO!", "CINCO!", "SEIS!", "SETE!", "OITO!", "NOVE!", "DEZ!", "ONZE!", "DOZE!", "TREZE!", "QUATORZE!", "QUINZE!", "DEZESSEIS!", "DEZESSETE!", "DEZOITO!", "DEZENOVE!", "VINTE!",
    "VINTE E UM!", "VINTE E DOIS!", "VINTE E TRÊS!", "VINTE E QUATRO!", "VINTE E CINCO!", "VINTE E SEIS!", "VINTE E SETE!", "VINTE E OITO!", "VINTE E NOVE!", "TRINTA!",
    "TRINTA E UM!", "TRINTA E DOIS!", "TRINTA E TRÊS!", "TRINTA E QUATRO!", "TRINTA E CINCO!", "TRINTA E SEIS!", "TRINTA E SETE!", "TRINTA E OITO!", "TRINTA E NOVE!", "QUARENTA!",
    "QUARENTA E UM!", "QUARENTA E DOIS!", "QUARENTA E TRÊS!", "QUARENTA E QUATRO!", "QUARENTA E CINCO!", "QUARENTA E SEIS!", "QUARENTA E SETE!", "QUARENTA E OITO!", "QUARENTA E NOVE!", "CINQUENTA!",
    "CINQUENTA E UM!", "CINQUENTA E DOIS!", "CINQUENTA E TRÊS!", "CINQUENTA E QUATRO!", "CINQUENTA E CINCO!", "CINQUENTA E SEIS!", "CINQUENTA E SETE!", "CINQUENTA E OITO!", "CINQUENTA E NOVE!", "SESSENTA!",
    "SESSENTA E UM!", "SESSENTA E DOIS!", "SESSENTA E TRÊS!", "SESSENTA E QUATRO!", "SESSENTA E CINCO!", "SESSENTA E SEIS!", "SESSENTA E SETE!", "SESSENTA E OITO!", "SESSENTA E NOVE!", "SETENTA!",
    "SETENTA E UM!", "SETENTA E DOIS!", "SETENTA E TRÊS!", "SETENTA E QUATRO!", "SETENTA E CINCO!", "SETENTA E SEIS!", "SETENTA E SETE!", "SETENTA E OITO!", "SETENTA E NOVE!", "OITENTA!",
    "OITENTA E UM!", "OITENTA E DOIS!", "OITENTA E TRÊS!", "OITENTA E QUATRO!", "OITENTA E CINCO!", "OITENTA E SEIS!", "OITENTA E SETE!", "OITENTA E OITO!", "OITENTA E NOVE!", "NOVENTA!",
    "NOVENTA E UM!", "NOVENTA E DOIS!", "NOVENTA E TRÊS!", "NOVENTA E QUATRO!", "NOVENTA E CINCO!", "NOVENTA E SEIS!", "NOVENTA E SETE!", "NOVENTA E OITO!", "NOVENTA E NOVE!", "CEM!",
    "CENTO E UM!", "CENTO E DOIS!", "CENTO E TRÊS!", "CENTO E QUATRO!", "CENTO E CINCO!", "CENTO E SEIS!", "CENTO E SETE!", "CENTO E OITO!", "CENTO E NOVE!", "CENTO E DEZ!",
    "CENTO E ONZE!", "CENTO E DOZE!", "CENTO E TREZE!", "CENTO E QUATORZE!", "CENTO E QUINZE!", "CENTO E DEZESSEIS!", "CENTO E DEZESSETE!", "CENTO E DEZOITO!", "CENTO E DEZENOVE!", "CENTO E VINTE!",
    "CENTO E VINTE E UM!", "CENTO E VINTE E DOIS!", "CENTO E VINTE E TRÊS!", "CENTO E VINTE E QUATRO!", "CENTO E VINTE E CINCO!", "CENTO E VINTE E SEIS!", "CENTO E VINTE E SETE!", "CENTO E VINTE E OITO!", "CENTO E VINTE E NOVE!", "CENTO E TRINTA!",
    "CENTO E TRINTA E UM!", "CENTO E TRINTA E DOIS!", "CENTO E TRINTA E TRÊS!", "CENTO E TRINTA E QUATRO!", "CENTO E TRINTA E CINCO!", "CENTO E TRINTA E SEIS!", "CENTO E TRINTA E SETE!", "CENTO E TRINTA E OITO!", "CENTO E TRINTA E NOVE!", "CENTO E QUARENTA!",
    "CENTO E QUARENTA E UM!", "CENTO E QUARENTA E DOIS!", "CENTO E QUARENTA E TRÊS!", "CENTO E QUARENTA E QUATRO!", "CENTO E QUARENTA E CINCO!", "CENTO E QUARENTA E SEIS!", "CENTO E QUARENTA E SETE!", "CENTO E QUARENTA E OITO!", "CENTO E QUARENTA E NOVE!", "CENTO E CINQUENTA!",
    "CENTO E CINQUENTA E UM!", "CENTO E CINQUENTA E DOIS!", "CENTO E CINQUENTA E TRÊS!", "CENTO E CINQUENTA E QUATRO!", "CENTO E CINQUENTA E CINCO!", "CENTO E CINQUENTA E SEIS!", "CENTO E CINQUENTA E SETE!", "CENTO E CINQUENTA E OITO!", "CENTO E CINQUENTA E NOVE!", "CENTO E SESSENTA!",
    "CENTO E SESSENTA E UM!", "CENTO E SESSENTA E DOIS!", "CENTO E SESSENTA E TRÊS!", "CENTO E SESSENTA E QUATRO!", "CENTO E SESSENTA E CINCO!", "CENTO E SESSENTA E SEIS!", "CENTO E SESSENTA E SETE!", "CENTO E SESSENTA E OITO!", "CENTO E SESSENTA E NOVE!", "CENTO E SETENTA!",
    "CENTO E SETENTA E UM!", "CENTO E SETENTA E DOIS!", "CENTO E SETENTA E TRÊS!", "CENTO E SETENTA E QUATRO!", "CENTO E SETENTA E CINCO!", "CENTO E SETENTA E SEIS!", "CENTO E SETENTA E SETE!", "CENTO E SETENTA E OITO!", "CENTO E SETENTA E NOVE!", "CENTO E OITENTA!",
    "CENTO E OITENTA E UM!", "CENTO E OITENTA E DOIS!", "CENTO E OITENTA E TRÊS!", "CENTO E OITENTA E QUATRO!", "CENTO E OITENTA E CINCO!", "CENTO E OITENTA E SEIS!", "CENTO E OITENTA E SETE!", "CENTO E OITENTA E OITO!", "CENTO E OITENTA E NOVE!", "CENTO E NOVENTA!",
    "CENTO E NOVENTA E UM!", "CENTO E NOVENTA E DOIS!", "CENTO E NOVENTA E TRÊS!", "CENTO E NOVENTA E QUATRO!", "CENTO E NOVENTA E CINCO!", "CENTO E NOVENTA E SEIS!", "CENTO E NOVENTA E SETE!", "CENTO E NOVENTA E OITO!", "CENTO E NOVENTA E NOVE!", "DUZENTOS!"
}

-- Interface
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TopBar = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseBtn = Instance.new("TextButton")
local MiniBtn = Instance.new("TextButton")
local StartBtn = Instance.new("TextButton")
local StopBtn = Instance.new("TextButton")

ScreenGui.Name = "CountSpammer_200"
ScreenGui.Parent = game:GetService("CoreGui")
ScreenGui.ResetOnSpawn = false

MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Size = UDim2.new(0, 220, 0, 160)
MainFrame.Position = UDim2.new(0.5, -110, 0.5, -80)
MainFrame.BorderSizePixel = 0
MainFrame.ClipsDescendants = true

TopBar.Parent = MainFrame
TopBar.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
TopBar.Size = UDim2.new(1, 0, 0, 35)
TopBar.BorderSizePixel = 0

Title.Parent = TopBar
Title.Size = UDim2.new(1, -70, 1, 0)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.Text = "Count 1-200"
Title.TextColor3 = Color3.fromRGB(0, 255, 127)
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.BackgroundTransparency = 1

CloseBtn.Parent = TopBar
CloseBtn.Position = UDim2.new(1, -35, 0, 0)
CloseBtn.Size = UDim2.new(0, 35, 0, 35)
CloseBtn.Text = "X"
CloseBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
CloseBtn.TextColor3 = Color3.new(1, 1, 1)

MiniBtn.Parent = TopBar
MiniBtn.Position = UDim2.new(1, -70, 0, 0)
MiniBtn.Size = UDim2.new(0, 35, 0, 35)
MiniBtn.Text = "-"
MiniBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
MiniBtn.TextColor3 = Color3.new(1, 1, 1)

StartBtn.Parent = MainFrame
StartBtn.Position = UDim2.new(0, 10, 0, 45)
StartBtn.Size = UDim2.new(1, -20, 0, 45)
StartBtn.Text = "ATIVAR CONTAGEM"
StartBtn.BackgroundColor3 = Color3.fromRGB(0, 100, 0)
StartBtn.TextColor3 = Color3.new(1, 1, 1)

StopBtn.Parent = MainFrame
StopBtn.Position = UDim2.new(0, 10, 0, 100)
StopBtn.Size = UDim2.new(1, -20, 0, 45)
StopBtn.Text = "PARAR"
StopBtn.BackgroundColor3 = Color3.fromRGB(100, 0, 0)
StopBtn.TextColor3 = Color3.new(1, 1, 1)

-- Lógica de Envio Atualizada
local function enviar(txt)
    -- Tenta o sistema novo (TextChatService)
    local chatChannel = TextChatService:FindFirstChild("TextChannels") and TextChatService.TextChannels:FindFirstChild("RBXGeneral")
    if chatChannel then
        chatChannel:SendAsync(txt)
    else
        -- Fallback para o sistema antigo (Legacy Chat)
        local sayMessage = ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents") and ReplicatedStorage.DefaultChatSystemChatEvents:FindFirstChild("SayMessageRequest")
        if sayMessage then
            sayMessage:FireServer(txt, "All")
        else
            -- Se for o TextChatService mas o canal não for RBXGeneral
            -- Tenta enviar via input simulado (último recurso)
            TextChatService.TextChannels.RBXGeneral:SendAsync(txt)
        end
    end
end

StartBtn.MouseButton1Click:Connect(function()
    if rodando then return end
    rodando = true
    StartBtn.Text = "CONTANDO..."
    for _, msg in ipairs(numeros) do
        if not rodando then break end
        enviar(msg)
        task.wait(0.3) -- Aumentado levemente para evitar o filtro de "Slow mode" do Roblox
    end
    rodando = false
    StartBtn.Text = "ATIVAR CONTAGEM"
end)

StopBtn.MouseButton1Click:Connect(function()
    rodando = false
end)

-- Fechar e Minimizar
CloseBtn.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)

local min = false
MiniBtn.MouseButton1Click:Connect(function()
    min = not min
    MainFrame:TweenSize(min and UDim2.new(0, 220, 0, 35) or UDim2.new(0, 220, 0, 160), "Out", "Quad", 0.3, true)
end)

-- Sistema Draggable (Movimentar)
local dragging, dragStart, startPos
TopBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

TopBar.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
end)

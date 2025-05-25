
game:GetService("StarterGui"):SetCore("SendNotification", {
    Title = "EZ SLOW + NPCS TRACK",
    Text = "By llEvilSayanll",
})

-- Configuración
local radio = 200000  -- Radio de detección de NPCs
_G.Track = true
_G.NoSlow = true


local function npcEstaVivo(npc)
    return npc.Parent
        and npc:FindFirstChild("HumanoidRootPart")
        and npc:FindFirstChild("Humanoid")
        and npc.Humanoid.Health > 0
end


local function rastrearNPC(npc)
    while _G.Track and npcEstaVivo(npc) and game:GetService("RunService").Heartbeat:Wait() do
        for _, orb in pairs(game.Workspace:GetChildren()) do
            if orb:FindFirstChild("Ki") and orb:FindFirstChild("Mesh") then
                orb.CFrame = npc.HumanoidRootPart.CFrame
            end
        end

        local jugador = game.Players.LocalPlayer.Character
        if jugador then
            for _, orb in pairs(jugador:GetChildren()) do
                if orb:FindFirstChild("Ki") and orb:FindFirstChild("Mesh") then
                    orb.CFrame = npc.HumanoidRootPart.CFrame
                end
            end
        end
    end
end


task.spawn(function()
    while game:GetService("RunService").Heartbeat:Wait() do
        if _G.Track then
            local jugador = game.Players.LocalPlayer.Character
            if jugador and jugador:FindFirstChild("HumanoidRootPart") then
                local npcsCercanos = {}
                for _, npc in pairs(game.Workspace.Live:GetChildren()) do
                    if not game.Players:GetPlayerFromCharacter(npc)
                        and npcEstaVivo(npc)
                        and (jugador.HumanoidRootPart.Position - npc.HumanoidRootPart.Position).Magnitude <= radio then

                        table.insert(npcsCercanos, npc)
                    end
                end

                if #npcsCercanos > 0 then
                    table.sort(npcsCercanos, function(a, b)
                        return (jugador.HumanoidRootPart.Position - a.HumanoidRootPart.Position).Magnitude <
                               (jugador.HumanoidRootPart.Position - b.HumanoidRootPart.Position).Magnitude
                    end)

                    rastrearNPC(npcsCercanos[1])
                end
            end
        end
        task.wait(0.1)
    end
end)

task.spawn(function()
    while task.wait() do
        if _G.NoSlow then
            for _, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
                if v.Name == "Justice Combination" then
                    local action = game.Players.LocalPlayer.Character:FindFirstChild("Action")
                    if action then action:Destroy() end
                end
                if table.find({
                    "Action", "Attacking", "Using", "hyper", "Hyper",
                    "heavy", "KiBlasted", "Tele", "tele", "Killed", "Slow"
                }, v.Name) then
                    v:Destroy()
                end
                if v.Name == "Block" and v:IsA("BoolValue") and v.Value == true then
                    v.Value = false
                end
            end
        end
    end
end)


game.Players.LocalPlayer.Chatted:Connect(function(msg)
    msg = msg:lower()
    if msg == ".stop" then
        _G.Track = false
        _G.NoSlow = false
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "EZ SYSTEM",
            Text = "Desactivado",
        })
    elseif msg == ".dtr" then
        _G.Track = true
        _G.NoSlow = true
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "EZ SYSTEM",
            Text = "Activado",
        })
    end
end)

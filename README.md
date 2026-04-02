local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
    Name = "subtoadepsYT",
    LoadingTitle = "Loading",
    LoadingSubtitle = "subtoadepsYT"
})

local Tab = Window:CreateTab("Main")

local running = false

-- 🔘 Toggle (ON/OFF)
Tab:CreateToggle({
    Name = "Run Loop",
    CurrentValue = false,
    Callback = function(Value)
        running = Value

        if running then
            task.spawn(function()
                local remote = game:GetService("ReplicatedStorage")
                    .Shared.Universe.Network.RemoteEvent.Actionable

                while running do
                    for i = 1000, 1500 do
                        if not running then break end
                        
                        remote:FireServer(i)
                        task.wait()
                    end
                end
            end)
        end
    end
})

-- ▶️ Start Button
Tab:CreateButton({
    Name = "Start",
    Callback = function()
        if running then return end
        running = true

        task.spawn(function()
            local remote = game:GetService("ReplicatedStorage")
                .Shared.Universe.Network.RemoteEvent.Actionable

            while running do
                for i = 1000, 1500 do
                    if not running then break end
                    
                    remote:FireServer(i)
                    task.wait()
                end
            end
        end)
    end
})

-- ⛔ Stop Button
Tab:CreateButton({
    Name = "Stop",
    Callback = function()
        running = false
    end
})

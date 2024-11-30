local user = "Tanos_loh"
local NPC = workspace:WaitForChild(user)

local attackCooldown = false

function getClosestPlayer()
    local closest_player, closest_distance = nil, 7
    for i, player in pairs(workspace:GetChildren()) do
        if player:FindFirstChild("Torso") and player ~= NPC then
            local distance = (NPC.Torso.Position - player.Torso.Position).Magnitude
            if distance < closest_distance then
                closest_player = player
                closest_distance = distance
            end
        end
    end
    return closest_player
end

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

local animationId = "rbxassetid://6170049100"
local animation = Instance.new("Animation")
animation.AnimationId = animationId

local humanoid = character:FindFirstChildOfClass("Humanoid")
local animator = humanoid:FindFirstChildOfClass("Animator")

if not animator then
    animator = Instance.new("Animator", humanoid)
end

function playAttackAnimation()
    local animationTrack = animator:LoadAnimation(animation)
    animationTrack:Play()
    print("play attack animation.")
end

function executeAttacks()
    if attackCooldown then
        print("Attack is on cooldown.")
        return
    end

    attackCooldown = true
    local closestPlayer = getClosestPlayer()
    if not closestPlayer then
        print("No nearby players found.")
        attackCooldown = false
        return
    end

    local sound = Instance.new("Sound")
    sound.SoundId = "rbxassetid://955633944"
    sound.Volume = 0.5
    sound.Parent = character

    for i = 1, 12 do
        playAttackAnimation()
        sound:Play()
        
        local args = {
            [1] = closestPlayer:FindFirstChild("Humanoid"),
            [2] = 3,
            [3] = CFrame.new(139.75120544433594, 29.41288948059082, -1176.201416015625, -0.6339665055274963, -0.6616520285606384, -0.40037795901298523, 0.5172971487045288, 0.02204027771949768, -0.8555218577384949, 0.5748821496963501, -0.7494869232177734, 0.328297883272171),
            [4] = Vector3.new(4.648889541625977, 0, 1.8406052589416504),
            [5] = 0.1,
            [6] = 2,
            [7] = "rbxassetid://3041190784",
            [8] = 2.25
        }
        
        game:GetService("ReplicatedStorage"):WaitForChild("Attacks"):WaitForChild("DamageOverHeaven"):FireServer(unpack(args))
        wait(1 / 12)
    end

    wait(1.3)

    local args = {
        [1] = closestPlayer:FindFirstChild("Humanoid"),
        [2] = 50,
        [3] = CFrame.new(138.66726684570312, 30.04323959350586, -1174.00927734375, -0.40443116426467896, -0.9060207605361938, -0.12474752962589264, 0.2939949333667755, 0.00036849488969892263, -0.955807089805603, 0.8660269379615784, -0.4232332408428192, 0.2662164270877838),
        [4] = Vector3.new(99.059814453125, 15, 13.680438995361328),
        [5] = 0.25,
        [6] = 0.75,
        [7] = "rbxassetid://1202656211",
        [8] = 2.25
    }

    game:GetService("ReplicatedStorage"):WaitForChild("Attacks"):WaitForChild("DamageOverwrite"):FireServer(unpack(args))

    local argsCooldown = {
        [1] = "KickCombo",
        [2] = "(B)",
        [3] = 15
    }
    game:GetService("ReplicatedStorage"):WaitForChild("CoolDowns"):FireServer(unpack(argsCooldown))

    wait(15)
    attackCooldown = false
end

game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessedEvent)
    if not gameProcessedEvent and input.KeyCode == Enum.KeyCode.B then
        executeAttacks()
    end
end)

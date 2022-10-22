-- This entire code is modified from HTDBarsi#3056's script, My code is totally different from this, UI is added by twist --
-- Feel free to change whatever in this script. This simple starter template is modified by twist --
_G.range = 100
_G.cooldown = 0.75
local plr = game:GetService'Players'['LocalPlayer']
local class = plr.Character.Properties.Class.Value
local Classes = {
   ["Swordmaster"]     = {"Swordmaster1", "Swordmaster2", "Swordmaster3", "Swordmaster4", "Swordmaster5", "Swordmaster6", "CrescentStrike1", "CrescentStrike2", "CrescentStrike3", "Leap"};
   ["Mage"]            = {"Mage1", "ArcaneBlastAOE", "ArcaneBlast", "ArcaneWave1", "ArcaneWave2", "ArcaneWave3", "ArcaneWave4", "ArcaneWave5", "ArcaneWave6", "ArcaneWave7", "ArcaneWave8", "ArcaneWave9"};
   ["Defender"]        = {"Defender1", "Defender2", "Defender3", "Defender4", "Defender5", "Groundbreaker", "Spin1", "Spin2", "Spin3", "Spin4", "Spin5"};
   ["DualWielder"]     = {"DualWield1", "DualWield2", "DualWield3", "DualWield4", "DualWield5", "DualWield6", "DualWield7", "DualWield8", "DualWield9", "DualWield10", "DashStrike", "CrossSlash1", "CrossSlash2", "CrossSlash3", "CrossSlash4"};
   ["Guardian"]        = {"Guardian1", "Guardian2", "Guardian3", "Guardian4", "SlashFury1", "SlashFury2", "SlashFury3", "SlashFury4", "SlashFury5", "SlashFury6", "SlashFury7", "SlashFury8", "SlashFury9", "SlashFury10", "SlashFury11", "SlashFury12", "SlashFury13", "RockSpikes1", "RockSpikes2", "RockSpikes3"};
   ["IcefireMage"]     = {"IcefireMage1", "IcySpikes1", "IcySpikes2", "IcySpikes3", "IcySpikes4", "IcefireMageFireballBlast", "IcefireMageFireball", "LightningStrike1", "LightningStrike2", "LightningStrike3", "LightningStrike4", "LightningStrike5", "IcefireMageUltimateFrost", "IcefireMageUltimateMeteor1"};
   ["Berserker"]       = {"Berserker1", "Berserker2", "Berserker3", "Berserker4", "Berserker5", "Berserker6", "AggroSlam", "GigaSpin1", "GigaSpin2", "GigaSpin3", "GigaSpin4", "GigaSpin5", "GigaSpin6", "GigaSpin7", "GigaSpin8", "Fissure1", "Fissure2", "FissureErupt1", "FissureErupt2", "FissureErupt3", "FissureErupt4", "FissureErupt5"};
   ["Paladin"]         = {"Paladin1", "Paladin2", "Paladin3", "Paladin4", "LightThrust1", "LightThrust2", "LightPaladin1", "LightPaladin2"};
   ["MageOfLight"]     = {"MageOfLight", "MageOfLightBlast"};
   ["Demon"]           = {"Demon1", "Demon4", "Demon7", "Demon10", "Demon13", "Demon16", "Demon19", "Demon22", "Demon25", "DemonDPS1", "DemonDPS2", "DemonDPS3", "DemonDPS4", "DemonDPS5", "DemonDPS6", "DemonDPS7", "DemonDPS8", "DemonDPS9", "ScytheThrowDPS1", "ScytheThrowDPS2", "ScytheThrowDPS3", "DemonLifeStealDPS", "DemonSoulDPS1", "DemonSoulDPS2", "DemonSoulDPS3"};
   ["Dragoon"]         = {"Dragoon1", "Dragoon2", "Dragoon3", "Dragoon4", "Dragoon5", "Dragoon6"};
   ["Archer"]          = {"Archer", "PiercingArrow1", "PiercingArrow2", "PiercingArrow3", "PiercingArrow4", "PiercingArrow5"};
   ["Warlord"]         = {"Warlord1", "Warlord2", "Warlord3", "Warlord4",};
};
local cl = Classes[class]
function closest()
   local Character = plr.Character
   local HumanoidRootPart = Character and Character:FindFirstChild("HumanoidRootPart")
   if not (Character or HumanoidRootPart) then return end
   local TargetDistance,Target = math.huge, nil
   for _,v in next, workspace.Mobs:GetChildren() do
       if v:FindFirstChild("Collider") then
           local mag = (HumanoidRootPart.Position - v.Collider.Position).magnitude
           if mag < TargetDistance and mag <= _G.range and v.HealthProperties.Health.Value > 0 then
               TargetDistance = mag
               Target = v
           end
       end
   end
   return Target
end
local function KillAura()
    local ind = 0
    repeat task.wait()
    local c = closest()
    if c then
        ind = ind + 1
        game:GetService("ReplicatedStorage").Shared.Combat.Attack:FireServer(cl[ind],c.Collider.Position, c.Collider.Position - plr.Character.HumanoidRootPart.Position)
        task.wait(_G.cooldown)
        if ind >= #cl then
            ind = 0
        end
    end
    until plr.Character.Humanoid.Health <= 0
end

local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/HeiKe2022/Mod-UI/main/ModTurtle.lua"))()
local SecA = library:window("World Zero")
SecA:toggle("Kill Aura", false, function(bool)
    if bool then
        KillAura()
    end
end)
SecA:slider("Cooldown",1,15,7, function(value)
    _G.cooldown = value/10
end)
SecA:toggle("Collect Drop", false, function(bool)
    if bool then
        while bool do
            for _,v in pairs(workspace.Coins:GetChildren'') do
                if v.Name == "CoinPart" then
                    v.CanCollide = false
                    v.Position = plr.Character.HumanoidRootPart.Position + Vector3.new(0,-1,0)
                end
            end
            task.wait(1/4)
        end
    end
end)
SecA:slider("Walk Speed",16, 120, 80, function(value)
    plr.Character.Humanoid.WalkSpeed = value
end)
SecA:slider("Jump Power",70, 160, 150, function(value)
    plr.Character.Humanoid.JumpPower = value
end)

local a = getrawmetatable(game)
local b = a.__index
local c = a.__newindex
setreadonly(a, false)
local d = plr.Character.Humanoid
local e = d.WalkSpeed
local f = d.JumpPower
a.__newindex =
    newcclosure(
    function(g, h, i)
        if checkcaller() then
            return c(g, h, i)
        elseif g:IsA "Humanoid" and h == "WalkSpeed" then
            i = tonumber(i)
            if not i then
                i = 0
            end
            e = i
        elseif g:IsA "Humanoid" and h == "JumpPower" then
            i = tonumber(i)
            if not i then
                i = 0
            end
            f = i
        else
            return c(g, h, i)
        end
    end
)
a.__index =
    newcclosure(
    function(g, h)
        if checkcaller() then
            return b(g, h)
        elseif g:IsA "Humanoid" and h == "WalkSpeed" then
            return e
        elseif g:IsA "Humanoid" and h == "JumpPower" then
            return f
        else
            return b(g, h)
        end
    end
)
setreadonly(a, true)

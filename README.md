
if game.PlaceId == 2753915549 then
    World1 = true
elseif game.PlaceId == 4442272183 then
    World2 = true
elseif game.PlaceId == 7449423635 then
    World3 = true
end

local function QuestCheck()
	local Lvl = game:GetService("Players").LocalPlayer.Data.Level.Value
	if Lvl >= 1 and Lvl <= 9 then
		if tostring(game.Players.LocalPlayer.Team) == "Marines" then
			MobName = "Trainee [Lv. 5]"
			QuestName = "MarineQuest"
			QuestLevel = 1
			Mon = "Trainee"
			NPCPosition = CFrame.new(-2709.67944, 24.5206585, 2104.24585, -0.744724929, -3.97967455e-08, -0.667371571, 4.32403588e-08, 1, -1.07884304e-07, 0.667371571, -1.09201515e-07, -0.744724929)
		elseif tostring(game.Players.LocalPlayer.Team) == "Pirates" then
			MobName = "Bandit [Lv. 5]"
			Mon = "Bandit"
			QuestName = "BanditQuest1"
			QuestLevel = 1
			NPCPosition = CFrame.new(1059.99731, 16.9222069, 1549.28162, -0.95466274, 7.29721794e-09, 0.297689587, 1.05190106e-08, 1, 9.22064114e-09, -0.297689587, 1.19340022e-08, -0.95466274)
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	if Lvl >= 375 and Lvl <= 399 then -- Fishman Warrior
		MobName = "Fishman Warrior [Lv. 375]"
		QuestName = "FishmanQuest"
		QuestLevel = 1
		Mon = "Fishman Warrior"
		NPCPosition = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
		MobCFrame = CFrame.new(60955.0625, 48.7988472, 1543.7168, -0.831178129, 6.20639318e-09, -0.556006253, 7.20035302e-08, 1, -9.64761853e-08, 0.556006253, -1.20223305e-07, -0.831178129)
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	if Lvl >= 15 and Lvl <= 29 then
		MobName = "Gorilla [Lv. 20]"
		QuestName = "JungleQuest"
		QuestLevel = 2
		Mon = "Gorilla"
		NPCPosition = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
		MobCFrame = CFrame.new(-1142.0293, 40.5877495, -516.118103, 0.55559355, 7.58965513e-08, 0.831454039, 1.24594361e-08, 1, -9.96073553e-08, -0.831454039, 6.57006538e-08, 0.55559355)
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	if Lvl >= 400 and Lvl <= 449 then -- Fishman Commando
		MobName = "Fishman Commando [Lv. 400]"
		QuestName = "FishmanQuest"
		QuestLevel = 2
		Mon = "Fishman Commando"
		NPCPosition = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
		MobCFrame = CFrame.new(61872.3008, 75.5976562, 1394.83484, -0.922134459, 4.36911973e-09, -0.38686946, -2.54707899e-08, 1, 7.20052e-08, 0.38686946, 7.62523484e-08, -0.922134459)
		if _G.Auto_Farm_Level and (NPCPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 3000 then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
		end
		return {
			[1] = QuestLevel,
			[2] = NPCPosition,
			[3] = MobName,
			[4] = QuestName,
			[5] = LevelRequire,
			[6] = Mon,
			[7] = MobCFrame
		}
	end

	--game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
	local GuideModule = require(game:GetService("ReplicatedStorage").GuideModule)
	local Quests = require(game:GetService("ReplicatedStorage").Quests)
	for i,v in pairs(GuideModule["Data"]["NPCList"]) do
		for i1,v1 in pairs(v["Levels"]) do
			if Lvl >= v1 then
				if not LevelRequire then
					LevelRequire = 0
				end
				if v1 > LevelRequire then
					NPCPosition = i["CFrame"]
					QuestLevel = i1
					LevelRequire = v1
				end
				if #v["Levels"] == 3 and QuestLevel == 3 then
					NPCPosition = i["CFrame"]
					QuestLevel = 2
					LevelRequire = v["Levels"][2]
				end
			end
		end
	end
	for i,v in pairs(Quests) do
		for i1,v1 in pairs(v) do
			if v1["LevelReq"] == LevelRequire and i ~= "CitizenQuest" then
				QuestName = i
				for i2,v2 in pairs(v1["Task"]) do
					MobName = i2
					Mon = string.split(i2," [Lv. ".. v1["LevelReq"] .. "]")[1]
				end
			end
		end
	end
	if QuestName == "MarineQuest2" then
		QuestName = "MarineQuest2"
		QuestLevel = 1
		MobName = "Chief Petty Officer [Lv. 120]"
		Mon = "Chief Petty Officer"
		LevelRequire = 120
	elseif QuestName == "ImpelQuest" then
		QuestName = "PrisonerQuest"
		QuestLevel = 2
		MobName = "Dangerous Prisoner [Lv. 190]"
		Mon = "Dangerous Prisoner"
		LevelRequire = 210
		NPCPosition = CFrame.new(5310.60547, 0.350014925, 474.946594, 0.0175017118, 0, 0.999846935, 0, 1, 0, -0.999846935, 0, 0.0175017118)
	elseif QuestName == "SkyExp1Quest" then
		if QuestLevel == 1 then
			NPCPosition = CFrame.new(-4721.88867, 843.874695, -1949.96643, 0.996191859, -0, -0.0871884301, 0, 1, -0, 0.0871884301, 0, 0.996191859)
		elseif QuestLevel == 2 then
			NPCPosition = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
		end
	elseif QuestName == "Area2Quest" and QuestLevel == 2 then
		QuestName = "Area2Quest"
		QuestLevel = 1
		MobName = "Swan Pirate [Lv. 775]"
		Mon = "Swan Pirate"
		LevelRequire = 775
	end
	MobName = MobName:sub(1,#MobName)

	return {
		[1] = QuestLevel,
		[2] = NPCPosition,
		[3] = MobName,
		[4] = QuestName,
		[5] = LevelRequire,
		[6] = Mon,
		[7] = MobCFrame
	}
end

function AutoHaki()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
end

function EquipWeapon(ToolSe)
    if not _G.NotAutoEquip then
        if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
            Tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
            wait(.1)
            game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
        end
    end
end


getgenv().ToTarget = function(Pos)
    Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
    pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/250, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
    tween:Play()
    if Distance <= 250 then
        tween:Cancel()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
    end
    if _G.StopTween == true then
        tween:Cancel()
        _G.Clip = false
    end
end

local function StopTween(target)
    if not target then
        getgenv().ToTarget(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame)
        if game.Players.LocalPlayer.Character:FindFirstChild("Root") then
            game.Players.LocalPlayer.Character:FindFirstChild("Root"):Destroy()
        end
    end
end

function GetDistance(target)
    return math.floor((target.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude)
end

function UseCode(Text)
    game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
end

spawn(function()
	while task.wait() do
		pcall(function()
			if _G.Auto_Farm_Level or _G.Auto_Farm_Mob_Aura or _G.Auto_New_World or _G.Auto_Farm_BF_Mastery or _G.Auto_Farm_Gun_Mastery or _G.Auto_Third_World or _G.AutoFarmChest or _G.Start_Tween_Island or _G.Auto_Farm_Boss or _G.Auto_Elite_Hunter or _G.Auto_Cake_Prince or _G.Auto_Farm_All_Boss or _G.AutoSaber or _G.Auto_Pole or _G.Auto_Factory_Farm or _G.Auto_Farm_Ectoplasm or _G.Auto_Bartilo_Quest or _G.Auto_Rengoku or _G.Auto_Evo_Race_V2 or _G.Auto_Swan_Glasses or _G.Auto_Dragon_Trident or _G.Auto_Farm_Bone or  _G.Auto_Rainbow_Haki or _G.Auto_Holy_Torch or _G.Auto_Canvander or _G.Auto_Twin_Hook or _G.Auto_Serpent_Bow or _G.AutoFarmMaterial or _G.Auto_Fully_Death_Step or _G.Auto_Fully_SharkMan_Karate or _G.Teleport_to_Player or _G.Auto_Kill_Player_Melee or _G.Auto_Kill_Player_Gun or _G.Auto_Next_Island or _G.AutoFarmSelectMonster or _G.Auto_Factory_Farm or _G.Auto_Tushita or _G.Auto_Yama or _G.Auto_Kill_Law or _G.Auto_Soul_Guitar or _G.Auto_Farm_Chest_Fast then
				if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
					local Noclip = Instance.new("BodyVelocity")
					Noclip.Name = "BodyClip"
					Noclip.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
					Noclip.MaxForce = Vector3.new(100000,100000,100000)
					Noclip.Velocity = Vector3.new(0,0,0)
				end
			else
				game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
			end
		end)
	end
end)

spawn(function()
	while task.wait() do
		pcall(function()
            if _G.Auto_Farm_Level or _G.Auto_Farm_Mob_Aura or _G.Auto_New_World or _G.Auto_Farm_BF_Mastery or _G.Auto_Farm_Gun_Mastery or _G.Auto_Third_World or _G.AutoFarmChest or _G.Start_Tween_Island or _G.Auto_Farm_Boss or _G.Auto_Elite_Hunter or _G.Auto_Cake_Prince or _G.Auto_Farm_All_Boss or _G.AutoSaber or _G.Auto_Pole or _G.Auto_Factory_Farm or _G.Auto_Farm_Ectoplasm or _G.Auto_Bartilo_Quest or _G.Auto_Rengoku or _G.Auto_Evo_Race_V2 or _G.Auto_Swan_Glasses or _G.Auto_Dragon_Trident or _G.Auto_Farm_Bone or  _G.Auto_Rainbow_Haki or _G.Auto_Holy_Torch or _G.Auto_Canvander or _G.Auto_Twin_Hook or _G.Auto_Serpent_Bow or _G.AutoFarmMaterial or _G.Auto_Fully_Death_Step or _G.Auto_Fully_SharkMan_Karate or _G.Teleport_to_Player or _G.Auto_Kill_Player_Melee or _G.Auto_Kill_Player_Gun or _G.Auto_Next_Island or _G.AutoFarmSelectMonster or _G.Auto_Factory_Farm or _G.Auto_Tushita or _G.Auto_Yama or _G.Auto_Kill_Law or _G.Auto_Soul_Guitar or _G.Auto_Farm_Chest_Fast then
                if not game.Players.LocalPlayer.Character:FindFirstChild('MAKEHI') then
                    local Test = Instance.new('Highlight')
                    Test.Name = "MAKEHI"
                    Test.Enabled = true
                    Test.FillColor = Color3.fromRGB(2, 197, 60)
                    Test.OutlineColor = Color3.fromRGB(0, 181, 6)
                    Test.FillTransparency = 0.2
                    Test.OutlineTransparency = 0.1
                    Test.Parent = game.Players.LocalPlayer.Character
                end
            else
                if game.Players.LocalPlayer.Character:FindFirstChild('MAKEHI') then
                    game.Players.LocalPlayer.Character:FindFirstChild('MAKEHI'):Destroy()
                end
            end
		end)
	end
end)

MethodFarm = CFrame.new(0, 30, 0)


-------------------------------------------------------------------------------------------------------------------------------------------
local ArrayField = loadstring(game:HttpGet("https://raw.githubusercontent.com/Hosvile/Refinement/main/MC%3AArrayfield%20Library"))()
local Window = ArrayField:CreateWindow({
        Name = "Manake Hub | Blox Fruit",
        LoadingTitle = "Manake Hub",
        LoadingSubtitle = "by Maruko and Sal",
        ConfigurationSaving = {
            Enabled = true,
            FolderName = nil, -- Create a custom folder for your hub/game
            FileName = "ArrayField"
        },
        Discord = {
            Enabled = false,
            Invite = "sirius", -- The Discord invite code, do not include discord.gg/
            RememberJoins = true -- Set this to false to make them join the discord every time they load it up
        },
    })

local Tab = Window:CreateTab("General", 4483362458) -- Title, Image
local Setting = Window:CreateTab("Setting") -- Title, Image

Tab:CreateSection("Main Funcrion",true)

local Toggle = Tab:CreateToggle({
    Name = "Auto Farm Level",
    Info = {
        Title = 'Auto Farm Level',
        Image = '12735851647',
        Description = 'ฟาร์มเพื่ออัพเลเวล จาก 1 - 2550',
    },
    CurrentValue = false,
    Flag = "FarmLv", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Farm_Level = Value
        StopTween(_G.Auto_Farm_Level)
    end,
})

spawn(function()
	while wait() do
		local MyLevel = game.Players.LocalPlayer.Data.Level.Value
		local QuestC = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest
		pcall(function()
			if _G.Auto_Farm_Level then
				if QuestC.Visible == true then
					if game:GetService("Workspace").Enemies:FindFirstChild(QuestCheck()[3]) then
						for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if string.find(_v.Name,QuestCheck()[3]) then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if string.find(v.Name,QuestCheck()[3]) then
										if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
											repeat wait()
												if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, QuestCheck()[6]) then
													game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
												else
													PosMon = v.HumanoidRootPart.CFrame
													v.HumanoidRootPart.Size = Vector3.new(50,50,50)
													v.HumanoidRootPart.CanCollide = false
													v.Humanoid.WalkSpeed = 0
													v.Head.CanCollide = false
													BringMobFarm = true
													AutoHaki()
													EquipWeapon(_G.Select_Weapon)
													v.HumanoidRootPart.Transparency = 1
													getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												end
											until not _G.Auto_Farm_Level or not v.Parent or v.Humanoid.Health <= 0 or QuestC.Visible == false or not v:FindFirstChild("HumanoidRootPart")
										end
									end
								end
							end
						end 
					else
						for i,v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
							if v.Name == QuestCheck()[6] then local CFrameEnemySpawns = v.CFrame  wait(0.5)
								getgenv().ToTarget(CFrameEnemySpawns * MethodFarm)
							end
						end
					end
				else
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
						BTP(QuestCheck()[2])
						return
					end
					repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1 or not _G.Auto_Farm_Level
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10 then
						BringMobFarm = false
						wait(0.2)
						game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) wait(0.5)
					else
						repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1 or not _G.Auto_Farm_Level
						for i,v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
							if v.Name == QuestCheck()[6] then local CFrameEnemySpawns = v.CFrame  wait(0.5)
								getgenv().ToTarget(CFrameEnemySpawns * MethodFarm)
							end
						end
					end
				end
			end
		end)
	end
end)


local Toggle = Tab:CreateToggle({
    Name = "Auto Farm Mob Aura",
    Info = {
        Title = 'Auto Farm Mob Aura',
        Image = '12735851647',
        Description = 'ฟาร์มมอน รอบเกาะที่เราอยู่',
    },
    CurrentValue = false,
    Flag = "FarmMobAura", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Farm_Mob_Aura = Value
        StopTween(_G.Auto_Farm_Mob_Aura)
    end,
})


spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Farm_Mob_Aura then
                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                    if _G.Auto_Farm_Mob_Aura and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 1000 then
                        repeat wait()
                            StartMagnet = true
                            EquipWeapon(_G.Select_Weapon)
                            AutoHaki()
                            PosMonAura = v.HumanoidRootPart.CFrame
                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.HumanoidRootPart.CanCollide = false
                            v.Humanoid:ChangeState(11)
                            getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
                        until not _G.Auto_Farm_Mob_Aura or not v.Parent or v.Humanoid.Health <= 0
                    end
                end
            end
        end)
    end
end)

if World3 then
    local Toggle = Tab:CreateToggle({
    Name = "Auto Farm Candy",
    Info = {
        Title = 'Auto Farm Candy',
        Image = '12735851647',
        Description = 'ฟาร์มแคนดี้',
    },
    CurrentValue = false,
    Flag = "FCandy", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        print(Value)
    end,
})
end




Tab:CreateSection("Setting",true)


local SelectWeapon = "Melee";
local Weapon = {
    "Melee",
    "Sword",
    "Fruit"
}

task.spawn(function()
    while wait() do
        pcall(function()
            if SelectWeapon == "Melee" then
                for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v.ToolTip == "Melee" then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                            _G.Select_Weapon = v.Name
                        end
                    end
                end
            elseif SelectWeapon == "Sword" then
                for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v.ToolTip == "Sword" then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                            _G.Select_Weapon = v.Name
                        end
                    end
                end
            elseif SelectWeapon == "Fruit" then
                for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v.ToolTip == "Blox Fruit" then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                            _G.Select_Weapon = v.Name
                        end
                    end
                end
            else
                for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v.ToolTip == "Melee" then
                        if game.Players.LocalPlayer.Backpack:FindFirstChild(tostring(v.Name)) then
                            _G.Select_Weapon = v.Name
                        end
                    end
                end
            end
        end)
    end
end)

local SingleSelection = Tab:CreateDropdown({
    Name = "Select Weapon",
    Options = Weapon,
    CurrentOption = "Melee",
    MultiSelection = false,
    Flag = "SelectWeapon",
    Callback = function(Option)
        SelectWeapon = Option
    end,
})

local Toggle = Tab:CreateToggle({
    Name = "Fast Attack",
    Info = {
        Title = 'Fast Attack',
        Image = '12735851647',
        Description = 'ตีเร็ว',
    },
    CurrentValue = false,
    Flag = "FastAttack", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.FastAttack = Value
    end,
})


function getHits(Size)
	local Hits = {}
	local nearbymon = false

	if nearbymon then
		local Enemies = workspace.Enemies:GetChildren()
		local Characters = workspace.Characters:GetChildren()

		for i = 1, #Enemies do
			local v = Enemies[i]
			local Human = v:FindFirstChildOfClass("Humanoid")

			if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < Size + 5 then
				table.insert(Hits, Human.RootPart)
			end
		end

		for i = 1, #Characters do
			local v = Characters[i]

			if v ~= Client.Character then
				local Human = v:FindFirstChildOfClass("Humanoid")

				if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < Size + 5 then
					table.insert(Hits, Human.RootPart)
				end
			end
		end
	end

	return Hits
end

Players = game.Players
Client = Players.LocalPlayer
Character = Client.Character:GetChildren()
Char = Client.Character
Root = Char.HumanoidRootPart
RunService = game:GetService("RunService")
vim = game:GetService('VirtualInputManager')
CollectionService = game:GetService("CollectionService")

CurrentAllMob = {}
canHits = {}

local CameraShaker = require(game.ReplicatedStorage.Util.CameraShaker)
CameraShaker:Stop()

local PC = require(Client.PlayerScripts.CombatFramework.Particle)
local RL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
local DMG = require(Client.PlayerScripts.CombatFramework.Particle.Damage)
local RigC = getupvalue(require(Client.PlayerScripts.CombatFramework.RigController), 2)
local Combat = getupvalue(require(Client.PlayerScripts.CombatFramework), 2)

task.spawn(function()
	pcall(function()
		local stacking = 0
		local printCooldown = 0

		while wait(0.075) do
			nearbymon = false
			CurrentAllMob = {}
			canHits = {}
			local mobs = CollectionService:GetTagged("ActiveRig")

			for i = 1, #mobs do
				local v = mobs[i]
				Human = v:FindFirstChildOfClass("Humanoid")

				if Human and Human.Health > 0 and Human.RootPart and v ~= Char then
					local IsPlayer = game.Players:GetPlayerFromCharacter(v)
					local IsAlly = IsPlayer and CollectionService:HasTag(IsPlayer, "Ally" .. Client.Name)

					if not IsAlly then
						CurrentAllMob[#CurrentAllMob + 1] = v

						if not nearbymon and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
							nearbymon = true
						end
					end
				end
			end

			if nearbymon then
				local Enemies = workspace.Enemies:GetChildren()
				local Players = Players:GetPlayers()

				for i = 1, #Enemies do
					local v = Enemies[i]
					local Human = v:FindFirstChildOfClass("Humanoid")

					if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
						canHits[#canHits + 1] = Human.RootPart
					end
				end

				for i = 1, #Players do
					local v = Players[i].Character

					if not Players[i]:GetAttribute("PvpDisabled") and v and v ~= Client.Character then
						local Human = v:FindFirstChildOfClass("Humanoid")

						if Human and Human.RootPart and Human.Health > 0 and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 50 then
							canHits[#canHits + 1] = Human.RootPart
						end
					end
				end
			end
		end
	end)
end)

local Data = Combat
local Blank = function() end
local RigEvent = game:GetService("ReplicatedStorage").RigControllerEvent
local Validator = game.ReplicatedStorage.Remotes.Validator
local Animation = Instance.new("Animation")
local RecentlyFired = 0
local AttackCD = 0
local Controller
local lastFireValid = 0
local MaxLag = 350
local fucker = 0.07
local TryLag = 0

local resetCD = function()
	local WeaponName = Controller.currentWeaponModel.Name
	local Cooldown = {
		combat = 0.07
	}
	AttackCD = tick() + (fucker and Cooldown[WeaponName:lower()] or fucker or 0.285) + ((TryLag / MaxLag) * 0.3)
	RigEvent:FireServer("weaponChange", WeaponName)
	TryLag = TryLag + 0.8
	task.delay((fucker or 0.285) + (TryLag + 0.5 / MaxLag) * 0.3, function()
		TryLag = TryLag - 0.8
	end)
end

if not shared.orl then
	shared.orl = RL.wrapAttackAnimationAsync
end

if not shared.cpc then
	shared.cpc = PC.play
end

if not shared.dnew then
	shared.dnew = DMG.new
end

if not shared.attack then
	shared.attack = RigC.attack
end

RL.wrapAttackAnimationAsync = function(a, b, c, d, func)
	if not _G.FastAttack then
		PC.play = shared.cpc
		return shared.orl(a, b, c, 65, func)
	end

	local Radius = (_G.FastAttack and _G.FastAttack) or 50

	if canHits and #canHits > 0 then
		PC.play = function() end
		a:Play(0.02, 0.02, 0.02)
		func(canHits)
		wait(a.length * 0.5)
		a:Stop()
	end
end

task.spawn(function()
	pcall(function()
		local Data = Combat
		local Blank = function() end
		local RigEvent = game:GetService("ReplicatedStorage").RigControllerEvent
		local Animation = Instance.new("Animation")
		local RecentlyFired = 0
		local AttackCD = 0
		local Controller
		local lastFireValid = 0
		local MaxLag = 350
		local fucker = 0.07
		local TryLag = 0

		local resetCD = function()
			local WeaponName = Controller.currentWeaponModel.Name
			local Cooldown = {
				combat = 0.07
			}
			AttackCD = tick() + (fucker and Cooldown[WeaponName:lower()] or fucker or 0.285) + ((TryLag / MaxLag) * 0.3)
			RigEvent:FireServer("weaponChange", WeaponName)
			TryLag = TryLag + 0.8
			task.delay((fucker or 0.285) + (TryLag + 0.5 / MaxLag) * 0.3, function()
				TryLag = TryLag - 0.8
			end)
		end

		if not shared.orl then
			shared.orl = RL.wrapAttackAnimationAsync
		end

		if not shared.cpc then
			shared.cpc = PC.play
		end

		if not shared.dnew then
			shared.dnew = DMG.new
		end

		if not shared.attack then
			shared.attack = RigC.attack
		end

		RL.wrapAttackAnimationAsync = function(a, b, c, d, func)
			if not _G.FastAttack then
				PC.play = shared.cpc
				return shared.orl(a, b, c, 50, func)
			end

			local Radius = _G.FastAttack or 50

			if canHits and #canHits > 0 then
				PC.play = function() end
				a:Play(0.02, 0.02, 0.02)
				func(canHits)
				wait(a.length * 0.5)
				a:Stop()
			end
		end

		while RunService.Stepped:Wait() do
			if #canHits > 0 then
				Controller = Data.activeController

				if Controller and Controller.equipped and Controller.currentWeaponModel then
					if _G.FastAttack then
						if _G.FastAttack and tick() > AttackCD then
							resetCD()
						end

						if tick() - lastFireValid > 0.5 or not _G.FastAttack then
							Controller.timeToNextAttack = 0
							Controller.hitboxMagnitude = 65
							pcall(task.spawn, Controller.attack, Controller)
							lastFireValid = tick()
							for i = 1, 10 do
								if i % 2 == 0 then
									break
								end
							end
						end

						local AID3 = Controller.anims.basic[3]
						local AID2 = Controller.anims.basic[2]
						local ID = AID3 or AID2
						Animation.AnimationId = ID
						local Playing = Controller.humanoid:LoadAnimation(Animation)
						Playing:Play(0.02, 0.02, 0.02)
						RigEvent:FireServer("hit", canHits, AID3 and 3 or 2, "")
						-- AttackSignal:Fire()
						delay(0.5, function()
							Playing:Stop()
						end)
					end
				end
			end
		end
	end)
end)

local Toggle = Tab:CreateToggle({
    Name = "Bring Mob",
    Info = {
        Title = 'Bring Mob',
        Image = '12735851647',
        Description = 'รวมมอน',
    },
    CurrentValue = false,
    Flag = "Bring_Mob", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Bring_Mob = Value
    end,
})
spawn(function()
	while task.wait() do
		pcall(function()
			if _G.Bring_Mob then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if _G.Auto_Farm_Level and BringMobFarm and string.find(v.Name,QuestCheck()[3]) and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then	
						v.HumanoidRootPart.CFrame = PosMon
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
					elseif _G.Auto_Farm_Bone and StartMagnetBoneMon and (v.Name == "Reborn Skeleton" or v.Name == "Living Zombie" or v.Name == "Demonic Soul" or v.Name == "Posessed Mummy") and (v.HumanoidRootPart.Position - PosMonBone.Position).magnitude <= 225 then
						v.HumanoidRootPart.CFrame = PosMonBone
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
					elseif _G.Auto_Cake_Prince and StartCakeMagnet and (v.Name == "Cookie Crafter" or v.Name == "Cake Guard" or v.Name == "Baking Staff" or v.Name == "Head Baker") and (v.HumanoidRootPart.Position - POSCAKE.Position).magnitude <= 225 then
						v.HumanoidRootPart.CFrame = POSCAKE
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
					elseif _G.Auto_Musketeer_Hat and (v.HumanoidRootPart.Position - PosMon.Position).magnitude <= 225 then
						v.HumanoidRootPart.CFrame = PosMon
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
					elseif _G.Auto_Farm_Mob_Aura and (v.HumanoidRootPart.Position - PosMonAura.Position).magnitude <= 225 then
						v.HumanoidRootPart.CFrame =  PosMonAura
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
					elseif _G.Auto_Rengoku and StartMagnet and (v.Name == "Snow Lurker" or v.Name == "Arctic Warrior") and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMon
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_EvoRace and StartEvoMagnet and v.Name == "Zombie" and (v.HumanoidRootPart.Position - PosMonEvo.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonEvo
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Bartilo and StartMagnet and v.Name == "Swan Pirate" and (v.HumanoidRootPart.Position - PosMonBarto.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMon
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_Gun_Mastery and StartMasteryGunMagnet and v.Name == "Monkey" and (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryGun
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_Gun_Mastery and v.Name == "Factory Staff" and (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryGun
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_Gun_Mastery and string.find(v.Name,QuestCheck()[3]) and (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryGun
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_BF_Mastery and StartMasteryFruitMagnet and v.Name == "Monkey" and (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryFruit
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_BF_Mastery and v.Name == "Factory Staff" and (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryFruit
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_BF_Mastery and string.find(v.Name,QuestCheck()[3]) and (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryFruit
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					end
				end
			end
		end)
	end
end)


Tab:CreateSection("Mastery",true)

local Toggle = Tab:CreateToggle({
    Name = "Auto Farm BF Mastery",
    Info = {
        Title = 'Auto Farm BF Mastery',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "Auto_Farm_BF_Mastery", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Farm_BF_Mastery = Value
        StopTween(_G.Auto_Farm_BF_Mastery)
    end,
})


if _G.Auto_Farm_BF_Mastery == false then
	UseSkill = false 
end

spawn(function()
	while wait() do
		local MyLevel = game.Players.LocalPlayer.Data.Level.Value
		local QuestC = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest
		pcall(function()
			if _G.Auto_Farm_BF_Mastery then
				if QuestC.Visible == true then
					for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if string.find(_v.Name,QuestCheck()[3]) then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if string.find(v.Name,QuestCheck()[3]) then
									if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat task.wait()
											if v.Humanoid.Health <= HealthMs then
												AutoHaki()
												EquipWeapon(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value)
												getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												v.HumanoidRootPart.CanCollide = false
												PosMonMasteryFruit = v.HumanoidRootPart.CFrame
												v.Humanoid.WalkSpeed = 0
												v.Head.CanCollide = false
												UseSkill = true
											else           
												UseSkill = false 
												AutoHaki()
												EquipWeapon(_G.Select_Weapon)
												getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												v.HumanoidRootPart.CanCollide = false
												v.HumanoidRootPart.Size = Vector3.new(50,50,50)
												PosMonMasteryFruit = v.HumanoidRootPart.CFrame
												v.Humanoid.WalkSpeed = 0
												v.Head.CanCollide = false
											end
											StartMasteryFruitMagnet = true
										until not _G.Auto_Farm_BF_Mastery or not v.Parent or v.Humanoid.Health <= 0 or QuestC.Visible == false or not v:FindFirstChild("HumanoidRootPart")
									end
								end
							end
						end
					end 
				else
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
						BTP(QuestCheck()[2])
						return
					end
					repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 0 or not _G.Auto_Farm_BF_Mastery
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10 then
						BringMobFarm = false
						wait(0.2)
						game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) wait(0.5)
					else
						repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 0 or not _G.Auto_Farm_BF_Mastery
						for i,v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
							if v.Name == QuestCheck()[6] then local CFrameEnemySpawns = v.CFrame  wait(0.5)
								getgenv().ToTarget(CFrameEnemySpawns * MethodFarm)

							end
						end
					end
				end
			end
		end)
	end
end)

spawn(function()
	while wait() do
		if UseSkill then
			pcall(function()
				for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
					if game:GetService("Players").LocalPlayer.Character:FindFirstChild(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value) then
						MasBF = game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Data.DevilFruit.Value].Level.Value
					elseif game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value) then
						MasBF = game:GetService("Players").LocalPlayer.Backpack[game:GetService("Players").LocalPlayer.Data.DevilFruit.Value].Level.Value
					end
					if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon-Dragon") then                      
						if _G.Skill_Z then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                        
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
						end
						if _G.Skill_X then          
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))               
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
						end
						if _G.Skill_C then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                          
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
							wait(2)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
						end
					elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom-Venom") then   
						if _G.Skill_Z then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                        
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
						end
						if _G.Skill_X then        
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))               
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
						end
						if _G.Skill_C then 
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                          
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
							wait(2)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
						end
					elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
						if _G.Skill_Z and game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Size == Vector3.new(2, 2.0199999809265, 1) then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                         
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
						end
						if _G.Skill_X then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                           
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
						end
						if _G.Skill_C then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                           
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
						end
						if _G.Skill_V then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"V",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"V",false,game)
						end
					elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(game:GetService("Players").LocalPlayer.Data.DevilFruit.Value) then
						if _G.Skill_Z then 
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                         
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
						end
						if _G.Skill_X then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                           
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
						end
						if _G.Skill_C then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))                           
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
						end
						if _G.Skill_V then
							local args = {
								[1] = PosMonMasteryFruit.Position
							}
							game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Tool").Name].RemoteEvent:FireServer(unpack(args))
							game:GetService("VirtualInputManager"):SendKeyEvent(true,"V",false,game)
							game:GetService("VirtualInputManager"):SendKeyEvent(false,"V",false,game)
						end
					end
				end
			end)
		end
	end
end)

spawn(function()
	game:GetService("RunService").RenderStepped:Connect(function()
		pcall(function()
			if UseSkill then
				for i,v in pairs(game:GetService("Players").LocalPlayer.PlayerGui.Notifications:GetChildren()) do
					if v.Name == "NotificationTemplate" then
						if string.find(v.Text,"Skill locked!") then
							v:Destroy()
						end
					end
				end
			end
		end)
	end)
end)

spawn(function()
	pcall(function()
		game:GetService("RunService").RenderStepped:Connect(function()
			if UseSkill then
				local args = {
					[1] = PosMonMasteryFruit.Position
				}
				game:GetService("Players").LocalPlayer.Character[game:GetService("Players").LocalPlayer.Data.DevilFruit.Value].RemoteEvent:FireServer(unpack(args))
			end
		end)
	end)
end)

local Toggle = Tab:CreateToggle({
    Name = "Auto Farm Gun Mastery",
    Info = {
        Title = 'Auto Farm Gun Mastery',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "Auto_Farm_Gun_Mastery", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Farm_Gun_Mastery = Value
        StopTween(_G.Auto_Farm_Gun_Mastery)
    end,
})


spawn(function()
	pcall(function()
		while wait() do
			for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do  
				if v:IsA("Tool") then
					if v:FindFirstChild("RemoteFunctionShoot") then 
						SelectWeaponGun = v.Name
					end
				end
			end
		end
	end)
end)

spawn(function()
	while wait() do
		local MyLevel = game.Players.LocalPlayer.Data.Level.Value
		local QuestC = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest
		pcall(function()
			if _G.Auto_Farm_Gun_Mastery then
				if QuestC.Visible == true then
					for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if string.find(_v.Name,QuestCheck()[3]) then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if string.find(v.Name,QuestCheck()[3]) then
									if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat task.wait()
											if string.find(QuestC.Container.QuestTitle.Title.Text, QuestCheck()[6]) then
												HealthMin = v.Humanoid.MaxHealth * _G.Kill_At/100
												if v.Humanoid.Health <= HealthMin then                                                
													EquipWeapon(SelectWeaponGun)
													getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
													v.Humanoid.WalkSpeed = 0
													v.HumanoidRootPart.CanCollide = false
													v.HumanoidRootPart.Size = Vector3.new(2,2,1)
													v.Head.CanCollide = false                                                
													local args = {
														[1] = v.HumanoidRootPart.Position,
														[2] = v.HumanoidRootPart
													}
													game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(unpack(args))
												else
													AutoHaki()
													EquipWeapon(_G.Select_Weapon)
													v.Humanoid.WalkSpeed = 0
													v.HumanoidRootPart.CanCollide = false
													v.Head.CanCollide = false               
													v.HumanoidRootPart.Size = Vector3.new(50,50,50)
													getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												end
												StartMasteryGunMagnet = true 
												PosMonMasteryGun = v.HumanoidRootPart.CFrame
											else
												StartMasteryGunMagnet = false
												game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
											end
										until not _G.Auto_Farm_Gun_Mastery or not v.Parent or v.Humanoid.Health <= 0 or QuestC.Visible == false or not v:FindFirstChild("HumanoidRootPart")
									end
								end
							end
						end
					end 
				else
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
						BTP(QuestCheck()[2])
						return
					end
					repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 0 or not _G.Auto_Farm_Gun_Mastery
					if (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 10 then
						BringMobFarm = false
						wait(0.2)
						game:GetService('ReplicatedStorage').Remotes.CommF_:InvokeServer("StartQuest", QuestCheck()[4], QuestCheck()[1]) wait(0.5)
					else
						repeat wait() getgenv().ToTarget(QuestCheck()[2]) until (QuestCheck()[2].Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 0 or not _G.Auto_Farm_Gun_Mastery
						for i,v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
							if v.Name == QuestCheck()[6] then local CFrameEnemySpawns = v.CFrame  wait(0.5)
								getgenv().ToTarget(CFrameEnemySpawns * MethodFarm)
							end
						end
					end
				end
			end
		end)
	end
end)

local Slider = Tab:CreateSlider({
    Name = "Kill At %",
    Range = {0, 100},
    Increment = 25,
    Suffix = "Kill",
    CurrentValue = 25,
    Flag = "Kill_At",
    Callback = function(Value)
        _G.Kill_At = Value
    end,
})

if World1 then
    
Tab:CreateSection("World",true)

local Toggle = Tab:CreateToggle({
    Name = "Auto New World",
    Info = {
        Title = 'Auto New World',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "NewWorld", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_New_World = Value
        StopTween(_G.Auto_New_World)
    end,
})


spawn(function()
    while wait() do
        if _G.Auto_New_World then
            pcall(function()
                if game.Players.LocalPlayer.Data.Level.Value >= 700 and World1 then
                    _G.Auto_Farm_Level = false
                    if game.Workspace.Map.Ice.Door.CanCollide == true and game.Workspace.Map.Ice.Door.Transparency == 0 then
                        repeat wait() getgenv().ToTarget(CFrame.new(4851.8720703125, 5.6514348983765, 718.47094726563)) until (CFrame.new(4851.8720703125, 5.6514348983765, 718.47094726563).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.Auto_New_World
                        wait(1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("DressrosaQuestProgress","Detective")
                        EquipWeapon("Key")
                        local pos2 = CFrame.new(1347.7124, 37.3751602, -1325.6488)
                        repeat wait() getgenv().ToTarget(pos2) until (pos2.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3 or not _G.Auto_New_World
                        wait(3)
                    elseif game.Workspace.Map.Ice.Door.CanCollide == false and game.Workspace.Map.Ice.Door.Transparency == 1 then
                        if game:GetService("Workspace").Enemies:FindFirstChild("Ice Admiral [Lv. 700] [Boss]") then
                            for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if string.find(_v.Name,"Ice Admiral [Lv. 700] [Boss]") and _v.Humanoid.Health > 0 then
                                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                        if string.find(v.Name,"Ice Admiral [Lv. 700] [Boss]") and v.Humanoid.Health > 0 then
                                            repeat wait()
                                                AutoHaki()
                                                EquipWeapon(_G.Select_Weapon)
                                                v.HumanoidRootPart.CanCollide = false
                                                v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                v.HumanoidRootPart.Transparency = 1
                                                getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
                                            until v.Humanoid.Health <= 0 or not v.Parent or not _G.Auto_New_World
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                                        end
                                    end
                                end
                            end
                        else
                            getgenv().ToTarget(CFrame.new(1347.7124, 37.3751602, -1325.6488))
                        end
                    else
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                    end
                end
            end)
        end
    end
end)

Tab:CreateSection("Other Funcrion",true)

local Toggle = Tab:CreateToggle({
    Name = "Auto Saber",
    Info = {
        Title = 'Auto Saber',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "Auto_Saber", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Saber = Value
        StopTween(_G.Auto_Saber)
    end,
})

task.spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Saber and game.Players.LocalPlayer.Data.Level.Value >= 200 and not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Saber") and not game.Players.LocalPlayer.Character:FindFirstChild("Saber") then
                _G.Auto_Farm_Level = false
                if game:GetService("Workspace").Map.Jungle.Final.Part.Transparency == 0 then
                    if game:GetService("Workspace").Map.Jungle.QuestPlates.Door.Transparency == 0 then
                        if (CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 100 then
                            getgenv().ToTarget(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame)
                            wait(1)
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate1.Button.CFrame
                            wait(1)
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate2.Button.CFrame
                            wait(1)
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate3.Button.CFrame
                            wait(1)
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate4.Button.CFrame
                            wait(1)
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Jungle.QuestPlates.Plate5.Button.CFrame
                            wait(1) 
                        else
                            if (CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
                                BTP(CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279))
                                return
                            end
                            getgenv().ToTarget(CFrame.new(-1612.55884, 36.9774132, 148.719543, 0.37091279, 3.0717151e-09, -0.928667724, 3.97099491e-08, 1, 1.91679348e-08, 0.928667724, -4.39869794e-08, 0.37091279))
                        end
                    else
                        if game:GetService("Workspace").Map.Desert.Burn.Part.Transparency == 0 then
                            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Torch") or game.Players.LocalPlayer.Character:FindFirstChild("Torch") then
                                EquipWeapon("Torch")
                                getgenv().ToTarget(CFrame.new(1114.61475, 5.04679728, 4350.22803, -0.648466587, -1.28799094e-09, 0.761243105, -5.70652914e-10, 1, 1.20584542e-09, -0.761243105, 3.47544882e-10, -0.648466587))
                            else
                                getgenv().ToTarget(CFrame.new(-1610.00757, 11.5049858, 164.001587, 0.984807551, -0.167722285, -0.0449818149, 0.17364943, 0.951244235, 0.254912198, 3.42372805e-05, -0.258850515, 0.965917408))                 
                            end
                        else
                            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") ~= 0 then
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","GetCup")
                                wait(0.5)
                                EquipWeapon("Cup")
                                wait(0.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","FillCup",game:GetService("Players").LocalPlayer.Character.Cup)
                                wait(0)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","SickMan") 
                            else
                                if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == nil then
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                                elseif  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 0 then
                                    if game:GetService("Workspace").Enemies:FindFirstChild("Mob Leader") or game:GetService("ReplicatedStorage"):FindFirstChild("Mob Leader") then
                                        getgenv().ToTarget(CFrame.new(-2967.59521, -4.91089821, 5328.70703, 0.342208564, -0.0227849055, 0.939347804, 0.0251603816, 0.999569714, 0.0150796166, -0.939287126, 0.0184739735, 0.342634559))
                                        for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if string.find(_v.Name,"Mob Leader") then
                                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                                    if string.find(v.Name,"Mob Leader") then
                                                        repeat wait()
                                                            StartMagnet = true
                                                            AutoHaki()
                                                            EquipWeapon(_G.Select_Weapon)
                                                            getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
                                                            PosMon = v.HumanoidRootPart.CFrame
                                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                            v.Humanoid.JumpPower = 0
                                                            v.Humanoid.WalkSpeed = 0
                                                            v.HumanoidRootPart.CanCollide = false
                                                            v.Humanoid:ChangeState(11)
                                                        until v.Humanoid.Health <= 0 or _G.Auto_Saber == false
                                                    end
                                                end
                                            end
                                        end
                                    end
                                elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon") == 1 then
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","RichSon")
                                    wait(0.5)
                                    EquipWeapon("Relic")
                                    wait(0.5)
                                    getgenv().ToTarget(CFrame.new(-1404.91504, 29.9773273, 3.80598116, 0.876514494, 5.66906877e-09, 0.481375456, 2.53851997e-08, 1, -5.79995607e-08, -0.481375456, 6.30572643e-08, 0.876514494))
                                end
                            end
                        end
                    end
                else
                    if game:GetService("Workspace").Enemies:FindFirstChild("Saber Expert") or game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert") then
                        getgenv().ToTarget(CFrame.new(-1401.85046, 29.9773273, 8.81916237, 0.85820812, 8.76083845e-08, 0.513301849, -8.55007443e-08, 1, -2.77243419e-08, -0.513301849, -2.00944328e-08, 0.85820812))
                        for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if string.find(_v.Name,"Saber Expert") then
                                for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                    if string.find(v.Name,"Saber Expert") then
                                        repeat wait()
                                            StartMagnet = true
                                            AutoHaki()
                                            EquipWeapon(_G.Select_Weapon)
                                            getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
                                            PosMon = v.HumanoidRootPart.CFrame
                                            v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                            v.Humanoid.JumpPower = 0
                                            v.Humanoid.WalkSpeed = 0
                                            v.HumanoidRootPart.CanCollide = false
                                            v.Humanoid:ChangeState(11)
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                                        until v.Humanoid.Health <= 0 or _G.Auto_Saber == false
                                        if v.Humanoid.Health <= 0 then
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ProQuestProgress","PlaceRelic")
                                        end
                                        _G.Auto_Farm_Level  = true
                                    end
                                end
                            end
                        end
                    end
                end
            end
        end)
    end
end)


local Toggle = Tab:CreateToggle({
    Name = "Auto Pole",
    Info = {
        Title = 'Auto Pole',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "Auto_Pole", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Pole = Value
        StopTween(_G.Auto_Pole)
    end,
})

task.spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Pole then
                if game.ReplicatedStorage:FindFirstChild("Thunder God") or game.Workspace.Enemies:FindFirstChild("Thunder God") then
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if string.find(v.Name,"Thunder God") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                            repeat wait()
                                StartMagnet = true
                                AutoHaki()
                                EquipWeapon(_G.Select_Weapon)
                                getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
                                PosMon = v.HumanoidRootPart.CFrame
                                v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                v.Humanoid.JumpPower = 0
                                v.Humanoid.WalkSpeed = 0
                                v.HumanoidRootPart.CanCollide = false
                                v.Humanoid:ChangeState(11)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetSpawnPoint")
                            until not _G.Auto_Pole or v.Humanoid.Health <= 0 or not v.Parent
                            StartMagnet = false
                        end
                    end
                else
                    Questtween = getgenv().ToTarget(CFrame.new(-7900.66406, 5606.90918, -2267.46436).Position,CFrame.new(-7900.66406, 5606.90918, -2267.46436))
                    if (CFrame.new(-7900.66406, 5606.90918, -2267.46436).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                        if Questtween then
                            Questtween:Stop()
                        end
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-7900.66406, 5606.90918, -2267.46436)
                    end
                end
            end
        end)
    end
end)

local Toggle = Tab:CreateToggle({
    Name = "Auto Buy Ablility",
    Info = {
        Title = 'Auto Buy Ablility',
        Image = '12735851647',
        Description = 'ไปโลกใหม่',
    },
    CurrentValue = false,
    Flag = "Auto_Buy_Ablility", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
    Callback = function(Value)
        _G.Auto_Buy_Ablility = Value
        StopTween(_G.Auto_Buy_Ablility)
    end,
})

task.spawn(function()
    while wait() do
        pcall(function()
            if _G.Auto_Buy_Ablility then
                local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
                local BusoCheck = false
                local SoruCheck = false
                local GeppoCheck = false
                local KenCheck = false
                if Beli >= 885000 then
                    repeat wait() 
                        local args = {
                            [1] = "BuyHaki",
                            [2] = "Buso"
                        }

                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        BusoCheck = true
                        local args = {
                            [1] = "BuyHaki",
                            [2] = "Geppo"
                        }
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        GeppoCheck = true
                        local args = {
                            [1] = "BuyHaki",
                            [2] = "Soru"
                        }
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        SoruCheck = true
                        local args = {
                            [1] = "KenTalk",
                            [2] = "Start"
                        }

                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))

                        local args = {
                            [1] = "KenTalk",
                            [2] = "Buy"
                        }

                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                        KenCheck = true
                    until not BusoCheck and not GeppoCheck and not SoruCheck and not KenCheck or not _G.Auto_Buy_Ablility
                end
            end
        end)
    end
end)

elseif World2 then

    Tab:CreateSection("World",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Third World",
        Info = {
            Title = 'Auto Third World',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Third_World", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Third_World = Value
            StopTween(_G.Auto_Third_World)
        end,
    })

    task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Third_World then
					if game.Players.LocalPlayer.Data.Level.Value >= 1500 then
						if Auto_Farm_Level then
							_G.Auto_Farm_Level = false
						end
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 3 then
							if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess ~= nil then
								Com("F_","TravelZou")
								if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("ZQuestProgress", "Check") == 0 then
									if game.Workspace.Enemies:FindFirstChild("rip_indra") then 	
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if string.find(v.Name,"rip_indra") and v:FindFirstChild("Humanoid")and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
												repeat wait()
                                                    AutoHaki()
                                                    EquipWeapon(_G.Select_Weapon)
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                    v.Humanoid.JumpPower = 0
                                                    v.Humanoid.WalkSpeed = 0
                                                    v.HumanoidRootPart.CanCollide = false
                                                    v.Humanoid:ChangeState(11)
                                                    getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												until not _G.Auto_Third_World or not v.Parent or v.Humanoid.Health <= 0 
												wait(.5)
												Check = 2
												repeat wait() Com("F_","TravelZou") until Check == 1
											end
										end
									else
										Com("F_","ZQuestProgress","Check")
										Com("F_","ZQuestProgress","Begin")
									end
								elseif game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("ZQuestProgress", "Check") == 1 then
									Com("F_","TravelZou")
								else
									if game.Workspace.Enemies:FindFirstChild("Don Swan") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if string.find(v.Name,"Don Swan") and v:FindFirstChild("Humanoid")and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
												repeat wait()
                                                    AutoHaki()
                                                    EquipWeapon(_G.Select_Weapon)
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                    v.Humanoid.JumpPower = 0
                                                    v.Humanoid.WalkSpeed = 0
                                                    v.HumanoidRootPart.CanCollide = false
                                                    v.Humanoid:ChangeState(11)
                                                    getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												until not _G.Auto_Third_World or not v.Parent or v.Humanoid.Health <= 0 
											end
										end
									else
										if (CFrame.new(2288.802, 15.1870775, 863.034607).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
											BTP(CFrame.new(2288.802, 15.1870775, 863.034607))
											return
										end
										TweenDonSwanthireworld = getgenv().ToTarget(CFrame.new(2288.802, 15.1870775, 863.034607).Position,CFrame.new(2288.802, 15.1870775, 863.034607))
										if (CFrame.new(2288.802, 15.1870775, 863.034607).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
											if TweenDonSwanthireworld then
												TweenDonSwanthireworld:Stop()
												game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2288.802, 15.1870775, 863.034607)
											end
										end
									end
								end
							else
								if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess == nil then
									TabelDevilFruitStore = {}
									TabelDevilFruitOpen = {}

									for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryFruits")) do
										for i1,v1 in pairs(v) do
											if i1 == "Name" then 
												table.insert(TabelDevilFruitStore,v1)
											end
										end
									end

									for i,v in next,game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("GetFruits") do
										if v.Price >= 1000000 then  
											table.insert(TabelDevilFruitOpen,v.Name)
										end
									end

									for i,DevilFruitOpenDoor in pairs(TabelDevilFruitOpen) do
										for i1,DevilFruitStore in pairs(TabelDevilFruitStore) do
											if DevilFruitOpenDoor == DevilFruitStore and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess == nil then    
												if not game.Players.LocalPlayer.Backpack:FindFirstChild(DevilFruitStore) then   
													Com("F_","LoadFruit",DevilFruitStore)
												else
													Com("F_","TalkTrevor","1")
													Com("F_","TalkTrevor","2")
													Com("F_","TalkTrevor","3")
												end
											end
										end
									end

									Com("F_","TalkTrevor","1")
									Com("F_","TalkTrevor","2")
									Com("F_","TalkTrevor","3")	
								end
							end
						else
							if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
								if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
									if game.Workspace.Enemies:FindFirstChild("Swan Pirate") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if string.find(v.Name,"Swan Pirate") then
												pcall(function()
													repeat wait()
                                                        AutoHaki()
                                                        EquipWeapon(_G.Select_Weapon)
                                                        PosMon = v.HumanoidRootPart.CFrame
                                                        v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                        v.Humanoid.JumpPower = 0
                                                        v.Humanoid.WalkSpeed = 0
                                                        v.HumanoidRootPart.CanCollide = false
                                                        v.Humanoid:ChangeState(11)
                                                        getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
													until not v.Parent or v.Humanoid.Health <= 0 or _G.Auto_Third_World == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
													StartMagnet = false
												end)
											end
										end
									else
										if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
											BTP(CFrame.new(1057.92761, 137.614319, 1242.08069))
											return
										end
										Questtween = getgenv().ToTarget(CFrame.new(1057.92761, 137.614319, 1242.08069).Position,CFrame.new(1057.92761, 137.614319, 1242.08069))
										if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
											if Bartilotween then Bartilotween:Stop() end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1057.92761, 137.614319, 1242.08069)
										end
									end
								else
									Bartilotween = getgenv().ToTarget(CFrame.new(-456.28952, 73.0200958, 299.895966).Position,CFrame.new(-456.28952, 73.0200958, 299.895966))
									if ( CFrame.new(-456.28952, 73.0200958, 299.895966).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Bartilotween then Bartilotween:Stop() end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =  CFrame.new(-456.28952, 73.0200958, 299.895966)
										Com("F_","StartQuest","BartiloQuest",1)
									end
								end
							elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
								if game.Workspace.Enemies:FindFirstChild("Jeremy") then
									for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
										if string.find(v.Name,"Jeremy") then
											repeat wait()
                                                AutoHaki()
                                                EquipWeapon(_G.Select_Weapon)
                                                PosMon = v.HumanoidRootPart.CFrame
                                                v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                v.Humanoid.JumpPower = 0
                                                v.Humanoid.WalkSpeed = 0
                                                v.HumanoidRootPart.CanCollide = false
                                                v.Humanoid:ChangeState(11)
                                                getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
											until not v.Parent or v.Humanoid.Health <= 0 or _G.Auto_Third_World == false
										end
									end
								else
									if (CFrame.new(2099.88159, 448.931, 648.997375).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(CFrame.new(2099.88159, 448.931, 648.997375))
										return
									end
									Bartilotween = getgenv().ToTarget(CFrame.new(2099.88159, 448.931, 648.997375).Position,CFrame.new(2099.88159, 448.931, 648.997375))
									if (CFrame.new(2099.88159, 448.931, 648.997375).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Bartilotween then Bartilotween:Stop() end
										game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2099.88159, 448.931, 648.997375)
									end
								end
							elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
								if (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
									Bartilotween = getgenv().ToTarget(CFrame.new(-1836, 11, 1714).Position,CFrame.new(-1836, 11, 1714))
								elseif (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									if Bartilotween then Bartilotween:Stop() end
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1836, 11, 1714)
									wait(.5)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1850.49329, 13.1789551, 1750.89685)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.87305, 19.3777466, 1712.01807)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1803.94324, 16.5789185, 1750.89685)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.55835, 16.8604317, 1724.79541)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1869.54224, 15.987854, 1681.00659)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1800.0979, 16.4978027, 1684.52368)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1819.26343, 14.795166, 1717.90625)
									wait(.1)
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1813.51843, 14.8604736, 1724.79541)
								end
							end
						end
					end
				end
			end)
		end
	end)

    Tab:CreateSection("Rengoku",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Rengoku",
        Info = {
            Title = 'Auto Rengoku',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Rengoku", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Rengoku = Value
            StopTween(_G.Auto_Rengoku)
        end,
    })

    task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Rengoku then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or game.Players.LocalPlayer.Character:FindFirstChild("Hidden Key") then
						EquipWeapon("Hidden Key")
						getgenv().ToTarget(CFrame.new(6571.1201171875, 299.23028564453, -6967.841796875))
					elseif game.Workspace.Enemies:FindFirstChild("Snow Lurker") or game:GetService("Workspace").Enemies:FindFirstChild("Arctic Warrior") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if string.find(v.Name,"Snow Lurker") or string.find(v.Name,"Arctic Warrior") and v.Humanoid.Health > 0 then
								repeat wait()
									StartMagnet = true
									AutoHaki()
									EquipWeapon(_G.Select_Weapon)
									PosMon = v.HumanoidRootPart.CFrame
									v.HumanoidRootPart.Size = Vector3.new(60,60,60)
									v.Humanoid.JumpPower = 0
									v.Humanoid.WalkSpeed = 0
									v.HumanoidRootPart.CanCollide = false
									v.Humanoid:ChangeState(11)
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
								until game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or not _G.Auto_Rengoku or not v.Parent or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						StartMagnet = false
						getgenv().ToTarget(CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438))
					end
				else 
					if _G.Auto_Rengoku_Hop and not game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or not game.Workspace.Enemies:FindFirstChild("Snow Lurker [Lv. 1375]") then
						Hop()
					else
						if (CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438))
							return
						end
						getgenv().ToTarget(CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438))
					end
				end
			end)
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Rengoku Hop",
        Info = {
            Title = 'Auto Rengoku Hop',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Rengoku Hop", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Rengoku_Hop = Value
        end,
    })

    Tab:CreateSection("Dragon Trident",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Dragon Trident",
        Info = {
            Title = 'Auto Dragon Trident',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Dragon_Trident", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Dragon_Trident = Value
            StopTween(_G.Auto_Dragon_Trident)
        end,
    })

    
	spawn(function()
		while wait() do
			if _G.Auto_Dragon_Trident then
				pcall(function()
					if _G.Auto_Dragon_Trident and game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") or game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
						if game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if string.find(v.Name,"Tide Keeper [Lv. 1475] [Boss]") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
									repeat wait()
										EquipWeapon(_G.Select_Weapon)
										AutoHaki()
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until _G.Auto_Dragon_Trident or v.Humanoid.Health <= 0 or not v.Parent
								end
							end
						else
							if (CFrame.new(-3914.830322265625, 123.29389190673828, -11516.8642578125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-3914.830322265625, 123.29389190673828, -11516.8642578125))
								return
							end
							getgenv().ToTarget(CFrame.new(-3914.830322265625, 123.29389190673828, -11516.8642578125))
						end
					else
						if _G.Auto_Dragon_Trident_Hop and not game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							Hop()
						end
					end
				end)
			end
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Dragon Trident Hop",
        Info = {
            Title = 'Auto Dragon Trident Hop',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Dragon_Trident_Hop", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Dragon_Trident_Hop = Value
        end,
    })

    Tab:CreateSection("Dark Coat",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Dark Coat",
        Info = {
            Title = 'Auto Dark Coat',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Dark_Coat", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Dark_Coat = Value
            StopTween(_G.Auto_Dark_Coat)
        end,
    })

    
	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Dark_Coat then
					if game:GetService("Workspace").Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if string.find(v.Name,"Darkbeard [Lv. 1000] [Raid Boss]") or string.find(v.Name,"Darkbeard [Lv. 1000] [Raid Boss]") and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
								repeat wait()
									StartMagnet = true
									AutoHaki()
									EquipWeapon(_G.Select_Weapon)
									PosMon = v.HumanoidRootPart.CFrame
									v.HumanoidRootPart.Size = Vector3.new(60,60,60)
									v.Humanoid.JumpPower = 0
									v.Humanoid.WalkSpeed = 0
									v.HumanoidRootPart.CanCollide = false
									v.Humanoid:ChangeState(11)
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
								until _G.Auto_Dark_Coat == false or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						getgenv().ToTarget(CFrame.new(3677.08203125, 62.751937866211, -3144.8332519531))
					end
				else 
					if _G.Auto_Dark_Coat_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
						Hop()
					else
						if (CFrame.new(3677.08203125, 62.751937866211, -3144.8332519531).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(3677.08203125, 62.751937866211, -3144.8332519531))
							return
						end
						getgenv().ToTarget(CFrame.new(3677.08203125, 62.751937866211, -3144.8332519531))
					end
				end
			end)
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Dark Coat Hop",
        Info = {
            Title = 'Auto Dark Coat Hop',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Dark_Coat_Hop", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Dark_Coat_Hop = Value
        end,
    })

    Tab:CreateSection("Swan Glasses",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Swan Glasses",
        Info = {
            Title = 'Auto Swan Glasses',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Swan_Glasses", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Swan_Glasses = Value
            StopTween(_G.Auto_Swan_Glasses)
        end,
    })

    task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Swan_Glasses then
					if game:GetService("Workspace").Enemies:FindFirstChild("Don Swan") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if string.find(v.Name,"Don Swan") and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
								repeat wait()
									StartMagnet = true
									AutoHaki()
									EquipWeapon(_G.Select_Weapon)
									PosMon = v.HumanoidRootPart.CFrame
									v.HumanoidRootPart.Size = Vector3.new(60,60,60)
									v.Humanoid.JumpPower = 0
									v.Humanoid.WalkSpeed = 0
									v.HumanoidRootPart.CanCollide = false
									v.Humanoid:ChangeState(11)
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
								until not _G.Auto_Swan_Glasses or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						repeat wait()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(2284.912109375, 15.537666320801, 905.48291015625)) 
						until (CFrame.new(2284.912109375, 15.537666320801, 905.48291015625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 or not _G.Settings.Main["Auto Swan Glasses"]
					end
				else 
					if _G.Auto_Swan_Glasses_Hop and not game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or not game.Workspace.Enemies:FindFirstChild("Snow Lurker [Lv. 1375]") then
						Hop()
					else
						if (CFrame.new(2284.912109375, 15.537666320801, 905.48291015625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(2284.912109375, 15.537666320801, 905.48291015625))
							return
						end
						repeat wait()
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(2284.912109375, 15.537666320801, 905.48291015625)) 
						until (CFrame.new(2284.912109375, 15.537666320801, 905.48291015625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 or not _G.Settings.Main["Auto Swan Glasses"]
					end
				end
			end)
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Swan Glasses Hop",
        Info = {
            Title = 'Auto Swan Glasses Hop',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Swan_Glasses_Hop", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Swan_Glasses_Hop = Value
        end,
    })

    Tab:CreateSection("Other Function",true)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Bartilo Quest",
        Info = {
            Title = 'Auto Bartilo Quest',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Bartilo_Quest", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Bartilo_Quest = Value
            StopTween(_G.Auto_Bartilo_Quest)
        end,
    })

    
	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Bartilo_Quest then
					if game.Players.LocalPlayer.Data.Level.Value >= 850 then
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
							if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
								if game.Workspace.Enemies:FindFirstChild("Swan Pirate") then
									for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
										if string.find(v.Name,"Swan Pirate") then
											pcall(function()
												repeat wait()
                                                    AutoHaki()
                                                    EquipWeapon(_G.Select_Weapon)
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                                    v.Humanoid.JumpPower = 0
                                                    v.Humanoid.WalkSpeed = 0
                                                    v.HumanoidRootPart.CanCollide = false
                                                    v.Humanoid:ChangeState(11)
                                                    getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												until not v.Parent or v.Humanoid.Health <= 0 or _G.Auto_Bartilo_Quest == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
												StartMagnet = false
											end)
										end
									end
								else
									if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(CFrame.new(1057.92761, 137.614319, 1242.08069))
										return
									end
									Questtween = getgenv().ToTarget(CFrame.new(1057.92761, 137.614319, 1242.08069).Position,CFrame.new(1057.92761, 137.614319, 1242.08069))
									if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Questtween then
											Questtween:Stop()
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1057.92761, 137.614319, 1242.08069)
									end
								end
							else
								Bartilotween = getgenv().ToTarget(CFrame.new(-456.28952, 73.0200958, 299.895966).Position,CFrame.new(-456.28952, 73.0200958, 299.895966))
								if ( CFrame.new(-456.28952, 73.0200958, 299.895966).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									if Bartilotween then
										Bartilotween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =  CFrame.new(-456.28952, 73.0200958, 299.895966)
									local args = {
										[1] = "StartQuest",
										[2] = "BartiloQuest",
										[3] = 1
									}
									game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
								end
							end
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
						if game.Workspace.Enemies:FindFirstChild("Jeremy") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if string.find(v.Name,"Jeremy") then
									repeat wait()
                                        AutoHaki()
                                        EquipWeapon(_G.Select_Weapon)
                                        PosMon = v.HumanoidRootPart.CFrame
                                        v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        v.HumanoidRootPart.CanCollide = false
                                        v.Humanoid:ChangeState(11)
                                        getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until not v.Parent or v.Humanoid.Health <= 0 or _G.Auto_Bartilo_Quest == false
								end
							end
						else
							if (CFrame.new(2099.88159, 448.931, 648.997375).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(2099.88159, 448.931, 648.997375))
								return
							end
							Bartilotween = getgenv().ToTarget(CFrame.new(2099.88159, 448.931, 648.997375).Position,CFrame.new(2099.88159, 448.931, 648.997375))
							if (CFrame.new(2099.88159, 448.931, 648.997375).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if Bartilotween then
									Bartilotween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2099.88159, 448.931, 648.997375)
							end
						end
					elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
						if (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
							Bartilotween = getgenv().ToTarget(CFrame.new(-1836, 11, 1714).Position,CFrame.new(-1836, 11, 1714))
						elseif (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
							if Bartilotween then
								Bartilotween:Stop()
							end
							game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1836, 11, 1714)
							wait(.5)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1850.49329, 13.1789551, 1750.89685)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.87305, 19.3777466, 1712.01807)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1803.94324, 16.5789185, 1750.89685)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.55835, 16.8604317, 1724.79541)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1869.54224, 15.987854, 1681.00659)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1800.0979, 16.4978027, 1684.52368)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1819.26343, 14.795166, 1717.90625)
							wait(1)
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1813.51843, 14.8604736, 1724.79541)
						end
					end
				end
			end)
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Ectoplasm",
        Info = {
            Title = 'Auto Ectoplasm',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Ectoplasm", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Ectoplasm = Value
            StopTween(_G.Auto_Ectoplasm)
        end,
    })

    
	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Ectoplasm then
					if game:GetService("Workspace").Enemies:FindFirstChild("Ship Deckhand") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Engineer") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Steward") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Officer") or game:GetService("Workspace").Enemies:FindFirstChild("Arctic Warrior") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if string.find(v.Name,"Ship Deckhand") or string.find(v.Name,"Ship Engineer") or string.find(v.Name,"Ship Steward") or string.find(v.Name,"Ship Officer") or string.find(v.Name,"Arctic Warrior") then
								if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
									repeat wait()
										StartMagnet = true
										AutoHaki()
										EquipWeapon(_G.Select_Weapon)
										PosMon = v.HumanoidRootPart.CFrame
										v.HumanoidRootPart.Size = Vector3.new(60,60,60)
										v.Humanoid.JumpPower = 0
										v.Humanoid.WalkSpeed = 0
										v.HumanoidRootPart.CanCollide = false
										v.Humanoid:ChangeState(11)
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until not _G.Auto_Ectoplasm or not v.Parent or v.Humanoid.Health <= 0
									StartMagnet = false
								end
							end
						end
					else
						StartMagnet = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
					end
				end
			end)
		end
	end)


    local Toggle = Tab:CreateToggle({
        Name = "Auto Evo Race V2",
        Info = {
            Title = 'Auto Evo Race V2',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Evo_Race_V2", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Evo_Race_V2 = Value
            StopTween(_G.Auto_Evo_Race_V2)
        end,
    })

	spawn(function()
		pcall(function()
			while wait() do
				if  _G.Auto_Evo_Race_V2 then
					if not game:GetService("Players").LocalPlayer.Data.Race:FindFirstChild("Evolved") then
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") == 0 then
							getgenv().ToTarget(CFrame.new(-2779.83521, 72.9661407, -3574.02002, -0.730484903, 6.39014104e-08, -0.68292886, 3.59963224e-08, 1, 5.50667032e-08, 0.68292886, 1.56424669e-08, -0.730484903))
							if (Vector3.new(-2779.83521, 72.9661407, -3574.02002) - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 then
								wait(1.3)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","2")
							end
						elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") == 1 then
							pcall(function()
								if not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flower 1") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flower 1") then
									getgenv().ToTarget(game:GetService("Workspace").Flower1.CFrame)
								elseif not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flower 2") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flower 2") then
									getgenv().ToTarget(game:GetService("Workspace").Flower2.CFrame)
								elseif not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flower 3") and not game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flower 3") then
									if game:GetService("Workspace").Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
										for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
											if v.Name == "Swan Pirate [Lv. 775]" then
												repeat wait()
													AutoHaki()
													EquipWeapon(_G.Select_Weapon)
													getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
													v.HumanoidRootPart.CanCollide = false
													v.HumanoidRootPart.Size = Vector3.new(50,50,50)
													PosMonEvo = v.HumanoidRootPart.CFrame
													StartEvoMagnet = true
												until game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flower 3") or not v.Parent or v.Humanoid.Health <= 0 or _G.Auto_Evo_Race_V2 == false
												StartEvoMagnet = false
											end
										end
									else
										StartEvoMagnet = false
										getgenv().ToTarget(CFrame.new(980.0985107421875, 121.331298828125, 1287.2093505859375))
									end
								end
							end)
						elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","1") == 2 then
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
						end
					end
				end
			end
		end)
	end)


    local Toggle = Tab:CreateToggle({
        Name = "Auto True Triple Katana",
        Info = {
            Title = 'Auto True Triple Katana',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_True_Triple_Katana", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_True_Triple_Katana = Value
        end,
    })

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_True_Triple_Katana then
					local string_1 = "MysteriousMan";
					local string_2 = "2";
					local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
					Target:InvokeServer(string_1, string_2);  
				end
			end)
		end
	end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Buy Legendary Sword",
        Info = {
            Title = 'Auto Buy Legendary Sword',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Buy_Legendary_Sword", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Buy_Legendary_Sword = Value
        end,
    })

    task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Buy_Legendary_Sword then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LegendarySwordDealer","1")
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LegendarySwordDealer","2")
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LegendarySwordDealer","3")
				end
			end)
		end
    end)

    local Toggle = Tab:CreateToggle({
        Name = "Auto Buy Enchanment Haki",
        Info = {
            Title = 'Auto Buy Enchanment Haki',
            Image = '12735851647',
            Description = 'ไปโลกใหม่',
        },
        CurrentValue = false,
        Flag = "Auto_Buy_Enchanment_Haki", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            _G.Auto_Buy_Enchanment_Haki = Value
        end,
    })

    task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Buy_Enchanment_Haki then
					local args = {
						[1] = "ColorsDealer",
						[2] = "2"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
			end)
		end
	end)

end

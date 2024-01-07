function Hop()
	local PlaceID = game.PlaceId
	local AllIDs = {}
	local foundAnything = ""
	local actualHour = os.date("!*t").hour
	local Deleted = false
	function TPReturner()
		local Site;
		if foundAnything == "" then
			Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
		else
			Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
		end
		local ID = ""
		if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
			foundAnything = Site.nextPageCursor
		end
		local num = 0;
		for i,v in pairs(Site.data) do
			local Possible = true
			ID = tostring(v.id)
			if tonumber(v.maxPlayers) > tonumber(v.playing) then
				for _,Existing in pairs(AllIDs) do
					if num ~= 0 then
						if ID == tostring(Existing) then
							Possible = false
						end
					else
						if tonumber(actualHour) ~= tonumber(Existing) then
							local delFile = pcall(function()
								AllIDs = {}
								table.insert(AllIDs, actualHour)
							end)
						end
					end
					num = num + 1
				end
				if Possible == true then
					table.insert(AllIDs, ID)
					wait()
					pcall(function()
						wait()
						game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
					end)
					wait(4)
				end
			end
		end
	end
	function Teleport() 
		while wait() do
			pcall(function()
				TPReturner()
				if foundAnything ~= "" then
					TPReturner()
				end
			end)
		end
	end
	local Hello = instance.new("Messange",workspace)
	Hello.Text = "Attack Hub Teleporting..."
	wait(.53)
	Teleport()
end
function TP(Pos)
	Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
	if _G.bypt and Distance > 1200 then
		tween:Cancel()
		wait(.1)
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(111111,111111,111111)
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
		game.Players.LocalPlayer.Character.Head:Destroy()
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
		local args = {
			[1] = "SetSpawnPoint"
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		
		wait()
		local args = {
			[1] = "SetSpawnPoint"
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait(0.1)
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
		local args = {
			[1] = "SetSpawnPoint"
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(111111,111111,111111)
		wait()
		game.Players.LocalPlayer.Character.Head:Destroy()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
		wait()
		local args = {
			[1] = "SetLastSpawnPoint",
			[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
		local args = {
			[1] = "SetSpawnPoint"
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(99999999,99999999,99999999)
		wait()
		local args = {
			[1] = "SetLastSpawnPoint",
			[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		local args = {
			[1] = "SetLastSpawnPoint",
			[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait(0.5)
		local args = {
			[1] = "SetLastSpawnPoint",
			[2] = tostring(game:GetService("Players").LocalPlayer.Data.SpawnPoint.Value)
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		wait()
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
		game.Players.LocalPlayer.Character.Head:Destroy()
		wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
		wait()
	else
    Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
    pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/190, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
	pcall(function()
    tween:Play()
	end)
    if Distance <= 250 then
        tween:Cancel()
        task.wait(0.3)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
    end
end
end
function EquipTools(Hello)
	pcall(function()
		if game.Players.LocalPlayer.Backpack:FindFirstChild(Hello) then 
			local Found = game.Players.LocalPlayer.Backpack:FindFirstChild(Hello) 
			game.Players.LocalPlayer.Character.Humanoid:EquipTool(Found) 
		end
	end)
end

function UnEquipTool(Tool)
    pcall(function()
    game.Players.LocalPlayer.Character.Humanoid:UnequipTools(game.Players.LocalPlayer.Backpack[Tool])
    end)
end

Buso = function()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
end

do
    local pussy = workspace:FindFirstChild("Hee")
    if pussy then
        pussy:Destroy()
    end
end

local helloguy = Instance.new("Part",workspace)
helloguy.Size = Vector3.new(30,5,30)
helloguy.Name = "Hee"
helloguy.Transparency = 1
helloguy.CanCollide = true
helloguy.Anchored = true

spawn(function()
    pcall(function()
        while task.wait() do
            if _G.AutoFarm or _G.AutoFarmBone or _G.AutoHallowEssence  or _G.AutoChest or _G.FarmQuestBoss or _G.FarmBoss or _G.FarmAllBoss or _G.AutoFarmCakePrince or _G.EliteHunter or _G.Start_Tween_Island or _G.Tweenfruit or _G.AutoFarmDungeon or _G.NextIsland or  _G.Awakening or _G.Auto_Complete_Trial or _G.AutoGhostShip then
                helloguy.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,-5,0)
            end
        end
    end)
end)

spawn(function()
	pcall(function()
		while wait() do
			if _G.AutoFarm or _G.AutoFarmBone or _G.AutoHallowEssence  or _G.AutoChest or _G.FarmQuestBoss or _G.FarmBoss or _G.FarmAllBoss or _G.AutoFarmCakePrince or _G.EliteHunter or _G.Start_Tween_Island or _G.Tweenfruit or _G.AutoFarmDungeon or _G.NextIsland or  _G.Awakening or _G.Auto_Complete_Trial or _G.AutoGhostShip then
				if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
					local Noclip = Instance.new("BodyVelocity")
					Noclip.Name = "BodyClip"
					Noclip.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
					Noclip.MaxForce = Vector3.new(100000,100000,100000)
					Noclip.Velocity = Vector3.new(0,0,0)
				end
            else
                if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
                end
			end
		end
	end)
end)

spawn(function()
    while game:GetService("RunService").Stepped:wait() do
		pcall(function()
        	if _G.AutoFarm or _G.AutoFarmBone or _G.AutoHallowEssence or _G.AutoChest or _G.FarmQuestBoss or _G.FarmBoss or _G.FarmAllBoss or _G.AutoFarmCakePrince or _G.EliteHunter or _G.Start_Tween_Island or _G.Tweenfruit or _G.AutoFarmDungeon or _G.NextIsland or  _G.Awakening or _G.Auto_Complete_Trial or _G.AutoGhostShip then
				local character = game.Players.LocalPlayer.Character
				for _, v in pairs(character:GetChildren()) do
					if v:IsA("BasePart") then
						v.CanCollide = false
					end
				end
			end
        end)
    end
end)

function StopTween(target)
	if not target then
		tween:Cancel()
		if game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
			game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
		end
		wait(0.2)
	end
end

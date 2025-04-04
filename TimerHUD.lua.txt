local player = game:GetService("Players").LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local timeGui = Instance.new("ScreenGui")
timeGui.Name = "TimeHUD"
timeGui.Parent = playerGui
timeGui.Enabled = false

local timeFrame = Instance.new("Frame")
timeFrame.Parent = timeGui
timeFrame.Size = UDim2.new(0.15, 0, 0.08, 0)
timeFrame.Position = UDim2.new(0.85, 0, 0, 10)
timeFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
timeFrame.BackgroundTransparency = 0.8
timeFrame.Active = true
timeFrame.Draggable = true

local timeImage = Instance.new("ImageLabel")
timeImage.Parent = timeFrame
timeImage.Image = "rbxassetid://122624724590940"
timeImage.Size = UDim2.new(1, 0, 1, 0)
timeImage.BackgroundTransparency = 1
timeImage.ScaleType = Enum.ScaleType.Slice
timeImage.SliceCenter = Rect.new(70, 70, 530, 530)

local timeText = Instance.new("TextLabel")
timeText.Parent = timeImage
timeText.Text = "Time: 00:00"
timeText.Size = UDim2.new(0.9, 0, 0.8, 0)
timeText.Position = UDim2.new(0.05, 0, 0.1, 0)
timeText.BackgroundTransparency = 1
timeText.TextColor3 = Color3.new(1, 1, 1)
timeText.FontFace = Font.new("rbxasset://fonts/families/Sarpanch.json")
timeText.TextSize = 25

local timeLabel = game.Workspace.Train.TrainControls.TimeDial.SurfaceGui.TextLabel

local function updateTime()
    timeText.Text = timeLabel.Text
end

game:GetService("RunService").Heartbeat:Connect(function()
    if _G.TimeGui then
        updateTime()
    end
end)

_G.ResetTimeGui = function()
    timeFrame.Position = UDim2.new(0.85, 0, 0, 10)
end

game:GetService("RunService").RenderStepped:Connect(function()
    timeGui.Enabled = if _G.TimeGui ~= nil then _G.TimeGui else false
end)

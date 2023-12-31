
_G.Color = Color3.fromRGB(152, 84, 255)
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local UIS = game:GetService('UserInputService')
local frame = script.Parent
local dragToggle = nil
local dragSpeed = 0.25
local dragStart = nil
local startPos = nil

local function updateInput(input)
	local delta = input.Position - dragStart
	local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
		startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	game:GetService('TweenService'):Create(frame, TweenInfo.new(dragSpeed), {Position = position}):Play()
end

frame.InputBegan:Connect(function(input)
	if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then 
		dragToggle = true
		dragStart = input.Position
		startPos = frame.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragToggle = false
			end
		end)
	end
end)

UIS.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		if dragToggle then
			updateInput(input)
		end
	end
end)

--Properties:
local library = {}
function library:Window(img,text,img1,img2,text1,text2,text3)

	local ScreenGui = Instance.new("ScreenGui")
	ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	local Frame = Instance.new("Frame")
	Frame.Parent = ScreenGui
	Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
	Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame.BorderSizePixel = 0
	Frame.Position = UDim2.new(0.261163145, 0, 0.286057681, 0)
	Frame.Size = UDim2.new(0, 520, 0, 330)
	
	updateInput(Frame)

	local UICorner = Instance.new("UICorner")
	UICorner.CornerRadius = UDim.new(0, 5)
	UICorner.Parent = Frame

	local Frame_2 = Instance.new("Frame")
	Frame_2.Parent = Frame
	Frame_2.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	Frame_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame_2.BorderSizePixel = 0
	Frame_2.Position = UDim2.new(0.0188555196, 0, 0.0254516602, 0)
	Frame_2.Size = UDim2.new(0, 503, 0, 312)

	local UICorner_2 = Instance.new("UICorner")
	UICorner_2.CornerRadius = UDim.new(0, 5)
	UICorner_2.Parent = Frame_2

	local Frame_3 = Instance.new("Frame")
	Frame_3.Parent = Frame_2
	Frame_3.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	Frame_3.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame_3.BorderSizePixel = 0
	Frame_3.Position = UDim2.new(-0.0175766721, 0, -0.0290355198, 0)
	Frame_3.Size = UDim2.new(0, 520, 0, 42)

	local UICorner_3 = Instance.new("UICorner")
	UICorner_3.CornerRadius = UDim.new(0, 5)
	UICorner_3.Parent = Frame_3

	local Frame_4 = Instance.new("Frame")
	Frame_4.Parent = Frame_3
	Frame_4.BackgroundColor3 = _G.Color
	Frame_4.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame_4.BorderSizePixel = 0
	Frame_4.Position = UDim2.new(-0.000269024196, 0, 0.970964968, 0)
	Frame_4.Size = UDim2.new(0, 520, 0, 1)

	local UICorner_4 = Instance.new("UICorner")
	UICorner_4.CornerRadius = UDim.new(0, 5)
	UICorner_4.Parent = Frame_4

	local ImageLabel = Instance.new("ImageLabel")
	ImageLabel.Parent = Frame_3
	ImageLabel.BackgroundColor3 = Color3.fromRGB(31, 31, 31)
	ImageLabel.BackgroundTransparency = 1.000
	ImageLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ImageLabel.BorderSizePixel = 0
	ImageLabel.Position = UDim2.new(0.0164928138, 0, -0.118440174, 0)
	ImageLabel.Size = UDim2.new(0, 50, 0, 50)
	ImageLabel.Image = img

	local UICorner_5 = Instance.new("UICorner")
	UICorner_5.CornerRadius = UDim.new(0, 5)
	UICorner_5.Parent = ImageLabel

	local TextLabel = Instance.new("TextLabel")
	TextLabel.Parent = Frame_3
	TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.BackgroundTransparency = 1.000
	TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel.BorderSizePixel = 0
	TextLabel.Position = UDim2.new(0.161538467, 0, -0.095238097, 0)
	TextLabel.Size = UDim2.new(0, 200, 0, 50)
	TextLabel.Font = Enum.Font.GothamSemibold
	TextLabel.Text = text
	TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.TextSize = 19.000

	local Frame_5 = Instance.new("Frame")
	Frame_5.Parent = Frame_2
	Frame_5.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	Frame_5.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame_5.BorderSizePixel = 0
	Frame_5.Position = UDim2.new(0.0213424042, 0, 0.150641024, 0)
	Frame_5.Size = UDim2.new(0, 482, 0, 250)

	local ImageLabel_2 = Instance.new("ImageLabel")
	ImageLabel_2.Parent = Frame_5
	ImageLabel_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ImageLabel_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ImageLabel_2.BorderSizePixel = 0
	ImageLabel_2.Position = UDim2.new(0.031120332, 0, 0.508000016, 0)
	ImageLabel_2.Size = UDim2.new(0, 213, 0, 108)
	ImageLabel_2.Image = img1

	local UICorner_6 = Instance.new("UICorner")
	UICorner_6.Parent = ImageLabel_2

	local ImageLabel_3 = Instance.new("ImageLabel")
	ImageLabel_3.Parent = Frame_5
	ImageLabel_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ImageLabel_3.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ImageLabel_3.BorderSizePixel = 0
	ImageLabel_3.Position = UDim2.new(0.514522851, 0, 0.0359999985, 0)
	ImageLabel_3.Size = UDim2.new(0, 224, 0, 118)
	ImageLabel_3.Image = img2

	local UICorner_7 = Instance.new("UICorner")
	UICorner_7.Parent = ImageLabel_3
	
	-------------------------------------------------------
	
	local TextButton = Instance.new("TextButton")
	TextButton.Parent = Frame_5
	TextButton.BackgroundColor3 = _G.Color
	TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextButton.BorderSizePixel = 0
	TextButton.Position = UDim2.new(0.514522851, 0, 0.768000007, 0)
	TextButton.Size = UDim2.new(0, 224, 0, 42)
	TextButton.Font = Enum.Font.GothamSemibold
	TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
	TextButton.TextSize = 14.000

	local UICorner_8 = Instance.new("UICorner")
	UICorner_8.CornerRadius = UDim.new(0, 5)
	UICorner_8.Parent = TextButton
	

	local ButtonFrame = Instance.new("Frame")

	ButtonFrame.Name = "ButtonFrame"
	ButtonFrame.Parent = Frame_5
	ButtonFrame.BackgroundColor3 = _G.Color
	ButtonFrame.BorderSizePixel = 0
	ButtonFrame.Position = UDim2.new(0.514522851, 0, 0.768000007, 0)
	ButtonFrame.AnchorPoint = Vector2.new(0.5, 0.5)
	ButtonFrame.Size = UDim2.new(0, 224, 0, 42) -- UDim2.new(0, 213, 0, 35)
	ButtonFrame.BackgroundTransparency  = 1
	ButtonFrame.ClipsDescendants = true

	local MheeFrameStroke = Instance.new("UIStroke")

	MheeFrameStroke.Thickness = 0
	MheeFrameStroke.Name = ""
	MheeFrameStroke.Parent = ButtonFrame
	MheeFrameStroke.LineJoinMode = Enum.LineJoinMode.Round
	MheeFrameStroke.Color = _G.Color
	MheeFrameStroke.Transparency = 0.7

	local Button = Instance.new("TextButton")

	Button.Parent = ButtonFrame
	Button.Name = "Button"
	Button.BackgroundColor3 = _G.Color
	Button.Size = UDim2.new(0,150, 0, 30)
	Button.Font = Enum.Font.GothamSemibold
	Button.Text = tostring(text)
	Button.TextColor3 = Color3.fromRGB(155, 155, 155)
	Button.TextSize = 13.000
	Button.AnchorPoint = Vector2.new(0.5, 0.5)
	Button.Position = UDim2.new(0.514522851, 0, 0.768000007, 0)
	Button.TextXAlignment = Enum.TextXAlignment.Center
	Button.BackgroundTransparency = 0.6
	Button.TextWrapped = true
	Button.AutoButtonColor = false
	Button.ClipsDescendants = true

	local ConnerPageMhee = Instance.new("UICorner")

	ConnerPageMhee.CornerRadius = UDim.new(0, 4)
	ConnerPageMhee.Name = ""
	ConnerPageMhee.Parent = Button

	Button.MouseEnter:Connect(function()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{Size =  UDim2.new(0, 170, 0, 25)} -- UDim2.new(0, 128, 0, 25)
		):Play()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{BackgroundTransparency = 0} -- UDim2.new(0, 128, 0, 25)
		):Play()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{TextColor3 = Color3.fromRGB(255, 255, 255)} -- UDim2.new(0, 128, 0, 25)
		):Play()
	end
	)
	Button.MouseLeave:Connect(function()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{Size =  UDim2.new(0, 150, 0, 25)} -- UDim2.new(0, 128, 0, 25)
		):Play()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{BackgroundTransparency = 0.6} -- UDim2.new(0, 128, 0, 25)
		):Play()
		TweenService:Create(
			Button,
			TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
			{TextColor3 = Color3.fromRGB(155, 155, 155)} -- UDim2.new(0, 128, 0, 25)
		):Play()
	end
	)

	Button.MouseButton1Click:Connect(function()
		CircleClick(Button, Mouse.X, Mouse.Y)
		Button.TextSize = 0
		TweenService:Create(
			Button,
			TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
			{TextSize = 12}
		):Play()
		callback()
	end)
	
	local TextLabel_2 = Instance.new("TextLabel")
	TextLabel_2.Parent = Frame_5
	TextLabel_2.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	TextLabel_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_2.BorderSizePixel = 0
	TextLabel_2.Position = UDim2.new(0.031120332, 0, 0.0359999985, 0)
	TextLabel_2.Size = UDim2.new(0, 213, 0, 50)
	TextLabel_2.Font = Enum.Font.GothamSemibold
	TextLabel_2.TextColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_2.TextSize = 14.000
	TextLabel_2.Text = text1

	local TextLabel_3 = Instance.new("TextLabel")
	TextLabel_3.Parent = Frame_5
	TextLabel_3.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	TextLabel_3.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_3.BorderSizePixel = 0
	TextLabel_3.Position = UDim2.new(0.031120332, 0, 0.263999999, 0)
	TextLabel_3.Size = UDim2.new(0, 213, 0, 50)
	TextLabel_3.Font = Enum.Font.GothamSemibold
	TextLabel_3.TextColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_3.TextSize = 14.000
	TextLabel_3.Text = text2

	local TextLabel_4 = Instance.new("TextLabel")
	TextLabel_4.Parent = Frame_5
	TextLabel_4.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	TextLabel_4.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_4.BorderSizePixel = 0
	TextLabel_4.Position = UDim2.new(0.514522851, 0, 0.532000005, 0)
	TextLabel_4.Size = UDim2.new(0, 224, 0, 50)
	TextLabel_4.Font = Enum.Font.GothamSemibold
	TextLabel_4.TextColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel_4.TextSize = 14.000
	TextLabel_4.Text = text3
end

local Mlibrary = library:Window("http://www.roblox.com/asset/?id=15817612086","Manake Hub Projects - Blox Fruit","http://www.roblox.com/asset/?id=15817612086","http://www.roblox.com/asset/?id=15817612086","OK","OK","OK")


local DisplayButton = game:GetService("Players").LocalPlayer.PlayerGui.Main.Settings.DisplayButton
local SettingsButton = game:GetService("Players").LocalPlayer.PlayerGui.Main.Settings

DisplayButton.TextLabel.Text = "Manake Hub"
DisplayButton.Notify.Text = "Enable or Disable UI script"
DisplayButton.Visible = false
Toggle = true

SettingsButton.MouseButton1Click:Connect(function()
	if Toggle then
		Toggle = false
		DisplayButton.Visible = true
	else
		Toggle = true
		DisplayButton.Visible = false
	end
end)

if DisplayButton.Visible == true then
	DisplayButton.MouseButton1Click:Connect(function()
		game:GetService("VirtualInputManager"):SendKeyEvent(true,305,false,game)
		game:GetService("VirtualInputManager"):SendKeyEvent(false,305,false,game)
	end)
end

repeat wait(1) until game:IsLoaded()

do
	local ui = game.CoreGui:FindFirstChild("ManakeUiLib")
	if ui then
		ui:Destroy()
	end
end

local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local LocalPlayer = game:GetService("Players").LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local tween = game:GetService("TweenService")
local Red = {RainbowColorValue = 0, HueSelectionPosition = 0}
local LogoButton = [[7040391851]]


local function Tween(instance, properties,style,wa)
	if style == nil or "" then
		return Back
	end
	tween:Create(instance,TweenInfo.new(wa,Enum.EasingStyle[style]),{properties}):Play()
end

local ActualTypes = {
	RoundFrame = "ImageLabel",
	Shadow = "ImageLabel",
	Circle = "ImageLabel",
	CircleButton = "ImageButton",
	Frame = "Frame",
	Label = "TextLabel",
	Button = "TextButton",
	SmoothButton = "ImageButton",
	Box = "TextBox",
	ScrollingFrame = "ScrollingFrame",
	Menu = "ImageButton",
	NavBar = "ImageButton"
}

local Properties = {
	RoundFrame = {
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554237731",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(3,3,297,297)
	},
	SmoothButton = {
		AutoButtonColor = false,
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554237731",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(3,3,297,297)
	},
	Shadow = {
		Name = "Shadow",
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554236805",
		ScaleType = Enum.ScaleType.Slice,
		SliceCenter = Rect.new(23,23,277,277),
		Size = UDim2.fromScale(1,1) + UDim2.fromOffset(30,30),
		Position = UDim2.fromOffset(-15,-15)
	},
	Circle = {
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5554831670"
	},
	CircleButton = {
		BackgroundTransparency = 1,
		AutoButtonColor = false,
		Image = "http://www.roblox.com/asset/?id=5554831670"
	},
	Frame = {
		BackgroundTransparency = 1,
		BorderSizePixel = 0,
		Size = UDim2.fromScale(1,1)
	},
	Label = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	Button = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	Box = {
		BackgroundTransparency = 1,
		Position = UDim2.fromOffset(5,0),
		Size = UDim2.fromScale(1,1) - UDim2.fromOffset(5,0),
		TextSize = 14,
		TextXAlignment = Enum.TextXAlignment.Left
	},
	ScrollingFrame = {
		BackgroundTransparency = 1,
		ScrollBarThickness = 0,
		CanvasSize = UDim2.fromScale(0,0),
		Size = UDim2.fromScale(1,1)
	},
	Menu = {
		Name = "More",
		AutoButtonColor = false,
		BackgroundTransparency = 1,
		Image = "http://www.roblox.com/asset/?id=5555108481",
		Size = UDim2.fromOffset(20,20),
		Position = UDim2.fromScale(1,0.5) - UDim2.fromOffset(25,10)
	},
	NavBar = {
		Name = "SheetToggle",
		Image = "http://www.roblox.com/asset/?id=5576439039",
		BackgroundTransparency = 1,
		Size = UDim2.fromOffset(20,20),
		Position = UDim2.fromOffset(5,5),
		AutoButtonColor = false
	}
}

local Types = {
	"RoundFrame",
	"Shadow",
	"Circle",
	"CircleButton",
	"Frame",
	"Label",
	"Button",
	"SmoothButton",
	"Box",
	"ScrollingFrame",
	"Menu",
	"NavBar"
}

function FindType(String)
	for _, Type in next, Types do
		if Type:sub(1, #String):lower() == String:lower() then
			return Type
		end
	end
	return false
end

local Objects = {}

function Objects.new(Type)
	local TargetType = FindType(Type)
	if TargetType then
		local NewImage = Instance.new(ActualTypes[TargetType])
		if Properties[TargetType] then
			for Property, Value in next, Properties[TargetType] do
				NewImage[Property] = Value
			end
		end
		return NewImage
	else
		return Instance.new(Type)
	end
end

local function GetXY(GuiObject)
	local Max, May = GuiObject.AbsoluteSize.X, GuiObject.AbsoluteSize.Y
	local Px, Py = math.clamp(Mouse.X - GuiObject.AbsolutePosition.X, 0, Max), math.clamp(Mouse.Y - GuiObject.AbsolutePosition.Y, 0, May)
	return Px/Max, Py/May
end

local function CircleAnim(GuiObject, EndColour, StartColour)
	local PX, PY = GetXY(GuiObject)
	local Circle = Objects.new("Circle")
	Circle.Size = UDim2.fromScale(0,0)
	Circle.Position = UDim2.fromScale(PX,PY)
	Circle.ImageColor3 = StartColour or GuiObject.ImageColor3
	Circle.ZIndex = 200
	Circle.Parent = GuiObject
	local Size = GuiObject.AbsoluteSize.X
	TweenService:Create(Circle, TweenInfo.new(0.5), {Position = UDim2.fromScale(PX,PY) - UDim2.fromOffset(Size/2,Size/2), ImageTransparency = 1, ImageColor3 = EndColour, Size = UDim2.fromOffset(Size,Size)}):Play()
	spawn(function()
		wait(0.5)
		Circle:Destroy()
	end)
end


local function MakeDraggable(topbarobject, object)
	local Dragging = nil
	local DragInput = nil
	local DragStart = nil
	local StartPosition = nil

	local function Update(input)
		local Delta = input.Position - DragStart
		local pos =
			UDim2.new(
				StartPosition.X.Scale,
				StartPosition.X.Offset + Delta.X,
				StartPosition.Y.Scale,
				StartPosition.Y.Offset + Delta.Y
			)
		local Tween = TweenService:Create(object, TweenInfo.new(0.2), {Position = pos})
		Tween:Play()
	end

	topbarobject.InputBegan:Connect(
		function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				Dragging = true
				DragStart = input.Position
				StartPosition = object.Position

				input.Changed:Connect(
					function()
						if input.UserInputState == Enum.UserInputState.End then
							Dragging = false
						end
					end
				)
			end
		end
	)

	topbarobject.InputChanged:Connect(
		function(input)
			if
				input.UserInputType == Enum.UserInputType.MouseMovement or
				input.UserInputType == Enum.UserInputType.Touch
			then
				DragInput = input
			end
		end
	)

	UserInputService.InputChanged:Connect(
		function(input)
			if input == DragInput and Dragging then
				Update(input)
			end
		end
	)
end

local library = {}

function library:Window(text,text2,text3,logo,keybind)
	local uihide = false
	local abc = false
	local logo = logo or 0
	local currentpage = ""
	local keybind = keybind or Enum.KeyCode.RightControl
	local yoo = string.gsub(tostring(keybind),"Enum.KeyCode.","")

	local ManakeUiLib = Instance.new("ScreenGui")
	ManakeUiLib.Name = "ManakeUiLib"
	ManakeUiLib.Parent = game.CoreGui
	ManakeUiLib.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	local Main = Instance.new("Frame")
	Main.Name = "Main"
	Main.Parent = ManakeUiLib
	Main.ClipsDescendants = true
	Main.AnchorPoint = Vector2.new(0.5,0.5)
	Main.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
	Main.Position = UDim2.new(0.5, 0, 0.5, 0)
	Main.Size = UDim2.new(0, 0, 0, 0)

	Main:TweenSize(UDim2.new(0, 656, 0, 300),"Out","Quad",0.4,true)

	local MCNR = Instance.new("UICorner")
	MCNR.Name = "MCNR"
	MCNR.Parent = Main


	local Top = Instance.new("Frame")
	Top.Name = "Top"
	Top.Parent = Main
	Top.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	Top.Size = UDim2.new(0, 656, 0, 27)

	local TCNR = Instance.new("UICorner")
	TCNR.Name = "TCNR"
	TCNR.Parent = Top

	local Logo = Instance.new("ImageLabel")
	Logo.Name = "Logo"
	Logo.Parent = Top
	Logo.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Logo.BackgroundTransparency = 1.000
	Logo.Position = UDim2.new(0, 10, 0, 1)
	Logo.Size = UDim2.new(0, 25, 0, 25)
	Logo.Image = "rbxassetid://"..tostring(logo)

	local Name = Instance.new("TextLabel")
	Name.Name = "Name"
	Name.Parent = Top
	Name.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Name.BackgroundTransparency = 1.000
	Name.Position = UDim2.new(0.0609756112, 0, 0, 0)
	Name.Size = UDim2.new(0, 61, 0, 27)
	Name.Font = Enum.Font.GothamSemibold
	Name.Text = text
	Name.TextColor3 = Color3.fromRGB(225, 225, 225)
	Name.TextSize = 17.000

	local Hub = Instance.new("TextLabel")
	Hub.Name = "Hub"
	Hub.Parent = Top
	Hub.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Hub.BackgroundTransparency = 1.000
	Hub.Position = UDim2.new(0, 110, 0, 0)
	Hub.Size = UDim2.new(0, 81, 0, 27)
	Hub.Font = Enum.Font.GothamSemibold
	Hub.Text = text2
	Hub.TextColor3 = _G.Color
	Hub.TextSize = 17.000
	Hub.TextXAlignment = Enum.TextXAlignment.Left

	local Ver = Instance.new("TextLabel")
	Ver.Name = "Ver"
	Ver.Parent = Top
	Ver.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Ver.BackgroundTransparency = 1.000
	Ver.Position = UDim2.new(0.847560000, 0, 0, 0)
	Ver.Size = UDim2.new(0, 100, 0, 27)
	Ver.Font = Enum.Font.GothamSemibold
	Ver.Text = text3
	Ver.TextColor3 = _G.Color
	Ver.TextSize = 15.000


	local BindButton = Instance.new("TextButton")
	BindButton.Name = "BindButton"
	BindButton.Parent = Top
	BindButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	BindButton.BackgroundTransparency = 1.000
	BindButton.Position = UDim2.new(0.227561002, 0, 0, 0)
	BindButton.Size = UDim2.new(0, 100, 0, 27)
	BindButton.Font = Enum.Font.GothamSemibold
	BindButton.Text = "        [ "..string.gsub(tostring(keybind),"Enum.KeyCode.","").." ]"
	BindButton.TextColor3 = Color3.fromRGB(100, 100, 100)
	BindButton.TextSize = 11.000

	BindButton.MouseButton1Click:Connect(function ()
		BindButton.Text = "         [ ... ]"
		local inputwait = game:GetService("UserInputService").InputBegan:wait()
		local shiba = inputwait.KeyCode == Enum.KeyCode.Unknown and inputwait.UserInputType or inputwait.KeyCode

		if shiba.Name ~= "Focus" and shiba.Name ~= "MouseMovement" then
			BindButton.Text = "         [ "..shiba.Name.." ]"
			yoo = shiba.Name
		end
	end)

	do  local ui =  game:GetService("CoreGui"):FindFirstChild("Manake")  if ui then ui:Destroy() end end


	local Luna = Instance.new("ScreenGui")
	local ToggleFrameUi = Instance.new("Frame")
	local UICorner = Instance.new("UICorner")
	local ToggleImgUi = Instance.new("ImageLabel")
	local Uitoggle = Instance.new("TextLabel")
	local Yedhee = Instance.new("TextLabel")
	local SearchStroke = Instance.new("UIStroke")


	Luna.Name = "Manake"
	Luna.Parent = game.CoreGui
	Luna.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	ToggleFrameUi.Name = "ToggleFrameUi"
	ToggleFrameUi.Parent = Luna
	ToggleFrameUi.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	ToggleFrameUi.Position = UDim2.new(0.883, 0,0.282, 0)
	ToggleFrameUi.Size = UDim2.new(0, 198, 0, 48)

	SearchStroke.Thickness = 1
	SearchStroke.Name = ""
	SearchStroke.Parent = ToggleFrameUi
	SearchStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	SearchStroke.LineJoinMode = Enum.LineJoinMode.Round
	SearchStroke.Color = _G.Color
	SearchStroke.Transparency = 0

	UICorner.CornerRadius = UDim.new(0, 4)
	UICorner.Parent = ToggleFrameUi

	ToggleImgUi.Name = "ToggleImgUi"
	ToggleImgUi.Parent = ToggleFrameUi
	ToggleImgUi.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ToggleImgUi.BackgroundTransparency = 1.000
	ToggleImgUi.Position = UDim2.new(0.0454545468, 0, 0.125000313, 0)
	ToggleImgUi.Size = UDim2.new(0, 35, 0, 35)
	ToggleImgUi.Image = "rbxassetid://12235359506"

	Uitoggle.Name = "Uitoggle"
	Uitoggle.Parent = ToggleFrameUi
	Uitoggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Uitoggle.BackgroundTransparency = 1.000
	Uitoggle.Position = UDim2.new(0.25757575, 0, 0, 0)
	Uitoggle.Size = UDim2.new(0, 137, 0, 25)
	Uitoggle.Font = Enum.Font.GothamSemibold
	Uitoggle.Text = "Ui Toggle :"
	Uitoggle.TextColor3 = Color3.fromRGB(255, 255, 255)
	Uitoggle.TextSize = 12.000

	Yedhee.Name = "Yedhee"
	Yedhee.Parent = ToggleFrameUi
	Yedhee.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Yedhee.BackgroundTransparency = 1.000
	Yedhee.Position = UDim2.new(0.25757575, 0, 0.479166657, 0)
	Yedhee.Size = UDim2.new(0, 137, 0, 25)
	Yedhee.Font = Enum.Font.GothamSemibold
	Yedhee.Text = "Lable"
	Yedhee.TextColor3 = Color3.fromRGB(255, 255, 255)
	Yedhee.TextSize = 12.000
	spawn(function()
		while wait() do
			Yedhee.Text = '['..yoo..']'
		end
	end)

	Yedhee.TextTransparency = 1
	Uitoggle.TextTransparency = 1
	ToggleImgUi.ImageTransparency = 1
	ToggleFrameUi.BackgroundTransparency = 1.000
	SearchStroke.Transparency = 1

	UserInputService.InputBegan:Connect(function(input)
		if input.KeyCode == Enum.KeyCode[yoo] then
			if uihide == false then
				ToggleFrameUi:TweenSize(UDim2.new(0, 198, 0, 48),"In","Quad",0.2,true)
				wait(.2)
				uihide = true
				Main:TweenSize(UDim2.new(0, 0, 0, 0),"In","Quad",0.4,true)
			else
				ToggleFrameUi:TweenSize(UDim2.new(0, 0, 0, 0),"In","Quad",0.2,true)
				wait(.2)
				uihide = false
				Main:TweenSize(UDim2.new(0, 656, 0, 300),"Out","Quad",0.4,true)
			end
		end
	end)

	MakeDraggable(ToggleFrameUi,ToggleFrameUi)





	local Tab = Instance.new("Frame")
	Tab.Name = "Tab"
	Tab.Parent = Main
	Tab.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	Tab.Position = UDim2.new(0, 5, 0, 30)
	Tab.Size = UDim2.new(0, 150, 0, 265)

	local TCNR = Instance.new("UICorner")
	TCNR.Name = "TCNR"
	TCNR.Parent = Tab

	local ScrollTab = Instance.new("ScrollingFrame")
	ScrollTab.Name = "ScrollTab"
	ScrollTab.Parent = Tab
	ScrollTab.Active = true
	ScrollTab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ScrollTab.BackgroundTransparency = 1.000
	ScrollTab.Size = UDim2.new(0, 150, 0, 265)
	ScrollTab.CanvasSize = UDim2.new(0, 0, 0, 0)
	ScrollTab.ScrollBarThickness = 0

	local PLL = Instance.new("UIListLayout")
	PLL.Name = "PLL"
	PLL.Parent = ScrollTab
	PLL.SortOrder = Enum.SortOrder.LayoutOrder
	PLL.Padding = UDim.new(0, 15)

	local PPD = Instance.new("UIPadding")
	PPD.Name = "PPD"
	PPD.Parent = ScrollTab
	PPD.PaddingLeft = UDim.new(0, 10)
	PPD.PaddingTop = UDim.new(0, 10)

	local Page = Instance.new("Frame")
	Page.Name = "Page"
	Page.Parent = Main
	Page.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
	Page.Position = UDim2.new(0.245426834, 0, 0, 30)
	Page.Size = UDim2.new(0, 490, 0, 365)

	local PCNR = Instance.new("UICorner")
	PCNR.Name = "PCNR"
	PCNR.Parent = Page

	local MainPage = Instance.new("Frame")
	MainPage.Name = "MainPage"
	MainPage.Parent = Page
	MainPage.ClipsDescendants = true
	MainPage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	MainPage.BackgroundTransparency = 1.000
	MainPage.Size = UDim2.new(0, 490, 0, 365)

	local PageList = Instance.new("Folder")
	PageList.Name = "PageList"
	PageList.Parent = MainPage

	local UIPageLayout = Instance.new("UIPageLayout")

	UIPageLayout.Parent = PageList
	UIPageLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIPageLayout.EasingDirection = Enum.EasingDirection.InOut
	UIPageLayout.EasingStyle = Enum.EasingStyle.Quad
	UIPageLayout.FillDirection = Enum.FillDirection.Vertical
	UIPageLayout.Padding = UDim.new(0, 15)
	UIPageLayout.TweenTime = 0.400
	UIPageLayout.GamepadInputEnabled = false
	UIPageLayout.ScrollWheelInputEnabled = false
	UIPageLayout.TouchInputEnabled = false

	MakeDraggable(Top,Main)


	local uitab = {}

	function uitab:Tab(text,logo1)
		local TabButton = Instance.new("TextButton")
		TabButton.Parent = ScrollTab
		TabButton.Name = text.."Server"
		TabButton.Text = text
		TabButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		TabButton.BackgroundTransparency = 1.000
		TabButton.Size = UDim2.new(0, 130, 0, 23)
		TabButton.Font = Enum.Font.GothamSemibold
		TabButton.TextColor3 = Color3.fromRGB(225, 225, 225)
		TabButton.TextSize = 15.000
		TabButton.TextTransparency = 0.500

		local IDK = Instance.new("ImageLabel")
		IDK.Name = "LogoIDK"
		IDK.Parent = TabButton
		IDK.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		IDK.BackgroundTransparency = 1.000
		IDK.Position = UDim2.new(0, 0, 0, 1)
		IDK.Size = UDim2.new(0, 20, 0, 20)
		IDK.Image = "rbxassetid://"..tostring(logo1)


		local MainFramePage = Instance.new("ScrollingFrame")
		MainFramePage.Name = text.."_Page"
		MainFramePage.Parent = PageList
		MainFramePage.Active = true
		MainFramePage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		MainFramePage.BackgroundTransparency = 1.000
		MainFramePage.BorderSizePixel = 0
		MainFramePage.Size = UDim2.new(0, 490, 0, 265)
		MainFramePage.CanvasSize = UDim2.new(0, 0, 0, 0)
		MainFramePage.ScrollBarThickness = 0

		local UIPadding = Instance.new("UIPadding")
		local UIListLayout = Instance.new("UIListLayout")

		UIPadding.Parent = MainFramePage
		UIPadding.PaddingLeft = UDim.new(0, 10)
		UIPadding.PaddingTop = UDim.new(0, 10)

		UIListLayout.Padding = UDim.new(0,15)
		UIListLayout.Parent = MainFramePage
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

		TabButton.MouseButton1Click:Connect(function()
			for i,v in next, ScrollTab:GetChildren() do
				if v:IsA("TextButton") then
					TweenService:Create(
						v,
						TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end
				TweenService:Create(
					TabButton,
					TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{TextTransparency = 0}
				):Play()
			end
			for i,v in next, PageList:GetChildren() do
				currentpage = string.gsub(TabButton.Name,"Server","").."_Page"
				if v.Name == currentpage then
					UIPageLayout:JumpTo(v)
				end
			end
		end)

		if abc == false then
			for i,v in next, ScrollTab:GetChildren() do
				if v:IsA("TextButton") then
					TweenService:Create(
						v,
						TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end
				TweenService:Create(
					TabButton,
					TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{TextTransparency = 0}
				):Play()
			end
			UIPageLayout:JumpToIndex(1)
			abc = true
		end

		game:GetService("RunService").Stepped:Connect(function()
			pcall(function()
				MainFramePage.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 20)
				ScrollTab.CanvasSize = UDim2.new(0,0,0,PLL.AbsoluteContentSize.Y + 20)
			end)
		end)


		local main = {}
		function main:Button(text,callback)
			local Button = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local TextBtn = Instance.new("TextButton")
			local UICorner_2 = Instance.new("UICorner")
			local Black = Instance.new("Frame")
			local UICorner_3 = Instance.new("UICorner")
			local IMGBUTTON = Instance.new("ImageLabel")

			Button.Name = "Button"
			Button.Parent = MainFramePage
			Button.BackgroundColor3 = _G.Color
			Button.Size = UDim2.new(0, 470, 0, 31)

			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = Button



			TextBtn.Name = "TextBtn"
			TextBtn.Parent = Button
			TextBtn.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
			TextBtn.Position = UDim2.new(0, 1, 0, 1)
			TextBtn.Size = UDim2.new(0, 468, 0, 29)
			TextBtn.AutoButtonColor = false
			TextBtn.Font = Enum.Font.GothamSemibold
			TextBtn.Text = text
			TextBtn.TextColor3 = Color3.fromRGB(225, 225, 225)
			TextBtn.TextSize = 15.000
			TextBtn.ClipsDescendants = true

			UICorner_2.CornerRadius = UDim.new(0, 5)
			UICorner_2.Parent = TextBtn

			IMGBUTTON.Name = "IconB"
			IMGBUTTON.Parent = TextBtn
			IMGBUTTON.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			IMGBUTTON.BackgroundTransparency = 1.000
			IMGBUTTON.Position = UDim2.new(0, 10, 0, 5)
			IMGBUTTON.Size = UDim2.new(0, 20, 0, 20)
			IMGBUTTON.Image = "http://www.roblox.com/asset/?id="..LogoButton


			Black.Name = "Black"
			Black.Parent = Button
			Black.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
			Black.BackgroundTransparency = 1.000
			Black.BorderSizePixel = 0
			Black.Position = UDim2.new(0, 1, 0, 1)
			Black.Size = UDim2.new(0, 468, 0, 29)

			UICorner_3.CornerRadius = UDim.new(0, 5)
			UICorner_3.Parent = Black

			TextBtn.MouseEnter:Connect(function()
				TweenService:Create(
					Black,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{BackgroundTransparency = 0.7}
				):Play()
			end)
			TextBtn.MouseLeave:Connect(function()
				TweenService:Create(
					Black,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{BackgroundTransparency = 1}
				):Play()
			end)
			TextBtn.MouseButton1Click:Connect(function()
				CircleAnim(TextBtn, Color3.fromRGB(255,255,255), Color3.fromRGB(255,255,255))
				TextBtn.TextSize = 1
				TweenService:Create(
					TextBtn,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{TextSize = 15}
				):Play()
				callback()
			end)
		end
		function main:Toggle(text,Imgidicon,config,callback)
			config = config or false
			local toggled = config
			local Toggle = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local Button = Instance.new("TextButton")
			local UICorner_2 = Instance.new("UICorner")
			local Label = Instance.new("TextLabel")
			local ToggleImage = Instance.new("Frame")
			local UICorner_3 = Instance.new("UICorner")
			local Circle = Instance.new("Frame")
			local UICorner_4 = Instance.new("UICorner")
			local imgLabelIcon = Instance.new("ImageLabel")


			Toggle.Name = "Toggle"
			Toggle.Parent = MainFramePage
			Toggle.BackgroundColor3 = Color3.fromRGB(40, 1, 140)
			Toggle.Size = UDim2.new(0, 470, 0, 31)

			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = Toggle

			Button.Name = "Button"
			Button.Parent = Toggle
			Button.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
			Button.Position = UDim2.new(0, 1, 0, 1)
			Button.Size = UDim2.new(0, 468, 0, 29)
			Button.AutoButtonColor = false
			Button.Font = Enum.Font.SourceSans
			Button.Text = ""
			Button.TextColor3 = Color3.fromRGB(0, 0, 0)
			Button.TextSize = 11.000

			UICorner_2.CornerRadius = UDim.new(0, 5)
			UICorner_2.Parent = Button

			Label.Name = "Label"
			Label.Parent = Toggle
			Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Label.BackgroundTransparency = 1.000
			Label.Position = UDim2.new(0, 1, 0, 1)
			Label.Size = UDim2.new(0, 468, 0, 29)
			Label.Font = Enum.Font.GothamSemibold
			Label.Text = text
			Label.TextColor3 = Color3.fromRGB(225, 225, 225)
			Label.TextSize = 15.000

			ToggleImage.Name = "ToggleImage"
			ToggleImage.Parent = Toggle
			ToggleImage.BackgroundColor3 = Color3.fromRGB(225, 225, 225)
			ToggleImage.Position = UDim2.new(0, 415, 0, 5)
			ToggleImage.Size = UDim2.new(0, 45, 0, 20)

			UICorner_3.CornerRadius = UDim.new(0, 10)
			UICorner_3.Parent = ToggleImage

			Circle.Name = "Circle"
			Circle.Parent = ToggleImage
			Circle.BackgroundColor3 = Color3.fromRGB(40, 1, 140)
			Circle.Position = UDim2.new(0, 2, 0, 2)
			Circle.Size = UDim2.new(0, 16, 0, 16)

			UICorner_4.CornerRadius = UDim.new(0, 10)
			UICorner_4.Parent = Circle

			imgLabelIcon.Name = "Icon"
			imgLabelIcon.Parent = Toggle
			imgLabelIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			imgLabelIcon.BackgroundTransparency = 1.000
			imgLabelIcon.Position = UDim2.new(0, 10, 0, 5)
			imgLabelIcon.Size = UDim2.new(0, 20, 0, 20)
			imgLabelIcon.Image = "http://www.roblox.com/asset/?id="..Imgidicon

			Button.MouseButton1Click:Connect(function()
				if toggled == false then
					toggled = true
					Circle:TweenPosition(UDim2.new(0,27,0,2),"Out","Sine",0.2,true)
					TweenService:Create(
						Toggle,
						TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{BackgroundColor3 = _G.Color}
					):Play()
					TweenService:Create(
						Circle,
						TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{BackgroundColor3 = _G.Color}
					):Play()
				else
					toggled = false
					Circle:TweenPosition(UDim2.new(0,2,0,2),"Out","Sine",0.2,true)
					TweenService:Create(
						Toggle,
						TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{BackgroundColor3 = Color3.fromRGB(255, 46, 46)}
					):Play()
					TweenService:Create(
						Circle,
						TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{BackgroundColor3 = Color3.fromRGB(255, 46, 46)}
					):Play()
				end
				pcall(callback,toggled)
			end)

			if config == true then
				toggled = true
				Circle:TweenPosition(UDim2.new(0,27,0,2),"Out","Sine",0.4,true)
				TweenService:Create(
					Toggle,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{BackgroundColor3 = _G.Color}
				):Play()
				TweenService:Create(
					Circle,
					TweenInfo.new(0.4,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{BackgroundColor3 = _G.Color}
				):Play()
				pcall(callback,toggled)
			end
		end
		function main:Dropdown(text,option,callback)
			local isdropping = false
			local Dropdown = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local DropTitle = Instance.new("TextLabel")
			local DropScroll = Instance.new("ScrollingFrame")
			local UIListLayout = Instance.new("UIListLayout")
			local UIPadding = Instance.new("UIPadding")
			local DropButton = Instance.new("TextButton")
			local DropImage = Instance.new("ImageLabel")

			Dropdown.Name = "Dropdown"
			Dropdown.Parent = MainFramePage
			Dropdown.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
			Dropdown.ClipsDescendants = true
			Dropdown.Size = UDim2.new(0, 470, 0, 31)

			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = Dropdown

			DropTitle.Name = "DropTitle"
			DropTitle.Parent = Dropdown
			DropTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropTitle.BackgroundTransparency = 1.000
			DropTitle.Size = UDim2.new(0, 470, 0, 31)
			DropTitle.Font = Enum.Font.GothamSemibold
			DropTitle.Text = text.. " : "
			DropTitle.TextColor3 = Color3.fromRGB(225, 225, 225)
			DropTitle.TextSize = 15.000

			DropScroll.Name = "DropScroll"
			DropScroll.Parent = DropTitle
			DropScroll.Active = true
			DropScroll.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropScroll.BackgroundTransparency = 1.000
			DropScroll.BorderSizePixel = 0
			DropScroll.Position = UDim2.new(0, 0, 0, 31)
			DropScroll.Size = UDim2.new(0, 470, 0, 100)
			DropScroll.CanvasSize = UDim2.new(0, 0, 0, 2)
			DropScroll.ScrollBarThickness = 3

			UIListLayout.Parent = DropScroll
			UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			UIListLayout.Padding = UDim.new(0, 5)

			UIPadding.Parent = DropScroll
			UIPadding.PaddingLeft = UDim.new(0, 5)
			UIPadding.PaddingTop = UDim.new(0, 5)

			DropImage.Name = "DropImage"
			DropImage.Parent = Dropdown
			DropImage.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropImage.BackgroundTransparency = 1.000
			DropImage.Position = UDim2.new(0, 445, 0, 6)
			DropImage.Rotation = -90
			DropImage.Size = UDim2.new(0, 20, 0, 20)
			DropImage.Image = "rbxassetid://6031090990"

			DropButton.Name = "DropButton"
			DropButton.Parent = Dropdown
			DropButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropButton.BackgroundTransparency = 1.000
			DropButton.Size = UDim2.new(0, 470, 0, 31)
			DropButton.Font = Enum.Font.SourceSans
			DropButton.Text = ""
			DropButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			DropButton.TextSize = 14.000

			for i,v in next,option do
				local Item = Instance.new("TextButton")

				Item.Name = "Item"
				Item.Parent = DropScroll
				Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Item.BackgroundTransparency = 1.000
				Item.Size = UDim2.new(0, 460, 0, 26)
				Item.Font = Enum.Font.GothamSemibold
				Item.Text = tostring(v)
				Item.TextColor3 = Color3.fromRGB(225, 225, 225)
				Item.TextSize = 13.000
				Item.TextTransparency = 0.500
				Item.ClipsDescendants = true


				Item.MouseEnter:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0}
					):Play()
				end)

				Item.MouseLeave:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end)

				Item.MouseButton1Click:Connect(function()
					CircleAnim(Item, Color3.fromRGB(255,255,255), Color3.fromRGB(255,255,255))
					isdropping = false
					Dropdown:TweenSize(UDim2.new(0,470,0,31),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = -90}
					):Play()
					DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)
					callback(Item.Text)
					DropTitle.Text = text.." : "..Item.Text
				end)
			end

			DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)

			DropButton.MouseButton1Click:Connect(function()
				if isdropping == false then
					isdropping = true
					Dropdown:TweenSize(UDim2.new(0,470,0,131),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = 180}
					):Play()
					DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)
				else
					isdropping = false
					Dropdown:TweenSize(UDim2.new(0,470,0,31),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = -90}
					):Play()
					DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)
				end
			end)

			local dropfunc = {}
			function dropfunc:Add(t)
				local Item = Instance.new("TextButton")
				Item.Name = "Item"
				Item.Parent = DropScroll
				Item.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Item.BackgroundTransparency = 1.000
				Item.Size = UDim2.new(0, 470, 0, 26)
				Item.Font = Enum.Font.GothamSemibold
				Item.Text = tostring(t)
				Item.TextColor3 = Color3.fromRGB(225, 225, 225)
				Item.TextSize = 13.000
				Item.TextTransparency = 0.500
				Item.ClipsDescendants = true

				Item.MouseEnter:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0}
					):Play()
				end)

				Item.MouseLeave:Connect(function()
					TweenService:Create(
						Item,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{TextTransparency = 0.5}
					):Play()
				end)

				Item.MouseButton1Click:Connect(function()
					isdropping = false
					CircleAnim(Item, Color3.fromRGB(255,255,255), Color3.fromRGB(255,255,255))
					Dropdown:TweenSize(UDim2.new(0,470,0,31),"Out","Quad",0.3,true)
					TweenService:Create(
						DropImage,
						TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
						{Rotation = -90}
					):Play()
					DropScroll.CanvasSize = UDim2.new(0,0,0,UIListLayout.AbsoluteContentSize.Y + 10)
					callback(Item.Text)
					DropTitle.Text = text.." : "..Item.Text
				end)
			end

			function dropfunc:Clear()
				DropTitle.Text = tostring(text).." : "
				isdropping = false
				Dropdown:TweenSize(UDim2.new(0,470,0,31),"Out","Quad",0.3,true)
				TweenService:Create(
					DropImage,
					TweenInfo.new(0.3,Enum.EasingStyle.Quad,Enum.EasingDirection.Out),
					{Rotation = -90}
				):Play()
				for i,v in next, DropScroll:GetChildren() do
					if v:IsA("TextButton") then
						v:Destroy()
					end
				end
			end
			return dropfunc
		end

		function main:Slider(text,min,max,set,callback)
			local Slider = Instance.new("Frame")
			local slidercorner = Instance.new("UICorner")
			local sliderr = Instance.new("Frame")
			local sliderrcorner = Instance.new("UICorner")
			local SliderLabel = Instance.new("TextLabel")
			local HAHA = Instance.new("Frame")
			local AHEHE = Instance.new("TextButton")
			local bar = Instance.new("Frame")
			local bar1 = Instance.new("Frame")
			local bar1corner = Instance.new("UICorner")
			local barcorner = Instance.new("UICorner")
			local circlebar = Instance.new("Frame")
			local UICorner = Instance.new("UICorner")
			local slidervalue = Instance.new("Frame")
			local valuecorner = Instance.new("UICorner")
			local TextBox = Instance.new("TextBox")
			local UICorner_2 = Instance.new("UICorner")

			Slider.Name = "Slider"
			Slider.Parent = MainFramePage
			Slider.BackgroundColor3 = _G.Color
			Slider.BackgroundTransparency = 0
			Slider.Size = UDim2.new(0, 470, 0, 51)

			slidercorner.CornerRadius = UDim.new(0, 5)
			slidercorner.Name = "slidercorner"
			slidercorner.Parent = Slider

			sliderr.Name = "sliderr"
			sliderr.Parent = Slider
			sliderr.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
			sliderr.Position = UDim2.new(0, 1, 0, 1)
			sliderr.Size = UDim2.new(0, 468, 0, 49)

			sliderrcorner.CornerRadius = UDim.new(0, 5)
			sliderrcorner.Name = "sliderrcorner"
			sliderrcorner.Parent = sliderr

			SliderLabel.Name = "SliderLabel"
			SliderLabel.Parent = sliderr
			SliderLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			SliderLabel.BackgroundTransparency = 1.000
			SliderLabel.Position = UDim2.new(0, 15, 0, 0)
			SliderLabel.Size = UDim2.new(0, 180, 0, 26)
			SliderLabel.Font = Enum.Font.GothamSemibold
			SliderLabel.Text = text
			SliderLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
			SliderLabel.TextSize = 16.000
			SliderLabel.TextTransparency = 0
			SliderLabel.TextXAlignment = Enum.TextXAlignment.Left

			HAHA.Name = "HAHA"
			HAHA.Parent = sliderr
			HAHA.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			HAHA.BackgroundTransparency = 1.000
			HAHA.Size = UDim2.new(0, 468, 0, 29)

			AHEHE.Name = "AHEHE"
			AHEHE.Parent = sliderr
			AHEHE.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			AHEHE.BackgroundTransparency = 1.000
			AHEHE.Position = UDim2.new(0, 10, 0, 35)
			AHEHE.Size = UDim2.new(0, 448, 0, 5)
			AHEHE.Font = Enum.Font.SourceSans
			AHEHE.Text = ""
			AHEHE.TextColor3 = Color3.fromRGB(0, 0, 0)
			AHEHE.TextSize = 14.000

			bar.Name = "bar"
			bar.Parent = AHEHE
			bar.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
			bar.Size = UDim2.new(0, 448, 0, 5)

			bar1.Name = "bar1"
			bar1.Parent = bar
			bar1.BackgroundColor3 = _G.Color
			bar1.BackgroundTransparency = 0
			bar1.Size = UDim2.new(set/max, 0, 0, 5)

			bar1corner.CornerRadius = UDim.new(0, 5)
			bar1corner.Name = "bar1corner"
			bar1corner.Parent = bar1

			barcorner.CornerRadius = UDim.new(0, 5)
			barcorner.Name = "barcorner"
			barcorner.Parent = bar

			circlebar.Name = "circlebar"
			circlebar.Parent = bar1
			circlebar.BackgroundColor3 = Color3.fromRGB(225, 225, 225)
			circlebar.Position = UDim2.new(1, -2, 0, -3)
			circlebar.Size = UDim2.new(0, 10, 0, 10)

			UICorner.CornerRadius = UDim.new(0, 100)
			UICorner.Parent = circlebar

			slidervalue.Name = "slidervalue"
			slidervalue.Parent = sliderr
			slidervalue.BackgroundColor3 = _G.Color
			slidervalue.BackgroundTransparency = 0
			slidervalue.Position = UDim2.new(0, 395, 0, 5)
			slidervalue.Size = UDim2.new(0, 65, 0, 18)

			valuecorner.CornerRadius = UDim.new(0, 5)
			valuecorner.Name = "valuecorner"
			valuecorner.Parent = slidervalue

			TextBox.Parent = slidervalue
			TextBox.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
			TextBox.Position = UDim2.new(0, 1, 0, 1)
			TextBox.Size = UDim2.new(0, 63, 0, 16)
			TextBox.Font = Enum.Font.GothamSemibold
			TextBox.TextColor3 = Color3.fromRGB(225, 225, 225)
			TextBox.TextSize = 9.000
			TextBox.Text = set
			TextBox.TextTransparency = 0

			UICorner_2.CornerRadius = UDim.new(0, 5)
			UICorner_2.Parent = TextBox

			local mouse = game.Players.LocalPlayer:GetMouse()
			local uis = game:GetService("UserInputService")

			if Value == nil then
				Value = set
				pcall(function()
					callback(Value)
				end)
			end

			AHEHE.MouseButton1Down:Connect(function()
				Value = math.floor((((tonumber(max) - tonumber(min)) / 448) * bar1.AbsoluteSize.X) + tonumber(min)) or 0
				pcall(function()
					callback(Value)
				end)
				TweenService:Create(
					bar1,
					TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)} -- UDim2.new(0, 128, 0, 25)
				):Play()
				--bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)
				TweenService:Create(
					circlebar,
					TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
					{Position =  UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)} -- UDim2.new(0, 128, 0, 25)
				):Play()
				--circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)
				moveconnection = mouse.Move:Connect(function()
					TextBox.Text = Value
					Value = math.floor((((tonumber(max) - tonumber(min)) / 448) * bar1.AbsoluteSize.X) + tonumber(min))
					pcall(function()
						callback(Value)
					end)
					TweenService:Create(
						bar1,
						TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
						{Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)} -- UDim2.new(0, 128, 0, 25)
					):Play()
					--bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)
					TweenService:Create(
						circlebar,
						TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
						{Position =  UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)} -- UDim2.new(0, 128, 0, 25)
					):Play()
					--circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)
				end)
				releaseconnection = uis.InputEnded:Connect(function(Mouse)
					if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
						Value = math.floor((((tonumber(max) - tonumber(min)) / 448) * bar1.AbsoluteSize.X) + tonumber(min))
						pcall(function()
							callback(Value)
						end)
						TweenService:Create(
							bar1,
							TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
							{Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)} -- UDim2.new(0, 128, 0, 25)
						):Play()
						--bar1.Size = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X, 0, 448), 0, 5)
						TweenService:Create(
							circlebar,
							TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
							{Position =  UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)} -- UDim2.new(0, 128, 0, 25)
						):Play()
						--circlebar.Position = UDim2.new(0, math.clamp(mouse.X - bar1.AbsolutePosition.X - 2, 0, 438), 0, -3)
						moveconnection:Disconnect()
						releaseconnection:Disconnect()
					end
				end)
			end)
			releaseconnection = uis.InputEnded:Connect(function(Mouse)
				if Mouse.UserInputType == Enum.UserInputType.MouseButton1 then
					Value = math.floor((((tonumber(max) - tonumber(min)) / 448) * bar1.AbsoluteSize.X) + tonumber(min))
					TextBox.Text = Value
				end
			end)

			TextBox.FocusLost:Connect(function()
				if tonumber(TextBox.Text) > max then
					TextBox.Text  = max
				end
				bar1.Size = UDim2.new((TextBox.Text or 0) / max, 0, 0, 5)
				circlebar.Position = UDim2.new(1, -2, 0, -3)
				TextBox.Text = tostring(TextBox.Text and math.floor( (TextBox.Text / max) * (max - min) + min) )
				pcall(callback, TextBox.Text)
			end)
		end

		function main:Textbox(text,disappear,callback)
			local Textbox = Instance.new("Frame")
			local TextboxCorner = Instance.new("UICorner")
			local Textboxx = Instance.new("Frame")
			local TextboxxCorner = Instance.new("UICorner")
			local TextboxLabel = Instance.new("TextLabel")
			local txtbtn = Instance.new("TextButton")
			local RealTextbox = Instance.new("TextBox")
			local UICorner = Instance.new("UICorner")

			Textbox.Name = "Textbox"
			Textbox.Parent = MainFramePage
			Textbox.BackgroundColor3 = _G.Color
			Textbox.BackgroundTransparency = 0
			Textbox.Size = UDim2.new(0, 470, 0, 31)

			TextboxCorner.CornerRadius = UDim.new(0, 5)
			TextboxCorner.Name = "TextboxCorner"
			TextboxCorner.Parent = Textbox

			Textboxx.Name = "Textboxx"
			Textboxx.Parent = Textbox
			Textboxx.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
			Textboxx.Position = UDim2.new(0, 1, 0, 1)
			Textboxx.Size = UDim2.new(0, 468, 0, 29)

			TextboxxCorner.CornerRadius = UDim.new(0, 5)
			TextboxxCorner.Name = "TextboxxCorner"
			TextboxxCorner.Parent = Textboxx

			TextboxLabel.Name = "TextboxLabel"
			TextboxLabel.Parent = Textbox
			TextboxLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextboxLabel.BackgroundTransparency = 1.000
			TextboxLabel.Position = UDim2.new(0, 15, 0, 0)
			TextboxLabel.Text = text
			TextboxLabel.Size = UDim2.new(0, 145, 0, 31)
			TextboxLabel.Font = Enum.Font.GothamSemibold
			TextboxLabel.TextColor3 = Color3.fromRGB(225, 225, 225)
			TextboxLabel.TextSize = 16.000
			TextboxLabel.TextTransparency = 0
			TextboxLabel.TextXAlignment = Enum.TextXAlignment.Left

			txtbtn.Name = "txtbtn"
			txtbtn.Parent = Textbox
			txtbtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			txtbtn.BackgroundTransparency = 1.000
			txtbtn.Position = UDim2.new(0, 1, 0, 1)
			txtbtn.Size = UDim2.new(0, 468, 0, 29)
			txtbtn.Font = Enum.Font.SourceSans
			txtbtn.Text = ""
			txtbtn.TextColor3 = Color3.fromRGB(0, 0, 0)
			txtbtn.TextSize = 14.000

			RealTextbox.Name = "RealTextbox"
			RealTextbox.Parent = Textbox
			RealTextbox.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
			RealTextbox.BackgroundTransparency = 0
			RealTextbox.Position = UDim2.new(0, 360, 0, 4)
			RealTextbox.Size = UDim2.new(0, 100, 0, 24)
			RealTextbox.Font = Enum.Font.GothamSemibold
			RealTextbox.Text = ""
			RealTextbox.TextColor3 = Color3.fromRGB(225, 225, 225)
			RealTextbox.TextSize = 11.000
			RealTextbox.TextTransparency = 0

			RealTextbox.FocusLost:Connect(function()
				callback(RealTextbox.Text)
				if disappear then
					RealTextbox.Text = ""
				end
			end)

			UICorner.CornerRadius = UDim.new(0, 5)
			UICorner.Parent = RealTextbox
		end
		function main:Label(text)
			local Label = Instance.new("TextLabel")
			local PaddingLabel = Instance.new("UIPadding")
			local labell = {}

			Label.Name = "Label"
			Label.Parent = MainFramePage
			Label.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Label.BackgroundTransparency = 1.000
			Label.Size = UDim2.new(0, 470, 0, 20)
			Label.Font = Enum.Font.GothamSemibold
			Label.TextColor3 = Color3.fromRGB(225, 225, 225)
			Label.TextSize = 16.000
			Label.Text = text
			Label.TextXAlignment = Enum.TextXAlignment.Left

			PaddingLabel.PaddingLeft = UDim.new(0,15)
			PaddingLabel.Parent = Label
			PaddingLabel.Name = "PaddingLabel"

			function labell:Set(newtext)
				Label.Text = newtext
			end

			return labell
		end
		function main:Seperator(text)
			local Seperator = Instance.new("Frame")
			local Sep1 = Instance.new("Frame")
			local Sep2 = Instance.new("TextLabel")
			local Sep3 = Instance.new("Frame")

			Seperator.Name = "Seperator"
			Seperator.Parent = MainFramePage
			Seperator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Seperator.BackgroundTransparency = 1.000
			Seperator.Size = UDim2.new(0, 470, 0, 20)

			Sep1.Name = "Sep1"
			Sep1.Parent = Seperator
			Sep1.BackgroundColor3 = _G.Color
			Sep1.BorderSizePixel = 0
			Sep1.Position = UDim2.new(0, 0, 0, 10)
			Sep1.Size = UDim2.new(0, 80, 0, 1)

			Sep2.Name = "Sep2"
			Sep2.Parent = Seperator
			Sep2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Sep2.BackgroundTransparency = 1.000
			Sep2.Position = UDim2.new(0, 185, 0, 0)
			Sep2.Size = UDim2.new(0, 100, 0, 20)
			Sep2.Font = Enum.Font.GothamSemibold
			Sep2.Text = text
			Sep2.TextColor3 = Color3.fromRGB(255, 255, 255)
			Sep2.TextSize = 14.000

			Sep3.Name = "Sep3"
			Sep3.Parent = Seperator
			Sep3.BackgroundColor3 = _G.Color
			Sep3.BorderSizePixel = 0
			Sep3.Position = UDim2.new(0, 390, 0, 10)
			Sep3.Size = UDim2.new(0, 80, 0, 1)
		end

		function main:Line()
			local Linee = Instance.new("Frame")
			local Line = Instance.new("Frame")

			Linee.Name = "Linee"
			Linee.Parent = MainFramePage
			Linee.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Linee.BackgroundTransparency = 1.000
			Linee.Position = UDim2.new(0, 0, 0.119999997, 0)
			Linee.Size = UDim2.new(0, 470, 0, 20)

			Line.Name = "Line"
			Line.Parent = Linee
			Line.BackgroundColor3 = _G.Color
			Line.BorderSizePixel = 0
			Line.Position = UDim2.new(0, 0, 0, 10)
			Line.Size = UDim2.new(0, 470, 0, 1)
		end
		return main
	end
	return uitab
end

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


function BTP(P)
	repeat wait(1)
		game.Players.LocalPlayer.Character.Humanoid:ChangeState(15)
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = P
		task.wait()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = P
	until (P.Position-game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 1500
end

function Com(com,...)
	local Remote = game:GetService('ReplicatedStorage').Remotes:FindFirstChild("Comm"..com)
	if Remote:IsA("RemoteEvent") then
		Remote:FireServer(...)
	elseif Remote:IsA("RemoteFunction") then
		Remote:InvokeServer(...)
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
		if game.Players.LocalPlayer.Character:FindFirstChild("BodyClip") then
			game.Players.LocalPlayer.Character:FindFirstChild("BodyClip"):Destroy()
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
			if _G.Auto_Farm_Level or _G.Auto_Observation or _G.AutoObservationv2 or _G.Auto_Farm_Mob_Aura or _G.Auto_New_World or _G.Auto_Farm_BF_Mastery or _G.Auto_Farm_Gun_Mastery or _G.Auto_Third_World or _G.AutoFarmChest or _G.Start_Tween_Island or _G.Auto_Farm_Boss or _G.Auto_Elite_Hunter or _G.Auto_Cake_Prince or _G.Auto_Farm_All_Boss or _G.AutoSaber or _G.Auto_Pole or _G.Auto_Factory_Farm or _G.Auto_Farm_Ectoplasm or _G.Auto_Bartilo_Quest or _G.Auto_Rengoku or _G.Auto_Evo_Race_V2 or _G.Auto_Swan_Glasses or _G.Auto_Dragon_Trident or _G.Auto_Farm_Bone or  _G.Auto_Rainbow_Haki or _G.Auto_Holy_Torch or _G.Auto_Canvander or _G.Auto_Twin_Hook or _G.Auto_Serpent_Bow or _G.AutoFarmMaterial or _G.Auto_Fully_Death_Step or _G.Auto_Fully_SharkMan_Karate or _G.Teleport_to_Player or _G.Auto_Kill_Player_Melee or _G.Auto_Kill_Player_Gun or _G.Auto_Next_Island or _G.AutoFarmSelectMonster or _G.Auto_Factory_Farm or _G.Auto_Tushita or _G.Auto_Yama or _G.Auto_Kill_Law or _G.Auto_Soul_Guitar or _G.Auto_Farm_Chest_Fast then
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


------------------------------------------------------------------------------------------------------------------------------

_G.Color = Color3.fromRGB(40, 1, 140)
_G.imgToggle = "6022668898"


local SOMEXHUB = library:Window(" Manake",[[HUB]],"Script",Enum.KeyCode.RightControl)
local Main = SOMEXHUB:Tab("Main",[[6026568198]])
local TabStats = SOMEXHUB:Tab("Stats",[[7040410130]])
local TabCombat = SOMEXHUB:Tab("Combat",[[7251993295]])
local Teleport = SOMEXHUB:Tab("Teleport",[[6035190846]])
local Dungeon = SOMEXHUB:Tab("Dungeon",[[7044284832]])
local Shop = SOMEXHUB:Tab("Shop",[[6031265976]])
local DevilFruit = SOMEXHUB:Tab("Devil Fruit",[[7044233235]])
local Misc = SOMEXHUB:Tab("Misc",[[6034509993]])

------------------------------------------------------------------------------------------------------------------------------
--\\ ระบบ script //--

--Webhook Script

Main:Seperator("Chack All")

Time = Main:Label("Server Time")

function UpdateTime()
	local GameTime = math.floor(workspace.DistributedGameTime+0.5)
	local Hour = math.floor(GameTime/(60^2))%24
	local Minute = math.floor(GameTime/(60^1))%60
	local Second = math.floor(GameTime/(60^0))%60
	Time:Set("Hr(s) : "..Hour.." Min(s) : "..Minute.." Sec(s) : "..Second)
end

spawn(function()
	while task.wait() do
		pcall(function()
			UpdateTime()
		end)
	end
end)

------------------------------------------------------------------------------------------------------------------------------
Main:Seperator("Auto Farm")

Main:Toggle("Auto Farm Level",_G.imgToggle,false,function(value)
	_G.Auto_Farm_Level = value
	StopTween(_G.Auto_Farm_Level)
end)

MethodFarm = CFrame.new(0, 30, 0)

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

Main:Toggle("Auto Farm Mob Aura",_G.imgToggle,false,function(value)
	_G.Auto_Farm_Mob_Aura = value
	StopTween(_G.Auto_Farm_Mob_Aura)
end)


task.spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Farm_Mob_Aura then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if _G.Auto_Farm_Mob_Aura and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 1000 then
						repeat wait()
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

------------------------------------------------------------------------------------------------------------------------------


if World1 then

	Main:Seperator("New World")

	Main:Toggle("Auto New World",_G.imgToggle,false,function(value)
		_G.Auto_New_World = value
		StopTween(_G.Auto_New_World)
	end)

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
									if _v.Name == "Ice Admiral [Lv. 700] [Boss]" and _v.Humanoid.Health > 0 then
										for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
											if v.Name == "Ice Admiral [Lv. 700] [Boss]" and v.Humanoid.Health > 0 then
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

	Main:Seperator("Other Funcrion")

	Main:Toggle("Auto Saber",_G.imgToggle,false,function(value)
		_G.Auto_Saber = value
		StopTween(_G.Auto_Saber)
	end)

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
										if game:GetService("Workspace").Enemies:FindFirstChild("Mob Leader [Lv. 120] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Mob Leader [Lv. 120] [Boss]") then
											getgenv().ToTarget(CFrame.new(-2967.59521, -4.91089821, 5328.70703, 0.342208564, -0.0227849055, 0.939347804, 0.0251603816, 0.999569714, 0.0150796166, -0.939287126, 0.0184739735, 0.342634559))
											for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
												if _v.Name == "Mob Leader [Lv. 120] [Boss]" then
													for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
														if v.Name == "Mob Leader [Lv. 120] [Boss]" then
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
						if game:GetService("Workspace").Enemies:FindFirstChild("Saber Expert [Lv. 200] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Saber Expert [Lv. 200] [Boss]") then
							getgenv().ToTarget(CFrame.new(-1401.85046, 29.9773273, 8.81916237, 0.85820812, 8.76083845e-08, 0.513301849, -8.55007443e-08, 1, -2.77243419e-08, -0.513301849, -2.00944328e-08, 0.85820812))
							for _i,_v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if _v.Name == "Saber Expert [Lv. 200] [Boss]" then
									for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
										if v.Name == "Saber Expert [Lv. 200] [Boss]" then
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

	Main:Toggle("Auto Pole",_G.imgToggle,false,function(value)
		_G.Auto_Pole = value
		StopTween(_G.Auto_Pole)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Pole then
					if game.ReplicatedStorage:FindFirstChild("Thunder God [Lv. 575] [Boss]") or game.Workspace.Enemies:FindFirstChild("Thunder God [Lv. 575] [Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if string.find(v.Name,"Thunder God [Lv. 575] [Boss]") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
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

	Main:Seperator("Auto Buy Ablility")

	Main:Toggle("Auto Buy Ablility",_G.imgToggle,false,function(value)
		_G.Auto_Buy_Ablility = value
	end)

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
end


------------------------------------------------------------------------------------------------------------------------------

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

local SelectWeapona = Main:Dropdown("Select Weapon",Weapon,function(value)
	SelectWeapon = value
end)

Main:Seperator("Settings")

Main:Toggle('Fast Attack',_G.imgToggle,true, function(value)
	_G.FastAttack = value
end)

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


Main:Toggle("Bring Mob",_G.imgToggle,true,function(value)
	_G.Bring_Mob = value
end)

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
					elseif _G.Auto_Farm_Bone and PosMonBone and (v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]") and (v.HumanoidRootPart.Position - PosMonBone.Position).magnitude <= 225 then
						v.HumanoidRootPart.CFrame = PosMonBone
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
					elseif _G.Auto_Cake_Prince and StartCakeMagnet and (v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]") and (v.HumanoidRootPart.Position - POSCAKE.Position).magnitude <= 225 then
						gv.HumanoidRootPart.CFrame = POSCAKE
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
					elseif _G.Auto_Rengoku and StartMagnet and (v.Name == "Snow Lurker [Lv. 1375]" or v.Name == "Arctic Warrior [Lv. 1350]") and (v.HumanoidRootPart.Position - PosMon.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMon
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_EvoRace and StartEvoMagnet and v.Name == "Zombie [Lv. 950]" and (v.HumanoidRootPart.Position - PosMonEvo.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonEvo
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Bartilo and StartMagnet and v.Name == "Swan Pirate [Lv. 775]" and (v.HumanoidRootPart.Position - PosMonBarto.Position).Magnitude <= 250 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMon
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_Gun_Mastery and StartMasteryGunMagnet and v.Name == "Monkey [Lv. 14]" and (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryGun
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_Gun_Mastery and v.Name == "Factory Staff [Lv. 800]" and (v.HumanoidRootPart.Position - PosMonMasteryGun.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
					elseif _G.Auto_Farm_BF_Mastery and StartMasteryFruitMagnet and v.Name == "Monkey [Lv. 14]" and (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						v.Humanoid:ChangeState(14)
						v.HumanoidRootPart.CanCollide = false
						v.Head.CanCollide = false
						v.HumanoidRootPart.CFrame = PosMonMasteryFruit
						if v.Humanoid:FindFirstChild("Animator") then
							v.Humanoid.Animator:Destroy()
						end
						sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", math.huge)
					elseif _G.Auto_Farm_BF_Mastery and v.Name == "Factory Staff [Lv. 800]" and (v.HumanoidRootPart.Position - PosMonMasteryFruit.Position).Magnitude <= 225 and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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

Main:Toggle("WhiteScreen",_G.imgToggle,false,function(value)
	if value == true then
		game:GetService("RunService"):Set3dRenderingEnabled(false)
	elseif value == false then
		game:GetService("RunService"):Set3dRenderingEnabled(true)
	end
end)


if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Death") then
	game:GetService("ReplicatedStorage").Effect.Container.Death:Destroy()
end
if game:GetService("ReplicatedStorage").Effect.Container:FindFirstChild("Respawn") then
	game:GetService("ReplicatedStorage").Effect.Container.Respawn:Destroy()
end

------------------------------------------------------------------------------------------------------------------------------

--[[Main:Seperator(" \\\\ Fighting Style // ")

Main:Toggle("Auto Superhuman","6022668898",_G.AutoSuperhuman,function(value)
    _G.AutoSuperhuman = value
end)

spawn(function()
    pcall(function()
        while wait() do 
            if _G.AutoSuperhuman then
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 150000 then
                    EquipWeapon("Combat")
                    wait(.1)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
                end   
                if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") then
                    _G.Select_Weapon = "Superhuman"
                end  
                if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") or game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") or game.Players.LocalPlayer.Character:FindFirstChild("Electro") or game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") or game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") then
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299 then
                        _G.Select_Weapon = "Black Leg"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299 then
                        _G.Select_Weapon = "Electro"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299 then
                        _G.Select_Weapon = "Fishman Karate"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299 then
                        _G.Select_Weapon = "Dragon Claw"
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                        EquipWeapon("Black Leg")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 300000 then
                        EquipWeapon("Black Leg")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                        EquipWeapon("Electro")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 750000 then
                        EquipWeapon("Electro")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                        EquipWeapon("Fishman Karate")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300 and game:GetService("Players")["Localplayer"].Data.Fragments.Value >= 1500 then
                        EquipWeapon("Fishman Karate")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2") 
                    end
                    if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                        EquipWeapon("Dragon Claw")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                    end
                    if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300 and game:GetService("Players")["LocalPlayer"].Data.Beli.Value >= 3000000 then
                        EquipWeapon("Dragon Claw")
                        wait(.1)
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
                    end 
                end
            end
        end
    end)
end)

Main:Toggle("Auto DeathStep","6022668898",_G.AutoDeathStep,function(value)
    _G.AutoDeathStep = value
end)

spawn(function()
    while wait() do wait()
        if _G.AutoDeathStep then
            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Death Step") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Death Step") then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 450 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
                    _G.Select_Weapon = "Death Step"
                end  
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 450 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
                    _G.Select_Weapon = "Death Step"
                end  
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 449 then
                    _G.Select_Weapon = "Black Leg"
                end 
            else 
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
            end
        end
    end
end)

Main:Toggle("Auto Sharkman Karate","6022668898",_G.AutoSharkman,function(value)
    _G.AutoSharkman = value
end)

spawn(function()
    pcall(function()
        while wait() do
            if _G.AutoSharkman then
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
                if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate"), "keys") then  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key") then
                        topos(CFrame.new(-2604.6958, 239.432526, -10315.1982, 0.0425701365, 0, -0.999093413, 0, 1, 0, 0.999093413, 0, 0.0425701365))
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                    elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 400 then
                    else 
                        Ms = "Tide Keeper [Lv. 1475] [Boss]"
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then   
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v.Name == Ms then    
                                    OldCFrameShark = v.HumanoidRootPart.CFrame
                                    repeat task.wait()
                                        AutoHaki()
                                        EquipWeapon(_G.Select_Weapon)
                                        v.Head.CanCollide = false
                                        v.Humanoid.WalkSpeed = 0
                                        v.HumanoidRootPart.CanCollide = false
                                        v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                                        v.HumanoidRootPart.CFrame = OldCFrameShark
                                        topos(v.HumanoidRootPart.CFrame * MethodFarm)
                                        game:GetService("VirtualUser"):CaptureController()
                                        game:GetService("VirtualUser"):Button1Down(Vector2.new(1280, 670))
                                        sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                    until not v.Parent or v.Humanoid.Health <= 0 or _G.AutoSharkman == false or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Water Key") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Water Key")
                                end
                            end
                        else
                            topos(CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202))
                            wait(3)
                        end
                    end
                else 
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
                end
            end
        end
    end)
end)

Main:Toggle("Auto Electric Claw","6022668898",_G.AutoElectricClaw,function(value)
    _G.AutoElectricClaw = value
    StopTween(_G.AutoElectricClaw)
end)

spawn(function()
    pcall(function()
        while wait() do 
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electric Claw") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electric Claw") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.Select_Weapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        _G.Select_Weapon = "Electric Claw"
                    end  
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 399 then
                        _G.Select_Weapon = "Electro"
                    end 
                else
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
                end
            end
            if _G.AutoElectricClaw then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") then
                    if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
                        if _G.Auto_Farm_Level == false then
                            repeat task.wait()
                                topos(CFrame.new(-10371.4717, 330.764496, -10131.4199))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-10371.4717, 330.764496, -10131.4199).Position).Magnitude <= 10
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(2)
                            repeat task.wait()
                                topos(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438).Position).Magnitude <= 10
                            wait(1)
                            repeat task.wait()
                                topos(CFrame.new(-10371.4717, 330.764496, -10131.4199))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-10371.4717, 330.764496, -10131.4199).Position).Magnitude <= 10
                            wait(1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                        elseif _G.Auto_Farm_Level == true then
                            _G.Auto_Farm_Level = false
                            wait(1)
                            repeat task.wait()
                                topos(CFrame.new(-10371.4717, 330.764496, -10131.4199))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-10371.4717, 330.764496, -10131.4199).Position).Magnitude <= 10
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw","Start")
                            wait(2)
                            repeat task.wait()
                                topos(CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-12550.532226563, 336.22631835938, -7510.4233398438).Position).Magnitude <= 10
                            wait(1)
                            repeat task.wait()
                                topos(CFrame.new(-10371.4717, 330.764496, -10131.4199))
                            until not _G.AutoElectricClaw or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position - CFrame.new(-10371.4717, 330.764496, -10131.4199).Position).Magnitude <= 10
                            wait(1)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
                            _G.Select_Weapon = "Electric Claw"
                            wait(.1)
                            _G.Auto_Farm_Level = true
                        end
                    end
                end
            end
        end
    end)
end)

Main:Toggle("Auto Dragon Talon","6022668898",_G.AutoDragonTalon,function(value)
    _G.AutoDragonTalon = value
end)

spawn(function()
    while wait() do
        if _G.AutoDragonTalon then
            if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Talon") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Talon") then
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 400 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    _G.Select_Weapon = "Dragon Talon"
                end  
                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 400 then
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
                    _G.Select_Weapon = "Dragon Talon"
                end  
                if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 399 then
                    _G.Select_Weapon = "Dragon Claw"
                end 
            else 
                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
            end
        end
    end
end)]]---


Main:Seperator("Mastery")

Main:Toggle("Auto Farm BF Mastery",_G.imgToggle,false,function(value)
	_G.Auto_Farm_BF_Mastery = value
	StopTween(_G.Auto_Farm_BF_Mastery)
end)

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

Main:Toggle("Auto Farm Gun Mastery",_G.imgToggle,false,function(value)
	_G.Auto_Farm_Gun_Mastery = value
	StopTween(_G.Auto_Farm_Gun_Mastery)
end)

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

_G.Kill_At = 25
Main:Slider("Kill At %",1,100,25,function(value)
	_G.Kill_At = value
end)

Main:Seperator("Observation")

local ObservationRange = Main:Label("")

spawn(function()
	while wait() do
		pcall(function()
			ObservationRange:Set("Observation Range Level : "..math.floor(game:GetService("Players").LocalPlayer.VisionRadius.Value))
		end)
	end
end)

Main:Toggle("Auto Farm Observation",_G.imgToggle,false,function(value)
	_G.Auto_Observation = value
	StopTween(_G.Auto_Observation)
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Observation then
				repeat task.wait()
					if not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
						game:GetService('VirtualUser'):CaptureController()
						game:GetService('VirtualUser'):SetKeyDown('0x65')
						wait(2)
						game:GetService('VirtualUser'):SetKeyUp('0x65')
					end
				until game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") or not _G.Auto_Observation
			end
		end)
	end
end)

Main:Toggle("Auto Farm Observation Hop",_G.imgToggle,false,function(value)
	_G.Auto_Observation_Hop = value
end)

spawn(function()
	pcall(function()
		while wait() do
			if _G.Auto_Observation then
				if game:GetService("Players").LocalPlayer.VisionRadius.Value >= 3000 then
					game:GetService("StarterGui"):SetCore("SendNotification", {
						Icon = "rbxassetid://0";
						Title = "Observation", 
						Text = "You Have Max Points"
					})
					wait(2)
				else
					if World2 then
						if game:GetService("Workspace").Enemies:FindFirstChild("Lava Pirate [Lv. 1200]") then
							if game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Lava Pirate [Lv. 1200]").HumanoidRootPart.CFrame * CFrame.new(3,0,0)
								until _G.Auto_Observation == false or not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							else
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Lava Pirate [Lv. 1200]").HumanoidRootPart.CFrame * CFrame.new(0,50,0)+
										wait(1)
									if not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") and _G.Auto_Observation_Hop == true then
										game:GetService("TeleportService"):Teleport(game.PlaceId,game:GetService("Players").LocalPlayer)
									end
								until _G.Auto_Observation == false or game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							end
						else
							getgenv().ToTarget(CFrame.new(-5478.39209, 15.9775667, -5246.9126))
						end
					elseif World1 then
						if game:GetService("Workspace").Enemies:FindFirstChild("Galley Captain [Lv. 650]") then
							if game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Galley Captain [Lv. 650]").HumanoidRootPart.CFrame * CFrame.new(3,0,0)
								until _G.Auto_Observation == false or not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							else
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Galley Captain [Lv. 650]").HumanoidRootPart.CFrame * CFrame.new(0,50,0)
									wait(1)
									if not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") and _G.Auto_Observation_Hop == true then
										game:GetService("TeleportService"):Teleport(game.PlaceId,game:GetService("Players").LocalPlayer)
									end
								until _G.Auto_Observation == false or game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							end
						else
							getgenv().ToTarget(CFrame.new(5533.29785, 88.1079102, 4852.3916))
						end
					elseif World3 then
						if game:GetService("Workspace").Enemies:FindFirstChild("Giant Islander [Lv. 1650]") then
							if game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Giant Islander [Lv. 1650]").HumanoidRootPart.CFrame * CFrame.new(3,0,0)
								until _G.Auto_Observation == false or not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							else
								repeat task.wait()
									game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Enemies:FindFirstChild("Giant Islander [Lv. 1650]").HumanoidRootPart.CFrame * CFrame.new(0,50,0)
									wait(1)
									if not game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") and _G.Auto_Observation_Hop == true then
										game:GetService("TeleportService"):Teleport(game.PlaceId,game:GetService("Players").LocalPlayer)
									end
								until _G.Auto_Observation == false or game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel")
							end
						else
							getgenv().ToTarget(CFrame.new(4530.3540039063, 656.75695800781, -131.60952758789))
						end
					end
				end
			end
		end
	end)
end)

Main:Toggle("Auto Observation Haki v2",_G.imgToggle,false,function(value)
	_G.AutoObservationv2 = value
	StopTween(_G.AutoObservationv2)
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.AutoObservationv2 then
				if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 3 then
					_G.AutoMusketeerHat = false
					if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Banana") and  game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Apple") and game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Pineapple") then
						repeat 
							getgenv().ToTarget(CFrame.new(-12444.78515625, 332.40396118164, -7673.1806640625)) 
							wait() 
						until not _G.AutoObservationv2 or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-12444.78515625, 332.40396118164, -7673.1806640625)).Magnitude <= 10
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen")
					elseif game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Fruit Bowl") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Fruit Bowl") then
						repeat 
							getgenv().ToTarget(CFrame.new(-10920.125, 624.20275878906, -10266.995117188)) 
							wait() 
						until not _G.AutoObservationv2 or (game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-10920.125, 624.20275878906, -10266.995117188)).Magnitude <= 10
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Start")
						wait(1)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Buy")
					else
						for i,v in pairs(game:GetService("Workspace"):GetDescendants()) do
							if v.Name == "Apple" or v.Name == "Banana" or v.Name == "Pineapple" then
								v.Handle.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,1,10)
								wait()
								firetouchinterest(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
								wait()
							end
						end   
					end
				else
					_G.AutoMusketeerHat = true
				end
			end
		end)
	end
end)


--[[Main:Seperator(" \\\\ Bosses // ")

local Boss = {}

for i, v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
    if string.find(v.Name, "Boss") then
        if v.Name == "Ice Admiral [Lv. 700] [Boss]" then

        else
            table.insert(Boss, v.Name)
        end
    end
end

local BossName = Main:Dropdown("Select Boss",Boss,function(value)
    _G.Select_Boss = value
end)

Main:Button("Refresh Boss",function()
    BossName:Clear()
    for i, v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
        if string.find(v.Name, "Boss") then
            BossName:Add(v.Name) 
        end
    end
end)

Main:Toggle("Auto Farm Boss","6022668898",_G.AutoFarmBoss,function(value)
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
    _G.AutoFarmBoss = value
    StopTween(_G.AutoFarmBoss)
end)

spawn(function()
    while wait() do
        if _G.AutoFarmBoss then
            pcall(function()
                if game:GetService("Workspace").Enemies:FindFirstChild(_G.Select_Boss) then
                    for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                        if v.Name == _G.Select_Boss then
                            if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                repeat task.wait()
                                    AutoHaki()
                                    EquipWeapon(_G.Select_Weapon)
                                    v.HumanoidRootPart.CanCollide = false
                                    v.Humanoid.WalkSpeed = 0
                                    v.HumanoidRootPart.Size = Vector3.new(80,80,80)                             
                                    topos(v.HumanoidRootPart.CFrame * MethodFarm)
                                    game:GetService("VirtualUser"):CaptureController()
                                    game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
                                    sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
                                until not _G.AutoFarmBoss or not v.Parent or v.Humanoid.Health <= 0
                            end
                        end
                    end
                else
                    if game:GetService("ReplicatedStorage"):FindFirstChild(_G.Select_Boss) then
                        topos(game:GetService("ReplicatedStorage"):FindFirstChild(_G.Select_Boss).HumanoidRootPart.CFrame * MethodFarm)
                    end
                end
            end)
        end
    end
end)

Main:Toggle("Auto Farm All Boss","6022668898",_G.AutoAllBoss,function(value)
    _G.AutoAllBoss = value
    StopTween(_G.AutoAllBoss)
end)

Main:Toggle("Auto Farm All Boss Hop","6022668898",_G.AutoAllBossHop,function(value)
    _G.AutoAllBossHop = value
end)

spawn(function()
    while wait() do
        if _G.AutoAllBoss then
            pcall(function()
                for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
                    if string.find(v.Name,"Boss") then
                        if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 17000 then
                            repeat task.wait()
                                AutoHaki()
                                EquipWeapon(_G.Select_Weapon)
                                v.Humanoid.WalkSpeed = 0
                                v.HumanoidRootPart.CanCollide = false
                                v.Head.CanCollide = false
                                v.HumanoidRootPart.Size = Vector3.new(80,80,80)
                                topos(v.HumanoidRootPart.CFrame * MethodFarm)
                                game:GetService'VirtualUser':CaptureController()
                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",math.huge)
                            until v.Humanoid.Health <= 0 or _G.AutoAllBoss == false or not v.Parent
                        end
                    else
                        if _G.AutoAllBossHop then
                            Hop()
                        end
                    end
                end
            end)
        end
    end
end)
]]--


if World2 then

	Main:Seperator("New World")

	Main:Toggle("Auto Third World",_G.imgToggle,false,function(value)
		_G.Auto_Third_World = value
		StopTween(_G.Auto_Third_World)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Third_World then
					if game.Players.LocalPlayer.Data.Level.Value >= 1500 then
						_G.Auto_Farm_Level = false
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 3 then
							if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess ~= nil then
								Com("F_","TravelZou")
								if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("ZQuestProgress", "Check") == 0 then
									if game.Workspace.Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") then 	
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "rip_indra [Lv. 1500] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "Don Swan [Lv. 1000] [Boss]" and v:FindFirstChild("Humanoid")and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									if game.Workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
										for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
											if v.Name == "Swan Pirate [Lv. 775]" then
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
								if game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
									for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
										if v.Name == "Jeremy [Lv. 850] [Boss]" then
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

	Main:Seperator("Rengoku")

	Main:Toggle("Auto Rengoku",_G.imgToggle,false,function(value)
		_G.Auto_Rengoku = value
		StopTween(_G.Auto_Rengoku)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Rengoku then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or game.Players.LocalPlayer.Character:FindFirstChild("Hidden Key") then
						EquipWeapon("Hidden Key")
						getgenv().ToTarget(CFrame.new(6571.1201171875, 299.23028564453, -6967.841796875))
					elseif game.Workspace.Enemies:FindFirstChild("Snow Lurker [Lv. 1375]") or game:GetService("Workspace").Enemies:FindFirstChild("Arctic Warrior [Lv. 1350]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if v.Name == "Snow Lurker [Lv. 1375]" or v.Name == "Arctic Warrior [Lv. 1350]" and v.Humanoid.Health > 0 then
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


	Main:Toggle("Auto Rengoku Hop",_G.imgToggle,false,function(value)
		_G.Auto_Rengoku_Hop = value
		StopTween(_G.Auto_Rengoku_Hop)
	end)

	Main:Seperator("Dragon Trident")

	Main:Toggle("Auto Dragon Trident",_G.imgToggle,false,function(value)
		_G.Auto_Dragon_Trident = value
		StopTween(_G.Auto_Dragon_Trident)
	end)

	spawn(function()
		while wait() do
			if _G.Auto_Dragon_Trident then
				pcall(function()
					if _G.Auto_Dragon_Trident and game.ReplicatedStorage:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") or game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
						if game.Workspace.Enemies:FindFirstChild("Tide Keeper [Lv. 1475] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Tide Keeper [Lv. 1475] [Boss]" and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
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

	Main:Toggle("Auto Dragon Trident Hop",_G.imgToggle,false,function(value)
		_G.Auto_Dragon_Trident_Hop = value
		StopTween(_G.Auto_Dragon_Trident_Hop)
	end)

	Main:Seperator("Dark Coat")

	Main:Toggle("Auto Dark Coat",_G.imgToggle,false,function(value)
		_G.Auto_Dark_Coat = value
		StopTween(_G.Auto_Dark_Coat)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Dark_Coat then
					if game:GetService("Workspace").Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Darkbeard [Lv. 1000] [Raid Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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

	Main:Toggle("Auto Dark Coat Hop",_G.imgToggle,false,function(value)
		_G.Auto_Dark_Coat_Hop = value
		StopTween(_G.Auto_Dark_Coat_Hop)
	end)


	Main:Seperator("Swan Glasses")

	Main:Toggle("Auto Swan Glasses",_G.imgToggle,false,function(value)
		_G.Auto_Swan_Glasses = value
		StopTween(_G.Auto_Swan_Glasses)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Swan_Glasses then
					if game:GetService("Workspace").Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Don Swan [Lv. 1000] [Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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

	Main:Toggle("Auto Swan Glasses Hop",_G.imgToggle,false,function(value)
		_G.Auto_Swan_Glasses_Hop = value
		StopTween(_G.Auto_Swan_Glasses_Hop)
	end)

	Main:Seperator("Other Function")

	Main:Toggle("Auto Bartilo Quest",_G.imgToggle,false,function(value)
		_G.Auto_Bartilo_Quest = value
		StopTween(_G.Auto_Bartilo_Quest)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Bartilo_Quest then
					if game.Players.LocalPlayer.Data.Level.Value >= 850 then
						if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
							if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
								if game.Workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
									for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
										if v.Name == "Swan Pirate [Lv. 775]" then
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
						if game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Jeremy [Lv. 850] [Boss]" then
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

	Main:Toggle("Auto Ectoplasm",_G.imgToggle,false,function(value)
		_G.Auto_Ectoplasm = value
		StopTween(_G.Auto_Ectoplasm)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Ectoplasm then
					if game:GetService("Workspace").Enemies:FindFirstChild("Ship Deckhand [Lv. 1250]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Engineer [Lv. 1275]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Steward [Lv. 1300]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Officer [Lv. 1325]") or game:GetService("Workspace").Enemies:FindFirstChild("Arctic Warrior [Lv. 1350]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Ship Deckhand [Lv. 1250]" or v.Name == "Ship Engineer [Lv. 1275]" or v.Name == "Ship Steward [Lv. 1300]" or v.Name == "Ship Officer [Lv. 1325]" or v.Name == "Arctic Warrior [Lv. 1350]" then
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

	Main:Toggle("Auto Evo Race V2",_G.imgToggle,false,function(value)
		_G.Auto_Evo_Race_V2 = value
		StopTween(_G.Auto_Evo_Race_V2)
	end)

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

	Main:Toggle("Auto True Triple Katana",_G.imgToggle,false,function(value)
		_G.Auto_True_Triple_Katana = value
	end)

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

	Main:Toggle("Auto Buy Legendary Sword",_G.imgToggle,false,function(value)
		_G.Auto_Buy_Legendary_Sword = value
	end)

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

	Main:Toggle("Auto Buy Enchanment Haki",_G.imgToggle,false,function(value)
		_G.Auto_Buy_Enchanment_Haki = value
	end)

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
elseif World3 then

	Main:Seperator("Elite Hunter")

	local EliteProgress = Main:Label("")

	spawn(function()
		pcall(function()
			while wait() do
				EliteProgress:Set("Elite Progress : "..game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter","Progress"))
			end
		end)
	end)

	Main:Toggle("Auto Elite Hunter",_G.imgToggle,false,function(value)
		_G.Auto_Elite_Hunter = value
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
		StopTween(_G.Auto_Elite_Hunter)
	end)


	spawn(function()
		while wait() do
			if _G.Auto_Elite_Hunter and World3 then
				pcall(function()
					if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Diablo") or string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Deandre") or string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Urban") then
							if game:GetService("Workspace").Enemies:FindFirstChild("Diablo") or game:GetService("Workspace").Enemies:FindFirstChild("Deandre ") or game:GetService("Workspace").Enemies:FindFirstChild("Urban") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Diablo" or v.Name == "Deandre" or v.Name == "Urban" then
										if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
											repeat wait()
												AutoHaki()
												EquipWeapon(_G.Select_Weapon)
												v.HumanoidRootPart.CanCollide = false
												v.Humanoid.WalkSpeed = 0
												v.HumanoidRootPart.Size = Vector3.new(50,50,50)
												getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
												sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
											until _G.Auto_Elite_Hunter == false or v.Humanoid.Health <= 0 or not v.Parent
										end
									end
								end
							else					
								if game:GetService("ReplicatedStorage"):FindFirstChild("Diablo") then
									if (game:GetService("ReplicatedStorage"):FindFirstChild("Diablo").HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo"))
										return
									end
									getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo").HumanoidRootPart.CFrame * MethodFarm)
								elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre") then
									if (game:GetService("ReplicatedStorage"):FindFirstChild("Deandre").HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre"))
										return
									end
									getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre").HumanoidRootPart.CFrame * MethodFarm)
								elseif game:GetService("ReplicatedStorage"):FindFirstChild("Urban") then
									if (game:GetService("ReplicatedStorage"):FindFirstChild("Urban").HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(game:GetService("ReplicatedStorage"):FindFirstChild("Urban"))
										return
									end
									getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild("Urban").HumanoidRootPart.CFrame * MethodFarm)
								end
							end                    
						end
					else
						if _G.Auto_Elite_Hunter_Hop and game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter") == "I don't have anything for you right now. Come back later." then
							Hop()
						else
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
						end
					end
				end)
			end
		end
	end)

	Main:Toggle("Auto Elite Hunter Hop",_G.imgToggle,false,function(value)
		_G.Auto_Elite_Hunter_Hop = value
		StopTween(_G.Auto_Elite_Hunter_Hop)
	end)

	Main:Seperator("Bone")

	local BoneCheck = Main:Label("Bone")

	spawn(function()
		while wait() do
			pcall(function()
				BoneCheck:Set("Bone : "..tostring(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Check")))
			end)
		end
	end)

	Main:Toggle("Auto Farm Bone",_G.imgToggle,false,function(value)
		_G.Auto_Farm_Bone = value
		StopTween(_G.Auto_Farm_Bone)
	end)
	
	spawn(function()
		while wait() do 
			if _G.Auto_Farm_Bone and World3 then
				pcall(function()
					if game:GetService("Workspace").Enemies:FindFirstChild("Reborn Skeleton") or game:GetService("Workspace").Enemies:FindFirstChild("Living Zombie") or game:GetService("Workspace").Enemies:FindFirstChild("Demonic Soul") or game:GetService("Workspace").Enemies:FindFirstChild("Posessed Mummy") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Reborn Skeleton" or v.Name == "Living Zombie" or v.Name == "Demonic Soul" or v.Name == "Posessed Mummy" then
								if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
									repeat task.wait()
										AutoHaki()
										EquipWeapon(_G.SelectWeapon)
										v.HumanoidRootPart.CanCollide = false
										v.Humanoid.WalkSpeed = 0
										v.Head.CanCollide = false 
										PosMonBone = true
										PosMonBone = v.HumanoidRootPart.CFrame
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
										game:GetService("VirtualUser"):CaptureController()
										game:GetService("VirtualUser"):Button1Down(Vector2.new(1280,672))
									until not _G.Auto_Farm_Bone or not v.Parent or v.Humanoid.Health <= 0
								end
							end
						end
					else
						PosMonBone = false
						for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do 
							if v.Name == "Reborn Skeleton" then
								getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
							elseif v.Name == "Living Zombie" then
								getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
							elseif v.Name == "Demonic Soul" then
								getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
							elseif v.Name == "Posessed Mummy" then
								getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
							end
						end
						if (CFrame.new(-9466.72949, 171.162918, 6132.01514).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(-9466.72949, 171.162918, 6132.01514))
							return
						end
						getgenv().ToTarget(CFrame.new(-9466.72949, 171.162918, 6132.01514))
					end
				end)
			end
		end
	end)

	Main:Toggle("Auto Random Bone",_G.imgToggle,false,function(value)
		_G.Auto_Random_Bone = value
	end)

	spawn(function()
		while wait(.1) do
			if _G.Auto_Random_Bone then
				local args = {
					[1] = "Bones",
					[2] = "Buy",
					[3] = 1,
					[4] = 1
				}

				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
		end
	end)

	Main:Seperator("Cake Prince")

	local MobKilled = Main:Label("Killed")

	spawn(function()
		while wait() do
			pcall(function()
				if string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 88 then
					MobKilled:SetText(" 🎂 Need Kill Mods : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,41))
				elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 87 then
					MobKilled:SetText(" 🎂 Need Kill Mods : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,40))
				elseif string.len(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")) == 86 then
					MobKilled:SetText(" 🎂 Need Kill Mods : "..string.sub(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),39,39))
				else
					MobKilled:SetText(" 🎂 Katakuri Is Spawning")
				end
			end)
		end
	end)

	Main:Toggle("Auto Cake Prince",_G.imgToggle,false,function(value)
		_G.Auto_Cake_Prince = value
		StopTween(_G.Auto_Cake_Prince)
	end)   

	
	spawn(function()
		while wait() do
			if _G.Auto_Cake_Prince then
				pcall(function()
					if game.ReplicatedStorage:FindFirstChild("Cake Prince") then   
						if game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do 
								if v.Name == "Cake Prince" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
									repeat wait()
										AutoHaki()
										EquipWeapon(_G.Select_Weapon)
										v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
										v.HumanoidRootPart.CanCollide = false
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until _G.Auto_Cake_Prince == false or not v.Parent or v.Humanoid.Health <= 0
								end    
							end    
						else
							for _,x in pairs(game.ReplicatedStorage:GetChildren()) do 
								if x.Name == "Cake Prince" then
									if (x.HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 1000 then
										getgenv().ToTarget(CFrame.new(-2145.89722, 70.0088272, -12399.6016, 0.99999702, 1.58276379e-08, 0.00245277886, -1.57982978e-08, 1, -1.19813057e-08, -0.00245277886, 1.19425199e-08, 0.99999702))
										return
									end
								end
							end
						end
					else
						if game:GetService("Workspace").Enemies:FindFirstChild("Cookie Crafter") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Guard") or game:GetService("Workspace").Enemies:FindFirstChild("Baking Staff") or game:GetService("Workspace").Enemies:FindFirstChild("Head Baker") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do  
								if v.Name == "Cookie Crafter" or v.Name == "Cake Guard" or v.Name == "Head Baker" or v.Name == "Baking Staff" then
									repeat wait()
										AutoHaki()
										EquipWeapon(_G.Select_Weapon)
										StartCakeMagnet = true
										v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)  
										POSCAKE = v.HumanoidRootPart.CFrame
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until _G.Auto_Cake_Prince == false or game:GetService("ReplicatedStorage"):FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or not v.Parent or v.Humanoid.Health <= 0
								end
							end
						else
							if (CFrame.new(-1820.0634765625, 210.74781799316406, -12297.49609375).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-1820.0634765625, 210.74781799316406, -12297.49609375))
								return
							end
							getgenv().ToTarget(CFrame.new(-1820.0634765625, 210.74781799316406, -12297.49609375))
							for i,v in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do
								if v.Name == "Cookie Crafter" or v.Name == "Cake Guard" or v.Name == "Head Baker" or v.Name == "Baking Staff" then
									local CFrameEnemySpawns = v.CFrame  wait(0.5)
									getgenv().ToTarget(CFrameEnemySpawns * MethodFarm)
								end
							end
						end
					end
				end)
			end
		end
	end)

	Main:Toggle("Auto Spawn Cake Prince",_G.imgToggle,false,function(value)
		_G.Auto_Spawn_Cake_Prince = value
	end)

	spawn(function()
		while wait() do
			if _G.Auto_Spawn_Cake_Prince then
				local args = {
					[1] = "CakePrinceSpawner",
					[2] = true
				}

				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))                    
				local args = {
					[1] = "CakePrinceSpawner"
				}

				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
		end
	end)

	Main:Seperator("Buddy Sword")

	Main:Toggle("Auto Buddy Sword",_G.imgToggle,false,function(value)
		_G.Auto_Farm_Boss_Hallow = value
		StopTween(_G.Auto_Farm_Boss_Hallow)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Buddy_Sword then
					if game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Cake Queen [Lv. 2175] [Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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
								until not _G.Auto_Buddy_Sword or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						if (CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438))
							return
						end
						getgenv().ToTarget(CFrame.new(5525.7045898438, 262.90060424805, -6755.1186523438))
					end
				else 
					if _G.Auto_Buddy_Sword_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
						Hop()
					end
				end
			end)
		end
	end)

	Main:Toggle("Auto Buddy Sword Hop",_G.imgToggle,false,function(value)
		_G.Auto_Buddy_Sword_Hop = value
		StopTween(_G.Auto_Buddy_Sword_Hop)
	end)

	Main:Seperator("Boss Hallow")

	Main:Toggle("Auto Farm Boss Hallow",_G.imgToggle,false,function(value)
		_G.Auto_Farm_Boss_Hallow = value
		StopTween(_G.Auto_Farm_Boss_Hallow)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Farm_Boss_Hallow then
					if game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Soul Reaper" then
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
								until v.Humanoid.Health <= 0 or not _G.Auto_Farm_Boss_Hallow
								StartMagnet = false
							end
						end
					else
						if (CFrame.new(-9524.7890625, 315.80429077148, 6655.7192382813).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(-9524.7890625, 315.80429077148, 6655.7192382813))
							return
						end
						getgenv().ToTarget(CFrame.new(-9524.7890625, 315.80429077148, 6655.7192382813))
					end
				else 
					if _G.Auto_Farm_Boss_Hallow_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						Hop()
					end
				end
			end)
		end
	end)

	Main:Toggle("Auto Farm Boss Hallow Hop",_G.imgToggle,false,function(value)
		_G.Auto_Farm_Boss_Hallow_Hop = value
	end)

	Main:Seperator("Twin Hook")

	Main:Toggle("Auto Twin Hook",_G.imgToggle,false,function(value)
		_G.Auto_Twin_Hook = value
		StopTween(_G.Auto_Twin_Hook)
	end)

	spawn(function()
		while wait() do
			if _G.Auto_Twin_Hook then
				pcall(function()
					if _G.Auto_Twin_Hook and game.ReplicatedStorage:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") or game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
						if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Captain Elephant [Lv. 1875] [Boss]" and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
									repeat wait()
										AutoHaki()
										EquipWeapon(_G.Select_Weapon)
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
									until _G.Auto_Twin_Hook or v.Humanoid.Health <= 0 or not v.Parent
								end
							end
						else
							if (CFrame.new(-13348.0654296875, 405.8904113769531, -8570.62890625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-13348.0654296875, 405.8904113769531, -8570.62890625))
								return
							end
							getgenv().ToTarget(CFrame.new(-13348.0654296875, 405.8904113769531, -8570.62890625))
						end
					else
						if _G.Auto_Twin_Hook_Hop then
							Hop()
						end
					end
				end)
			end
		end
	end)

	Main:Toggle("Auto Twin Hook Hop",_G.imgToggle,false,function(value)
		_G.Auto_Twin_Hook_Hop = value
	end)

	Main:Seperator("Cavander")

	Main:Toggle("Auto Cavander",_G.imgToggle,false,function(value)
		_G.Auto_Cavander = value
		StopTween(_G.Auto_Cavander)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Cavander then
					if game:GetService("Workspace").Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Beautiful Pirate [Lv. 1950] [Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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
								until not _G.Auto_Cavander or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						if _G.Auto_Cavander_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
							wait(10)
							Hop()
						else						
							if (CFrame.new(5283.609375, 22.56223487854, -110.78285217285).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(5283.609375, 22.56223487854, -110.78285217285))
								return
							end
							getgenv().ToTarget(CFrame.new(5283.609375, 22.56223487854, -110.78285217285))
						end
					end
				end
			end)
		end
	end)

	Main:Toggle("Auto Cavander Hop",_G.imgToggle,false,function(value)
		_G.Auto_Cavander_Hop = value
	end)

	Main:Seperator("Yama")

	Main:Toggle("Auto Yama",_G.imgToggle,false,function(value)
		_G.Auto_Yama = value
		StopTween(_G.Auto_Yama)
	end)

	local Yama_All_Mon = {
		["Mon Quest"] = {"Diablo [Lv. 1750]","Deandre [Lv. 1750]","Urban [Lv. 1750]"},
		["Mon"] = {"Diablo","Deandre","Urban"},
		["Item"] = "God's Chalice",
	}

	spawn(function()
		while wait() do
			if _G.Auto_Yama then
				pcall(function()
					if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter","Progress") >= 30 then
						fireclickdetector(game:GetService("Workspace").Map.Waterfall.SealedKatana.Handle.ClickDetector)
					else
						local QuestUI = game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest
						for _,_l1 in ipairs(Yama_All_Mon["Mon Quest"]) do
							for _,l in ipairs(Yama_All_Mon["Mon"]) do
								if QuestUI.Visible == true then
									if game:GetService("Workspace").Enemies:FindFirstChild(_l1) or game:GetService("ReplicatedStorage"):FindFirstChild(_l1) then
										for _,_v1 in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
											if _v1.Name == _l1 then
												if _v1:FindFirstChild("Humanoid") and _v1:FindFirstChild("HumanoidRootPart") and _v1.Humanoid.Health > 0 then
													repeat wait()
														_v1.HumanoidRootPart.Size = Vector3.new(60,60,60)
														_v1.HumanoidRootPart.CanCollide = false
														_v1.Head.CanCollide = false
														BringMobFarm = true
														EquipWeapon(_G.Select_Weapon)
														_v1.HumanoidRootPart.Transparency = 1
														getgenv().ToTarget(_v1.HumanoidRootPart.CFrame * MethodFarm)
													until not _G.Auto_Yama or _v1.Humanoid.Health <= 0 or not _v1.Parent
												end
											else
												if (game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
													BTP(game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame)
													return
												end
												getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame * MethodFarm)
											end
										end
									end
								else
									if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter") == "I don't have anything for you right now. Come back later." and not ( game:GetService("Workspace").Enemies:FindFirstChild(_l1) or game:GetService("ReplicatedStorage"):FindFirstChild(_l1) ) then
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
										if (game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
											BTP(game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame)
											return
										end
										getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild(_l1).HumanoidRootPart.CFrame * MethodFarm)
									end
								end
							end
						end
					end
				end)
			end
		end
	end)

	Main:Seperator("Tushita")

	Main:Toggle("Auto Tushita",_G.imgToggle,false,function(value)
		_G.Auto_Tushita = value
		StopTween(_G.Auto_Tushita)
	end)

	spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Tushita then
					if game:GetService("Workspace").Map.Turtle.TushitaGate:GetChildren()[2].Transparency == 1 or game:GetService("Workspace").Map.Turtle.TushitaGate:GetChildren()[1].Transparency == 1 then
						if #game:GetService("Workspace").Enemies:GetChildren() > 0 then
							if game:GetService("Workspace").Enemies:FindFirstChild("Longma [Lv. 2000] [Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Longma [Lv. 2000] [Boss]") then
								for _,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Longma [Lv. 2000] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat wait()
											v.HumanoidRootPart.Size = Vector3.new(60,60,60)
											v.HumanoidRootPart.CanCollide = false
											v.Head.CanCollide = false
											BringMobFarm = true
											AutoHaki()
											EquipWeapon(_G.Select_Weapon)
											v.HumanoidRootPart.Transparency = 1
											getgenv().ToTarget(v.HumanoidRootPart.CFrame * MethodFarm)
										until not __G.Auto_Tushita or not v.Humanoid.Health <= 0 or not v.Parent
									else
										if (game:GetService("ReplicatedStorage"):FindFirstChild("Longma [Lv. 2000] [Boss]").HumanoidRootPart.CFrame.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
											BTP(game:GetService("ReplicatedStorage"):FindFirstChild("Longma [Lv. 2000] [Boss]").HumanoidRootPart.CFrame * MethodFarm)
											return
										end
										getgenv().ToTarget(game:GetService("ReplicatedStorage"):FindFirstChild("Longma [Lv. 2000] [Boss]").HumanoidRootPart.CFrame * MethodFarm)
									end
								end
							end
						end
					else
						if game:GetService("Workspace").Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
							if game:GetService("Players").LocalPlayer.Data.LastSpawnPoint.Value == tostring(GetIsLand(CFrame.new(-13274.528320313, 531.82073974609, -7579.22265625))) then
								wait(1)
								repeat getgenv().ToTarget(CFrame.new(-10752, 417, -9366)) wait() until not _G.Auto_Holy_Torch or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-10752, 417, -9366)).Magnitude <= 1
								wait(1)
								repeat getgenv().ToTarget(CFrame.new(-11672, 334, -9474)) wait() until not _G.Auto_Holy_Torch or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-11672, 334, -9474)).Magnitude <= 1
								wait(1)
								repeat getgenv().ToTarget(CFrame.new(-12132, 521, -10655)) wait() until not _G.Auto_Holy_Torch or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-12132, 521, -10655)).Magnitude <= 1
								wait(1)
								repeat getgenv().ToTarget(CFrame.new(-13336, 486, -6985)) wait() until not _G.Auto_Holy_Torch or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13336, 486, -6985)).Magnitude <= 1
								wait(1)
								repeat getgenv().ToTarget(CFrame.new(-13489, 332, -7925)) wait() until not _G.Auto_Holy_Torch or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13489, 332, -7925)).Magnitude <= 1
							else
								if (CFrame.new(5148.03613, 162.352493, 910.548218, 0, 0, -1, 0, 1, 0, 1, 0, 0).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(5148.03613, 162.352493, 910.548218, 0, 0, -1, 0, 1, 0, 1, 0, 0))
									return
								end
								getgenv().ToTarget(CFrame.new(5148.03613, 162.352493, 910.548218, 0, 0, -1, 0, 1, 0, 1, 0, 0))
								wait(2.5)
								return
							end
						end
					end
				else
					_G.Auto_Tushita = false
				end
			end)
		end
	end)

--[[
    Main:Seperator("Cursed Dual Katana")

    Main:Toggle("Auto Cursed Dual Katana",_G.imgToggle,false,function(value)
        _G.Auto_Cursed_Dual_Katana = value
        StopTween(_G.Auto_Cursed_Dual_Katana)
    end)

	spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Cursed_Dual_Katana then
					if GetWeaponInventory("Cursed Dual Katana") == true then
						if game.Players.LocalPlayer.Character:FindFirstChild("Cursed Dual Katana") or game.Players.LocalPlayer.Backpack:FindFirstChild("Cursed Dual Katana") then

						else
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadItem","Cursed Dual Katana")
						end
					else
						if game.Players.LocalPlayer.Character:FindFirstChild("Tushita") or game.Players.LocalPlayer.Backpack:FindFirstChild("Tushita") or game.Players.LocalPlayer.Character:FindFirstChild("Yama") or game.Players.LocalPlayer.Backpack:FindFirstChild("Yama") then
							if game.Players.LocalPlayer.Character:FindFirstChild("Tushita") or game.Players.LocalPlayer.Backpack:FindFirstChild("Tushita") then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Tushita") then
									EquipWeapon("Tushita")
								else
									for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
										if v.Name == "Tushita" and v:IsA("Tool") then
											if v.Level.Value >= 350 then
												game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadItem","Yama")
												_G.Auto_Farm_Bone = false
											else
												_G.Select_Weapon = "Tushita"
												_G.Auto_Farm_Bone = true
											end
										end
									end
								end
							elseif game.Players.LocalPlayer.Character:FindFirstChild("Yama") or game.Players.LocalPlayer.Backpack:FindFirstChild("Yama") then
								if game.Players.LocalPlayer.Backpack:FindFirstChild("Yama") then
									EquipWeapon("Yama")
								else
									for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
										if v.Name == "Yama" and v:IsA("Tool") then
											if v.Level.Value >= 350 then
												Auto_CDK_Quest = true
												_G.Auto_Farm_Bone = false
											else
												_G.Select_Weapon = "Yama"
												_G.Auto_Farm_Bone = true
											end
										end
									end
								end
							end
						else
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadItem","Tushita")
						end      
					end
				end
			end)
		end
	end)


	spawn(function()
		while wait() do
			pcall(function()
				if Auto_CDK_Quest then
					if GetMaterial("Alucard Fragment") == 0 then
						Auto_Quest_Yama_1 = true
						Auto_Quest_Yama_2 = false
						Auto_Quest_Yama_3 = false
						Auto_Quest_Tushita_1 = false
						Auto_Quest_Tushita_2 = false
						Auto_Quest_Tushita_3 = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Evil")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Evil")
					elseif GetMaterial("Alucard Fragment") == 1 then
						Auto_Quest_Yama_1 = false
						Auto_Quest_Yama_2 = true
						Auto_Quest_Yama_3 = false
						Auto_Quest_Tushita_1 = false
						Auto_Quest_Tushita_2 = false
						Auto_Quest_Tushita_3 = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Evil")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Evil")
					elseif GetMaterial("Alucard Fragment") == 2 then
						Auto_Quest_Yama_1 = false
						Auto_Quest_Yama_2 = false
						Auto_Quest_Yama_3 = true
						Auto_Quest_Tushita_1 = false
						Auto_Quest_Tushita_2 = false
						Auto_Quest_Tushita_3 = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Evil")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Evil")
					elseif GetMaterial("Alucard Fragment") == 3 then
						Auto_Quest_Yama_1 = false
						Auto_Quest_Yama_2 = false
						Auto_Quest_Yama_3 = false
						Auto_Quest_Tushita_1 = true
						Auto_Quest_Tushita_2 = false
						Auto_Quest_Tushita_3 = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Good")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Good")
					elseif GetMaterial("Alucard Fragment") == 4 then
						Auto_Quest_Yama_1 = false
						Auto_Quest_Yama_2 = false
						Auto_Quest_Yama_3 = false
						Auto_Quest_Tushita_1 = false
						Auto_Quest_Tushita_2 = true
						Auto_Quest_Tushita_3 = false
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Good")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Good")
					elseif GetMaterial("Alucard Fragment") == 5 then
						Auto_Quest_Yama_1 = false
						Auto_Quest_Yama_2 = false
						Auto_Quest_Yama_3 = false
						Auto_Quest_Tushita_1 = false
						Auto_Quest_Tushita_2 = false
						Auto_Quest_Tushita_3 = true
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Good")
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Good")
					elseif GetMaterial("Alucard Fragment") == 6 then
						if game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton Boss [Lv. 2025] [Boss]") or game:GetService("Workspace").ReplicatedStorage:FindFirstChild("Cursed Skeleton Boss [Lv. 2025] [Boss]") then
							Auto_Quest_Yama_1 = false
							Auto_Quest_Yama_2 = false
							Auto_Quest_Yama_3 = false
							Auto_Quest_Tushita_1 = false
							Auto_Quest_Tushita_2 = false
							Auto_Quest_Tushita_3 = false
							if game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton Boss [Lv. 2025] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton [Lv. 2200]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if string.find(v.Name,"Cursed Skeleton Boss [Lv. 2025] [Boss]") or string.find(v.Name,"Cursed Skeleton [Lv. 2200]") then
										if v.Humanoid.Health > 0 then
											v.HumanoidRootPart.CanCollide = false
											v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
											getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,50,0))
											game:GetService'VirtualUser':CaptureController()
											game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
										end
									end
								end
							end
						else
							if (CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 100 then
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Good")
								wait(1)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress","Evil")
								wait(1)
								getgenv().ToTarget(CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875))
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)
								getgenv().ToTarget(CFrame.new(-12253.5419921875, 598.8999633789062, -6546.8388671875))
							else
								getgenv().ToTarget(CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875))
							end   
						end
					end
				end
			end)
		end
	end)


	spawn(function()
		while wait() do
			if Auto_Quest_Yama_1 then
				pcall(function()
					if game:GetService("Workspace").Enemies:FindFirstChild("Mythological Pirate [Lv. 1850]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if string.find(v.Name,"Mythological Pirate [Lv. 1850]") then
								repeat wait()
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,0,-2))
								until not Auto_CDK_Quest or not Auto_Cursed_Dual_Katana 
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Evil")
							end
						end
					else
						getgenv().ToTarget(CFrame.new(-13451.46484375, 543.712890625, -6961.0029296875))
					end
				end)
			end
		end
	end)

	spawn(function()
		while wait() do
			pcall(function()
				if Auto_Quest_Yama_2 then
					for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if v:FindFirstChild("HazeESP") then
							v.HazeESP.Size = UDim2.new(50,50,50,50)
							v.HazeESP.MaxDistance = "inf"
						end
					end
					for i,v in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
						if v:FindFirstChild("HazeESP") then
							v.HazeESP.Size = UDim2.new(50,50,50,50)
							v.HazeESP.MaxDistance = "inf"
						end
					end
				end
			end)
		end
	end)

	spawn(function()
		while wait() do
			pcall(function()
				for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
					if Auto_Quest_Yama_2 and v:FindFirstChild("HazeESP") and (v.HumanoidRootPart.Position - PosMonsEsp.Position).magnitude <= 300 then
						v.HumanoidRootPart.CFrame = PosMonsEsp
						v.HumanoidRootPart.CanCollide = false
						v.HumanoidRootPart.Size = Vector3.new(50,50,50)
						if not v.HumanoidRootPart:FindFirstChild("BodyVelocity") then
							local vc = Instance.new("BodyVelocity", v.HumanoidRootPart)
							vc.MaxForce = Vector3.new(1, 1, 1) * math.huge
							vc.Velocity = Vector3.new(0, 0, 0)
						end
					end
				end
			end)
		end
	end)

	spawn(function()
		while wait() do
			if Auto_Quest_Yama_2 then 
				pcall(function() 
					for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if v:FindFirstChild("HazeESP") then
							repeat wait()
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(v.HumanoidRootPart.CFrameMon* CFrame.new(0,20,0))
								else
									StartMagnet = true
									EquipWeapon(_G.Select_Weapon)
									PosMonsEsp = v.HumanoidRootPart.CFrame
									v.HumanoidRootPart.Size = Vector3.new(60,60,60)
									v.Humanoid.JumpPower = 0
									v.Humanoid.WalkSpeed = 0
									v.HumanoidRootPart.CanCollide = false
									v.Humanoid:ChangeState(11)
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,20,0))								
								end      
							until _G.Auto_Cursed_Dual_Katana == false or Auto_Quest_Yama_2 == false or not v.Parent or v.Humanoid.Health <= 0 or not v:FindFirstChild("HazeESP")
						else
							for x,y in pairs(game:GetService("ReplicatedStorage"):GetChildren()) do
								if y:FindFirstChild("HazeESP") then
									if (y.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
										BTP(y.HumanoidRootPart.CFrameMon* CFrame.new(0,20,0))
									else
										getgenv().ToTarget(y.HumanoidRootPart.CFrame * CFrame.new(0,20,0))
									end
								end
							end
						end
					end
				end)
			end
		end
	end)

	spawn(function()
		while wait() do
			if Auto_Quest_Yama_3 then
				pcall(function()
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") then         
						_G.Auto_Farm_Bone = false           
						getgenv().ToTarget(game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.CFrame)
					elseif game:GetService("Workspace").Map:FindFirstChild("HellDimension") then
						repeat wait()
							if game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton [Lv. 2200]") or game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton [Lv. 2200] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Hell's Messenger [Lv. 2200] [Boss]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if string.find(v.Name,"Cursed Skeleton [Lv. 2200]") or string.find(v.Name,"Cursed Skeleton [Lv. 2200] [Boss]") or string.find(v.Name,"Hell's Messenger [Lv. 2200] [Boss]") then
										if v.Humanoid.Health > 0 then
											repeat wait()
												StartMagnet = true
												EquipWeapon(_G.Select_Weapon)
												PosMonsEsp = v.HumanoidRootPart.CFrame
												v.HumanoidRootPart.Size = Vector3.new(60,60,60)
												v.Humanoid.JumpPower = 0
												v.Humanoid.WalkSpeed = 0
												v.HumanoidRootPart.CanCollide = false
												v.Humanoid:ChangeState(11)
												getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,50,0))
											until v.Humanoid.Health <= 0 or not v.Parent or Auto_Quest_Yama_3 == false
										end
									end
								end
							else
								wait(5)
								getgenv().ToTarget(game:GetService("Workspace").Map.HellDimension.Torch1.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)        
								getgenv().ToTarget(game:GetService("Workspace").Map.HellDimension.Torch2.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)     
								getgenv().ToTarget().ToTarget(game:GetService("Workspace").Map.HellDimension.Torch3.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)     
								getgenv().ToTarget().ToTarget(game:GetService("Workspace").Map.HellDimension.Exit.CFrame)
							end
						until _G.Auto_Cursed_Dual_Katana == false or Auto_Quest_Yama_3 == false or GetMaterial("Alucard Fragment") == 3
					else
						if game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
							if game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if string.find(v.Name,"Soul Reaper [Lv. 2100] [Raid Boss]") then
										if v.Humanoid.Health > 0 then
											repeat wait()
												getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,0,-2))
											until _G.Auto_Cursed_Dual_Katana == false or Auto_Quest_Yama_3 == false or game:GetService("Workspace").Map:FindFirstChild("HellDimension")
										end
									end
								end
							else
								getgenv().ToTarget(CFrame.new(-9570.033203125, 315.9346923828125, 6726.89306640625))
							end
						else
							_G.Auto_Farm_Bone = true
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
						end
					end
				end)
			end
		end
	end)

	spawn(function() 
		while wait() do
			if Auto_Quest_Tushita_1 then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","BoatQuest",workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
			end
		end
	end)

	spawn(function()
		while wait() do
			if Auto_Quest_Tushita_1 then
				BTP(CFrame.new(-9546.990234375, 21.139892578125, 4686.1142578125))
				wait(5)
				BTP(CFrame.new(-6120.0576171875, 16.455780029296875, -2250.697265625))
				wait(5)
				BTP(CFrame.new(-9533.2392578125, 7.254445552825928, -8372.69921875))    
			end
		end
	end)

	spawn(function()
		while wait() do
			if Auto_Quest_Tushita_2 then
				pcall(function()
					if (CFrame.new(-5539.3115234375, 313.800537109375, -2972.372314453125).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 500 then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if Auto_Quest_Tushita_2 and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude < 2000 then
									repeat wait()
										v.HumanoidRootPart.CanCollide = false
										v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
										getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,50,0))
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
									until v.Humanoid.Health <= 0 or not v.Parent or Auto_Quest_Tushita_2 == false
								end
							end
						end
					else
						getgenv().ToTarget(CFrame.new(-5545.1240234375, 313.800537109375, -2976.616455078125))
					end
				end)
			end
		end
	end)

	spawn(function()
		while wait() do
			if Auto_Quest_Tushita_3 then
				pcall(function()
					if game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") or game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if string.find(v.Name,"Cake Queen [Lv. 2175] [Boss]") then
									if v.Humanoid.Health > 0 then
										repeat wait()
											AutoHaki()
											EquipWeapon(_G.Select_Weapon)
											v.HumanoidRootPart.Size = Vector3.new(60,60,60)
											v.Humanoid.JumpPower = 0
											v.Humanoid.WalkSpeed = 0
											v.HumanoidRootPart.CanCollide = false
											v.Humanoid:ChangeState(11)
											getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,50,0))
										until _G.Auto_Cursed_Dual_Katana == false or Auto_Quest_Tushita_3 == false or game:GetService("Workspace").Map:FindFirstChild("HeavenlyDimension")
									end
								end
							end
						else
							getgenv().ToTarget(CFrame.new(-709.3132934570312, 381.6005859375, -11011.396484375))
						end
					elseif game:GetService("Workspace").Map:FindFirstChild("HeavenlyDimension") then
						repeat wait()
							if game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton [Lv. 2200]") or game:GetService("Workspace").Enemies:FindFirstChild("Cursed Skeleton [Lv. 2200] [Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Heaven's Guardian [Lv. 2200] [Boss]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if string.find(v.Name,"Cursed Skeleton [Lv. 2200]") or string.find(v.Name,"Cursed Skeleton [Lv. 2200] [Boss]") or string.find(v.Name,"Heaven's Guardian [Lv. 2200] [Boss]") then
										if v.Humanoid.Health > 0 then
											repeat wait()
												AutoHaki()
												EquipWeapon(_G.Select_Weapon)
												v.HumanoidRootPart.Size = Vector3.new(60,60,60)
												v.Humanoid.JumpPower = 0
												v.Humanoid.WalkSpeed = 0
												v.HumanoidRootPart.CanCollide = false
												v.Humanoid:ChangeState(11)
											until v.Humanoid.Health <= 0 or not v.Parent or Auto_Quest_Tushita_3 == false
										end
									end
								end
							else
								wait(5)
								getgenv().ToTarget(game:GetService("Workspace").Map.HeavenlyDimension.Torch1.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)        
								getgenv().ToTarget(game:GetService("Workspace").Map.HeavenlyDimension.Torch2.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)     
								getgenv().ToTarget(game:GetService("Workspace").Map.HeavenlyDimension.Torch3.CFrame)
								wait(1.5)
								game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
								wait(1.5)     
								getgenv().ToTarget(game:GetService("Workspace").Map.HeavenlyDimension.Exit.CFrame)
							end
						until _G.Auto_Cursed_Dual_Katana == false or Auto_Quest_Tushita_3 == false or GetMaterial("Alucard Fragment") == 6
					else
						Hop()
					end
				end)
			end
		end
	end)

	Tushita_Quest1 = nil
	-- Page_Main.Button({Title = "Tushita Quest : 1",callback = function()
	-- 	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("LoadItem","Tushita")
	-- 	wait(1)
	-- 	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial","Good")
	-- 	Tushita_Quest1 = true
	-- 	toTarget(CFrame.new(-6127.5712890625, 16.446542739868164, -2247.595703125))
	-- 	wait(60)
	-- 	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
	-- 	wait(1)
	-- 	toTarget(CFrame.new(-127.23313903808594, 6.755744934082031, 5259.51025390625))    
	-- 	wait(60)
	-- 	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
	-- 	wait(1)
	-- 	toTarget(CFrame.new(-2067.349365234375, 4.701088905334473, -9890.4501953125))
	-- 	wait(60)
	-- 	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
	-- 	Tushita_Quest1 = false
	-- end})
]]--
	Main:Seperator("Serpent Bow")

	Main:Toggle("Auto Serpent Bow",_G.imgToggle,false,function(value)
		_G.Auto_Serpent_Bow = value
		StopTween(_G.Auto_Serpent_Bow)
	end)

	task.spawn(function()
		while wait() do
			if _G.Auto_Serpent_Bow then
				if game:GetService("Workspace").Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
					for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
						if v.Name == "Island Empress [Lv. 1675] [Boss]" or v.Name == "Island Empress [Lv. 1675] [Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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
							until not _G.Auto_Serpent_Bow or not v.Parent or v.Humanoid.Health <= 0
							StartMagnet = false
						end
					end
				else
					if _G.Auto_Serpent_Bow_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
						Hop()
					else
						if (CFrame.new(5543.86328125, 668.97399902344, 199.0341796875).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(5543.86328125, 668.97399902344, 199.0341796875))
							return
						end
						getgenv().ToTarget(CFrame.new(5543.86328125, 668.97399902344, 199.0341796875))
					end
				end
			end
		end
	end)

	Main:Toggle("Auto Serpent Bow Hop",_G.imgToggle,false,function(value)
		_G.Auto_Serpent_Bow_Hop = value
	end)

	Main:Seperator("Dark Dagger")

	Main:Toggle("Auto Dark Dagger Hop",_G.imgToggle,false,function(value)
		_G.Auto_Dark_Dagger = value
		StopTween(_G.Auto_Dark_Dagger)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Dark_Dagger then
					if game:GetService("Workspace").Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
						for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "rip_indra True Form [Lv. 5000] [Raid Boss]" and v.Humanoid.Health > 0 and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") then
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
								until not _G.Auto_Dark_Dagger or not v.Parent or v.Humanoid.Health <= 0
								StartMagnet = false
							end
						end
					else
						if _G.Auto_Dark_Dagger_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
							Hop()
						else
							if (CFrame.new(-5344.822265625, 423.98541259766, -2725.0930175781).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-5344.822265625, 423.98541259766, -2725.0930175781))
								return
							end
							getgenv().ToTarget(CFrame.new(-5344.822265625, 423.98541259766, -2725.0930175781))
						end
					end
				end
			end)
		end
	end)	

	Main:Toggle("Auto Dark Dagger Hop",_G.imgToggle,false,function(value)
		_G.Auto_Dark_Dagger_Hop = value
	end)

	Main:Seperator("Rainbow Haki")

	Main:Toggle("Auto Rainbow Haki",_G.imgToggle,false,function(value)
		_G.Auto_Rainbow_Haki = value
		StopTween(_G.Auto_Rainbow_Haki)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Rainbow_Haki then
					if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						getgenv().ToTarget(CFrame.new(-11892.0703125, 930.57672119141, -8760.1591796875))
						if (Vector3.new(-11892.0703125, 930.57672119141, -8760.1591796875) - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 30 then
							wait(1.5)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("HornedMan","Bet")
						end
					elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true and string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Stone") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Stone [Lv. 1550] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
							if v.Name == "Stone [Lv. 1550] [Boss]" then
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
									until not _G.Auto_Rainbow_Haki or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
									StartMagnet = false
								end
							end
						else
							if _G.Auto_Rainbow_Haki_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Stone [Lv. 1550] [Boss]") then
								wait(10)
								Hop()
							else
								if (CFrame.new(-1086.11621, 38.8425903, 6768.71436, 0.0231462717, -0.592676699, 0.805107772, 2.03251839e-05, 0.805323839, 0.592835128, -0.999732077, -0.0137055516, 0.0186523199).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(CFrame.new(-1086.11621, 38.8425903, 6768.71436, 0.0231462717, -0.592676699, 0.805107772, 2.03251839e-05, 0.805323839, 0.592835128, -0.999732077, -0.0137055516, 0.0186523199)))
									return
								end
								getgenv().ToTarget(CFrame.new(-1086.11621, 38.8425903, 6768.71436, 0.0231462717, -0.592676699, 0.805107772, 2.03251839e-05, 0.805323839, 0.592835128, -0.999732077, -0.0137055516, 0.0186523199))
							end
						end
					elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true and string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Island Empress") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Island Empress [Lv. 1675] [Boss]" then
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
									until not _G.Auto_Rainbow_Haki or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
									StartMagnet = false
								end
							end
						else
							if _G.Auto_Rainbow_Haki_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
								wait(10)
								Hop()
							else
								if (CFrame.new(5713.98877, 601.922974, 202.751251, -0.101080291, -0, -0.994878292, -0, 1, -0, 0.994878292, 0, -0.101080291).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(5713.98877, 601.922974, 202.751251, -0.101080291, -0, -0.994878292, -0, 1, -0, 0.994878292, 0, -0.101080291))
									return
								end
								getgenv().ToTarget(CFrame.new(5713.98877, 601.922974, 202.751251, -0.101080291, -0, -0.994878292, -0, 1, -0, 0.994878292, 0, -0.101080291))
							end
						end
					elseif string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Kilo Admiral") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Kilo Admiral [Lv. 1750] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Kilo Admiral [Lv. 1750] [Boss]" then
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
									until not _G.Auto_Rainbow_Haki or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
									StartMagnet = false
								end
							end
						else
							if _G.Auto_Rainbow_Haki_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Kilo Admiral [Lv. 1750] [Boss]") then
								wait(10)
								Hop()
							else
								if (CFrame.new(2877.61743, 423.558685, -7207.31006, -0.989591599, -0, -0.143904909, -0, 1.00000012, -0, 0.143904924, 0, -0.989591479).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(2877.61743, 423.558685, -7207.31006, -0.989591599, -0, -0.143904909, -0, 1.00000012, -0, 0.143904924, 0, -0.989591479))
									return
								end
								getgenv().ToTarget(CFrame.new(2877.61743, 423.558685, -7207.31006, -0.989591599, -0, -0.143904909, -0, 1.00000012, -0, 0.143904924, 0, -0.989591479))
							end
						end
					elseif string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Captain Elephant") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Captain Elephant [Lv. 1875] [Boss]" then
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
									until not _G.Auto_Rainbow_Haki or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
									StartMagnet = false
								end
							end
						else
							if _G.Auto_Rainbow_Haki_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
								wait(10)
								Hop()
							else
								if (CFrame.new(-13485.0283, 331.709259, -8012.4873, 0.714521289, 7.98849911e-08, 0.69961375, -1.02065748e-07, 1, -9.94383065e-09, -0.69961375, -6.43015241e-08, 0.714521289).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(-13485.0283, 331.709259, -8012.4873, 0.714521289, 7.98849911e-08, 0.69961375, -1.02065748e-07, 1, -9.94383065e-09, -0.69961375, -6.43015241e-08, 0.714521289))
									return
								end
								getgenv().ToTarget(CFrame.new(-13485.0283, 331.709259, -8012.4873, 0.714521289, 7.98849911e-08, 0.69961375, -1.02065748e-07, 1, -9.94383065e-09, -0.69961375, -6.43015241e-08, 0.714521289))
							end
						end
					elseif string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Beautiful Pirate") then
						if game:GetService("Workspace").Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
							for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
								if v.Name == "Beautiful Pirate [Lv. 1950] [Boss]" then
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
									until not _G.Auto_Rainbow_Haki or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
									StartMagnet = false
								end
							end
						else
							if _G.Auto_Rainbow_Haki_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
								wait(10)
								Hop()
							else
								if (CFrame.new(5312.3598632813, 20.141201019287, -10.158538818359).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(5312.3598632813, 20.141201019287, -10.158538818359))
									return
								end
								getgenv().ToTarget(CFrame.new(5312.3598632813, 20.141201019287, -10.158538818359))
							end
						end
					else
						if (CFrame.new(-11892.0703125, 930.57672119141, -8760.1591796875).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(-11892.0703125, 930.57672119141, -8760.1591796875))
							return
						end
						getgenv().ToTarget(CFrame.new(-11892.0703125, 930.57672119141, -8760.1591796875))
						if (Vector3.new(-11892.0703125, 930.57672119141, -8760.1591796875) - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 30 then
							wait(1.5)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("HornedMan","Bet")
						end
					end
				end
			end)
		end
	end)

	Main:Toggle("Auto Rainbow Haki Hop",_G.imgToggle,false,function(value)
		_G.Auto_Rainbow_Haki_Hop = value
		StopTween(_G.Auto_Rainbow_Haki_Hop)
	end)

	Main:Seperator("Musketeer")

	Main:Toggle("Auto Musketeer Hati",_G.imgToggle,false,function(value)
		_G.Auto_Musketeer_Hat = value
		StopTween(_G.Auto_Musketeer_Hat)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Musketeer_Hat then
					if game:GetService("Players").LocalPlayer.Data.Level.Value >= 1800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress").KilledBandits == false then
						if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Forest Pirate") and string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
							if game:GetService("Workspace").Enemies:FindFirstChild("Forest Pirate [Lv. 1825]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Forest Pirate [Lv. 1825]" then
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
										until not _G.Auto_Musketeer_Hat or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
										StartMagnet = false
									end
								end
							else
								if (CFrame.new(-13206.452148438, 425.89199829102, -7964.5537109375).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
									BTP(CFrame.new(-13206.452148438, 425.89199829102, -7964.5537109375))
									return
								end
								getgenv().ToTarget(CFrame.new(-13206.452148438, 425.89199829102, -7964.5537109375))
							end
						else
							if (CFrame.new(-12443.8671875, 332.40396118164, -7675.4892578125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-12443.8671875, 332.40396118164, -7675.4892578125))
								return
							end
							getgenv().ToTarget(CFrame.new(-12443.8671875, 332.40396118164, -7675.4892578125))
							if (Vector3.new(-12443.8671875, 332.40396118164, -7675.4892578125) - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 30 then
								wait(1.5)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","CitizenQuest",1)
							end
						end
					elseif game:GetService("Players").LocalPlayer.Data.Level.Value >= 1800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress").KilledBoss == false then
						if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible and string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Captain Elephant") and game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
							if game:GetService("Workspace").Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Captain Elephant [Lv. 1875] [Boss]" then
										OldCFrameElephant = v.HumanoidRootPart.CFrame
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
										until not  _G.Auto_Musketeer_Hat or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
										StartMagnet = false
									end
								end
							else
								if  _G.Auto_Musketeer_Hat_Hop and not game:GetService("Workspace").Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
									wait(10)
									Hop()
								else
									getgenv().ToTarget(CFrame.new(-13374.889648438, 421.27752685547, -8225.208984375))
								end
							end
						else
							getgenv().ToTarget(CFrame.new(-12443.8671875, 332.40396118164, -7675.4892578125))
							if (CFrame.new(-12443.8671875, 332.40396118164, -7675.4892578125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 4 then
								wait(1.5)
								game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen")
							end
						end
					elseif game:GetService("Players").LocalPlayer.Data.Level.Value >= 1800 and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen") == 2 then
						if (CFrame.new(-12512.138671875, 340.39279174805, -9872.8203125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
							BTP(CFrame.new(-12512.138671875, 340.39279174805, -9872.8203125))
							return
						end
						getgenv().ToTarget(CFrame.new(-12512.138671875, 340.39279174805, -9872.8203125))
					end
				end
			end)
		end
	end)

	Main:Toggle("Auto Musketeer Hati Hop",_G.imgToggle,false,function(value)
		_G.Auto_Musketeer_Hat_Hop = value
		StopTween(_G.Auto_Musketeer_Hat_Hop)
	end)


	Main:Seperator("Other Function")

	Main:Toggle("Auto Ken Haki V2",_G.imgToggle,false,function(value)
		_G.Auto_Ken_Haki_V2 = value
		StopTween(_G.Auto_Ken_Haki_V2)
	end)

	Main:Toggle("Teleport to Sea Beast",_G.imgToggle,false,function(value)
		_G.Teleport_to_Sea_Beast = value
		StopTween(_G.Teleport_to_Sea_Beast)
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Teleport_to_Sea_Beast then
					for i,v in pairs(game.Workspace.SeaBeasts:GetChildren()) do
						if v:FindFirstChild("HumanoidRootPart") then
							getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(1,500,1))
						end
					end
				end
			end)
		end
	end)

	task.spawn(function()
		while wait() do
			pcall(function()
				if _G.Auto_Ken_Haki_V2 then
					if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
						repeat 
							if (CFrame.new(-12444.78515625, 332.40396118164, -7673.1806640625).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude > 2000 then
								BTP(CFrame.new(-12444.78515625, 332.40396118164, -7673.1806640625))
								return
							end
							getgenv().ToTarget(CFrame.new(-12444.78515625, 332.40396118164, -7673.1806640625)) 
							wait() 
						until not _G.Auto_Ken_Haki_V2 or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-12444.78515625, 332.40396118164, -7673.1806640625)).Magnitude <= 10
						wait(.5)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen")
						wait(1)
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest","CitizenQuest",1)
					else
						if game.Players.LocalPlayer.Backpack:FindFirstChild("Banana") and  game.Players.LocalPlayer.Backpack:FindFirstChild("Apple") and game.Players.LocalPlayer.Backpack:FindFirstChild("Pineapple") then
							repeat 
								getgenv().ToTarget(CFrame.new(-12444.78515625, 332.40396118164, -7673.1806640625)) 
								wait() 
							until not _G.Auto_Ken_Haki_V2 or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-12444.78515625, 332.40396118164, -7673.1806640625)).Magnitude <= 10
							wait(.5)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CitizenQuestProgress","Citizen")
						elseif game.Players.LocalPlayer.Backpack:FindFirstChild("Fruit Bowl") or game.Players.LocalPlayer.Character:FindFirstChild("Fruit Bowl") then
							repeat 
								getgenv().ToTarget(CFrame.new(-10920.125, 624.20275878906, -10266.995117188)) 
								wait() 
							until not _G.Auto_Ken_Haki_V2 or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-10920.125, 624.20275878906, -10266.995117188)).Magnitude <= 10
							wait(.5)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Start")
							wait(1)
							game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk2","Buy")
						elseif string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Defeat 50 Forest Pirates") then
							if game:GetService("Workspace").Enemies:FindFirstChild("Forest Pirate [Lv. 1825]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Forest Pirate [Lv. 1825]" then
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
										until not _G.Auto_Ken_Haki_V2 or v.Humanoid.Health <= 0
										StartMagnet = false
									end
								end
							else
								repeat 
									getgenv().ToTarget(CFrame.new(-13277.568359375, 370.34185791016, -7821.1572265625)) 
									wait() 
								until not _G.Auto_Ken_Haki_V2 or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13277.568359375, 370.34185791016, -7821.1572265625)).Magnitude <= 10
							end
						elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text ==  "Defeat  Captain Elephant (0/1)" then 
							if game:GetService("Workspace").Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
								for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
									if v.Name == "Captain Elephant [Lv. 1875] [Boss]" then
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
										until not _G.Auto_Ken_Haki_V2 or v.Humanoid.Health <= 0
										StartMagnet = false
									end
								end
							else
								repeat 
									getgenv().ToTarget(CFrame.new(-13493.12890625, 318.89553833008, -8373.7919921875)) 
									wait() 
								until not _G.Auto_Ken_Haki_V2 or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13493.12890625, 318.89553833008, -8373.7919921875)).Magnitude <= 10
							end
						else
							for i,v in pairs(game.Workspace:GetDescendants()) do
								if v.Name == "Apple" or v.Name == "Banana" or v.Name == "Pineapple" then
									v.Handle.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,1,10)
									wait()
									firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
									wait()
								end
							end  
						end
					end
				end
			end)
		end
	end)


end

------------------------------------------------------------------------------------------------------------------------------

TabStats:Seperator("Stats")

local Pointstat = TabStats:Label("Stat Points")

spawn(function()
	while wait() do
		pcall(function()
			Pointstat:Set("Stat Points : "..tostring(game:GetService("Players")["LocalPlayer"].Data.Points.Value))
		end)
	end
end)

TabStats:Toggle("Auto Melee",_G.imgToggle,false,function(value)
	_G.Auto_Melee = value
end)

TabStats:Toggle("Auto Defense",_G.imgToggle,false,function(value)
	_G.Auto_Defense = value
end)

TabStats:Toggle("Auto Sword",_G.imgToggle,false,function(value)
	_G.Auto_Sword = value
end)

TabStats:Toggle("Auto Gun",_G.imgToggle,false,function(value)
	_G.Auto_Gun = value
end)

TabStats:Toggle("Auto Devil Fruits",_G.imgToggle,false,function(value)
	_G.Auto_DevilFruit = value
end)

_G.PointStats = 1
TabStats:Slider("Select Point",1,100,1,function(value)
	_G.PointStats = value
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Melee then
				if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Melee",_G.PointStats)
				end
			end
		end)
	end
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Defense then
				if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Defense",_G.PointStats)
				end
			end
		end)
	end
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Sword then
				if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Sword",_G.PointStats)
				end
			end
		end)
	end
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_Gun then
				if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Gun",_G.PointStats)
				end
			end
		end)
	end
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.Auto_DevilFruit then
				if game:GetService("Players")["LocalPlayer"].Data.Points.Value ~= 0 then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AddPoint","Demon Fruit",_G.PointStats)
				end
			end
		end)
	end
end)


------------------------------------------------------------------------------------------------------------------------------

TabStats:Seperator("Fake")

TabStats:Toggle("Enabled Fake",_G.imgToggle,false,function(value)
	_G.EnabledStat = value
end)

TabStats:Textbox("Level","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Level.Value = tonumber(value)
	end
end)

TabStats:Textbox("Exp ","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Exp.Value = tonumber(value)
	end
end)

TabStats:Textbox("Beli","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Beli.Value = tonumber(value)
	end
end)

TabStats:Textbox("Fragments","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["Localplayer"].Data.Fragments.Value = tonumber(value)
	end
end)

TabStats:Textbox("Melee","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Stats.Melee.Level.Value = tonumber(value)
	end
end)

TabStats:Textbox("Defense","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Stats.Defense.Level.Value = tonumber(value)
	end
end)

TabStats:Textbox("Sword","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Stats.Sword.Level.Value = tonumber(value)
	end
end)

TabStats:Textbox("Gun","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Stats.Gun.Level.Value = tonumber(value)
	end
end)
TabStats:Textbox("Fruit","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].Data.Stats["Demon Fruit"].Level.Value = tonumber(value)
	end
end)

TabStats:Textbox("Bounty","",true,function(value)
	if _G.EnabledStat then
		game:GetService("Players")["LocalPlayer"].leaderstats["Bounty/Honor"].Value = tonumber(value)
	end
end)

------------------------------------------------------------------------------------------------------------------------------


TabCombat:Seperator("Player")

Playerslist = {}

for i,v in pairs(game:GetService("Players"):GetChildren()) do
	table.insert(Playerslist,v.Name)
end

local SelectedPly = TabCombat:Dropdown("Select Players",Playerslist,function(value)
	_G.Select_Player = value
end)

TabCombat:Button("Refresh Player",function()
	Playerslist = {}
	SelectedPly:Clear()
	for i,v in pairs(game:GetService("Players"):GetChildren()) do  
		SelectedPly:Add(v.Name)
	end
end)

TabCombat:Toggle("Spectate Player",_G.imgToggle,false,function(value)
	_G.Spectate_Player = value
end)


spawn(function()
	while wait() do
		if _G.Spectate_Player then
			pcall(function()
				if game.Players:FindFirstChild(_G.Select_Player) then
					game.Workspace.Camera.CameraSubject = game.Players:FindFirstChild(_G.Select_Player).Character.Humanoid
				end
			end)
		else
			game.Workspace.Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
		end
	end
end)

spawn(function()
	game:GetService("RunService").RenderStepped:Connect(function()
		if UseGunKillPlayer then
			pcall(function()
				for i,v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
					if v.Name == _G.Select_Player then
						local args = {
							[1] = v.HumanoidRootPart.Position,
							[2] = v.HumanoidRootPart
						}
						game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].RemoteFunctionShoot:InvokeServer(unpack(args))
					end
				end
			end)
		end
	end)
end)

TabCombat:Toggle("Teleport to Player",_G.imgToggle,false,function(value)
	_G.Teleport_to_Player = value
	StopTween(_G.Teleport_to_Player)
end)


spawn(function()
	while wait() do
		if _G.Teleport_to_Player then
			pcall(function()
				if game.Players:FindFirstChild(_G.Select_Player) then
					getgenv().ToTarget(game.Players[_G.Select_Player].Character.HumanoidRootPart.CFrame)
				end
			end)
		end
	end
end)

TabCombat:Toggle("Auto Kill Player",_G.imgToggle,false,function(value)
	_G.Auto_Kill_Player_Melee = value
	StopTween(_G.Auto_Kill_Player_Melee)
end)


spawn(function()
	while wait() do 
		pcall(function()
			if _G.Auto_Kill_Player_Melee then
				if game.Players:FindFirstChild(_G.Select_Player) then
					for i,v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
						if v.Name == _G.Select_Player and v.Humanoid.Health > 0 then
							repeat wait()
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,5,0))
								elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									AutoHaki()
									EquipWeapon(_G.Select_Weapon)
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,5,0))
									game:GetService'VirtualUser':CaptureController()
									game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
								end
							until game.Players:FindFirstChild(_G.Select_Player).Character.Humanoid.Health <= 0 or not _G.Auto_Kill_Player_Melee or not game.Players:FindFirstChild(_G.Select_Player)
						end
					end
				end
			end
		end)
	end
end)

TabCombat:Toggle("Auto Kill Player [Gun]",_G.imgToggle,false,function(value)
	_G.Auto_Kill_Player_Gun = value
	StopTween(_G.Auto_Kill_Player_Gun)
end)

spawn(function()
	while wait() do
		for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
			if v:IsA("Tool") then
				if v:FindFirstChild("RemoteFunctionShoot") then 
					SelectToolWeaponGun = v.Name
				end
			end
		end
	end
end)

spawn(function()
	while wait() do 
		pcall(function()
			if _G.Auto_Kill_Player_Gun then
				if game.Players:FindFirstChild(_G.Select_Player) then
					for i,v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
						if v.Name == _G.Select_Player and v.Humanoid.Health > 0 then
							repeat wait()
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
									getgenv().ToTarget(v.HumanoidRootPart.CFrame)
								elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									AutoHaki()
									EquipWeapon(SelectToolWeaponGun)
									UseGunKillPlayer = true
									game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].Cooldown.Value = 0
									v.HumanoidRootPart.Size = Vector3.new(60,60,60)
									v.HumanoidRootPart.Transparency = 0.7
									getgenv().ToTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,50,-10))
									game:GetService'VirtualUser':CaptureController()
									game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
								end
							until game.Players:FindFirstChild(_G.Select_Player).Character.Humanoid.Health <= 0 or not _G.Auto_Kill_Player_Gun or not game.Players:FindFirstChild(_G.Select_Player)
						end
					end
				end
			else
				UseGunKillPlayer = false
			end
		end)
	end
end)

TabCombat:Toggle("Enabled PvP ",_G.imgToggle,false,function(value)
	_G.EnabledPvP = value
end)

spawn(function()
	pcall(function()
		while wait() do
			if _G.EnabledPvP then
				if game:GetService("Players").LocalPlayer.PlayerGui.Main.PvpDisabled.Visible == true then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EnablePvp")
				end
			end
		end
	end)
end)

------------------------------------------------------------------------------------------------------------------------------

Teleport:Seperator("Island")

Teleport:Seperator("World - Monster")

Teleport:Button("Teleport To Old World",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
end)

Teleport:Button("Teleport To Second Sea",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
end)

Teleport:Button("Teleport To Third Sea",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
end)


if World1 then
	Teleport:Dropdown("Select Island",{
		"WindMill",
		"Marine",
		"Middle Town",
		"Jungle",
		"Pirate Village",
		"Desert",
		"Snow Island",
		"MarineFord",
		"Colosseum",
		"Sky Island 1",
		"Sky Island 2",
		"Sky Island 3",
		"Prison",
		"Magma Village",
		"Under Water Island",
		"Fountain City",
		"Shank Room",
		"Mob Island"
	},function(value)
		_G.SelectIsland = value
	end)
end

if World2 then
	Teleport:Dropdown("Select Island",{
		"The Cafe",
		"Frist Spot",
		"Dark Area",
		"Flamingo Mansion",
		"Flamingo Room",
		"Green Zone",
		"Factory",
		"Colossuim",
		"Zombie Island",
		"Two Snow Mountain",
		"Punk Hazard",
		"Cursed Ship",
		"Ice Castle",
		"Forgotten Island",
		"Ussop Island",
		"Mini Sky Island"
	},function(value)
		_G.SelectIsland = value
	end)
end

if World3 then
	Teleport:Dropdown("Select Island",{
		"Mansion",
		"Port Town",
		"Great Tree",
		"Castle On The Sea",
		"MiniSky", 
		"Hydra Island",
		"Floating Turtle",
		"Haunted Castle",
		"Ice Cream Island",
		"Peanut Island",
		"Cake Island",
		"Sea to Treats New"
	},function(value)
		_G.SelectIsland = value
	end)
end

Teleport:Toggle("Teleport",_G.imgToggle,false,function(value)
	_G.TeleportIsland = value
	if _G.TeleportIsland == true then
		repeat wait()
			if _G.SelectIsland == "WindMill" then
				getgenv().ToTarget(CFrame.new(979.79895019531, 16.516613006592, 1429.0466308594))
			elseif _G.SelectIsland == "Marine" then
				getgenv().ToTarget(CFrame.new(-2566.4296875, 6.8556680679321, 2045.2561035156))
			elseif _G.SelectIsland == "Middle Town" then
				getgenv().ToTarget(CFrame.new(-690.33081054688, 15.09425163269, 1582.2380371094))
			elseif _G.SelectIsland == "Jungle" then
				getgenv().ToTarget(CFrame.new(-1612.7957763672, 36.852081298828, 149.12843322754))
			elseif _G.SelectIsland == "Pirate Village" then
				getgenv().ToTarget(CFrame.new(-1181.3093261719, 4.7514905929565, 3803.5456542969))
			elseif _G.SelectIsland == "Desert" then
				getgenv().ToTarget(CFrame.new(944.15789794922, 20.919729232788, 4373.3002929688))
			elseif _G.SelectIsland == "Snow Island" then
				getgenv().ToTarget(CFrame.new(1347.8067626953, 104.66806030273, -1319.7370605469))
			elseif _G.SelectIsland == "MarineFord" then
				getgenv().ToTarget(CFrame.new(-4914.8212890625, 50.963626861572, 4281.0278320313))
			elseif _G.SelectIsland == "Colosseum" then
				getgenv().ToTarget( CFrame.new(-1427.6203613281, 7.2881078720093, -2792.7722167969))
			elseif _G.SelectIsland == "Sky Island 1" then
				getgenv().ToTarget(CFrame.new(-4869.1025390625, 733.46051025391, -2667.0180664063))
			elseif _G.SelectIsland == "Sky Island 2" then  
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-4607.82275, 872.54248, -1667.55688))
			elseif _G.SelectIsland == "Sky Island 3" then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-7894.6176757813, 5547.1416015625, -380.29119873047))
			elseif _G.SelectIsland == "Prison" then
				getgenv().ToTarget( CFrame.new(4875.330078125, 5.6519818305969, 734.85021972656))
			elseif _G.SelectIsland == "Magma Village" then
				getgenv().ToTarget(CFrame.new(-5247.7163085938, 12.883934020996, 8504.96875))
			elseif _G.SelectIsland == "Under Water Island" then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
			elseif _G.SelectIsland == "Fountain City" then
				getgenv().ToTarget(CFrame.new(5127.1284179688, 59.501365661621, 4105.4458007813))
			elseif _G.SelectIsland == "Shank Room" then
				getgenv().ToTarget(CFrame.new(-1442.16553, 29.8788261, -28.3547478))
			elseif _G.SelectIsland == "Mob Island" then
				getgenv().ToTarget(CFrame.new(-2850.20068, 7.39224768, 5354.99268))
			elseif _G.SelectIsland == "The Cafe" then
				getgenv().ToTarget(CFrame.new(-380.47927856445, 77.220390319824, 255.82550048828))
			elseif _G.SelectIsland == "Frist Spot" then
				getgenv().ToTarget(CFrame.new(-11.311455726624, 29.276733398438, 2771.5224609375))
			elseif _G.SelectIsland == "Dark Area" then
				getgenv().ToTarget(CFrame.new(3780.0302734375, 22.652164459229, -3498.5859375))
			elseif _G.SelectIsland == "Flamingo Mansion" then
				getgenv().ToTarget(CFrame.new(-483.73370361328, 332.0383605957, 595.32708740234))
			elseif _G.SelectIsland == "Flamingo Room" then
				getgenv().ToTarget(CFrame.new(2284.4140625, 15.152037620544, 875.72534179688))
			elseif _G.SelectIsland == "Green Zone" then
				getgenv().ToTarget( CFrame.new(-2448.5300292969, 73.016105651855, -3210.6306152344))
			elseif _G.SelectIsland == "Factory" then
				getgenv().ToTarget(CFrame.new(424.12698364258, 211.16171264648, -427.54049682617))
			elseif _G.SelectIsland == "Colossuim" then
				getgenv().ToTarget( CFrame.new(-1503.6224365234, 219.7956237793, 1369.3101806641))
			elseif _G.SelectIsland == "Zombie Island" then
				getgenv().ToTarget(CFrame.new(-5622.033203125, 492.19604492188, -781.78552246094))
			elseif _G.SelectIsland == "Two Snow Mountain" then
				getgenv().ToTarget(CFrame.new(753.14288330078, 408.23559570313, -5274.6147460938))
			elseif _G.SelectIsland == "Punk Hazard" then
				getgenv().ToTarget(CFrame.new(-6127.654296875, 15.951762199402, -5040.2861328125))
			elseif _G.SelectIsland == "Cursed Ship" then
				getgenv().ToTarget(CFrame.new(923.40197753906, 125.05712890625, 32885.875))
			elseif _G.SelectIsland == "Ice Castle" then
				getgenv().ToTarget(CFrame.new(6148.4116210938, 294.38687133789, -6741.1166992188))
			elseif _G.SelectIsland == "Forgotten Island" then
				getgenv().ToTarget(CFrame.new(-3032.7641601563, 317.89672851563, -10075.373046875))
			elseif _G.SelectIsland == "Ussop Island" then
				getgenv().ToTarget(CFrame.new(4816.8618164063, 8.4599885940552, 2863.8195800781))
			elseif _G.SelectIsland == "Mini Sky Island" then
				getgenv().ToTarget(CFrame.new(-288.74060058594, 49326.31640625, -35248.59375))
			elseif _G.SelectIsland == "Great Tree" then
				getgenv().ToTarget(CFrame.new(2681.2736816406, 1682.8092041016, -7190.9853515625))
			elseif _G.SelectIsland == "Castle On The Sea" then
				getgenv().ToTarget(CFrame.new(-5074.45556640625, 314.5155334472656, -2991.054443359375))
			elseif _G.SelectIsland == "MiniSky" then
				getgenv().ToTarget(CFrame.new(-260.65557861328, 49325.8046875, -35253.5703125))
			elseif _G.SelectIsland == "Port Town" then
				getgenv().ToTarget(CFrame.new(-290.7376708984375, 6.729952812194824, 5343.5537109375))
			elseif _G.SelectIsland == "Hydra Island" then
				getgenv().ToTarget(CFrame.new(5228.8842773438, 604.23400878906, 345.0400390625))
			elseif _G.SelectIsland == "Floating Turtle" then
				getgenv().ToTarget(CFrame.new(-13274.528320313, 531.82073974609, -7579.22265625))
			elseif _G.SelectIsland == "Mansion" then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-12471.169921875, 374.94024658203, -7551.677734375))
			elseif _G.SelectIsland == "Haunted Castle" then
				getgenv().ToTarget(CFrame.new(-9515.3720703125, 164.00624084473, 5786.0610351562))
			elseif _G.SelectIsland == "Ice Cream Island" then
				getgenv().ToTarget(CFrame.new(-902.56817626953, 79.93204498291, -10988.84765625))
			elseif _G.SelectIsland == "Peanut Island" then
				getgenv().ToTarget(CFrame.new(-2062.7475585938, 50.473892211914, -10232.568359375))
			elseif _G.SelectIsland == "Cake Island" then
				getgenv().ToTarget(CFrame.new(-1884.7747802734375, 19.327526092529297, -11666.8974609375))
			elseif _G.SelectIsland == "Sea to Treats New" then
				getgenv().ToTarget(CFrame.new(-1141.0223388671875, 47.25519561767578, -14204.609375))	
			end
		until not _G.TeleportIsland
	end
	StopTween(_G.TeleportIsland)
end)
------------------------------------------------------------------------------------------------------------------------------

Dungeon:Seperator("Dungeon")

Dungeon:Toggle("Auto Farm Dungeon ",_G.imgToggle,false,function(value)
	_G.Auto_Raid = value
	StopTween(_G.Auto_Raid)
end)

spawn(function()
	pcall(function()
		while wait() do
			if _G.Auto_Raid or _G.Auto_Next then
				if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
					if game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
						getgenv().ToTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame*CFrame.new(0,30,0))
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
						getgenv().ToTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame*CFrame.new(0,30,0))
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
						getgenv().ToTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame*CFrame.new(0,30,0))
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
						getgenv().ToTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame*CFrame.new(0,30,0))
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
						getgenv().ToTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame*CFrame.new(0,30,0))
					end
				end
			end
		end
	end)
end)

Dungeon:Toggle("Kill Aura ",_G.imgToggle,false,function(value)
	_G.Kill = value
end)

spawn(function()
	pcall(function() 
		while wait() do
			if _G.Auto_Raid or _G.Kill then
				if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == true then
					for i,v in pairs(game:GetService("Workspace").Enemies:GetDescendants()) do
						if v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
							pcall(function()
								repeat task.wait()                                    
									v.Humanoid.Health = 0
									v.HumanoidRootPart.CanCollide = false
									sethiddenproperty(game:GetService("Players").LocalPlayer,"SimulationRadius",math.huge)
								until not _G.Auto_Dungeon and _G.kill or not v.Parent or v.Humanoid.Health <= 0
							end)
						end
					end
				end
			end
		end
	end)
end)

Dungeon:Toggle("Auto Next Island ",_G.imgToggle,false,function(value)
	_G.Auto_Next = value
	StopTween(_G.Auto_Next)
end)

Dungeon:Dropdown("Select Chips",{"Flame","Ice","Quake","Light","Dark","String","Rumble","Magma","Human: Buddha","Sand","Bird: Phoenix","Dough"},function(value)
	_G.SelectChip = value
end)

Dungeon:Toggle("Auto Select Dungeon",_G.imgToggle,false,function(value)
	_G.AutoSelectDungeon = value
end)

spawn(function()
	while wait() do
		if _G.AutoSelectDungeon then
			pcall(function()
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame-Flame") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame-Flame") then
					_G.SelectChip = "Flame"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice-Ice") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice-Ice") then
					_G.SelectChip = "Ice"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake-Quake") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake-Quake") then
					_G.SelectChip = "Quake"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light-Light") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light-Light") then
					_G.SelectChip = "Light"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark-Dark") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark-Dark") then
					_G.SelectChip = "Dark"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("String-String") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String-String") then
					_G.SelectChip = "String"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble-Rumble") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble-Rumble") then
					_G.SelectChip = "Rumble"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma-Magma") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma-Magma") then
					_G.SelectChip = "Magma"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
					_G.SelectChip = "Human: Buddha"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand-Sand") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand-Sand") then
					_G.SelectChip = "Sand"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird-Bird: Phoenix") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird-Bird: Phoenix") then
					_G.SelectChip = "Bird: Phoenix"
				elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough-Dough") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough-Dough") then
					_G.SelectChip = "Dough"
				else
					_G.SelectChip = "Flame"
				end
			end)
		end
	end
end)

Dungeon:Toggle("Auto Buy Chip ",_G.imgToggle,false,function(value)
	_G.AutoBuyChip = value
end)

Dungeon:Toggle("Auto Start Raid ",_G.imgToggle,false,function(value)
	_G.Auto_StartRaid = value
end)

spawn(function()
	pcall(function()
		while wait() do
			if game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game:GetService("Players").LocalPlayer.Character:FindFirstChild("Special Microchip") then
				if not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
					if _G.Auto_StartRaid then
						if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Timer.Visible == false then
							if World2 then
								fireclickdetector(game:GetService("Workspace").Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
							elseif World3 then
								fireclickdetector(game:GetService("Workspace").Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
							end
						end
					end
				end
			else
				if _G.AutoBuyChip then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("RaidsNpc", "Select", _G.SelectChip)
				end
			end
		end
	end)
end)

------------------------------------------------------------------------------------------------------------------------------

DevilFruit:Seperator("Devil Fruit")

FruitList = {
	"Bomb-Bomb",
	"Spike-Spike",
	"Chop-Chop",
	"Spring-Spring",
	"Kilo-Kilo",
	"Spin-Spin",
	"Bird: Falcon",
	"Smoke-Smoke",
	"Flame-Flame",
	"Ice-Ice",
	"Sand-Sand",
	"Dark-Dark",
	"Revive-Revive",
	"Diamond-Diamond",
	"Light-Light",
	"Love-Love",
	"Rubber-Rubber",
	"Barrier-Barrier",
	"Magma-Magma",
	"Door-Door",
	"Quake-Quake",
	"Human-Human: Buddha",
	"String-String",
	"Bird-Bird: Phoenix",
	"Rumble-Rumble",
	"Paw-Paw",
	"Gravity-Gravity",
	"Dough-Dough",
	"Venom-Venom",
	"Shadow-Shadow",
	"Control-Control",
	"Soul-Soul",
	"Dragon-Dragon"
}

_G.SelectFruit = ""
DevilFruit:Dropdown("Select Fruits Sniper",FruitList,function(value)
	_G.SelectFruit = value
end)

DevilFruit:Toggle("Auto Buy Fruit Sniper",_G.imgToggle,false,function(value)
	_G.AutoBuyFruitSniper = value
end)



DevilFruit:Dropdown("Select Fruits Eat",FruitList,function(value)
	_G.SelectFruitEat = value
end)

DevilFruit:Toggle("Auto Eat Fruit",_G.imgToggle,false,function(value)
	_G.AutoEatFruit = value
end)

spawn(function()
	pcall(function()
		while wait(.1) do
			if _G.AutoEatFruit then
				game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat).EatRemote:InvokeServer()
			end
		end
	end)
end)

DevilFruit:Toggle("Auto Eat Fruit Hop",_G.imgToggle,false,function(value)
	_G.AutoEatFruitHop = value
end)

spawn(function()
	pcall(function()
		while wait(.1) do wait(10)
			if _G.AutoEatFruitHop and _G.SelectFruitEat ~= nil then
				if not game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat) or not game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(_G.SelectFruitEat) then
					Hop()
				else
					game:GetService("Players").LocalPlayer.Character:FindFirstChild(_G.SelectFruitEat).EatRemote:InvokeServer()
				end
			end
		end
	end)
end)

spawn(function()
	pcall(function()
		while wait(.1) do
			if _G.AutoBuyFruitSniper then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetFruits")
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("PurchaseRawFruit",_G.SelectFruit)
			end 
		end
	end)
end)

DevilFruit:Toggle("Auto Random Fruit",_G.imgToggle,false,function(value)
	_G.Random_Auto = value
end)

spawn(function()
	pcall(function()
		while wait(.1) do
			if _G.Random_Auto then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
			end 
		end
	end)
end)

DevilFruit:Button("Random Fruit",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
end)


DevilFruit:Toggle("Auto Drop Fruit",_G.imgToggle,false,function(value)
	_G.DropFruit = value
end)

spawn(function()
	while wait() do
		if _G.DropFruit then
			pcall(function()
				for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
					if v.Name == "Fruit" then
						EquipWeapon(v.Name)
						wait(.1)
						if game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible == true then
							game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible = false
						end
						EquipWeapon(v.Name)
						game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectFruit).EatRemote:InvokeServer("Drop")
					end
				end
				for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetChildren()) do
					if v.Name == "Fruit" then
						EquipWeapon(v.Name)
						wait(.1)
						if game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible == true then
							game:GetService("Players").LocalPlayer.PlayerGui.Main.Dialogue.Visible = false
						end
						EquipWeapon(v.Name)
						game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectFruit).EatRemote:InvokeServer("Drop")
					end
				end
			end)
		end
	end
end)

DevilFruit:Toggle("Auto Store Fruit",_G.imgToggle,false,function(value)
	_G.AutoStoreFruit = value
end)

spawn(function()
	while wait() do
		if _G.AutoStoreFruit then
			pcall(function()
				wait()
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bomb Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bomb Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bomb-Bomb",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bomb Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bomb Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spike Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spike Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spike-Spike",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spike Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spike Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Chop Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Chop Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Chop-Chop",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Chop Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Chop Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spring Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spring Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spring-Spring",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spring Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spring Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Kilo Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Kilo Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Kilo-Kilo",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Kilo Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Kilo Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Smoke Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Smoke Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Smoke-Smoke",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Smoke Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Smoke Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spin Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spin Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Spin-Spin",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Spin Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Spin Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Flame-Flame",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Flame Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Flame Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Falcon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Falcon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Falcon",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Falcon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Falcon Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Ice-Ice",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Ice Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Ice Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Sand-Sand",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Sand Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Sand Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dark-Dark",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dark Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dark Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Revive Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Revive Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Revive-Revive",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Revive Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Revive Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Diamond Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Diamond Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Diamond-Diamond",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Diamond Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Diamond Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Light-Light",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Light Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Light Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Love Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Love Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Love-Love",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Love Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Love Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rubber Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rubber Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rubber-Rubber",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rubber Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rubber Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Barrier Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Barrier Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Barrier-Barrier",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Barrier Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Barrier Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Magma-Magma",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Magma Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Magma Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Door Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Door Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Door-Door",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Door Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Door Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Quake-Quake",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Quake Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Quake Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Human-Human: Buddha",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Human-Human: Buddha Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("String Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","String-String",game:GetService("Players").LocalPlayer.Character:FindFirstChild("String Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("String Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Bird-Bird: Phoenix",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Bird: Phoenix Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Bird: Phoenix Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Rumble-Rumble",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Rumble Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Rumble Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Paw Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Paw Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Paw-Paw",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Paw Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Paw Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Gravity Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Gravity-Gravity",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Gravity Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Gravity Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dough-Dough",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dough Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dough Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Shadow Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Shadow-Shadow",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Shadow Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Shadow Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Venom Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Venom-Venom",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Venom Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Control Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Control Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Control-Control",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Control Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Control Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Dragon-Dragon",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Dragon Fruit"))
				end
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Leopard Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Leopard Fruit") then
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StoreFruit","Leopard-Leopard",game:GetService("Players").LocalPlayer.Character:FindFirstChild("Leopard Fruit") or game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Leopard Fruit"))
				end
			end)
		end
	end
end)


DevilFruit:Toggle("Grab Fruit",_G.imgToggle,false,function(value)
	_G.BringFruit = value
	pcall(function()
		while _G.BringFruit do wait(.1)
			for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
				if v:IsA("Tool") then
					local OldCFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame				
					game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.Handle.CFrame * CFrame.new(0,0,8)
					v.Handle.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame
					wait(.1)
					game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = OldCFrame
				end
			end
		end
	end)
end)

------------------------------------------------------------------------------------------------------------------------------

Shop:Seperator("Abilities")

Shop:Button("Buy Geppo [ $10,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Geppo")
end)

Shop:Button("Buy Buso Haki [ $25,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Buso")
end)

Shop:Button("Buy Soru [ $25,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Soru")
end)

Shop:Button("Buy Observation Haki [ $750,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Buy")
end)

Shop:Toggle("Auto Buy Abilities",_G.imgToggle,false,function(value)
	Abilities = value
	while Abilities do wait(.1)
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Geppo")
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Buso")
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Soru")
	end
end)

Shop:Seperator(" \\\\  Boats // ")

BoatList = {
	"Pirate Sloop",
	"Enforcer",
	"Rocket Boost",
	"Dinghy",
	"Pirate Basic",
	"Pirate Brigade"
}

spawn(function()
	while wait() do
		pcall(function()
			if SelectBoat == "Pirate Sloop" then
				_G.SelectBoat = "PirateSloop"
			else
				if SelectBoat == "Enforcer" then
					_G.SelectBoat = "Enforcer"
				else
					if SelectBoat == "RocketBoost" then
						_G.SelectBoat = "RocketBoost"
					else
						if SelectBoat == "PirateBasic" then
							_G.SelectBoat = "PirateBasic"
						else
							if SelectBoat == "PirateBrigade" then
								_G.SelectBoat = "PirateBrigade"
							end
						end
					end
				end
			end
		end)
	end
end)

Shop:Dropdown("Select Boats",BoatList,function(value)
	SelectBoat = value
end)

Shop:Button("Buy Boat",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBoat",_G.SelectBoat)
end)

Shop:Seperator("Fighting Style")

Shop:Button("Buy Black Leg [ $150,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
end)

Shop:Button("Buy Electro [ $550,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectro")
end)

Shop:Button("Buy Fishman Karate [ $750,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyFishmanKarate")
end)

Shop:Button("Buy Dragon Claw [ $1,500 Fragments ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
end)

Shop:Button("Buy Superhuman [ $3,000,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
end)

Shop:Button("Buy Death Step [ $5,000 Fragments $5,000,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
end)

Shop:Button("Buy Sharkman Karate [ $5,000 Fragments $2,500,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true)
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate")
end)

Shop:Button("Buy Electric Claw [ $5,000 Fragments $3,000,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
end)

Shop:Button("Buy Dragon Talon [ $5,000 Fragments $3,000,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon")
end)

Shop:Button("Buy God Human [ $5,000 Fragments $5,000,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman")
end)
-----Shop----------------

Shop:Seperator("Sword")

Shop:Button("Cutlass [ $1,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
end)

Shop:Button("Katana [ $1,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
end)

Shop:Button("Iron Mace [ $25,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
end)

Shop:Button("Dual Katana [ $12,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
end)

Shop:Button("Triple Katana [ $60,000 Beli ]", function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
end)

Shop:Button("Pipe [ $100,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
end)

Shop:Button("Dual-Headed Blade [ $400,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
end)

Shop:Button("Bisento [ $1,200,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
end)

Shop:Button("Soul Cane [ $750,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
end)

Shop:Button("Pole v.2 [ 5,000 Fragments ]",function()
	game.ReplicatedStorage.Remotes.CommF_:InvokeServer("ThunderGodTalk")
end)

Shop:Toggle("Yama Sword [ Elite Hunter 30 ]",_G.imgToggle,false,function(value)
	_G.AutoYama = value
end)

spawn(function()
	while wait() do
		if _G.AutoYama then
			if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter","Progress") >= 30 then
				repeat wait(.1)
					fireclickdetector(game:GetService("Workspace").Map.Waterfall.SealedKatana.Handle.ClickDetector)
				until game:GetService("Players").LocalPlayer.Backpack:FindFirstChild("Yama") or not _G.AutoYama
			end
		end
	end
end)
Shop:Seperator("Gun")

Shop:Button("Slingshot [ $5,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
end)

Shop:Button("Musket [ $8,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
end)

Shop:Button("Flintlock [ $10,500 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
end)

Shop:Button("Refined Slingshot [ $30,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
end)

Shop:Button("Refined Flintlock [ $65,000 Beli ]",function()
	local args = {
		[1] = "BuyItem",
		[2] = "Refined Flintlock"
	}
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

Shop:Button("Cannon [ $100,000 Beli ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
end)

Shop:Button("Kabucha [ 1,500 Fragments]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
end)

Shop:Button("Bizarre Rifle [ 250 Ectoplasm ]", function()
	local A_1 = "Ectoplasm"
	local A_2 = "Buy"
	local A_3 = 1
	local Event = game:GetService("ReplicatedStorage").Remotes["CommF_"]
	Event:InvokeServer(A_1, A_2, A_3) 
	local A_1 = "Ectoplasm"
	local A_2 = "Buy"
	local A_3 = 1
	local Event = game:GetService("ReplicatedStorage").Remotes["CommF_"]
	Event:InvokeServer(A_1, A_2, A_3)
end)

------------Bone------------------

Shop:Seperator("Bones")

Shop:Button("Buy Surprise [ $50 Bone ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
end)

Shop:Button("Stat Refund [ $50 Bone ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,2)
end)

Shop:Button("Race Reroll [ $50 Bone ]",function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,3)
end)

------------Stat------------------

Shop:Seperator("Stat")

Shop:Button("Reset Stats (Use 2.5K Fragments)", function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
end)

Shop:Button("Random Race (Use 3K Fragments)", function()
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Reroll","1")
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Reroll","2")
end)
--------------Accessories-----------------
Shop:Seperator("Accessories")
Shop:Button("Black Cape [ $50,000 Beli ]",function()
	local args = {
		[1] = "BuyItem",
		[2] = "Black Cape"
	}
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Swordsman Hat [ 150k Beli ]",function()
	local args = {
		[1] = "BuyItem",
		[2] = "Swordsman Hat"
	}
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)
Shop:Button("Tomoe Ring [ $500k Beli ]",function()
	local args = {
		[1] = "BuyItem",
		[2] = "Tomoe Ring"
	}
	game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
end)

------------------------------------------------------------------------------------------------------------------------------

Misc:Seperator("Codes")

local x2Code = {
	"3BVISITS",
	"UPD16",
	"FUDD10",
	"BIGNEWS",
	"THEGREATACE",
	"SUB2GAMERROBOT_EXP1",
	"StrawHatMaine",
	"Sub2OfficialNoobie",
	"SUB2NOOBMASTER123",
	"Sub2Daigrock",
	"Axiore",
	"TantaiGaming",
	"STRAWHATMAINE",
	"Enyu_is_Pro",
	"Sub2Fer999",
	"Bluxxy",
	"JCWK",
	"Magicbus",
	"Starcodeheo",
	"SUB2UNCLEKIZARU"
}

Misc:Button("Redeem All Codes",function()
	for i,v in pairs(x2Code) do
		UseCode(v)
	end
end)

Misc:Dropdown("Selected Codes",x2Code,function(value)
	_G.CodeSelect = value
end)

Misc:Button("Redeem Code",function()
	game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(_G.CodeSelect)
end)

Misc:Seperator("Abilities")

Misc:Toggle("Infinite Ability",_G.imgToggle,false,function(value)
	if value then
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
		local Agility = game:GetService("ReplicatedStorage").FX["Agility"]:Clone()
		Agility.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
	else
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart["Agility"]:Destroy()
	end
end)

Misc:Toggle("Infinite Obversation Range",_G.imgToggle,false,function(value)
	_G.InfiniteObRange = value
	local VS = game:GetService("Players").LocalPlayer.VisionRadius.Value
	while _G.InfiniteObRange do
		wait()
		local player = game:GetService("Players").LocalPlayer
		local char = player.Character
		local VisionRadius = player.VisionRadius
		if player then
			if char.Humanoid.Health <= 0 then 
				wait(5) 
			end
			VisionRadius.Value = math.huge
		elseif getgenv().InfiniteObRange == false and player then
			VisionRadius.Value = VS
		end
	end
end)

Misc:Toggle("Infinite Geppo",_G.imgToggle,false,function(value)
	_G.InfGeppo = value
end)

spawn(function()
	while wait() do
		pcall(function()
			if _G.InfGeppo then
				for i,v in next, getgc() do
					if game:GetService("Players").LocalPlayer.Character.Geppo then
						if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.Character.Geppo then
							for i2,v2 in next, getupvalues(v) do
								if tostring(i2) == "9" then
									repeat wait(.1)
										setupvalue(v,i2,0)
									until not getgenv().InfGeppo or game:GetService("Players").LocalPlayer.Character.Humanoid.Health <= 0 
								end
							end
						end
					end
				end
			end
		end)
	end
end)

Misc:Toggle("Infinite Soru",_G.imgToggle,false,function(value)
	_G.InfSoru = value
end)

spawn(function()
	while wait() do
		pcall(function()
			if getgenv().InfSoru and game:GetService("Players").LocalPlayer.Character:FindFirstChild("HumanoidRootPart") ~= nil  then
				for i,v in next, getgc() do
					if game:GetService("Players").LocalPlayer.Character.Soru then
						if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.Character.Soru then
							for i2,v2 in next, getupvalues(v) do
								if typeof(v2) == "table" then
									repeat wait(.1)
										v2.LastUse = 0
									until not getgenv().InfSoru or game:GetService("Players").LocalPlayer.Character.Humanoid.Health <= 0
								end
							end
						end
					end
				end
			end
		end)
	end
end)

Misc:Toggle("Infinite Jump",_G.imgToggle,false,function(value)
	_G.Infinite = State
end)
game:GetService("UserInputService").JumpRequest:connect(function()
	if _G.Infinite then
		game:GetService"Players".LocalPlayer.Character:FindFirstChildOfClass'Humanoid':ChangeState("Jumping")
	end
end)

Misc:Seperator(" \\\\ Highlight // ")

Misc:Toggle("Show Chat disabled",_G.imgToggle,false,function(value)
	_G.chat = value
	if _G.chat == true then
		local StarterGui = game:GetService('StarterGui')
		StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Chat, false)    
	elseif _G.chat == false then
		local StarterGui = game:GetService('StarterGui')
		StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Chat, true)    
	end
end)

Misc:Toggle("Show leaderboard disabled",_G.imgToggle,false,function(value)
	_G.leaderboard = value
	if _G.leaderboard == true then
		local StarterGui = game:GetService('StarterGui')
		game:GetService('StarterGui'):SetCoreGuiEnabled(Enum.CoreGuiType.PlayerList, false)   
	elseif _G.leaderboard == false then
		local StarterGui = game:GetService('StarterGui')
		game:GetService('StarterGui'):SetCoreGuiEnabled(Enum.CoreGuiType.PlayerList, true)   
	end
end)

Misc:Toggle("Highlight Mode",_G.imgToggle,false,function(value)
	if value == true then
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Beli.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.HP.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Energy.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.StatsButton.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ShopButton.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Skills.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Level.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.MenuButton.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Code.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Settings.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Mute.Visible = false
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.CrewButton.Visible = false
	else
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Beli.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.HP.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Energy.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.StatsButton.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ShopButton.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Skills.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Level.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.MenuButton.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Code.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Settings.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.Mute.Visible = true
		game:GetService("Players")["LocalPlayer"].PlayerGui.Main.CrewButton.Visible = true
	end
end)

local transparent = false -- xray
function x(v)
	if v then
		for _,i in pairs(workspace:GetDescendants()) do
			if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
				i.LocalTransparencyModifier = 0.7
			end
		end
	else
		for _,i in pairs(workspace:GetDescendants()) do
			if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
				i.LocalTransparencyModifier = 0
			end
		end
	end
end

---- [RainbowHaki]
spawn(function()
	while wait() do
		if RainbowHaki then
			pcall(function()
				if game.Players.LocalPlayer.Character.HasBuso then
					for i,v in pairs(game.Players.LocalPlayer.Character.Humanoid:GetChildren()) do
						if v.Name == "RightLowerArm_BusoLayer1" or v.Name == "RightLowerArm_BusoLayer2" or v.Name == "RightHand_BusoLayer1" or v.Name == "RightHand_BusoLayer2" or v.Name == "LeftLowerArm_BusoLayer1" or v.Name == "LeftLowerArm_BusoLayer2" or v.Name == "LeftHand_BusoLayer1" or v.Name == "LeftHand_BusoLayer2" or v.Name == "LeftHand_BusoLayer1" or v.Name == "RightUpperArm_BusoLayer1" or v.Name == "RightUpperArm_BusoLayer2" or v.Name == "LeftUpperArm_BusoLayer1" or v.Name == "LeftUpperArm_BusoLayer2" or v.Name == "UpperTorso_BusoLayer1" or v.Name == "UpperTorso_BusoLayer2" or v.Name == "LowerTorso_BusoLayer1" or v.Name == "LowerTorso_BusoLayer2" or v.Name == "Head_BusoLayer1" or v.Name == "Head_BusoLayer2" or v.Name == "RightUpperLeg_BusoLayer1" or v.Name == "RightUpperLeg_BusoLayer2" or v.Name == "LeftUpperLeg_BusoLayer1" or v.Name == "LeftUpperLeg_BusoLayer2" or v.Name == "RightLowerLeg_BusoLayer1" or v.Name == "RightLowerLeg_BusoLayer2" or v.Name == "LeftLowerLeg_BusoLayer1" or v.Name == "LeftLowerLeg_BusoLayer2" or v.Name == "LeftFoot_BusoLayer1" or v.Name == "LeftFoot_BusoLayer2" or v.Name == "RightFoot_BusoLayer1" or v.Name == "RightFoot_BusoLayer2" then
							v.Color = Color3.fromHSV(tick() * 24 % 255/255, 1, 1)
						end
					end
				end
			end)
		end
	end
end)

Misc:Toggle("Rainbow Haki",_G.imgToggle,false,function(value)
	RainbowHaki = value
end)

Misc:Toggle("Rainbow Yoru",_G.imgToggle,false,function(value)
	RainbowYoru = value
end)

---- [RainbowYoru]

spawn(function()
	while wait() do
		if RainbowYoru then
			pcall(function()
				for i,v in pairs(game.Players.LocalPlayer.Character.DarkBlade.Right:GetChildren()) do
					if v.Name == "Runes" or v.Name == "Hold" or v.Name == "Bottom" or v.Name == "Gems" or v.Name == "Wings" or v.Name == "Blade" or v.Name == "Tape" then
						v.Color = Color3.fromHSV(tick() * 24 % 255/255, 1, 1)
						v.Material = "Neon"
					end

				end
			end)
		end
	end
end)

spawn(function()
	while wait(1) do
		if RainbowYoru then
			pcall(function()
				for i,v in pairs(game.Players.LocalPlayer.Character.DarkBlade.Right.Handle:GetChildren()) do
					if v.Name == "Trail" then
						v.LightEmission = 1
					end

				end
			end)
		end
	end
end)

spawn(function()
	while wait(1) do
		if RainbowYoru then
			pcall(function()
				for i,v in pairs(game.Players.LocalPlayer.Character.DarkBlade.Right.Handle.Attachment0:GetChildren()) do
					if v.Name == "Beam" then
						v.LightEmission = 1 v.Texture = 0 v.Width0 = 0 v.Width1 = 0
					end

				end
			end)
		end
	end
end)

Misc:Seperator("Server")

Misc:Button("Rejoin Server",function()
	game:GetService("TeleportService"):Teleport(game.PlaceId, game:GetService("Players").LocalPlayer)
end)

Misc:Button("Server Hop",function()
	Hop()
end)

Misc:Button("Hop To Lower Player",function()
	getgenv().AutoTeleport = true
	getgenv().DontTeleportTheSameNumber = true 
	getgenv().CopytoClipboard = false
	if not game:IsLoaded() then
		print("Game is loading waiting...")
	end
	local maxplayers = math.huge
	local serversmaxplayer;
	local goodserver;
	local gamelink = "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?sortOrder=Asc&limit=100" 
	function serversearch()
		for _, v in pairs(game:GetService("HttpService"):JSONDecode(game:HttpGetAsync(gamelink)).data) do
			if type(v) == "table" and v.playing ~= nil and maxplayers > v.playing then
				serversmaxplayer = v.maxPlayers
				maxplayers = v.playing
				goodserver = v.id
			end
		end       
	end
	function getservers()
		serversearch()	
		for i,v in pairs(game:GetService("HttpService"):JSONDecode(game:HttpGetAsync(gamelink))) do
			if i == "nextPageCursor" then
				if gamelink:find("&cursor=") then
					local a = gamelink:find("&cursor=")
					local b = gamelink:sub(a)
					gamelink = gamelink:gsub(b, "")
				end
				gamelink = gamelink .. "&cursor=" ..v
				getservers()
			end
		end
	end 
	getservers()
	if AutoTeleport then
		if DontTeleportTheSameNumber then 
			if #game:GetService("Players"):GetPlayers() - 4  == maxplayers then
				return warn("It has same number of players (except you)")
			elseif goodserver == game.JobId then
				return warn("Your current server is the most empty server atm") 
			end
		end
		game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, goodserver)
	end
end)

JobiJoin = ""

Misc:Textbox("JOJ ID","",true,function(value)
	JobiJoin = Value
end)

Misc:Button("Join Server",function()
	game:GetService("TeleportService"):TeleportToPlaceInstance(game.placeId, JobiJoin, game.Players.LocalPlayer)
end)


Misc:Seperator("Misc")

Misc:Toggle("Auto Rejoin",_G.imgToggle,false,function(value)
	_G.AutoRejoin = value
end)

spawn(function()
	while wait() do
		if _G.AutoRejoin then
			getgenv().rejoin = game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(child)
				if child.Name == 'ErrorPrompt' and child:FindFirstChild('MessageArea') and child.MessageArea:FindFirstChild("ErrorFrame") then
					game:GetService("TeleportService"):Teleport(game.PlaceId)
				end
			end)
		end
	end
end)

Misc:Toggle("No Clip",_G.imgToggle,false,function(value)
	_G.NoClip = value
end)

local WebHookLog = {}

local AllRequest = http_request or request or HttpPost or syn.request
function WebHookLog:WebHookKaiTanSend(WebHookUrl)

	function GetFightingStyle(Style)
		local ReturnText = ""
		for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v.Name
				end
			end
		end
		for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v.Name
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetAwaken()
		local ReturnText = ""
		local Awakened_Z = ":x:"
		local Awakened_X = ":x:"
		local Awakened_C = ":x:"
		local Awakened_V = ":x:"
		local Awakened_F = ":x:"
		for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == "Blox Fruit" then
					if v:FindFirstChild("AwakenedMoves") then
						if v.AwakenedMoves:FindFirstChild("Z") then
							Awakened_Z = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("X") then
							Awakened_X = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("C") then
							Awakened_C = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("V") then
							Awakened_V = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("F") then
							Awakened_F = ":white_check_mark:"
						end
						ReturnText = ":regional_indicator_z:"..Awakened_Z..
							"\n"..":regional_indicator_x:"..Awakened_X..
							"\n"..":regional_indicator_c:"..Awakened_C..
							"\n"..":regional_indicator_v:"..Awakened_V..
							"\n"..":regional_indicator_f:"..Awakened_F
					else
						ReturnText = "This Fruit Can't Awakened"
					end
				end
			end
		end
		for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == "Blox Fruit" then
					if v:FindFirstChild("AwakenedMoves") then
						if v.AwakenedMoves:FindFirstChild("Z") then
							Awakened_Z = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("X") then
							Awakened_X = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("C") then
							Awakened_C = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("V") then
							Awakened_V = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("F") then
							Awakened_F = ":white_check_mark:"
						end
						ReturnText = ":regional_indicator_z:"..Awakened_Z..
							"\n"..":regional_indicator_x:"..Awakened_X..
							"\n"..":regional_indicator_c:"..Awakened_C..
							"\n"..":regional_indicator_v:"..Awakened_V..
							"\n"..":regional_indicator_f:"..Awakened_F
					else
						ReturnText = "This Fruit Can't Awakened"
					end
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetWeapon(Rare)
		if Rare == "Common" then
			RareNumber = 0
		elseif Rare == "Uncommon" then
			RareNumber = 1
		elseif Rare == "Rare" then
			RareNumber = 2
		elseif Rare == "Legendary" then
			RareNumber = 3
		elseif Rare == "Mythical" then
			RareNumber = 4
		else
			return "Worng InPut"
		end
		local ReturnText = ""
		for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryWeapons")) do
			if type(v) == "table" then
				if v.Rarity then
					if tonumber(v.Rarity) == RareNumber then
						ReturnText = ReturnText .. v.Name .. "\n"
					end
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetFruitInU()
		local ReturnText = ""
		for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryFruits")) do
			if type(v) == "table" then
				if v ~= nil then
					ReturnText = ReturnText .. v.Name .. " : " .. v.Price .. "\n"
				end
			end
		end

		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetAllMelee()
		local BuyDragonTalon = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon",true))
		if BuyDragonTalon then
			if BuyDragonTalon == 1 then
				TalComplete = true
			end
		end
		local BuySuperhuman = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman",true))
		if BuySuperhuman then
			if BuySuperhuman == 1 then
				SupComplete = true
			end
		end
		local BuySharkmanKarate = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true))
		if BuySharkmanKarate then
			if BuySharkmanKarate == 1 then
				SharkComplete = true
			end
		end
		local BuyDeathStep = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep",true))
		if BuyDeathStep then
			if BuyDeathStep == 1 then
				DeathComplete = true
			end
		end
		local BuyElectricClaw = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw",true))
		if BuyElectricClaw then
			if BuyElectricClaw == 1 then
				EClawComplete = true
			end
		end
		local BuyGod = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman",true))
		if BuyGod then
			if BuyGod == 1 then
				GodComplete = true
			end
		end
		ReturnText = {}
		if SupComplete == true then
			table.insert(ReturnText,"SuperHuman")
		end
		if EClawComplete == true then
			table.insert(ReturnText,"Electric Claw")
		end
		if TalComplete == true then
			table.insert(ReturnText,"Dragon Talon")
		end
		if SharkComplete == true then
			table.insert(ReturnText,"Sharkman Karate")
		end
		if DeathComplete == true then
			table.insert(ReturnText,"Death Step")
		end
		if GodComplete == true then
			table.insert(ReturnText,"God Human")
		end

		if #ReturnText ~= 0 then
			return table.concat(ReturnText,",")
		else
			return "Not Have"
		end
	end

	local Embeds = {{
		["title"] = "**Maruko Hub Webhooks Status**",
		["color"] = tonumber(0xD936FF),
		["fields"] = {
			{
				["name"] = "User Name",
				["value"] = "||"..tostring(game.Players.LocalPlayer.Name).."||",
				["inline"] = true
			},
			{
				["name"] = "Level",
				["value"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Level").Value),
				["inline"] = true
			},
			{
				["name"] = "Fragments",
				["value"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Fragments").Value),
				["inline"] = true
			},
			{
				["name"] = "Bounty/Honor",
				["value"] = tostring(game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value),
				["inline"] = true
			},
			{
				["name"] = "Beli",
				["value"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Beli").Value),
				["inline"] = true
			},
			{
				["name"] = "Fighting Style",
				["value"] = GetFightingStyle("Melee"),
				["inline"] = true
			},
			{
				["name"] = "Sword",
				["value"] = GetFightingStyle("Sword"),
				["inline"] = true
			},
			{
				["name"] = "Devil Fruit",
				["value"] = GetFightingStyle("Blox Fruit"),
				["inline"] = true
			},
			{
				["name"] = "Gun",
				["value"] = GetFightingStyle("Gun"),
				["inline"] = true
			},
			{
				["name"] = "Accessory",
				["value"] = GetFightingStyle("Wear"),
				["inline"] = true
			},
			{
				["name"] = "Race",
				["value"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Race").Value),
				["inline"] = true
			},
			{
				["name"] = "Awakened",
				["value"] = tostring(GetAwaken()),
				["inline"] = true
			},
			{
				["name"] = "Status",
				["value"] = "```sml\n"..tostring("Melee : "..game:GetService("Players").LocalPlayer.Data.Stats.Melee:WaitForChild("Level").Value .. 
					"\nDefense : "..game:GetService("Players").LocalPlayer.Data.Stats.Defense:WaitForChild("Level").Value .. 
					"\nSword : "..game:GetService("Players").LocalPlayer.Data.Stats.Sword:WaitForChild("Level").Value.. 
					"\nGun : "..game:GetService("Players").LocalPlayer.Data.Stats.Gun:WaitForChild("Level").Value .. 
					"\nDevil Fruit : "..game:GetService("Players").LocalPlayer.Data.Stats["Demon Fruit"]:WaitForChild("Level").Value).."```",
				["inline"] = true
			},
			{
				["name"] = "Common :blue_circle:",
				["value"] = "```sml\n"..tostring(GetWeapon("Common")).."```",
				["inline"] = true
			},
			{
				["name"] = "Uncommon :green_circle:",
				["value"] = "```sml\n"..tostring(GetWeapon("Uncommon")).."```",
				["inline"] = true
			},
			{
				["name"] = "Rare :yellow_circle:",
				["value"] = "```sml\n"..tostring(GetWeapon("Rare")).."```",
				["inline"] = true
			},
			{
				["name"] = "Legendary :purple_circle:",
				["value"] = "```sml\n"..tostring(GetWeapon("Legendary")).."```",
				["inline"] = true
			},
			{
				["name"] = "Mythical :red_circle:",
				["value"] = "```sml\n"..tostring(GetWeapon("Mythical")).."```",
				["inline"] = true
			},
			{
				["name"] = "Fruit In Inventory",
				["value"] = "```sml\n"..tostring(GetFruitInU()).."```",
				["inline"] = true
			},
			{
				["name"] = "All Melee",
				["value"] = "```sml\n"..tostring(GetAllMelee()).."```",
				["inline"] = true
			},



			{
				["name"] = "ㅤ",
				["value"] = tostring("ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ"),
				["inline"] = false
			}},
		["footer"] = {
			["text"] = "Made by ! aExeur#4748".."\nTime".." : "..os.date("%c").." ("..os.date("%X")..")",
			["icon_url"] = "https://cdn.discordapp.com/attachments/834780708551393349/1035779918795112448/20221013140538_1.png"
		},
	}}

	local Message
	if _G.SendWebHookPing then
		Message = {
			['username'] = "Unique Webhook",
			["avatar_url"] = "https://cdn.discordapp.com/attachments/834780708551393349/1035779918795112448/20221013140538_1.png",
			["content"] = "@everyone",
			["embeds"] = Embeds,
		}
	else
		Message = {
			['username'] = "Unique Webhook",
			["avatar_url"] = "https://cdn.discordapp.com/attachments/834780708551393349/1035779918795112448/20221013140538_1.png",
			["embeds"] = Embeds,
		}
	end

	local DataCallBack = AllRequest({
		Url = WebHookUrl,
		Method = 'POST',
		Headers = {
			["Content-Type"] = "application/json"
		},
		Body = game:GetService("HttpService"):JSONEncode(Message)
	})
	return DataCallBack
end

function WebHookLog:SheetBestLogSend(SheetBestUrl)

	function GetFightingStyle(Style)
		ReturnText = ""
		for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v.Name
				end
			end
		end
		for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v.Name
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetAllMelee()
		BuyDragonTalon = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon",true))
		if BuyDragonTalon then
			if BuyDragonTalon == 1 then
				TalComplete = true
			end
		end
		BuySuperhuman = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman",true))
		if BuySuperhuman then
			if BuySuperhuman == 1 then
				SupComplete = true
			end
		end
		BuySharkmanKarate = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate",true))
		if BuySharkmanKarate then
			if BuySharkmanKarate == 1 then
				SharkComplete = true
			end
		end
		BuyDeathStep = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep",true))
		if BuyDeathStep then
			if BuyDeathStep == 1 then
				DeathComplete = true
			end
		end
		BuyElectricClaw = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw",true))
		if BuyElectricClaw then
			if BuyElectricClaw == 1 then
				EClawComplete = true
			end
		end
		BuyGod = tonumber(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman",true))
		if BuyGod then
			if BuyGod == 1 then
				GodComplete = true
			end
		end
		ReturnText = {}
		if SupComplete == true then
			table.insert(ReturnText,"SuperHuman")
		end
		if EClawComplete == true then
			table.insert(ReturnText,"Electric Claw")
		end
		if TalComplete == true then
			table.insert(ReturnText,"Dragon Talon")
		end
		if SharkComplete == true then
			table.insert(ReturnText,"Sharkman Karate")
		end
		if DeathComplete == true then
			table.insert(ReturnText,"Death Step")
		end
		if GodComplete == true then
			table.insert(ReturnText,"God Human")
		end

		if #ReturnText ~= 0 then
			return table.concat(ReturnText,",")
		else
			return "Not Have"
		end
	end

	function GetAwaken()
		ReturnText = ""
		Awakened_Z = "❌"
		Awakened_X = "❌"
		Awakened_C = "❌"
		Awakened_V = "❌"
		Awakened_F = "❌"
		for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == "Blox Fruit" then
					if v:FindFirstChild("AwakenedMoves") then
						if v.AwakenedMoves:FindFirstChild("Z") then
							Awakened_Z = "Z"
						end
						if v.AwakenedMoves:FindFirstChild("X") then
							Awakened_X = "X"
						end
						if v.AwakenedMoves:FindFirstChild("C") then
							Awakened_C = "C"
						end
						if v.AwakenedMoves:FindFirstChild("V") then
							Awakened_V = "V"
						end
						if v.AwakenedMoves:FindFirstChild("F") then
							Awakened_F = "F"
						end
						ReturnText = Awakened_Z..
							" : "..Awakened_X..
							" : "..Awakened_C..
							" : "..Awakened_V..
							" : "..Awakened_F
					else
						ReturnText = "This Fruit Can't Awakened"
					end
				end
			end
		end
		for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == "Blox Fruit" then
					if v:FindFirstChild("AwakenedMoves") then
						if v.AwakenedMoves:FindFirstChild("Z") then
							Awakened_Z = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("X") then
							Awakened_X = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("C") then
							Awakened_C = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("V") then
							Awakened_V = ":white_check_mark:"
						end
						if v.AwakenedMoves:FindFirstChild("F") then
							Awakened_F = ":white_check_mark:"
						end
						ReturnText = ":regional_indicator_z:"..Awakened_Z..
							" : "..":regional_indicator_x:"..Awakened_X..
							" : "..":regional_indicator_c:"..Awakened_C..
							" : "..":regional_indicator_v:"..Awakened_V..
							" : "..":regional_indicator_f:"..Awakened_F
					else
						ReturnText = "This Fruit Can't Awakened"
					end
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetWeapon()
		local ReturnText = ""
		for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryWeapons")) do
			if type(v) == "table" then
				if v.Name then
					ReturnText = ReturnText .. v.Name .. " "
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetFruitInU()
		local ReturnText = ""
		for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryFruits")) do
			if type(v) == "table" then
				if v ~= nil then
					ReturnText = ReturnText .. v.Name .. " "
				end
			end
		end

		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function GetWeaponMastery(Style)
		ReturnText = ""
		for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v:FindFirstChild("Level").Value
				end
			end
		end
		for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
			if v:IsA("Tool") then
				if v.ToolTip == Style then
					ReturnText = v:FindFirstChild("Level").Value
				end
			end
		end
		if ReturnText ~= "" then
			return ReturnText
		else
			return "Not Have"
		end
	end

	function Abbreviate(x)
		local abbreviations = {
			"K", -- 4 digits
			"M", -- 7 digits
			"B", -- 10 digits
			"T", -- 13 digits
			"QD", -- 16 digits
			"QT", -- 19 digits
			"SXT", -- 22 digits
			"SEPT", -- 25 digits
			"OCT", -- 28 digits
			"NON", -- 31 digits
			"DEC", -- 34 digits
			"UDEC", -- 37 digits
			"DDEC", -- 40 digits
		}
		if x < 1000 then 
			return tostring(x)
		end

		local digits = math.floor(math.log10(x)) + 1
		local index = math.min(#abbreviations, math.floor((digits - 1) / 3))
		local front = x / math.pow(10, index * 3)

		return string.format("%i%s+", front, abbreviations[index])
	end

	local Message
	Message = {
		["UserName"] = tostring(game.Players.LocalPlayer.Name),
		["Level"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Level").Value),
		["Weapon inventory"] = tostring(GetWeapon()),
		["Fruit inventory"] = tostring(GetFruitInU()),
		["Melee"] = tostring(GetAllMelee()),
		["Fruit"] = tostring(GetFightingStyle("Blox Fruit")),
		["Fruit Mastery"] = tostring(GetWeaponMastery("Blox Fruit")),
		["Fruit Awake"] = tostring(GetAwaken()),
		["Beli"] = tostring(Abbreviate(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Beli").Value)),
		["Fragment"] = tostring(Abbreviate(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Fragments").Value)),
		["Race"] = tostring(game:GetService("Players").LocalPlayer.Data:FindFirstChild("Race").Value)
	}

	local DataCallBack = AllRequest({
		Url = SheetBestUrl,
		Method = 'POST',
		Headers = {
			["Content-Type"] = "application/json"
		},
		Body = game:GetService("HttpService"):JSONEncode(Message)
	})
	return DataCallBack
end

Misc:Seperator("Main - Mob")

Misc:Button("Remove Lave",function()
	for i,v in pairs(game.Workspace:GetDescendants()) do
		if v.Name == "Lava" then   
			v:Destroy()
		end
	end
	for i,v in pairs(game.ReplicatedStorage:GetDescendants()) do
		if v.Name == "Lava" then   
			v:Destroy()
		end
	end
end)

Misc:Button("Invisible (lag)",function()
	game.Players.LocalPlayer.Character.LowerTorso.Root:Destroy()
end)

Misc:Button("Invisible [Remove]",function()
	local removeNametags = true -- remove custom billboardgui nametags from hrp, could trigger anticheat

	local plr = game:GetService("Players").LocalPlayer
	local character = plr.Character
	local hrp = character.HumanoidRootPart
	local old = hrp.CFrame

	if not character:FindFirstChild("LowerTorso") or character.PrimaryPart ~= hrp then
		return print("unsupported")
	end

	if removeNametags then
		local tag = hrp:FindFirstChildOfClass("BillboardGui")
		if tag then tag:Destroy() end

		hrp.ChildAdded:Connect(function(item)
			if item:IsA("BillboardGui") then
				task.wait()
				item:Destroy()
			end
		end)
	end

	local newroot = character.LowerTorso.Root:Clone()
	hrp.Parent = workspace
	character.PrimaryPart = hrp
	character:MoveTo(Vector3.new(old.X,9e9,old.Z))
	hrp.Parent = character
	task.wait(0.5)
	newroot.Parent = hrp
	hrp.CFrame = old
end)

Misc:Button("Max Zoom", function()
	while wait() do
		game.Players.LocalPlayer.CameraMaxZoomDistance = 9223372036854718
	end
end)

Misc:Textbox("BaseSheet","",true,function(value)
	Baselink = Value
end)

Misc:Button("Send BaseSheet", function()
	WebHookLog:SheetBestLogSend(Baselink)
end)

Misc:Button("Max Zoom", function()
	while wait() do
		game.Players.LocalPlayer.CameraMaxZoomDistance = 9223372036854718
	end
end)

Misc:Seperator("State")

Misc:Dropdown("Select Haki State",{"State 0","State 1","State 2","State 3","State 4","State 5"},function(value)
	_G.SelectStateHaki = value
end)

Misc:Button("Change Buso Haki State",function()
	if _G.SelectStateHaki == "State 0" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",0)
	elseif _G.SelectStateHaki == "State 1" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",1)
	elseif _G.SelectStateHaki == "State 2" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",2)
	elseif _G.SelectStateHaki == "State 3" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",3)
	elseif _G.SelectStateHaki == "State 4" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",4)
	elseif _G.SelectStateHaki == "State 5" then
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("ChangeBusoStage",5)
	end
end)

Misc:Seperator("Boost FPS")

Misc:Button("FPS Booster",function()
	FPSBooster()
end)

function FPSBooster()
	local decalsyeeted = true
	local g = game
	local w = g.Workspace
	local l = g.Lighting
	local t = w.Terrain
	sethiddenproperty(l,"Technology",2)
	sethiddenproperty(t,"Decoration",false)
	t.WaterWaveSize = 0
	t.WaterWaveSpeed = 0
	t.WaterReflectance = 0
	t.WaterTransparency = 0
	l.GlobalShadows = false
	l.FogEnd = 9e9
	l.Brightness = 0
	settings().Rendering.QualityLevel = "Level01"
	for i, v in pairs(g:GetDescendants()) do
		if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
			v.Material = "Plastic"
			v.Reflectance = 0
		elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
			v.Transparency = 1
		elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
			v.Lifetime = NumberRange.new(0)
		elseif v:IsA("Explosion") then
			v.BlastPressure = 1
			v.BlastRadius = 1
		elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
			v.Enabled = false
		elseif v:IsA("MeshPart") then
			v.Material = "Plastic"
			v.Reflectance = 0
			v.TextureID = 10385902758728957
		end
	end
	for i, e in pairs(l:GetChildren()) do
		if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
			e.Enabled = false
		end
	end
end

Misc:Button("Invisible",function()
	game:GetService("Players").LocalPlayer.Character.LowerTorso:Destroy()
end)

Misc:Button("Click TP Tool",function()
	ClickTpTool()
end)

function ClickTpTool()
	local plr = game:GetService("Players").LocalPlayer
	local mouse = plr:GetMouse()
	local tool = Instance.new("Tool")
	tool.RequiresHandle = false
	tool.Name = "Teleport Tool"
	tool.Activated:Connect(function()
		local root = plr.Character.HumanoidRootPart
		local pos = mouse.Hit.Position+Vector3.new(0,2.5,0)
		local offset = pos-root.Position
		root.CFrame = root.CFrame+offset
	end)
	tool.Parent = plr.Backpack
end

Misc:Toggle("Remove Fog",_G.imgToggle,false,function(value)
	_G.RVFG_SsXz = value
end)

task.spawn(function()
	while wait(0.01) do
		pcall(function()
			if _G.RVFG_SsXz then
				if game:GetService("Lighting"):FindFirstChild("Sky") then game:GetService("Lighting").Sky:Destroy()
				end
			end
		end)
	end
end)

Misc:Toggle("Auto Click",_G.imgToggle,false,function(value)
	_G.click = value
end)

spawn(function()
	game:GetService("RunService").RenderStepped:Connect(function()
		if _G.click then
			pcall(function()
				game:GetService'VirtualUser':CaptureController()
				game:GetService'VirtualUser':Button1Down(Vector2.new(0,1,0,1))
			end)
		end
	end)
end)

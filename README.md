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
    
    local Tab = Window:CreateTab("Tab Example", 4483362458) -- Title, Image
    local Tab2 = Window:CreateTab("Tab Example 2") -- Title, Image
    local Section = Tab:CreateSection("Section Example",false) -- The 2nd argument is to tell if its only a Title and doesnt contain element
    local Button = Tab:CreateButton({
        Name = "Button Example",
        Info = {
            Title = 'This is a Button',
            Description = 'This is a description for the button you know.',
        },
        Interact = 'Changable',
        Callback = function()
            print('Pressed')
        end,
    })
    local Toggle = Tab:CreateToggle({
        Name = "Toggle Example",
        Info = {
            Title = 'Slider template',
            Image = '12735851647',
            Description = 'Just a slider for stuff',
        },
        CurrentValue = false,
        Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
        Callback = function(Value)
            print(Value)
        end,
    })

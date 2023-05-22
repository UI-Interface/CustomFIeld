# Rayfield Interface Suite
This is the written documentation for Rayfield Interface Suite

Last updated for the Beta 7R release

## Booting the Library
```lua
local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/Saturn12132/ArrayField/main/Module.lua'))()
```

### Secure Mode
If the game you're trying to run Rayfield Interface Suite on, is detecting or crashing when you use Rayfield Interface Suite, try using Secure Mode:
- Place `getgenv().SecureMode = true` above the initial Rayfield loadstring

Rayfield will now use Secure Mode and attempt to reduce detection
- Note: This may cause some elements of the UI to look lower quality or may increase loading times slightly

### Enabling Configuration Saving
- Enable ConfigurationSaving in the CreateWindow function
- Choose an appropiate FileName in the CreateWindow function
- Choose an unique flag identifier for each supported element you create
- Place `Rayfield:LoadConfiguration()` at the bottom of all your code

Rayfield will now automatically save and load your configuration

## Creating a Window
```lua
local Window = Rayfield:CreateWindow({
	Name = "Rayfield Example Window",
	LoadingTitle = "Rayfield Interface Suite",
	LoadingSubtitle = "by Sirius",
	ConfigurationSaving = {
		Enabled = true,
		FolderName = nil, -- Create a custom folder for your hub/game
		FileName = "Big Hub"
	},
        Discord = {
        	Enabled = false,
        	Invite = "sirius", -- The Discord invite code, do not include discord.gg/
        	RememberJoins = true -- Set this to false to make them join the discord every time they load it up
        },
	KeySystem = true, -- Set this to true to use our key system
	KeySettings = {
		Title = "Sirius Hub",
		Subtitle = "Key System",
		Note = "Join the discord (discord.gg/sirius)",
		FileName = "SiriusKey",
		SaveKey = true,
		GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
		Key = "Hello"
	}
})
```

## Creating a Tab
```lua
local Tab = Window:CreateTab("Tab Example", 4483362458) -- Title, Image
```

## Creating a Section
```lua
local Section = Tab:CreateSection("Section Example", true/false)
```
### Updating a Section
```lua
Section:Set("Section Example")

Section:Destroy()
Section:Lock()
Section:Unlock()
```

## Notifying the user
```lua
Rayfield:Notify({
    Title = "Notification Title",
    Content = "Notification Content",
    Duration = 6.5,
    Image = 4483362458,
    Actions = { -- Notification Buttons
        Ignore = {
            Name = "Okay!",
            Callback = function()
                print("The user tapped Okay!")
            end
		},
	},
})
```

## Creating a Button
```lua
local Button = Tab:CreateButton({
	Name = "Button Example",
	Callback = function()
		-- The function that takes place when the button is pressed
	end,
})
```
### Updating a Button
```lua
Button:Set("Button Example")
```

## Creating a Toggle
```lua
local Toggle = Tab:CreateToggle({
	Name = "Toggle Example",
	CurrentValue = false,
	Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		-- The function that takes place when the toggle is pressed
    		-- The variable (Value) is a boolean on whether the toggle is true or false
	end,
})
```
### Updating a Toggle
```lua
Toggle:Set(false)
```

## Creating a Color Picker
```lua
local ColorPicker = Tab:CreateColorPicker({
	Name = "Color Picker",
	Info = 'info or description',
	SectionParent = Section, -- The Section it's parented to. (Optional)
	Color = Color3.fromRGB(2,255,255),
	Flag = "ColorPicker1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		-- The function that takes place every time the color picker is moved/changed
		-- The variable (Value) is a Color3fromRGB value based on which color is selected
	end
})
```


## Creating a Slider
```lua
local Slider = Tab:CreateSlider({
	Name = "Slider Example",
	Range = {0, 100},
	Increment = 10,
	Suffix = "Bananas",
	CurrentValue = 10,
	Flag = "Slider1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Value)
		-- The function that takes place when the slider changes
    		-- The variable (Value) is a number which correlates to the value the slider is currently at
	end,
})
```
### Updating a Slider
```lua
Slider:Set(10) -- The new slider integer value
```

## Creating a Label
```lua
local Label = Tab:CreateLabel("Label Example")
```
### Updating a Label
```lua
Label:Set("Label Example")
```

## Creating a Paragraph
```lua
local Paragraph = Tab:CreateParagraph({Title = "Paragraph Example", Content = "Paragraph Example"})
```
### Updating a Paragraph
```lua
Paragraph:Set({Title = "Paragraph Example", Content = "Paragraph Example"})
```

## Creating an Adaptive Input (TextBox)
```lua
local Input = Tab:CreateInput({
   Name = "Input Example",
   Info = "Input info/Description.", -- Speaks for itself, Remove if none.
   PlaceholderText = "Input Placeholder",
   NumbersOnly = true, -- If the user can only type numbers. Remove if none.
   CharacterLimit = 15, --max character limit. Remove if none.
   OnEnter = true, -- Will callback only if the user pressed ENTER while the box is focused.
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
   -- The function that takes place when the input is changed
   -- The variable (Text) is a string for the value in the text box
   end,
})
```



## Creating a Keybind
```lua
local Keybind = Tab:CreateKeybind({
	Name = "Keybind Example",
	CurrentKeybind = "Q",
	HoldToInteract = false,
	Flag = "Keybind1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Keybind)
		-- The function that takes place when the keybind is pressed
    		-- The variable (Keybind) is a boolean for whether the keybind is being held or not (HoldToInteract needs to be true)
	end,
})
```
### Updating a Keybind
```lua
Keybind:Set("RightCtrl") -- Keybind (string)
```

## Creating a Dropdown menu
```lua
local Dropdown = Tab:CreateDropdown({
	Name = "Dropdown Example",
	Options = {"Option 1","Option 2"},
	CurrentOption = "Option 1",
  	MultiSelection = false,
	Flag = "Dropdown1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
	Callback = function(Option)
	  	  -- The function that takes place when the selected option is changed
    	  -- The variable (Option) is a string for the value that the dropdown was changed to
	end,
})
```
### Updating a Dropdown
```lua
Dropdown:Set("Option 2") -- The new option value
Dropdown:Refresh({<table>},<selected>)

Dropdown:Add('test')
Dropdown:Remove('test')
```

## Check the value of an existing element
To check the current value of an existing element, using the variable, you can do `ElementName.CurrentValue`, if it's a keybind or dropdown, you will need to use `KeybindName.CurrentKeybind` or `DropdownName.CurrentOption`
You can also check it via the flags from `Rayfield.Flags`


## Destroying the Interface
```lua
Rayfield:Destroy()
```

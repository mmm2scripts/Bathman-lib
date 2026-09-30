# CrimsonUI

A lightweight, themeable Roblox UI library built for clean and responsive interfaces.

CrimsonUI provides a simple API for creating polished menus with tabs, controls, notifications, themes, keybinds, and configuration support.

## Features

### Elements

* Buttons
* Button rows
* Toggles
* Sliders
* Textboxes
* Single-select dropdowns
* Multi-select dropdowns
* Keybinds
* Labels
* Sections
* Dividers

### Library Features

* Multiple built-in themes
* Custom themes
* Live theme switching
* Tabs
* Animated notifications
* Draggable toggle button
* UI scaling
* Config save/load
* Config export/import
* Element flags
* Runtime UI controls

## Quick Start

```lua
local Library = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/YOUR_USER/CrimsonUI/main/CrimsonUI.lua"
))()

local Window = Library.new({
    Title = "My Hub"
})

local Main = Window:AddTab("Main")

Main:AddButton({
    Text = "Hello",
    Callback = function()
        print("Hello from CrimsonUI")
    end
})

Window:AddSettingsTab()
```

For a complete example, see [`examples/example.lua`](examples/example.lua).

## Built-in Themes

CrimsonUI includes several ready-to-use themes:

* `Crimson`
* `Midnight`
* `Emerald`
* `Mono`

Themes can be changed while the UI is running.

```lua
Window:SetTheme("Midnight")
```

Custom themes are also supported through `Library.MakeTheme()`.

## Configuration

Elements can use flags to automatically include their values in configurations.

```lua
Main:AddToggle({
    Name = "Auto Farm",
    Flag = "AutoFarm",
    Default = false,

    Callback = function(Value)
        print(Value)
    end
})
```

Available configuration methods:

```lua
Window:SaveConfig()
Window:LoadConfig()
Window:DeleteConfig()
Window:ListConfigs()
Window:ExportConfig()
Window:ImportConfig()
```

## Example

```lua
local Main = Window:AddTab("Main")

Main:AddSection("Player")

Main:AddSlider({
    Name = "WalkSpeed",
    Flag = "WalkSpeed",
    Min = 16,
    Max = 200,
    Default = 16,

    Callback = function(Value)
        print("WalkSpeed:", Value)
    end
})

Main:AddToggle({
    Name = "Infinite Jump",
    Flag = "InfiniteJump",
    Default = false,

    Callback = function(Value)
        print("Infinite Jump:", Value)
    end
})
```

## Real-world integration

[`MonoMM2.lua`](../MonoMM2.lua) at the repository root is a full Murder Mystery 2
script whose menu runs entirely on CrimsonUI. It is a useful reference if you are
porting a large script onto this library, because it shows how to work around the
one thing CrimsonUI deliberately does not have:

* **Per-element keybinds.** CrimsonUI toggles have no key chip, so the script
  builds a `Keybinds` tab of `AddKeybind` pickers (using `ChangedCallback` only)
  and drives the toggles from one shared `InputBegan` / `InputEnded` handler.

It runs on the default Crimson theme, uses the flag system for save/load, wraps
`Elements[]._opts.Callback` to implement autosave, and maps Mono's six categories
onto six tabs — ten in total, adding Keybinds, Players, Server and Settings.

Note that elements take no description or tooltip field, so there is nowhere to
hang long help text for a feature. If your script needs it, add your own
`AddLabel` rows.

## Project Structure

```text
Bathman-lib/
├── MonoMM2.lua
└── CrimsonUI/
    ├── CrimsonUI.lua
    ├── README.md
    ├── LICENSE
    └── examples/
        └── example.lua
```

## Requirements

CrimsonUI is designed to work without requiring external UI frameworks.

Configuration features use the executor's file functions when available:

* `writefile`
* `readfile`
* `isfile`
* `makefolder`

The core UI does not depend on configuration functionality.

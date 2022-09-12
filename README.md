# auto-dark-mode.nvim
A Neovim plugin for macOS, Linux, and Windows that automatically changes the
editor appearance based on system settings.

## Installation
### Using [vim-plug](https://github.com/junegunn/vim-plug)

```vim
Plug 'charlesnchr/auto-dark-mode.nvim'
```

## Dark mode setting
On macOS the dark mode status is controlled via system settings and the plugin reads the status via a system call.

In contrast, for support on Linux the current dark mode status is controlled via an environment variable, e.g.  

```
> cat ~/dotfiles/is_dark_mode
1
```
which indicates that the dark mode is on.

The value can be toggled by editing this file, or for instance by a zshrc command such as

```
colo() {
    if [ $(cat ~/dotfiles/is_dark_mode) -eq 1 ]; then x=0; else x=1; fi; echo $x > ~/dotfiles/is_dark_mode
}
```



## Configuration
You need to call `setup` for initialization.
`setup` accepts a table with options – `set_dark_mode` function,
`set_light_mode` function, and `update_interval` integer.

`set_dark_mode` is called when the system appearance changes to dark mode, and
`set_light_mode` is called when it changes to light mode.
By default, they just change the background option, but you can do whatever you like.

`update_interval` is how frequently the system appearance is checked.
The value is stored in milliseconds. Defaults to `3000`.

```lua
local auto_dark_mode = require('auto-dark-mode')

auto_dark_mode.setup({
	update_interval = 1000,
	set_dark_mode = function()
		vim.api.nvim_set_option('background', 'dark')
		vim.cmd('colorscheme gruvbox')
	end,
	set_light_mode = function()
		vim.api.nvim_set_option('background', 'light')
		vim.cmd('colorscheme gruvbox')
	end,
})
```

### Using [lazy](https://github.com/folke/lazy.nvim)

```lua
return {
  "f-person/auto-dark-mode.nvim",
  config = {
    update_interval = 1000,
    set_dark_mode = function()
      vim.api.nvim_set_option("background", "dark")
      vim.cmd("colorscheme gruvbox")
    end,
    set_light_mode = function()
      vim.api.nvim_set_option("background", "light")
      vim.cmd("colorscheme gruvbox")
    end,
  },
}
```


#### Disable
You can disable `auto-dark-mode.nvim` at runtime via `lua require('auto-dark-mode').disable()`.

## Thanks To
* [@nekowinston](https://github.com/nekowinston) for implementing Linux support and other contributions! <3
* [@adityamwagh](https://github.com/adityamwagh) for implementing Windows support

# Support
If you enjoy the plugin and want to support what I do

<a href="https://www.buymeacoffee.com/fperson" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41"  width="174"></a>
## Requirements
* Linux
* macOS
* Neovim


### Credits

The macOS functionality of the plugin is based on [https://github.com/f-person/auto-dark-mode.nvim](https://github.com/f-person/auto-dark-mode.nvim).

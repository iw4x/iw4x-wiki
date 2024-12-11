<!-- TITLE:Configuration -->

IW4x (and the base game) are configured using DVars, or Dynamic Variables.
DVars can be set using the console or configuration files (.cfg).

# Console
To open the console, press `~` (tilde) on your keyboard. This key may differ by layout, its usually the key under `esc`, next to `1`.

IW4x supports autocompletion, so you can type the beginning of a DVar name and press `tab` to autocomplete it.
If you want to set the value of a new/undefined DVar, you can do so using the `set` command:

```
set cg_coolDvar 1
```

# Configuration Files
IW4x can use multiple configuration files
- `players/iw4x_config.cfg`
- `players/autoexec.cfg`

Server configs are stored in the userraw folder instead, they can be named however you like. Pre-made configs are available on [GitHub](https://github.com/iw4x/iw4-server-configs).
:::download
https://github.com/iw4x/iw4-server-configs/archive/refs/heads/main.zip
:::
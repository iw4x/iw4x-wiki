<!-- TITLE:Configuration -->

IW4x (and the base game) are configured using DVars, or Dynamic Variables.
DVars can be set using the console or configuration files (.cfg).
Some DVars can be set in the game's options menu, but most of them can only be set in the console. Many DVars are restricted to the server or client, some will also depend on other DVars like `sv_cheats` being set to a specific value.

# Console
To open the console, press `~` (tilde) on your keyboard. This key may differ by layout, its usually the key under `esc`, next to `1`.

The IW4x console supports autocompletion, so you can type the beginning of a DVar name and press `tab` to autocomplete it.
You can expand the whole console using `shift + ~`.

Changing the value of a DVar/executing a command is as simple as typing it, followed by its value and pressing `enter`.
```
com_maxfps 333{ENTER}
```


If you want to set the value of a new/undefined DVar, you can do so using the `set` command:

```
set cg_coolDvar 1
```

# Configuration Files
IW4x automatically loads `players/iw4x_config.cfg`, which is the default config file.

Server configs are stored in the userraw folder instead, they can be named however you like. Pre-made configs are available on [GitHub](https://github.com/iw4x/iw4-server-configs). On servers `userraw/autoexec.cfg` or `mods/modname/autoexec.cfg` will also be executed automatically.

Config files can be loaded using the `exec` command.

```
exec my_custom_config.cfg
```

# Commonly modified DVars


| DVar | Example | Description |
| -------- | -------- | -------- |
| name | name "Unknown Soldier" | Changes the player name |
| unlockstats | unlockstats | Unlock everything and rank up to max prestige |
| cg_fov | cg_fov 90 (default 65) | Changes your field of view |
| sensitivity | sensitivity 0.9 | Used to fine- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

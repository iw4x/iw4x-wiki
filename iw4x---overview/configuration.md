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

# Commonly DVars/Commands


| DVar/Command | Example | Description |
| -------- | -------- | -------- |
| name | name "Unknown Soldier" | Changes the player name |
| unlockstats | unlockstats | Unlock everything and rank up to max prestige |
| cg_fov | cg_fov 90 (default 65) | Changes your field of view |
| sensitivity | sensitivity 0.9 | Used to fine-tune your mouse sensitivity |
| intro | intro 0 | Toggle the IW4x intro on startup |
| cg_drawfps | cg_drawFPS 1 | Display the FPS counter |
| cl_yawspeed | cl_yawspeed 800 | Adjust the yaw(turn)speed |
| customtitle | customtitle "IW4x" | Sets a custom title on your calling card |
| com_maxfps | com_maxfps 333 | Sets the FPS limit |
| connect | connect 127.0.0.1:26960 | Connect to a server |
| map | map mp_rust | Change the current map |
| fast_restart | fast_restart | Restart the current map without loading screen |
| map_restart | map_restart | Restart the current map |
| devmap | devmap mp_rust | Load a map with sv_cheats enabled  |
| developer | developer 1 | Enable developer debug mode |
| god | god | Makes the player invinicible |
| ufo | ufo | Enable ufo mode |
| noclip | noclip | Disables collosions and allows the player to fly |
| g_gametype | g_gametype gun | Change the gametype |
| rcon login | rcon login [password] | Login to rcon server console |
| rcon | rcon map mp_rust | Execute command on the rcon server |
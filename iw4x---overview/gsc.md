<!-- TITLE:GSC -->

# GSC Scripting Language Documentation

GSC (Game Script Code) is a scripting language designed for creating and managing game logic, behaviors, and interactions within the game environment. This documentation provides a short overview of the GSC syntax and operators. GSC syntax is similiar to C++ and generally rather easy to understand.
This documentation is specifically targeted at IW4x and is __not__ meant to teach you how to code but rather as a reference to get you started.
Your most important resource for modding will be a [GSC dump](https://github.com/FreeTheTech101/IW4-Dump-Files) from the original game.

## Variables and Data Types

GSC supports various data types, including integers, floats, strings, arrays, vectors, and entities. Variables are dynamically typed and can be assigned without explicit type declarations.

```cpp
score = 0;
playerName = "PlayerOne";
position = (0, 0, 0);
isAlive = true;
ent = undefined;
```

## Functions

Functions are the building blocks of GSC scripts, allowing for reusable code and organized logic. The entry-point function is called `init`.

### Function Definition

Functions are defined with a name and a list of parameters. They can perform actions, return values, or manipulate entities.

```cpp
activate_exploder(num)
{
    // Function body
}
```

### Mandatory and Optional Arguments

Functions can have both mandatory and optional arguments. Optional arguments are handled using `IsDefined` to check if they were provided.

```cpp
getClosest(org, array, maxdist)
{
    if (!IsDefined(maxdist))
        maxdist = 500000; // Default value
    // Function body
}
```

## Control Structures

GSC provides standard control structures for managing the flow of execution within scripts.

### Conditional Statements

Conditional statements execute code blocks based on specified conditions. GSC supports `if`, `else if`, `else`, and `switch` statements.

```cpp
if (condition)
{
    // Code if condition is true
}
else if (anotherCondition)
{
    // Code if anotherCondition is true
}
else
{
    // Code if none of the above conditions are true
}

switch(variable)
{
    case "option1":
        // Code for option1
        break;
    case "option2":
        // Code for option2
        break;
}
```

GSC also supports single line if statements.

```cpp
if (condition)
    println("True");
```

### Loops

Loops allow for repeated execution of code blocks.
GSC supports `for`, `foreach` and `while` loops. Infinite loops are usually created using `for (;;)`.
Loops can be paused using `waittill` and `waittill_either` until a certain event occurs, for example `waittill("connected", player);` will pause the loop until a player connects to the match. `wait(0.1)` is used to pause the loop for a set amount of time. The minimum wait time used is usually 0.05. Loops support the typical `continue` and `break` statements.

- `for(;;)`, `while(true)` - Infinite loop
- `for (i = 0;i < 15;i++)`, `while (i < 15)` - Conditional loop
- `foreach (player in level.players)`
- `waittill("connected", player)` - Pause thread until event is fired
- `waittill_either("weapon_fired", "giveLoadout")`
- `wait(0.1)`, `wait(15)`
- `continue`, `break`


```cpp
for (;;)
{
    // Repeating actions
    wait(1)
}

foreach (player in level.players)
{
    println(player.name);
}

while (true)
{
    // Repeating actions
    wait(0.05)
}
```

## Operators

GSC includes standard operators for arithmetic, comparison, and logical operations.

- **Arithmetic Operators**: `+`, `-`, `*`, `/`, `%`
- **Comparison Operators**: `==`, `!=`, `<`, `>`, `<=`, `>=`
- **Logical Operators**: `&&` (AND), `||` (OR), `!` (NOT)

```cpp
sum = a + b;
isEqual = (a == b);
isValid = (x > 0) && (y < 10);
```

Example power and rounding functions.

```cpp
pow(base, exp) {
    if (exp == 0) { return 1; }
    return base * pow(base, exp - 1);
}

round(num, dec) {
    power = pow(10, dec);
    x = num * power;
    x += 0.5;
    x = floor(x) / power;
    return x;
}
```

## Arrays

Arrays store collections of elements and can hold various data types, including entities.

```cpp
players = [];
players[size] = player1;
players[size] = player2;

foreach (player in players)
{
    println(player.name);
}
```

## Strings

```
- `isSubStr`
- `string_starts_with`
```

## Threads and Coroutines

GSC utilizes threads to handle concurrent execution.
Threads can be stored on different entities, for example the `level` or `player`. You will often see the use of `self` to refer to the current entity.
Threads can be set to end when a certain event occurs using `endon`.

```cpp
init()
{
	level thread onPlayerConnect();
}

onPlayerConnect()
{
    // This thread does not contain an endon, so it will run until the match ends or the map changes.
    while (true)
    {
        level waittill("connected", player);
        player thread onPlayerSpawned();
    }
}

onPlayerSpawned()
{
    // This thread will end itself when the player disconnects
    self endon("disconnect");
    while (true)
    {
        self waittill("spawned_player");
        self setClientDvar("r_fog", 0);
    }
}
```

## Notifiers

Notifiers are used to send an Event that can be caught with `waittill`.

```cpp
level notify("spawned_player")
self notify("graceComplete")
```

You can implement custom player commands (triggered using the console or a keybind) using a notifier too:
```cpp
self notifyOnplayerCommand("notifiername", "+commandname");
while (true)
{
    self waittill("notifiername");
    println("Command executed");
}
```

## Events
- `connect`
  - player; emitted on player connected
- `disconnect`
  - player, emitted on disconnect
- `player_spawned`, `spawned`
  - player; emitted on player (re)spawn
- `giveLoadout`
  - player; emitted when the player is given their chosen loadout (on spawn & class change)

## HUD
It's possible to create fully custom HUDs.
`createFontString` and `createServerFontString` can be used to create text elements on either a specific player or the entire server.

```cpp
info = level createServerFontString("objective", 0.95);
info setPoint("CENTER", "BOTTOM", 0, -10);
info.glowalpha = .6;
info.hideWhenInMenu = true;
info.glowcolor = ( .7, .3, 1 );
info setText("Fancy texty");
```

## Weapons/Perks
- `player getCurrentWeapon()`
- `player takeWeapon("semtex_mp")`
- `player _unsetperk("specialty_pistoldeath")`
- `player maps\mp\perks\_perks::givePerk("specialty_quickdraw")`
- `player switchToWeapon(weapon)`

Weapons are built to a weapon string which contains the base weapon, attachments and camos.
To check for a base weapon `isSubStr` can be used `isSubStr(weapon, "cheytac")` (cheytac = intervention).


## Comments

Comments are used to annotate and explain code. GSC supports single-line and multi-line comments.

```cpp
// This is a single-line comment

/*
  This is a
  multi-line comment
*/
```

## Includes

Includes go at the top of a script and are used to include other scripts, mostly utility collections that provide pre-defined functions for common tasks.
Reference a GSC dump to find includes and functions.

```cpp
#include maps\mp\gametypes\_hud_util;
```

## IW4X-Specific Features

### Loading scripts

Scripts are loaded automatically from the `userraw/scripts` folder. They are simple text files with the `.gsc` extension. Only the host (dedicated or private match) will load scripts, but they affect all clients.

### replaceFunc

`replaceFunc` allows replacing an existing function with a new one.

```cpp
#include maps\mp\gametypes\_damage;

init()
{
        replaceFunc(maps\mp\gametypes\_damage::Callback_PlayerDamage, ::playerDamage_stub);
}

isAllowedWeapon(weapon) {
        if (!(
                isSubStr(weapon, "thermal") ||
                isSubStr(weapon, "heartbeat") ||
                isSubStr(weapon, "acog") ||
                isSubStr(weapon, "silencer") ||
                isSubStr(weapon, "riotshield")
        ) && (
                isSubStr(weapon, "cheytac") ||
                isSubStr(weapon, "m40a3") ||
                isSubStr(weapon, "throwingknife")
        )) {
                return true;
        }
        return false;
}

playerDamage_stub(eInflictor, eAttacker, iDamage, iDFlags, sMeansOfDeath, sWeapon, vPoint, vDir, sHitLoc, psOffsetTime) {
        damage = 0;
        if (isAllowedWeapon(sWeapon)) {
                damage = 1000;
        }
        if (sMeansOfDeath == "MOD_FALLING") {
                damage = iDamage * 0.8;
        }

        maps\mp\gametypes\_damage::Callback_PlayerDamage_internal(
                eInflictor,
                eAttacker,
                self,
                damage,
                iDFlags,
                sMeansOfDeath,
                sWeapon,
                vPoint,
                vDir,
                sHitLoc,
                psOffsetTime
        );
}

```

## Example scripts

### Player-togglable Crosshair
```cpp
#include maps\mp\gametypes\_hud_util;

init() {
    level thread onPlayerConnect();
}

onPlayerConnect() {
    while (true) {
        level waittill("connected", player);
        player thread crosshair();
    }
}

crosshair() {
    self endon("disconnect");

    // Create a text element on the HUD. We could use `createServerFontString` to create a global crosshair.
    crosshair = self createFontString("objective", 0.95);
    crosshair setPoint("CENTER", "CENTER", 0, 0);
    crosshair.glowalpha = .8;
    crosshair.hideWhenInMenu = true;
    crosshair.glowcolor = ( .2, .2, .2 );
    crosshair.color = ( .75, .75, .75 );
    crosshair.alpha = 0.9;
    crosshair setText("+");

    // Store the state of the crosshair in a variable
    crosshair_enabled = true;

    // Register a command that toggles the crosshair
    self notifyOnplayerCommand("crosshair", "+crosshair");

    while (true) {
        // Wait for the command to be executed
        self waittill("crosshair");

        // Toggle the crosshair
        if (crosshair_enabled) {
            crosshair setText("");
            crosshair_enabled = false;
        } else {
            crosshair setText("+");
            crosshair_enabled = true;
        }
    }
}
```

### Setting client dvars

```cpp
init()
{
    level thread onPlayerConnect();
}

onPlayerConnect()
{
    while (true)
    {
        level waittill("connected", player);
        player thread onPlayerSpawned();
    }
}

onPlayerSpawned()
{
    self endon("disconnect");

    while (true)
    {
        self waittill("spawned_player");
        self setClientDvar("r_fog", 0);
        self setClientDvar("fx_enable", 0);
    }
}
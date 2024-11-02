<!-- TITLE:GSC -->

# GSC Scripting Language Documentation

GSC (Game Script Code) is a scripting language designed for creating and managing game logic, behaviors, and interactions within the game environment. This documentation provides a comprehensive overview of the GSC syntax and operators. It also highlights IW4X-specific extensions and functionalities that enhance the standard GSC capabilities.

## Table of Contents

- [Basic Syntax](#basic-syntax)
- [Variables and Data Types](#variables-and-data-types)
- [Functions](#functions)
  - [Function Definition](#function-definition)
  - [Mandatory and Optional Arguments](#mandatory-and-optional-arguments)
- [Control Structures](#control-structures)
  - [Conditional Statements](#conditional-statements)
  - [Loops](#loops)
- [Operators](#operators)
- [Arrays](#arrays)
- [Threads and Coroutines](#threads-and-coroutines)
- [Entities and Entity Functions](#entities-and-entity-functions)
- [Events and Endons](#events-and-endons)
- [Event Notifications](#event-notifications)
- [Comments](#comments)
- [IW4X-Specific Features](#iw4x-specific-features)
- [Examples](#examples)

## Basic Syntax

GSC scripts are organized into functions and threads that define the behavior of game entities. Functions are declared using their name followed by parentheses, containing parameters if any. Code blocks are enclosed within braces `{}`.

```gsc
function_name(arg1, arg2)
{
    // Code block
}
```

## Variables and Data Types

GSC supports various data types, including integers, floats, strings, vectors, and entities. Variables are dynamically typed and can be assigned without explicit type declarations.

```gsc
score = 0
playerName = "PlayerOne"
position = (0, 0, 0)
isAlive = true
ent = undefined
```

## Functions

Functions are the building blocks of GSC scripts, allowing for reusable code and organized logic.

### Function Definition

Functions are defined with a name and a list of parameters. They can perform actions, return values, or manipulate entities.

```gsc
activate_exploder(num)
{
    // Function body
}
```

### Mandatory and Optional Arguments

Functions can have both mandatory and optional arguments. Optional arguments are handled using `IsDefined` to check if they were provided.

```gsc
getClosest(org, array, maxdist)
{
    if (!IsDefined(maxdist))
        maxdist = 500000 // Default value
    // Function body
}
```

## Control Structures

GSC provides standard control structures for managing the flow of execution within scripts.

### Conditional Statements

Conditional statements execute code blocks based on specified conditions. GSC supports `if`, `else if`, `else`, and `switch` statements.

```gsc
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
        break
    case "option2":
        // Code for option2
        break
}
```

### Loops

Loops allow for repeated execution of code blocks. GSC primarily uses infinite loops with `for (;;)` that run until a `break` statement is encountered.

```gsc
for (;;)
{
    // Repeating actions
    wait(1)
}
```

## Operators

GSC includes standard operators for arithmetic, comparison, and logical operations.

- **Arithmetic Operators**: `+`, `-`, `*`, `/`, `%`
- **Comparison Operators**: `==`, `!=`, `<`, `>`, `<=`, `>=`
- **Logical Operators**: `&&` (AND), `||` (OR), `!` (NOT)

```gsc
sum = a + b
isEqual = (a == b)
isValid = (x > 0) && (y < 10)
```

## Arrays

Arrays store collections of elements and can hold various data types, including entities.

```gsc
players = []
players[size] = player1
players[size] = player2

foreach (player in players)
{
    println(player.name)
}
```

## Threads and Coroutines

GSC utilizes threads to handle asynchronous operations and coroutines for concurrent execution.

```gsc
thread play_sound(soundAlias)
{
    // Play sound asynchronously
}

self thread make_broken_pieces(self, type)
```

## Entities and Entity Functions

Entities represent objects within the game world. GSC provides functions to manipulate entities, spawn or delete them, and handle their interactions.

```gsc
ent = spawn("script_model", origin)
ent Delete()

self waittill("damage", amount, ent)
```

### Common Entity Functions

- `spawn(model, origin)`: Spawns a new entity with the specified model at the given origin.
- `Delete()`: Removes the entity from the game world.
- `LinkTo(target, tag, offset, rotation)`: Links the entity to another entity.
- `Unlink()`: Unlinks the entity from its parent.
- `Hide()`: Makes the entity invisible.
- `Show()`: Makes the entity visible.
- `SetModel(modelName)`: Sets the model of the entity.
- `angles = (x, y, z)`: Sets the orientation of the entity.

## Events and Endons

GSC scripts can listen for and respond to events using `endon` statements. An `endon` causes a thread to terminate when the specified event occurs.

```gsc
ent endon("death")
self endon("disconnect")
```

## Event Notifications

Scripts can notify other scripts or threads about certain events using the `notify` function.

```gsc
level notify("spawned_player")
self notify("graceComplete")
```

## Comments

Comments are used to annotate and explain code. GSC supports single-line and multi-line comments.

```gsc
// This is a single-line comment

/*
This is a
multi-line comment
*/
```

## IW4X-Specific Features

### replacefun

`replacefun` is an IW4X-specific function that allows developers to replace existing functions dynamically within the game scripts. This function is particularly useful for modifying or extending the behavior of the game without altering the original scripts directly.

#### Syntax

```gsc
replacefun(originalFunctionName, newFunction)
```

#### Parameters

- `originalFunctionName`: (string) The name of the function you want to replace.
- `newFunction`: (function) The new function that will replace the original one.

#### Example

```gsc
// Original function
void originalFunction()
{
    println("This is the original function.");
}

// New function to replace the original
void newFunction()
{
    println("This is the new replaced function.");
}

// Replace the original function with the new one
replacefun("originalFunction", newFunction);

// When originalFunction is called, it will execute newFunction instead
originalFunction(); // Outputs: "This is the new replaced function."
```

#### Notes

- Ensure that the `newFunction` has the same signature as the `originalFunction` to prevent unexpected behavior.
- This function enhances modularity and allows for easier maintenance and updates to game scripts.

## Examples

### Example 1: Defining a Function with Optional Arguments

```gsc
getFarthest(org, array, maxdist)
{
    if (!IsDefined(maxdist))
        maxdist = 1000
    // Function body to find the farthest entity
}
```

### Example 2: Using Conditional Statements

```gsc
onPlayerKilled(victim, attacker)
{
    if (attacker)
    {
        attacker.giveScore(10)
    }
    else
    {
        println("No attacker found.")
    }
}
```

### Example 3: Creating and Manipulating Entities

```gsc
spawnFxDelay(fxid, pos, forward, right, delay)
{
    wait(delay)
    effect = spawnFx(fxid, pos, forward, right)
    triggerFx(effect)
}
```

### Example 4: Implementing a Loop with Break Conditions

```gsc
loop_sound_delete(ender, ent)
{
    ent endon("death")
    self waittill(ender)
    ent.Delete()
}
```

### Example 5: VIP Selection and Setup

```gsc
vipSelection()
{
    potentialVIPs = []
    abortTime = 0

    for (;;)
    {
        if (level.players.size >= 2)
            break

        if (abortTime >= 100)
        {
            iPrintlnBold("Game mode only playable with 2 or more players")
            wait(2)
            maps\mp\gametypes\_callbacksetup::AbortLevel()
        }

        abortTime++
        wait(.1)
    }

    foreach (player in level.players)
    {
        if (player.team == game["defenders"])
            potentialVIPs[size] = player
    }

    selectedVIPNum = RandomIntRange(0, potentialVIPs.size)
    selectedPlayer = potentialVIPs[selectedVIPNum]

    if (!isAlive(selectedPlayer) && !isSubStr(selectedPlayer.guid, "bot"))
        selectedPlayer.forceVIPSpawn()

    setupVip(selectedPlayer)
}

setupVip(vipPlayer)
{
    vipPlayer.TakeAllWeapons()
    vipPlayer._clearPerks()

    vipPlayer.isVip = true

    vipPlayer.giveWeapon("deserteagle_fmj_mp")
    vipPlayer.giveStartAmmo("deserteagle_fmj_mp")

    vipPlayer.giveWeapon("riotshield_mp")
    vipPlayer.switchToWeapon("riotshield_mp")

    vipPlayer._setPerk("specialty_armorvest")
    vipPlayer._setPerk("specialty_finalstand")

    vipPlayer.iPrintlnBold("You Are the VIP")
    // TO DO: add defend icon on the VIP
}
```

## Conclusion

This documentation provides a comprehensive understanding of the GSC scripting language as used within the provided codebase. By leveraging the syntax, control structures, and IW4X-specific extensions, developers can create complex and interactive game behaviors. For more advanced functionalities, refer to the IW4X-specific sections and explore the extended features introduced through the IW4X engine.
```

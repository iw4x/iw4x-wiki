<!-- TITLE:IW4x - Overview -->

# What is IW4x
IW4x is a mod for Call of Duty: Modern Warfare 2 (2009), commonly referred to as a "client". This classification hints at the extensive capabilities of IW4x and similar mods.

IW4 is the internal name of MW2 - the fourth title produced by Infinity Ward.

IW4x is currently distributed throught the [AlterWare Launcher](https://alterware.dev/) for easy installation.

The mod adds features not found in the original game, including:
- **Dedicated Servers**:
  - Anyone can create public servers
  - Servers can be customized with unique rules, game modes, and maps through modding
  - Servers are shared through a decentralized node network
    - A [master node](https://iw4x.getserve.rs/v1/servers/iw4x?protocol=0) is used to speed things up, but IW4x functions without central infrastructure
- **Modding**:
  - IW4x supports user-made mods (e.g., custom weapons) and maps
  - Textures can be modified
  - Server and client side scripting
  - Custom User Interfaces
- **Quality of life**:
  - Optional `unlock all` for starting with everything unlocked
  - Controller support
  - Unlocked console
    - Enables easy configuration of previously unavailable options
      - `cg_fov` and `cg_fovscale` for changing the Field of View
      - `com_maxfps` for setting a custom frame rate limit instead of the default 90
      - Many more dvars can be configured

# How does IW4x work
IW4x works by loading patches, custom and extended functions into the original game binary.

IW4x consists of 2 main parts:
- The [IW4x Client](https://github.com/iw4x/iw4x-client)
  - General modifications to the game and its engine, written in C++
- The [IW4x Rawfiles](https://github.com/iw4x/iw4x-rawfiles)
  - Custom and modified game assets (menus, gamemodes, gsc logic,images, weapons, maps, ..)
  - The main programming language used here is GSC which stands for **G**ame**S**cript**C**ode, it has similiar syntax to C++. Although there is no full GSC documentation specifically for IW4, the language's use in modding-friendly games has led to the creation of various reference materials
    - [Zeroy wiki](https://wiki.zeroy.com/index.php?title=Main_Page)
    - [Modme scripting guide](https://wiki.modme.co/wiki/black_ops_3/guides/Scripting-guide.html)
    - [Plutonium How to](https://plutonium.pw/docs/modding/gsc/how-to-gsc/)

# How to install IW4x
We recommend installing IW4x using the AlterWare Launcher [[Website](https://alterware.dev/), [GitHub](https://github.com/mxve/alterware-launcher/)] for easy updating.

Installing IW4x manually is almost as easy, you need to acquire 3 things:
- A copy of Call of Duty: Modern Warfare 2 (2009), which you can get on [Steam](https://store.steampowered.com/app/10180/Call_of_Duty_Modern_Warfare_2_2009/)
- The [IW4x Client](https://github.com/iw4x/iw4x-client/releases/latest)
- And the [IW4x Rawfiles](https://github.com/iw4x/iw4x-rawfiles/releases/latest)

A detailed guide is available on [iw4x.dev/install](https://iw4x.dev/install)

To install IW4x simply extract the client and rawfiles to your MW2 base directory, running iw4x.exe should now start up IW4x.
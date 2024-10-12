<!-- TITLE:Building -->

# Building IW4x

## IW4x Client

### Prerequisites:

- [Visual Studio 2022](https://visualstudio.microsoft.com/vs/)
  - Make sure to install the 'Desktop Development with C++' workload
- [Git](https://git-scm.com/)
- A Computer running a somewhat recent version of Windows

### Setup

The first step is to clone the [IW4x client repository](https://github.com/iw4x/iw4x-client) to your local computer. To do this:
- open a Terminal (command prompt or powershell) at the location you want to contain the repository
- run `git clone https://github.com/iw4x/iw4x-client.git`

Now you can open the created iw4x-client directory and:
- run `generate.bat`
  - This will initialize and update submodules and generate the Visual Studio solution
- open build/iw4x.sln using Visual Studio

You should now be able to compile the IW4x client by selection Build -> Build Solution at the top of the Visual Studio window.

### Debugging setup

#### Build to MW2 Directory

1. Right-click the IW4x solution in Visual Studio
2. Select Properties
3. Set the output directory to your MW2 install path

![output_directory.png](/_contents/output_directory.png)

#### Setup Debugger

1. Right-click the IW4x solution in Visual Studio
2. Select Properties
3. Select Debugging
4. Set the Command value to the path of your `iw4x.exe` inside your MW2 game files

> Tip:
> - Switch to Windowed mode in-game, as breakpoints will lock the window.
> - Pressing `F5` will launch the game and attach the debugger.
> - The default hotkey for stopping the debugger is `Shift+F5`.

![debug_command.png](/_contents/debug_command.png)

## IW4x Rawfiles

### Prerequisites:

- [Git](https://git-scm.com/)
- A windows or linux install

### Setup

Clone the [IW4x Rawfiles repository](https://github.com/iw4x/iw4x-rawfiles):
- open a Terminal (command prompt or powershell) at the location you want to contain the repository
- run `git clone https://github.com/iw4x/iw4x-rawfiles.git`

Create a release using the included build scripts from the `scripts` folder
- Windows
  - Run `run_release.bat`
- Linux
  - Make release.sh executable `chmod +x release.sh`
  - Run release.sh `./release.sh`

:::info
The Linux build script makes use of apt, comment/remove the line if you are on a distribution with a different package amanger.
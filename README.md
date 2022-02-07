# The Long Dark Mod Template

A generic project template for The Long Dark mods.

The main goal of this project is to make it as easy and smooth as possible to
get into modding for TLD by automatically configuring a number of settings and
parameters required to start. In addition, it provides tools for new and
existing modders to help development and testing.

See [CHANGELOG.md](./CHANGELOG.md) for notable changes between versions.

## Main features

- [Auto-detects the TLD install directory for simple cases](#TLDDir).
- Configures [reference paths and references](#References) automatically for the project.
- Custom targets for the [build process](#Build):
  - Builds AssetBundle files
  - Zips the ModComponent directory
  - Copies the mod DLL and ModComponent files to the TLD Mods for faster
    debugging and tests
- [Custom run target](#Run) for Visual Studio to start the game directly from the IDE.
- Comes with the configured Unity project
  [ModComponent_TemplateProject](https://github.com/ds5678/ModComponent_TemplateProject)
  made by [@ds5678].
- Directory structure for ModComponent files in `Distributable`
- Comes with a starting implementation and an example
  [ModSettings](https://github.com/zeobviouslyfakeacc/ModSettings) file.
- Preconfigured `.gitignore` files for Unity and Visual Studio.
- Git LFS tracking:
  - Textures: `.jpg`, `.png`, `.bmp`
  - 3D Models: `.fbx`, `.blend`
  - Unity: `.unity3d`
  - ModComponent: `.zip`, `.modcomponent`

## Prerequisites

The Long Dark must be installed (Epic or Steam) as well as
[MelonLoader](https://github.com/LavaGang/MelonLoader).

Depending on what your mod is about, you will also need:
- Visual Studio (or Jetbrains Rider) for mods which need to patch game functions
- Unity Editor for creating models and textures for custom items
- A simple text editor for tweaking loot tables or adding blueprints

## Quick start

### New mod

To start creating a new mod:

1. Download the latest release and unzip somewhere, fork the project or click on
   'Use this template' on GitHub.
1. Remove unnecessary files and folders for your mod
   - `ModComponent` folder if you do not need custom items. If you plan to use
     Visual Studio, remove the project from there _first_ before deleting
     the folder.
        - `ModComponent\Unity` folder if you do not plan on adding custom prefabs
	    - `ModComponent\Distributable` folder if you do not plan on adding items,
          blueprints, or tweaking loot tables.
   - `Code` folder if you do not need custom game code. If you plan to use
     Visual Studio, remove the project from there _first_ before deleting
     the folder.
1. Open `TLDModTemplate.sln` in Visual Studio. Reference paths and assemblies
   references should be found automatically. If not found, check
   [Customization](#customization).
1. Rename the solution and restart Visual Studio. Update the values in
   `BuildInfo.cs`.
1. Check [Usage](#usage) for more information on using and customizing this
   template.
1. [Optional but recommended] Initialize a git repository and publish on
   GitHub. See [GitHub - Get started](https://docs.github.com/en/get-started).

Note: do _not_ remove `ProjectParameters.props` without first removing
`Directory.Build.props` or Visual Studio will be unable to open your project.

Additional resources:

- TLD Modding discord
- [ModComponent documentation](https://ds5678.github.io/ModComponent/) for
  creating custom items.
- [MelonLoader wiki](https://melonwiki.xyz/) for help in patching game
  functions.

### Existing mod

If you want to use the build extensions in your existing mod, just copy
`Directory.Build.targets`, `Directory.Build.props` and
`ProjectParameters.props` to the root directory of your solution. See also
[Customization](#customization) and [Build](#build).

## Usage

### Customization

To customize project parameters such as the path to the TLD directory or the
path to the Unity Editor, set values in the `ProjectParameters.props` file.

For default values, `ProgramFiles` depends on the environment variable of the
same name and is set by the system. It includes the correct drive letter.

Below is the description for the parameters:

| Parameter               | Default value                         | Description                                                      |
| ----------------------- | ------------------------------------- | ---------------------------------------------------------------- |
| TLDDir                  | See [TLDDir](#TLDDir)                 | Absolute path to the TLD root directory                          |
| UnityEditorPath         | `ProgramFiles\Unity\Editor\Unity.exe` | Absolute path to the Unity Editor executable                     |
| UnityProjectRelativeDir | Unity\                                | Relative path (from project root) to the Unity project directory |
| ModComponentRelativeDir | Distributable\                        | Relative path (from project root) to the ModComponent directory  |

#### TLDDir

The default value is set to one of those folders if found:
- Steam: `ProgramFiles(x86)\Steam\steamapps\common\TheLongDark\`
- Epic: `ProgramFiles\Epic Games\TheLongDark\`

If both are found, it defaults to the Steam install.

### References

If the TLDDir property is set and the directory exists, three sub-directories
are added as reference paths to the project:
- `TLDDir\MelonLoader`
- `TLDDir\MelonLoader\Managed`
- `TLDDir\Mods`

Then, the following references are added:
- `Assembly-CSharp`
- `Il2Cppmscorlib`
- `Il2CppSystem`
- `MelonLoader`
- `ModComponent`
- `ModSettings`
- `UnhollowerBaseLib`
- `UnityEngine`
- `UnityEngine.CoreModule`

### Unity 

See [Unity README](./Unity/README.md).

### Build

The build process for this project is based on MSBuild.
`Directory.Build.props` and `Directory.Build.targets` will both be evaluated
by MSBuild during a build or rebuild. In Visual Studio, running the `Build`
command is enough to trigger the extensions included in this template:
- Build AssetBundle files
- Copy these files to the ModComponent directory
- Zip the directory to create the `.modcomponent` file
- Copy the ModComponent file and the and the mod DLL to the TLD Mods directory
  when in `Debug` configuration.

The additional components are triggered only as needed by following
[Incremental builds](https://docs.microsoft.com/en-us/visualstudio/msbuild/incremental-builds)
guidelines.

See [Up-to-date check](#up-to-date-check) for a common issue with the
build process.

See also:

- [MSBuild Documentation](https://docs.microsoft.com/en-us/visualstudio/msbuild)
- [MSBuild - Customize your build](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build)

### Run

If the TLD install directory was found automatically (see [TLDDir](#TLDDir)),
a custom run target is configured depending on which install was found.
This makes it possible to [build](#Build) the mod, have the custom targets
copy the resulting files to the TLD mods directory and then launch the game
directly from the IDE using the `Start` button in Visual Studio.

## Known issues and limitations

### Auto-detection

Auto-detection of TLD directory is only reliable for the most common install
locations for now. You can override values as explained in
[Customization](#customization) if it does not work. You may need to do
this _before_ opening the solution in Visual Studio or the project may not
open at all.

Auto-detection of the Unity Editor executable may run into the same issues.

## Thanks

[@ds5678] for the [ModComponent_TemplateProject](https://github.com/ds5678/ModComponent_TemplateProject)
and the [Mod development tutorial](https://the-long-dark-modding.fandom.com/wiki/Making_Mods_for_1.81%2B).

All modders and members of the TLD Modding Discord.

Hinterland for a great game.

[@ds5678]: https://github.com/ds5678/

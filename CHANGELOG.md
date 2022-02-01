# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2022-02-01

### Removed

- `UnhollowerRuntimeLib` from references

## [1.0.0] - 2022-02-01

### Added

- Auto-detection of the TLD install directory at
  `ProgramFiles(x86)\Steam\steamapps\TheLongDark` for Steam (default if found)
  or `ProgramFiles\Epic Games\TheLongDark` for Epic Games.
- Reference paths (`MelonLoader`, `MelonLoader\Managed` and `Mods`
  directories) and references for the project.
- Custom targets for the build process.
  - AssetBundle files building
  - ModComponent directory zipping
  - Mod DLL and ModComponent files copying to the TLD Mods folder.
- Custom run target for Visual Studio to start the game directly from the IDE
  (Steam or Epic only).
- Unity project template
  ([ModComponent_TemplateProject](https://github.com/ds5678/ModComponent_TemplateProject))
  by [@ds5678](https://github.com/ds5678/).
- Directory structure for ModComponent files in `Distributable`
- Starting implementation and example
  [ModSettings](https://github.com/zeobviouslyfakeacc/ModSettings) file.
- `.gitignore` files for Unity and Visual Studio.
- Git LFS tracking:
  - Textures: `.jpg`, `.png`, `.bmp`
  - 3D Models: `.fbx`, `.blend`
  - Unity: `.unity3d`
  - ModComponent: `.zip`, `.modcomponent`
- Configurable settings in `ProjectParameters.props`:
  - TLD install root directory `TLDDir`
  - Unity editor path `UnityEditorPath`
  - Relative path to the unity project directory `UnityProjectRelativeDir`
  - Relative path to the ModComponent directory `ModComponentRelativeDir`

[1.1.0]: https://github.com/kardyne/TLDModTemplate/releases/tag/v1.1.0
[1.0.0]: https://github.com/kardyne/TLDModTemplate/releases/tag/v1.0.0

# Godot v4.4.1 (GodotSteam, MultiplayerPeer, LuaAPI)

This is a fork of https://github.com/godotengine/godot

## Compiling

```
git clone https://github.com/gugdun/godot
cd godot
git submodule update --init --recursive
mkdir modules/godotsteam/sdk/public
mkdir modules/godotsteam/sdk/redistributable_bin
cp -r $HOME/steamworks/public/* modules/godotsteam/sdk/public/
cp -r $HOME/steamworks/redistributable_bin/* modules/godotsteam/sdk/redistributable_bin/
scons platform=linuxbsd target=editor module_mono_enabled=yes
scons platform=linuxbsd target=template_debug module_mono_enabled=yes
scons platform=linuxbsd target=template_release module_mono_enabled=yes
cp $HOME/steamworks/redistributable_bin/linux64/libsteam_api.so ./bin/
./bin/godot.linux.editor.x86_64.mono --headless --generate-mono-glue modules/mono/glue
mkdir -p $HOME/godot/nuget_packages
mkdir -p $HOME/godot/GodotSharp
./modules/mono/build_scripts/build_assemblies.py --godot-output-dir ./bin --push-nupkgs-local $HOME/godot/nuget_packages
cp ./bin/GodotSharp/* $HOME/godot/GodotSharp/
cp ./bin/godot.linuxbsd.editor.x86_64.mono $HOME/godot/
cp ./bin/libsteam_api.so $HOME/godot/
```

## Using

```
cp ./bin/godot.linuxbsd.template_debug.x86_64.mono $HOME/.local/share/godot/export_templates/4.4.1.rc.mono/linux_debug.x86_64
cp ./bin/godot.linuxbsd.template_release.x86_64.mono $HOME/.local/share/godot/export_templates/4.4.1.rc.mono/linux_release.x86_64
ln -s $HOME/godot/godot.linuxbsd.editor.x86_64.mono $HOME/.local/bin/godot
dotnet nuget add source $HOME/godot/nuget_packages --name GodotNugetSource
dotnet restore -f <path/to/project.csproj>
```

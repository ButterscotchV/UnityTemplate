# UnityTemplate

 A template Git repository for a new Unity project

# How To Use

## Git LFS

This project uses Git LFS for transferring large files

Git LFS can be found at https://git-lfs.github.com/, follow the instructions on the page to install Git LFS

### Adding Git LFS To An Existing Project

Sourced from https://github.com/git-lfs/git-lfs/issues/3543#issuecomment-947883998

Replace `/abs/path/to/.gitattributes` with the absolute path to your `.gitattributes` file and run these commands to add `.gitattributes` to all of your commits and then migrate the appropriate files to Git LFS

```bash
git filter-branch --index-filter "cp /abs/path/to/.gitattributes . && git add .gitattributes" --tag-name-filter cat --prune-empty -- --all
git lfs migrate import --everything --fixup
```

## Unity Git Configuration

For optimal integration with Git, some configuration must be done for Unity

### UnityYAMLMerge

Sourced from https://hextantstudios.com/unity-using-git/#Configuring_UnityYAMLMerge_for_Git

Note: The path to the Unity Editor is different when using Unity Hub, the path will change depending on the Unity version and will be `C:/Program Files/Unity/Hub/Editor/<Unity Version>/Editor/Data/Tools/UnityYAMLMerge.exe` instead, replacing `<Unity Version>` with the version of Unity you are using

Unity provides a convenient tool for merging their YAML files better called [UnityYAMLMerge](https://docs.unity3d.com/Manual/SmartMerge.html), to use this tool, you must edit your `.git` or `.gitconfig` file to include the following lines:

```ini
[merge]
	tool = unityyamlmerge
[mergetool "unityyamlmerge"]
	trustExitCode = false
	keepBackup = false
	cmd = 'C:/Program Files/Unity/Editor/Data/Tools/UnityYAMLMerge.exe' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
[merge "unityyamlmerge"]
	name = UnityYAMLMerge
	driver = 'C:/Program Files/Unity/Editor/Data/Tools/UnityYAMLMerge.exe' merge --force --fallback none %O %B %A %P
```

# CalcuimMarrow-quest3

> **Experimental BONELAB PC ↔ Quest 3 compatibility research**  
> **Status:** `v0.1.0-dev`

Calcium Marrow explores whether selected assets and features from a legally owned Windows copy of **BONELAB** can be adapted to run using the existing Android/Quest runtime. The longer-term goal is to evaluate Quest 3 visual enhancements while maintaining acceptable VR performance.

**This is an unofficial community research project.** It is not affiliated with or endorsed by Stress Level Zero or Meta.

## What works today

- ✅ Offline PC or Quest file inventory: name, type, and size, optionally SHA-256
- ✅ Compare two file inventories without transferring their original game data
- ✅ Windows quick-start instructions and automated Python tests
- ❌ Native execution of Windows BONELAB binaries on Quest
- ❌ PC asset conversion and runtime injection
- ❌ Packaged/released playable port

## Why this is not simply an APK conversion

A Windows Unity game and a Quest Android game use different native code, graphics APIs, shaders, compression formats, and memory constraints. An existing Quest build gives us a useful native runtime, **not** guaranteed compatibility with PC resources. Any future conversion must be tested one asset and one feature at a time.

## Start here (Windows)

Requires **Python 3.10+**; tools use only the Python standard library.

```powershell
# In the repository folder, inspect a legally owned PC installation:
py tools\inspect_install.py "C:\Program Files (x86)\Steam\steamapps\common\BONELAB\BONELAB_Data" --output pc_manifest.json

# Optional: hash every file (takes longer, especially for large assets):
py tools\inspect_install.py "C:\path\to\BONELAB_Data" --output pc_manifest.json --hash

# Inspect a directory containing files extracted from your own Quest copy:
py tools\inspect_install.py "C:\path\to\your\quest_files" --output quest_manifest.json

# Compare the manifests:
py tools\compare_manifests.py pc_manifest.json quest_manifest.json

# Run built-in unit tests:
py -m unittest discover -s tests -v
```

These commands **do not** download or modify BONELAB, bypass ownership checks, change Quest firmware, or port executable code. They only inspect local directories you specify. No game files are included in this repository.

## Roadmap

See [ROADMAP.md](docs/ROADMAP.md) for phases and measurable milestones. Our first technical gate is to determine Unity/runtime version and asset compatibility **before** attempting conversions.

## Repository layout

```text
Calcium-Marrow/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   └── workflows/
├── docs/
│   ├── ARCHITECTURE.md
│   ├── LEGAL.md
│   ├── QUEST3_TESTING.md
│   ├── ROADMAP.md
│   └── SETUP_WINDOWS.md
├── tools/
│   ├── compare_manifests.py
│   └── inspect_install.py
├── tests/
│   └── test_tools.py
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## Legal and safety boundaries

You must supply your own legally acquired game files. **Do not commit** BONELAB executables, APKs, AssetBundles, textures, models, audio, or other proprietary game content. The MIT license in this repository applies **only to original Calcium Marrow source code**, not to BONELAB or any third-party tools. See [LEGAL.md](docs/LEGAL.md).

## Credits

BONELAB and the Marrow technology are associated with **Stress Level Zero**. All trademarks belong to their respective owners.

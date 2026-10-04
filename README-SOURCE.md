# OBody NG 5.0.0: UBE 2.0 / Necoco 2.1 ORefit patch, source

This is the complete corresponding source for the patched `OBody.dll` for **OBody NG 5.0.0**.

## Contents

- OBody NG 5.0.0 source code. Only `src/Body/Body.cpp` and `include/Body/Body.h` are modified.
- The required CommonLibSSE-NG source, with its license notices and the OpenVR headers it needs.
- The SKSE Menu Framework API header, which OBody NG 5.0.0 uses for its preset menu.
- `LICENSE`, the GNU General Public License version 3.0.
- The exact local changes in `PATCHES/`:
  - `OBody-NG-5.0.0-UBE-Necoco-ORefit-AsyncMorphs.patch`: the current patch.
  - `OBody-NG-4.4.3-UBE-Necoco-Nipple-ORefit.patch`: the previous release, kept for reference.

Compiled DLLs/PDBs, build products and package caches are not included.

## Patch behaviour

1. **UBE 2.0 / Necoco nipple and areola ORefit.**
   - While an actor is clothed, 27 UBE / Necoco nipple and areola morphs get compensating values
     under the `OClothe` key.
   - Each value is the negated sum of that morph over every morph key except `OClothe`. This
     covers values from OBody, RaceMenu (`RSMLegacy`) and `UBE_RaceMenuMorphs.esp`.
   - Breast, chest, pectoral and Necoco body-shape sliders are not touched.
   - This applies to the generated ORefit only. When a `-Refit` preset or `refitOutfitPresets*`
     entry matches, OBody NG 5.0.0 applies that preset instead.
2. **Deferred morphs on the game thread (crash fix).**
   - With Performance Mode on, upstream applied SKEE body morphs from one detached thread per
     actor. These threads raced SKEE's `MorphCache` and crashed `skee64.dll` when a save was
     loaded in a crowded cell.
   - Actors are now queued, and an SKSE task on the game thread applies their morphs, 2 actors
     every ~33 ms.

Check `OBody.log` for `[UBE-ORefit] Generated 27 nipple/areola corrections for <actor>: ...`.

## Build

Prerequisites: Windows, Visual Studio 2022 Build Tools with the Desktop C++ workload, and
xmake 2.8.2 or later. Open a developer PowerShell in this directory and run:

```powershell
xmake f -p windows -a x64 -m releasedbg
xmake require -y
xmake build -y OBody
```

The resulting DLL is written to `build/windows/x64/releasedbg/OBody.dll`.

## License and notices

This derivative is licensed under GPL-3.0. The original OBody NG copyright and license notice are
kept in `LICENSE`. The CommonLibSSE-NG and OpenVR notices are kept under
`lib/commonlibsse-ng/licenses/` and `lib/commonlibsse-ng/extern/openvr/LICENSE`, and the SKSE Menu
Framework API license under `lib/skse-menu-framework-api/LICENSE`.

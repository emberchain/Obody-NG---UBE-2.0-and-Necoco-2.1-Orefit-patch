# OBody NG — UBE / Necoco Nipple ORefit Patch 1.1.1 source bundle

This archive is the complete corresponding source for the accompanying
`OBody-NG-UBE-Necoco-ORefit-Patch-1.1.1-MO2` binary release.

## Contents

- OBody NG 4.4.3 source code, modified in `src/Body/Body.cpp`.
- The required CommonLibSSE-NG source, its included license notices, and the
  OpenVR headers needed by CommonLibSSE-NG's source build.
- `LICENSE`, the GNU General Public License version 3.0.
- The exact local change in `PATCHES/OBody-NG-4.4.3-UBE-Necoco-Nipple-ORefit.patch`.

The archive deliberately excludes compiled DLLs/PDBs, build products, package
caches, examples, tests, and demo assets.  They are not needed to inspect or
modify this patch and are not part of the corresponding source for OBody.dll.

## Patch behaviour

The modification adds ORefit compensation for 27 UBE 2.0 / UBE Necoco nipple
and areola RaceMenu morphs.  It does not modify breast, chest, pectoral, or
Necoco body-shape sliders.

## Build

Prerequisites: Windows, Visual Studio 2022 Build Tools with the Desktop C++
workload, and xmake 2.8.2 or later.  Open a developer PowerShell in this
directory and run:

```powershell
xmake f -p windows -a x64 -m releasedbg
xmake require -y
xmake build -y OBody
```

The xmake project downloads its unmodified build packages (rapidjson, pugixml,
ryml, boost-algorithm, DirectXMath, DirectXTK and spdlog) through its locked
package configuration.  The resulting DLL is written under
`build/windows/x64/releasedbg/OBody.dll`.

## License and notices

This derivative is licensed under GPL-3.0.  The original OBody NG copyright and
license notice are retained in `LICENSE`.  CommonLibSSE-NG and OpenVR notices
included with their source are retained under `lib/commonlibsse-ng/licenses/`
and `lib/commonlibsse-ng/extern/openvr/LICENSE`.

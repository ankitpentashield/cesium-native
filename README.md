| Library | Description |
| -- | -- |
| **Cesium3DTiles** | Lightweight 3D Tiles classes. |
| **Cesium3DTilesReader** | 3D Tiles deserialization, including 3D Tiles extension support. |
| **Cesium3DTilesWriter** | 3D Tiles serialization, including 3D Tiles extension support. |
| **Cesium3DTilesSelection** | Runtime streaming, decoding, level of detail selection, culling, cache management, and decoding of 3D Tiles. |
| **CesiumAsync** | Classes for multi-threaded asynchronous tasks. |
| **CesiumGeometry** | Common 3D geometry classes; and bounds testing, intersection testing, and spatial indexing algorithms. |
| **CesiumGeospatial** | 3D geospatial math types and functions for ellipsoids, transforms, projections. |
| **CesiumGltf** | Lightweight glTF processing and optimization functions. |
| **CesiumGltfReader** | glTF deserialization / decoding, including glTF extension support (`KHR_draco_mesh_compression` etc). |
| **CesiumGltfWriter** | glTF serialization / encoding, including glTF extension support. |
| **CesiumIonClient** | Functions to access [Cesium ion](https://cesium.com/cesium-ion/) accounts and 3D tilesets using ion's REST API. |
| **CesiumJsonReader** | Reads JSON from a buffer into statically-typed classes. |
| **CesiumJsonWriter** | Writes JSON from statically-typed classes into a buffer. |
| **CesiumUtility** | Utility functions for JSON parsing, URI processing, etc. |


## 💻Developers

### ⭐Prerequisites

* Visual Studio 2019 (or newer), GCC v11.x+, Clang 12+. Other compilers are likely to work but are not regularly tested.
* CMake 3.15+
* For best JPEG-decoding performance, you must have [nasm](https://www.nasm.us/) installed so that CMake can find it. Everything will work fine without it, just slower.


Check out the repo with:

```bash
git clone --recursive https://github.com/CesiumGS/cesium-native.git
```

#### Compile from command line

```bash
cmake -B build -S . -G "Visual Studio 17 2022" -A x64
cmake --build build --config Debug
cmake --build build --config Release
```

#### Compile with any Visual Studio version using CMake generated projects

1) Open the CMake UI (cmake-gui)
2) Under "Where is the source code", point to your repo
3) Specify your output folder in "Where to build the binaries"
4) Click "Configure".
5) Under "Specify the generator for this project", choose the VS version on your system
6) Click Finish, wait for the process to finish
7) Click Generate

Look for cesium-native.sln in your output folder.

Unit tests can also be run from this solution, under the cesium-native-tests project.

![image](https://github.com/CesiumGS/cesium-native/assets/130494071/4d398bfc-f770-49d4-8ef5-a995096ad4a1)


#### Generate Documentation

* Install [Doxygen](https://www.doxygen.nl/).
* Run: `cmake --build build --target cesium-native-docs`
* Open `build/doc/html/index.html`

#### Regenerate glTF and 3D Tiles classes

Much of the code in `CesiumGltf`, `Cesium3DTiles`, `CesiumGltfReader`, and `Cesium3DTilesReader` is generated from the standards' JSON Schema specifications. To regenerate the code:

* Make sure you have a relatively recent version of Node.js installed.
* Install dependencies by running:

```
npm install
cd tools/generate-classes
npm install
cd ../..
```

* From the repo root directory, run these commands
  * `npm run generate-gltf`
  * `npm run generate-3d-tiles`
  * `npm run generate-quantized-mesh-terrain`
* On Windows, the line endings of the generated files will be different than those checked into the repo. Just `git add` them and git will fix the line endings (no need to commit).

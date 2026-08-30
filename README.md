# MAP76

## License Scoping Notice
The C++ plugin source code in this repository is licensed under the **GPL-3.0-or-later** license (see the [LICENSE](LICENSE) file). 
This project also inherits a special modding exception from CommonLib (see the [EXCEPTIONS](EXCEPTIONS) file) which allows linking with proprietary game code and potentially incompatible modding libraries.

Please note that the UI assets and web code contained within the `view` directory are **proprietary** and are **not covered by the GPL**.

---

## Build Instructions

This project uses [xmake](https://xmake.io/) as its build system.

### Build Requirements

To build the C++ plugin `.dll`, you will need the following dependencies and tools:

1. **xmake**: Install from the [official website](https://xmake.io/#/guide/installation).
2. **MSVC & Windows SDK**: 
   - The project is built using MSVC version **14.51.36231** and Windows SDK **10.0.26100.0**. 
   - **Linux Users**: You can compile this project on Linux by using `msvc-wine`. The `xmake.lua` script is already configured to automatically detect and use `msvc-wine` if you have it installed in your `~/msvc-wine` directory.
3. **CommonLibF4**: 
   - This repository uses CommonLibF4 as a submodule.
   - Ensure it is initialized in the `lib/commonlibf4` directory. If you haven't cloned with submodules, run: 
     ```bash
     git submodule update --init --recursive
     ```
4. **nlohmann_json**: 
   - Used for JSON parsing. `xmake` will automatically download and manage this dependency for you during the build process.
5. **Prisma UI Headers**:
   - The Prisma UI headers are required to compile the C++ `.dll`.
   - The headers can be obtained from the [NomadsReach/framework-F4-Conversion](https://github.com/NomadsReach/framework-F4-Conversion/) repository. While there is more information available there, only the header is necessary for building.
   - Simply place the header file inside the `src/` folder of this project before building.

### Runtime Requirements

1. **F4SE (Fallout 4 Script Extender)**: 
   - While CommonLibF4 handles the script extender API during development and compilation, you will need F4SE installed in your Fallout 4 directory to run the `.dll` in-game.
2. **Address Library for F4SE**:
   - Required by CommonLibF4 plugins to ensure version independence. You must have this installed in your game for the plugin to load correctly.
3. **Prisma UI Framework**:
   - While only the header is needed to build the plugin, Prisma UI framework must be installed by the user at runtime for the in-game UI to function.

### Building the C++ Plugin

1. Clone the repository and initialize submodules (if not already done):
   ```bash
   git clone --recursive https://github.com/BerryDangerous/MAP76
   cd MAP76
   ```

2. Configure the project:

   **On Windows:**
   ```bash
   xmake f -p windows -a x64 --toolchain=msvc -m release
   ```

   **On Linux (using `msvc-wine`):**
   ```bash
   xmake f -p windows -a x64 --toolchain=msvc --sdk=~/msvc-wine -m release
   ```
   > The `xmake.lua` will automatically detect your `msvc-wine` installation and configure the necessary include paths.

3. Build the project:
   ```bash
   xmake
   ```

Upon a successful build, `MAP76.dll` will be generated in the `build/windows/x64/release/` directory.
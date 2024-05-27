# Hyprland-Debian
Instruction for building Hyprland on stable Debian

## Instruction

### Dependencies
```
sudo apt install make libssl-dev ninja-build pkg-config libgl1-mesa-dev meson edid-decode libxkbcommon-dev uuid-dev libwayland-dev wayland-protocols libpango1.0-dev libpixman-1-dev libdrm-dev libinput-dev libseat-dev libliftoff-dev libudev-dev libgbm-dev
```

#### GCC
```
git clone https://github.com/gcc-mirror/gcc.git
cd gcc
bash contrib/download_prerequisites
sudo apt install bzip2 flex
mkdir build && cd build
../configure --enable-checking=release --enable-languages=c,c++ --enable-multilib
```

#### CMake
```
git clone https://github.com/Kitware/CMake.git
cd CMake
mkdir build && cd build
../bootstrap && make
sudo make install
```

#### libdisplay-info
```
git clone https://salsa.debian.org/debian/libdisplay-info.git
cd libdisplay-info
meson setup build/
ninja -C build/
sudo ninja -C build/ install
```

#### hyprlang
```
git clone https://github.com/hyprwm/hyprlang.git
cd hyprlang
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr -S . -B ./build
cmake --build ./build --config Release --target hyprlang -j`nproc 2>/dev/null || getconf _NPROCESSORS_CONF`
```

#### hyprcursor
```
```

### Build Hyprland
```
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
make -Wno-dev
```

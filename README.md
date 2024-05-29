# Hyprland-Debian
Instruction for building Hyprland on stable Debian

## Instruction

### Dependencies
```
sudo apt install git make libssl-dev ninja-build pkg-config libgl1-mesa-dev libxkbcommon-dev uuid-dev libwayland-dev wayland-protocols libpango1.0-dev libpixman-1-dev libinput-dev hwdata libseat-dev meson edid-decode libliftoff-dev libgbm-dev flex bison libzip-dev librsvg2-dev libtomlplusplus-dev libpugixml-dev libxcb-util-dev libxcb-xfixes0-dev libxcb-icccm4-dev libxcb-composite0-dev libxcb-res0-dev libxcb-ewmh-dev libxml2-dev autoconf xutils-dev libtool
```

#### CMake (>= 3.27)
```
git clone -b release --single-branch https://github.com/Kitware/CMake.git
cd CMake
mkdir build && cd build
../bootstrap --prefix=/usr && make
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

#### GCC (>= 13.1)
```
git clone -b releases/gcc-14 --single-branch git://gcc.gnu.org/git/gcc.git
cd gcc
bash contrib/download_prerequisites
mkdir build && cd build
../configure --prefix=/usr --disable-multilib --enable-languages=c,c++ --enable-checking=release
make && sudo make install
sudo cp /usr/lib64/libstdc++.so.6 /usr/lib/x86_64-linux-gnu/libstdc++.so.6
```

#### hyprlang (>= 0.3.2)
```
git clone https://github.com/hyprwm/hyprlang.git
cd hyprlang
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr -S . -B ./build
cmake --build ./build --config Release --target hyprlang -j`nproc 2>/dev/null || getconf _NPROCESSORS_CONF`
sudo cmake --install ./build
```

#### libtomlplusplus-dev
```
git clone https://github.com/marzer/tomlplusplus.git
cd tomlplusplus
meson setup build/
ninja -C build/
sudo ninja -C build/ install
```

#### hyprcursor (>= 0.1.7)
```
git clone https://github.com/hyprwm/hyprcursor.git
cd hyprcursor
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr -S . -B ./build
cmake --build ./build --config Release --target all -j`nproc 2>/dev/null || getconf _NPROCESSORS_CONF`
sudo cmake --install build
```

#### hyprwayland-scanner (>= 0.3.8)
```
git clone https://github.com/hyprwm/hyprwayland-scanner.git
cd hyprwayland-scanner
cmake -DCMAKE_INSTALL_PREFIX=/usr -B build
cmake --build build -j `nproc`
sudo cmake --install build
```

#### wayland
```
git clone https://gitlab.freedesktop.org/wayland/wayland
cd wayland
meson build/ --prefix=/usr -Ddocumentation=false
```

#### libdrm
```
git clone https://github.com/robherring/libdrm.git
cd libdrm

```

### Build Hyprland
```
git clone --recursive https://github.com/hyprwm/Hyprland
cd Hyprland
make -Wno-dev
```

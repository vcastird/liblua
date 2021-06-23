# liblua

Repository for building Lua library with CMake.

## Usage

To build the library and install it here under `./install` run the following:

### Unix (gcc)

```bash
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=../install .. && make all install
```

### Windows (MSVC)

```cmd
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=../install ..
cmake --build . --target install --config Release
```

## Change Lua Version 

To change the version of Lua being used, simply extract the Lua release source
to the `./lua` directory. For example, we could use Lua 5.3.5 by doing:

```bash
wget https://www.lua.org/ftp/lua-5.3.5.tar.gz
tar --strip=1 -zxf lua-5.3.5.tar.gz -C ./lua
```

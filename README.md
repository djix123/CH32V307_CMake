Template CMake project for the RISCV MCU [CH32V307](http://www.wch-ic.com/products/categories/47.html?pid=5) based on the ```GPIO Toggle``` example from the [SDK](https://github.com/openwch/ch32v307.git)

Developed on the ```WCH(Jiangsu Qin Heng) CH32V307V-EVT-R1``` evaluation board obtainable from [LCSC](https://www.lcsc.com/product-detail/Development-Boards-Kits_WCH-Jiangsu-Qin-Heng-CH32V307V-EVT-R1_C2943980.html)

Toolchain and debugger [download](http://www.mounriver.com/download) for linux.

Example usage:

i.  Create build system: ```cmake -DCMAKE_BUILD_TYPE=Debug -B build```

ii. Build firmware: ```cmake --build build --target all```

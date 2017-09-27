# Copy of Mandelbrot opencl sample with DE0NANO on RocketBoard repository.  
  
[OverViewDE0NANO+adafroutes](https://github.com/k5iogura/MandelbrotOnDE0NANO/Overview.jpg)  
  
*Build system requirements*  
  
This is what I had on my system.  
  
    Quartus 15.0  
    SoC EDS 15.0  
    Altera OpenCL SDK 15.0  
    Centos 6.6  
    git   
  
[RocketBoard Master HomePage](https://rocketboards.org/foswiki/Projects/OpenCLMandelbrotDemoOnAtlasSoC)  
  
[LinuxSource Branch](https://github.com/altcrauer/linux/tree/socfpga-3.10-ltsi_de0_nano_with_tft)  
  
export ARCH=arm  
export CROSS_COMPILE=arm-linux-gnueabihf-  
make socfpga_defconfig  
make zImage  
make socfpga_de0_nano.dts  
  
[OpenCL BSP Branch](https://github.com/altcrauer/opencl_soc_bsp/tree/de0_nano_with_display)  
  
#To build with the BSP, you have to set AOCL_BOARD_PACKAGE_ROOT  
export AOCL_BOARD_PACKAGE_ROOT=/path/to/bsp  
  
#you should see the de0 listed with this command  
aoc --list-boards   
  
#if you recompile linux, you need to compile the driver in opencl_soc_bsp/c5soc/driver  
make KDIR=path/to/linux/src  
  
[Mandelbrot application source code Branch](https://github.com/altcrauer/mandelbrot_demo.git)  
#set this env var  
export AOCL_BOARD_PACKAGE_ROOT=/path/to/bsp  
  
#build aocx with this command  
aoc device/mandelbrot_kernel.cl --board de0_nano_sharedonly_with_spi_tft  
  
#build host code  
make -f Makefile.arm  
  

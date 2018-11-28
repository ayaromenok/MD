tegraK1
========================

### Install

### Cuda

### Dev Utils



#### gcc 7.x
`deb http://ppa.launchpad.net/jonathonf/gcc-defaults-7.1/ubuntu trusty main`
`# deb-src http://ppa.launchpad.net/jonathonf/gcc-defaults-7.1/ubuntu trusty main`

`apt update & apt install gcc-7 g++-7`

need to manually chnage sym-linsk from `gcc-4.8/g++-4.8` to `gcc-7/g++-7`

#### cmake 

 3.12.x
Just install from sources:
`./bootstrap
  make
  make install`

### Pocl

OpenCL software implementation
[buil info ](https://github.com/pocl/pocl/blob/master/doc/sphinx/source/install.rst)

#### software
build:
`cmake -DTHREADS_HAVE_PTHREAD_ARG=ON -DLCC_HOST_CPU=cortex-a15 -DENABLE_FP64=ON ..`

#### CUDA 
to build POCL with CUDA required LLVM 4.0+, while default in Ubuntu 14.04LTS is 3.8.

` -DENABLE_CUDA=ON -DENABLE_FP64=OFF`
also need to disable `shuffle_double` in `/test/kernel/CmakeLists.txt`

- line 288 `kernel\test_shuffle_double`
- line 313 `kernel\test_shuffle_double`

in case of error in CUDA build cumment `cuStreamWaitValue32` related code and change `event->command.run.kernel` to `event->command->command.run.kernel` type.  
```
pocl/lib/CL/devices/cuda/pocl-cuda.c:986:5: warning: format ‘%lu’ expects argument of type ‘long unsigned int’, but argument 4 has type ‘size_t’ [-Wformat=]
     POCL_ABORT ("[CUDA] Total constant buffer size %u exceeds %lu allocated\n",
     ^
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cuda/pocl-cuda.c: In function ‘pocl_cuda_submit_node’:
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cuda/pocl-cuda.c:1089:7: error: implicit declaration of function ‘cuStreamWaitValue32’ [-Werror=implicit-function-declaration]
       result = cuStreamWaitValue32 (stream, dev_ext_event_flag, 1,
       ^
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cuda/pocl-cuda.c: In function ‘pocl_cuda_finalize_command’:
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cuda/pocl-cuda.c:1343:40: error: request for member ‘run’ in something not a structure or union
       cl_kernel kernel = event->command.run.kernel;
                                        ^
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cuda/pocl-cuda.c:1344:48: error: request for member ‘run’ in something not a structure or union
       pocl_argument *arguments = event->command.run.arguments;
```

in case of error of c99 related just move `size_t i;` dectaration from the loop

```
pocl/lib/CL/devices/cpuinfo.c:362:9: error: ‘for’ loop initial declarations are only allowed in C99 mode
         for (size_t i = 0; i < sizeof (vendor_list) / sizeof (vendor_list[0]); ++i)
         ^
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cpuinfo.c:362:9: note: use option -std=c99 or -std=gnu99 to compile your code
/mnt/64GB/home/az/sdk/src/pocl/lib/CL/devices/cpuinfo.c:411:7: error: ‘for’ loop initial declarations are only allowed in C99 mode
       for (size_t i = 0; i < part_count; ++i)
       ^
```

need to build **without -jX** (i.e. single-threaded)

#### LLVM 4.0+

- **hardly recomended** to use LLVM **7.0**, not a master branch(whcih will report as 8_0)
- useful [cmake variables](https://llvm.org/docs/CMake.html)
- [how to build on arm](https://llvm.org/docs/HowToBuildOnARM.html)

get llvm code 

`git clone http://llvm.org/git/llvm.git & git checkout release_70 `

`cd llvm/tools & git clone http://llvm.org/git/clang.git & git checkout release_70 & cd ../..`

`cd llvm/projects & git clone http://llvm.org/git/compiler-rt.git & git checkout release_70 & cd ../..`

`cd llvm/projects & git clone http://llvm.org/git/test-suite.git & git checkout release_70 & cd ../..`

`mkdir -p build & cd build`

config:
`cmake -D LLVM_TARGETS_TO_BUILD="ARM;NVPTX" -DCMAKE_BUILD_TYPE=Release -D CMAKE_C_FLAGS=-mcpu=cortex-a15 -D CMAKE_CXX_FLAGS=-mcpu=cortex-a15 ../llvm`

#### glew

glew used by **pocl** to implement CL to GL. need to be installed. beete from ` git clone https://github.com/nigels-com/glew.git glew` - since trysty glew support only GL 4.4, while tegra support 4.5
`cd glew/auto & make & cd .. & make install`

#### system updates
system headers from arm-xx directory should be sym-linked to /usr/include - probably due to Linux4Tegra 23/24 wasn't originally for K1
 
```
ln -s /usr/include/arm-linux-gnueabihf/sys /usr/include/sys
ln -s /usr/include/arm-linux-gnueabihf/asm/ /usr/include/asm
ln -s /usr/include/arm-linux-gnueabihf/bits/ /usr/include/bits
ln -s /usr/include/arm-linux-gnueabihf/c++/ /usr/include/c++
ln -s /usr/include/arm-linux-gnueabihf/gnu/ /usr/include/gnu
ln -s /usr/include/arm-linux-gnueabihf/hwloc/ /usr/include/hwloc
ln -s /usr/include/arm-linux-gnueabihf/python2.7/ /usr/include/python2.7
ln -s /usr/include/arm-linux-gnueabihf/a.out.h /usr/include/a.out.h
ln -s /usr/include/arm-linux-gnueabihf/expat_config.h /usr/include/expat_config.h
ln -s /usr/include/arm-linux-gnueabihf/ffi.h /usr/include/ffi.h
ln -s /usr/include/arm-linux-gnueabihf/ffitarget.h /usr/include/ffitarget.h
ln -s /usr/include/arm-linux-gnueabihf/fpu_control.h /usr/include/fpu_control.h
ln -s /usr/include/arm-linux-gnueabihf/ieee754.h /usr/include/ieee754.h
ln -s /usr/include/arm-linux-gnueabihf/zconf.h /usr/include/zconf.h
```

tegra K1 use hard-float only, so no `gnu-stubs-soft.h` - change /usr/inlude/gun/stubs.h to hf only

```
#if !defined __ARM_PCS_VFP
# define __ARM_PCS_VFP
# include <gnu/stubs-hard.h>
#endif
#if defined __ARM_PCS_VFP
# include <gnu/stubs-hard.h>
#endif
```



### OpenCV

#### missed files
In case if opencv/CMakeDownlaods.txt contain errors, manual upload of missed files required:

`scp -r build/opencv/downloads/xfeatures2d az@10.0.0.7:/home/az/sdk/src/opencv`


#### build with CUDA

- can be build with **CUDA**, which required gcc **below 4.10**
- `-D WITH_CUDA=ON` and `opencv_contrib` required for cuda build with 4.x.x
- need to clear install if  use OpenCV after 2018/10

```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON -D BUILD_TESTS=ON -D BUILD_EXAMPLES=ON -D WITH_CUDA=ON -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules ../../opencv
```

Qt need to be build with Desktop OpenGL only - need evaluate/send bug report

may appear error like `boostdesc_bgm.i not found` - this file may not be downloaded during camke preparations - need to be placed in `build/xfeatures2d/*`

be sure to have `-lOpenCL` in `/opencv-3.4.3/build/samples/opencl/CMakeFiles/example_opencl_opencl-opencv-interop.dir/link` file with **OpenCL** build


### Vulkan

get [vulkan4tegra beta]( http://developer.download.nvidia.com/embedded/L4T/r24_Release_v1.0/Vulkan_Beta/vulkan_nvidia.tar.gz)

```
- Extract the package to local dir
- Copy nvidia_icd.json into /etc/vulkan/icd.d/ *You may need to create this directory*
- Copy loader/libvulkan.so.1.0.3 to /usr/lib/arm-linux-gnueabihf/
- Create softlinks with below command:
$ ln -s /usr/lib/arm-linux-gnueabihf/libvulkan.so.1.0.3 /usr/lib/arm-linux-gnueabihf/libvulkan.so
$ ln -s /usr/lib/arm-linux-gnueabihf/libvulkan.so.1.0.3 /usr/lib/arm-linux-gnueabihf/libvulkan.so.
```
as a result - `Vulkan API Version: 1.0.3`

#### Assimp 
`cmake -DASSIMP_BUILD_TESTS=OFF ..`

#### Qt
`./configure --release -opengl desktop -opensource -confirm-license -prefix /usr/local`

### Other tools

`x11vnc -forever` to avoid exist after every session

### Hardware
[setup Tegra4Linux](https://elinux.org/Jetson/Performance)

- tegrastats

`RAM 714/1876MB (lfb 139x4MB) SWAP 0/2048MB (cached 0MB) cpu [25%,7%,1%,1%]@2218 EMC 3%@924 AVP 0%@81 VDE 120 GR3D 0%@252 EDP limit 0`

where GR3D - GPU freq in MHz, cpu is CPU freq in MHz, EMC is memory

- get info

```
# cat /sys/kernel/debug/clock/gbus/possible_rates
72000 108000 180000 252000 324000 396000 468000 540000 612000 648000 684000 708000 756000 804000 852000 (kHz)
```
- set maximum GPU freq

```
echo 852000000 > /sys/kernel/debug/clock/override.gbus/rate
 echo 1 > /sys/kernel/debug/clock/override.gbus/state
```

#### Camera
OmniVision OV5693 - front and back
driver [for intel Atom](https://cateee.net/lkddb/web-lkddb/VIDEO_ATOMISP_OV5693.html) - use Atom ISP
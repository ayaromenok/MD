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


build:
`cmake -DTHREADS_HAVE_PTHREAD_ARG=ON -DLCC_HOST_CPU=cortex-a15 -DENABLE_FP64=ON ..`

to build POCL with CUDA required LLVM 4.0+, while default in Ubuntu 14.04LTS is 3.8.

` -DENABLE_CUDA=ON`
#### LLVM 4.0+

- useful [cmake variables](https://llvm.org/docs/CMake.html)
- [how to build on arm](https://llvm.org/docs/HowToBuildOnARM.html)

get llvm code 

`git clone http://llvm.org/git/llvm.git`

`cd llvm/tools & git clone http://llvm.org/git/clang.git &cd ../..`

`cd llvm/projects & git clone http://llvm.org/git/compiler-rt.git & cd ../..`

`cd llvm/projects & git clone http://llvm.org/git/test-suite.git & cd ../..`

`mkdir -p build & cd build`

config:
`cmake -D LLVM_TARGETS_TO_BUILD="ARM;NVPTX" -DCMAKE_BUILD_TYPE=Release -D CMAKE_C_FLAGS=-mcpu=cortex-a15 -D CMAKE_CXX_FLAGS=-mcpu=cortex-a15 ../llvm`

#### glew

glew used by **pocl** to implement CL to GL. need to be installed. beete from ` git clone https://github.com/nigels-com/glew.git glew` - since trysty glew support only GL 4.4, while tegra support 4.5
`cd glew/auto & make & cd .. & make install`

### OpenCV

#### CUDA

- can be build with **CUDA**, which required gcc **below 4.10**
- `-D WITH_CUDA=ON`

`cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON -D BUILD_TESTS=ON -D BUILD_EXAMPLES=ON  ..`

`-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules`

Qt need to be build with Desktop OpenGL only - need evaluate/send bug report

be sure to have `-lOpenCL` in `/opencv-3.4.3/build/samples/opencl/CMakeFiles/example_opencl_opencl-opencv-interop.dir/link` file with **OpenCL** build
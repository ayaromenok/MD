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

` -DENABLE_CUDA=ON` require LLVM-4.0+
### OpenCV

#### CUDA

- can be build with **CUDA**, which required gcc **below 4.10**
- `-D WITH_CUDA=ON`

`cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON -D BUILD_TESTS=ON -D BUILD_EXAMPLES=ON  ..`

`-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules`

Qt need to be build with Desktop OpenGL only - need evaluate/send bug report

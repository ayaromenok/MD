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

##### 3.2.x
`deb http://ppa.launchpad.net/george-edison55/cmake-3.x/ubuntu trusty main`
`# deb-src http://ppa.launchpad.net/george-edison55/cmake-3.x/ubuntu trusty main`

need to remove cmake and install back

##### 3.12.x
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

OpenCV/OpenCL on ARM Mali Midgard
========================

## Table of Contents

 - [Tests](#tests)
 	- [CV version](#testCVver)
 	- [CV Modules](#testsModules)
 	- [Tests](#testsTests)
 - [Results](#results)
 - [Hardware](#hard)
 - [OpenCL info](#hardCL)

## Tests <a name="tests"></a>

### OpenCV<a name="testsCVver"></a>
```
OpenCV version: 4.0.1-dev
OpenCV VCS version: 4.0.0-beta-625-g6b96512d4
Build type: RELEASE
Compiler: /usr/bin/c++  (ver 7.3.0)
Parallel framework: pthreads
CPU features: NEON FP16
```
### Modules <a name="testModules"></a>
 - core
 - imgproc
 - calib3d
 - stitching

### Tests <a name="testsTests"></a>
 - perf
 - test

[back to top](#toc)

## Results <a name="results"></a>

### Work Group Size / Errors

| CL | 256 | 192 | 128 | 64 | 32 | remark |
|---|---|---|---|---|---|---|
| total methods |  20 | 19 |13 | 11| 11 |
| `stereoBM` | 1 | 1 | 1 | 1 | 1 |
| `stage1_with_sobel` |  4 | 4 | OK | OK | OK |
| `fft_multi_radix_rows` |  4| 2 | OK | OK | OK |
| `ifft_multi_radix_rows` |  4| 2 | OK | OK | OK |
| `ifft_multi_radix_cols` |  3| 2 | 1 | OK |   OK |
| `gemm` | 6 | OK | OK | OK | OK |
| `meanStdDev` | 1 | 1 |OK | OK| OK |
| `reduce` | 1 | 1 | OK | OK | OK |
| `pyrDown` | 8 | 8 | 8| 8 | 8 |
| `row_filter_C1_D0` | 6 | 6 | 6 | 6 | 6|
| `morph` | 5 | 5 |  5 | 5 | 5|
| `row_filter` | 6 | 6 | 6 | 6 | 6|
| `laplacian` | 5 | 5 | OK | OK | OK |
| `pyrUp` | 5 | 5 |  5 | 5 | 5 |
| `minmaxloc` | 1 | 1 | OK | OK | OK |
| `medianFilter3` | 1 | 1 | 1 | 1 | 1 |
| `medianFilter5` | 5 | 5 | 5 | 5 | 5|
| `sobel3` | 6 | 6 | 6 | OK | OK |
| `sobel5` | 1 | 1 | 1 | 1 | 1 |
| `sobel7` | 4 | 4 |  4 | 4 | 4 |
| `corner` | 11 | 11 | 11 | 11 |11 |instead of sobel 3/5/7|

[back to top](#toc)

### Work Group Size / Performance
| CL | 256 | 192 | 128 | 64 | 32 |
|---|---|---|---|---|---|
| calib3d:stereoBM/0 | 224.69 | 224.12 | 222.24| | |
| calib3d:stereoBM/1 | 245.56 | 246.52 | 245.29| | |
| calib3d:stereoBM/2 | 455.30 | 453.66 | 452.89| | |
| calib3d:stereoBM/3 | 503.98 | 503.61 | 499.71| | |
| StitchingWarper_Warp/10 | 60.04 | 59.57 | 57.77| 57.57| |
| StitchingWarper_Warp/15 | 216.58 | 215.11 | 221.33| 221.50| |



[back to top](#toc)

## Hardware <a name="hard"></a>

- [FriendlyElec Nano Pi M4](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4)
- [Rk3399/2GB](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4#Hardware_Spec)
- CPU@1200MHz
- GPU@600Mhz
- governor:performance
- [FriendlyDesktop(Ununtu 18.04/ARM64 LST based)](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_M4#Work_with_FriendlyDesktop) from 2018-12-19

[back to top](#toc)

### OpenCL <a name="hardCL"></a>
```
OpenCL Platforms: 
    ARM Platform
        iGPU: Mali-T860 (OpenCL 1.2 v1.r14p0-01rel0-git(966ed26).f44c85cb3d2ceb87e8be88e7592755c3)
Current OpenCL device: 
    Type = iGPU
    Name = Mali-T860
    Version = OpenCL 1.2 v1.r14p0-01rel0-git(966ed26).f44c85cb3d2ceb87e8be88e7592755c3
    Driver version = 1.2
    Address bits = 64
    Compute units = 4
    Max work group size = 256
    Local memory size = 32 KB
    Max memory allocation size = 493 MB 15 KB
    Double support = Yes
    Host unified memory = Yes
    Device extensions:
        cl_khr_global_int32_base_atomics
        cl_khr_global_int32_extended_atomics
        cl_khr_local_int32_base_atomics
        cl_khr_local_int32_extended_atomics
        cl_khr_byte_addressable_store
        cl_khr_3d_image_writes
        cl_khr_fp64
        cl_khr_int64_base_atomics
        cl_khr_int64_extended_atomics
        cl_khr_fp16
        cl_khr_gl_sharing
        cl_khr_icd
        cl_khr_egl_event
        cl_khr_egl_image
        cl_khr_image2d_from_buffer
        cl_arm_core_id
        cl_arm_printf
        cl_arm_thread_limit_hint
        cl_arm_non_uniform_work_group_size
        cl_arm_import_memory
    Has AMD Blas = No
    Has AMD Fft = No
    Preferred vector width char = 16
    Preferred vector width short = 8
    Preferred vector width int = 4
    Preferred vector width long = 2
    Preferred vector width float = 4
    Preferred vector width double = 2
```

[back to top](#toc)
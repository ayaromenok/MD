README
========================

# OpenCV
[OpenCV](https://opencv.org) - Open Source Computer Vision Library. Sometimes accelerated with OpenCL/Cuda; Supported on Linux (includng Raspberry Pi), Windows, Linux, iOS, Android;

## Table of Context <a name="toc"></a>
- [Data types](#datatypes)
- [Performance test](#perftests)
- [Build](#build)

### Data Types <a name="datatypes"></a>
 - [cv::Point](DataTypes.md#pointtype)
 - [cv::Scalar](DataTypes.md#scalartype)
 - [cv::Size](DataTypes.md#sizetype)
 - [cv::Rect](DataTypes.md#recttype)
 - [cv::RotatedRect](DataTypes.md#rotatedrecttype)
 - [cv::Matx](DataTypes.md#matxtype)

[back to top](#toc)

### Performance Test<a name="perftests"></a>
- [General results](PerformanceTests.md#generalResults)
- [Raspberry Pi 3](PerformanceTests.md#RPI3)
- [Nvidia Tegra K1](PerformanceTests.md#TegraK1)
- [Intel Core i5-3320M+OpenCL](PerformanceTests.md#x230CL)
- [Intel Core i5-3320M CPU only](PerformanceTests.md#x230)

[back to top](#toc)

### DNN BackEnd/Target
```
    enum Backend
    {
        //! DNN_BACKEND_DEFAULT equals to DNN_BACKEND_INFERENCE_ENGINE if
        //! OpenCV is built with Intel's Inference Engine library or
        //! DNN_BACKEND_OPENCV otherwise.
        DNN_BACKEND_DEFAULT = 0,
        DNN_BACKEND_HALIDE,                //1
        DNN_BACKEND_INFERENCE_ENGINE,      //2
        DNN_BACKEND_OPENCV,                //3
        DNN_BACKEND_VKCOM,                 //4 
        DNN_BACKEND_CUDA                   //5   
    };
```
   
```     
    enum Target
    {
        DNN_TARGET_CPU = 0,
        DNN_TARGET_OPENCL,     //1
        DNN_TARGET_OPENCL_FP16,//2
        DNN_TARGET_MYRIAD,     //3
        DNN_TARGET_VULKAN,     ///4
        DNN_TARGET_FPGA,       //5
        DNN_TARGET_CUDA,       //6
        DNN_TARGET_CUDA_FP16   //7
    };
```

### Build<a name="build"></a>

#### Android

android tools required to be R25.2.5 (need to manually downgrade in 2018 and above)

`cmake -D CMAKE_TOOLCHAIN_FILE=../../opencv/platforms/android/android.toolchain.cmake -DANDROID_NATIVE_API_LEVEL=android-21 -DBUILD_ANDROID_PROJECTS=OFF ../../opencv`

OpenCV should be build with the same compiler/libstd++/stl, as other libs(Qt etc). errors in std::sting and similar appear

[back to top](#toc)

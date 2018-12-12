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

### Build<a name="build"></a>

#### Android

android tools required to be R25.2.5 (need to manually downgrade in 2018 and above)

`cmake -D CMAKE_TOOLCHAIN_FILE=../../opencv/platforms/android/android.toolchain.cmake -DANDROID_NATIVE_API_LEVEL=android-21 -DBUILD_ANDROID_PROJECTS=OFF ../../opencv`

OpenCV should be build with the same compiler/libstd++/stl, as other libs(Qt etc). errors in std::sting and similar appear

[back to top](#toc)
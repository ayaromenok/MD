PerformanceTests
========================
### Table Of Content <a name="toc"></a>
- [Intro](#intro)
- [General results](#generalResults)
- [Raspberry Pi 3](PerformanceTests.md#RPI3)
- [Nvidia Tegra K1](PerformanceTests.md#TegraK1)
- [Intel Core i5-3320M+OpenCL](PerformanceTests.md#x230CL)
- [Intel Core i5-3320M CPU only](PerformanceTests.md#x230)

### Introduction
Performance test collected with OpenCV 4.0.0Alpha of 3.4.2 on platforms without C++11 like Tegra4Linux/Ubuntu 14.04

####

### General results <a name="generalResults"> </a>


| Test | X230 | TegraK | RPI3 | single| multi|threading| opencl| comment|
|---|---|---|---|---|---|---|---| ---|
| bio | 30.271 |  53.480| 66.561 | - | + |- | -|  |
| calib3D | 157.321| | 680.995| +|+ |- |- |  particulary singlecore|
| core | 382.581| | | | | | +| |
| dnn| 153.069 || | | + | + | | |
| fea2D | 657.46 | | | + | + | - |- | particulary singlecore |
| imgCodecs | 0.189 | | | |  | | | ?|
| imgProcs | 1316.562 | | | |  | | |  particulary singlecore |
| lineDesc | 27.178 | | | + | - |- |- | |
| objDetect |32.531 | | | |  | | +| |
| optFlow | 27.913| | |- | + |+ |- | |
| photo | 16.596| | | |  | |+ | |
| reg| 4.698 |  | | +| - | | |single core |
| stereo | 33.932 | | |- | + | +| | |
| stitching| 932.264| | | |  | |+ |  particulary singlecore |
| superRes | 30.086 | | |- | + |- | | |
| tracking | 343.655 | | |- | + | -| | |
| video | 403.917| | | -| + |+ |+ | |
| videoIO| 0.851 | | | |  | | |? |
| xFea2D | 86.322| | |- | +| + |- | |
| xImgeProc | 332.847| -|+ |+ | -| | | |
| xPhoto | 8.7 | | | +|  | | | single core?|
| | | | |
| | | | |



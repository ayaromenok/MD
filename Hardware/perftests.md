perftests
========================

## Table of Context <a name="toc"></a>
- OpenCL
 	- [LuxMark 4.0a](#luxmark40a)
	- [LuxMark 3.1](#luxmark31)

## OpenCL/LuxMark 4.0.a <a name="luxmark40a"></a>
OS Window/Gangut
| Name | Result | Details|
|---|---|---|
| AMD Ryzen3 2200G(3.5GHz) | 408    | CPU only |
| GF1050(5CU, 1445MHZ)| 589 | OpenCL 3.0/Cuda 11.7.101|
| GF1050(5CU, 1445MHZ)+Ryzen3 2200G | 832 | OpenCL 3.0/Cuda 11.7.101|

## OpenCL/LuxMark 3.1 <a name="luxmark31"></a>
OS Linux/ThinkPad

| Name | Result | Details|
|---|---|---|
| i5-3320M @ ~3.0 GHz|1037| Intel Core/CPU only|
| i5-5300U @ ~2.6GHz| 1061 | Intel Core/CPU only|
| GT2 (16CU,1GHz) | 1438| GPU only from i5-3320M|
| HD5500 (24CU,900MHz) | 1143 | GPU only from i5-5300U|
| GF1050 (5CU, 1.455GHz) | 6632 | GeForce 1050/2GB/external|
| GF1050+GT2 | 8012 | GeForce 1050/2GB/external + GT2(i5-3320M) |
| CPU+GF1050+GT2 | 8224 | GeForce 1050/2GB/external + GT2 + Intel I5-3320M|

OS Windows/Gangut
| Name | Result | Details|
|---|---|---|
| AMD Ryzen3G(3.5GHz)    | 1320 | CPU only |
| GF1050 (5CU, 1.455GHz) | 7121 | GeForce 1050/2GB|

[back to top](#toc)

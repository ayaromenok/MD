perftests
========================

## Table of Context <a name="toc"></a>
- OpenCL
 	- [LuxMark 4.0a](#luxmark40a)
	- [LuxMark 3.1](#luxmark31)
	- [Civ6](#civ6)
	- [Hardware info](#hwinfo)

## OpenCL/LuxMark 4.0.a <a name="luxmark40a"></a>
OS Window/Gangut
| Name | Result | Details|
|---|---|---|
| AMD Ryzen3 2200G(3.5GHz)  | 408 | CPU only |
| AMD Ryzen3 2200G(3.5GHz)  | 298 | GPU only |
| GF1050(5CU, 1445MHZ)      | 589 | OpenCL 3.0/Cuda 11.7.101|
| GF1050 + Ryzen3 CPU       | 832 | OpenCL 3.0/Cuda 11.7.101|
| GF1050 + Ryzen3 GPU       | 856 | Dual GPU |
| GF1050 + Ryzen3 CPU+GPU   | 1075 | Dual GPU + CPU |

[back to top](#toc)

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
| AMD Ryzen3 2200G(3.5GHz)    | 1320 | CPU only |
| AMD Ryzen3 2200G(3.5GHz)    | 3120 | GPU only |
| GF1050 (5CU, 1.455GHz) | 7121 | GeForce 1050/2GB|
| GF1050 + Ryzen3 GPU | 10385 | Dual GPU |

[back to top](#toc)

## Civ6 <a name="civ6"></a>
OS Windows/Gangut
| Name | Result | Details|
|---|---|---|
| AMD Ryzen3 2200G(3.5GHz)    | xxx |  |
| GF1050 + Ryzen3 GPU | xxx |  |

[back to top](#toc)

## Hardware info <a name="hwinfo"></a>
| Name | Mark|Details|
|---|---|---|
| AMD Ryzen3 2200G   | CPU only | 4core, 3500MHz|
| AMD Ryzen3 2200G   | GPU only | gfx902, 5CU, 1100MHz, OpenCL 2.1(3444.0)|
| NVidia GF 1050/2GB | GPU only | gf1050, 8CU, 1455MHz, OpenCL 3.0/CUDA 11.7.101 |

[back to top](#toc)

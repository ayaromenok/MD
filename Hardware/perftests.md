perftests
========================

## Table of Context <a name="toc"></a>
- OpenCL
	- [LuxMark 3.1](#luxmark31)

## OpenCL/LuxMark 3.1 <a name="luxmark31"></a>
OS Linux

| Name | Result | Details|
|---|---|---|
| i5-3320M @ 2.6GHz|721| Intel Core/CPU only|
| GT2 (16CU,1GHz) | 1280 | GPU only from i5-3320M|
| GF1050 (5CU, 1.455GHz) | 6632 | GeForce 1050/2GB/external|
| GF1050+GT2 | 8012 | GPU from above |
| CPI+GF1050+GT2 | 8224 | CPU+GPU from above|

[back to top](#toc)

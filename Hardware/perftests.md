perftests
========================

## Table of Context <a name="toc"></a>
- [CPU/OpenCV](#cpucv)

## CPU/OpenCV <a name="cpucv"></a>
`./opencv_perf_line_descriptor`

| test | rpi3 | tegrak1 | rk3399 |  |
|---|---|---|---|---|
|`matching.single_match` |  | 119| 81 |  |
|`knn_match_distances_test` |  | fail | fail |  |
|`radius_match.radius_match_distances_test`|  | 2395 | 1262 |  |
|`file_str_descriptors.descriptors/0`|  | 544 | 467 |  |
|`file_str_descriptors.descriptors/0`|  | 460 | 414 |  |
|`file_str_detect.detect/0`|  | 2745 | 229 |  |
|`file_str_detect.detect/1`|  | 3518 | 273 |  |
|`file_str_detect_lsd.detect_lsd/0`|  | 12532 | 926|  |
|`file_str_detect_lsd.detect_lsd/1`|  | 1242 | 11105 |  |


[back to top](#toc)

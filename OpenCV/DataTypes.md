DataTypes
========================
### Table of Content <a name = "toc"></a>

1. [Point type](#pointtype)
2. [Scalar type](#scalartype)
3. [Size type](#sizetype)

### 1. Point Type <a name = "pointtype"></a>

Data type for `point 2x / 3x`

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Point2i p; cv::Point3f p;` |  |
| Copy constructor | `cv::Point3f p2(p1);` |  |
| Value constructor | `cv::Point2i p(x0, x1); cv::Point3d p(x0, x1, x2);` |  |
| Cast to fixed vector class | `(cv::Vec3f) p;` |  |
| Member access | `p.x; p.y` | `p.z` for three-dimentional point class |
| Dot product | `float x = p1.dot(p2);` |  |
| FP64 dot product | `double x = 1.ddot(p2);` |  |
| Cross product | `p1.cross(p2);` | for three-dimentional point only |
| Query if point `p` inside triange `r` | `p.inside (r);` | for three-dimentional point only  |

[back to top](#toc)

### 2. Scalar Type <a name="scalartype"></a>

Data type for `scalar`, which is `point 4x`;

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Scalar s;` |  |
| Copy constructor | `cv::Scalar s2(s1);` |  |
| Value constructor | `cv::Scalar s(x0); cv::Scalar s(x0, x1, x2, x3);` |  |
| Element-wise multiplication | `s1.mul(s2);` |  |
| (Quaternion) conjugation | `s.conj();`| returns `cv::Scalar(s0, -s1, -s2, -s2)` |
| (Quaternion) real test| `s.isReal();` | returns `true` if `s1==s2==s3==0` |

[back to top](#toc)

### 3. Size Type <a name="sizetype"></a>

Data type for `size`, which is `point 2x`;  Can't cast to fixed vector classes;

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Size sz; cvSize2i sz; cv::Size2f sz;` |  |
| Copy constructor | `cv::Size sz2(sz1);` |  |
| Value constructor | `cv::Size2f sz(w,h);` |  |
| Member access | `sz.width; sz.height;` |  |
| Compute area | `sz.area();` |  |

[back to top](#toc)

### Appendix
|  |  |  |

[back to top](#toc)
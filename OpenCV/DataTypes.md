DataTypes
========================
### Table of Content <a name = "toc"></a>

1. [Point type](#pointtype)
2. [Scalar type](#scalartype)
3. [Size type](#sizetype)
4. [Rect type](#recttype)
 	- [Rect operatos](#rectoperators)	
5. [RotatedRect type](#rotatedrecttype)
6. [Matx type](#matxtype)


### 1. cv::Point <a name = "pointtype"></a>

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

### 2. cv::Scalar <a name="scalartype"></a>

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

### 3. cv::Size <a name="sizetype"></a>

Data type for `size`, which is `point 2x`;  Can't cast to fixed vector classes;

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Size sz; cvSize2i sz; cv::Size2f sz;` |  |
| Copy constructor | `cv::Size sz2(sz1);` |  |
| Value constructor | `cv::Size2f sz(w,h);` |  |
| Member access | `sz.width; sz.height;` |  |
| Compute area | `sz.area();` |  |

[back to top](#toc)

### 4. cv::Rect  <a name="recttype"></a>

Data type for `rect`, which is `point 2x`and `size`;

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Rect r();` |  |
| Copy constructor | `cv::Rect r(r1);` |  |
| Value constructor | `cv::Rect R(x,y,w,h);` |  |
| Construct from origin and size | `cv::Rect(p,sz);` |  |
| Construct from two corners | `cv::Rect(p1,p2);` |  |
| Member access | `r.x; r.y; r.width; r.height;` |  |
| Compute area | `r.area();` |  |
| Extract upper-left corner | `r.tl();` | Top-Left |
| Extract bottom-right corner | `r.br();` | Bottom-Right |
| Determinate if point `p`p inside rectangle `r` | `r.contains(p);` |  |

[back to top](#toc)

####  4.1 cv::Rect operators  <a name="rectoperators"></a>

Operators, supported by `cv::Rect``;

| Operation | Example | Comments |
|---|---|---|
| Intersection of rectangles `r1` and `r2` | `cv::Rect r3 = r1 & r2; r1 &= r2;` |  |
| Minimum area rectangle containing rectangles `r1` and `r2` | `cv::Rect r3 = r1|r2; r1 |= r2;` |  |
| Translate rectangle `r` by an amount `x` | `cv::Rect rx = r+x; r += x;` |  |
| Enlarge a rectangle `r` by an amount given by size `s` | `cv::Rect rs = r+s; r+= s;` |  |
| Compare rectangles `r1` and `r2` for exact equality | `bool eq = (r1 == r2);` |  |
| Compare rectangles `r1` and `r2` for inequality  | `bool ne = (r1 != r2);` |  |

[back to top](#toc)

### 5. cv::RotatedRect  <a name="rotatedrecttype"></a>

`cv::RotatedRect` located in relation to it's center, while `cv::Rect` to it's uppler-left conner

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::RotatedRect rr();` |  |
| Copy constructor | `cv::RotatedRect rr2(rr1);` |  |
| Value constructor | `cv::RotetedRect R(p, sz, theta);` |  |
| Construct from two corners | `cv::RotetedRect(p1,p2);` |  |
| Member access | `rr.center; rr.size; rr.angle` |  |
| Return a list of the corners | `rr.points(pts[4);` |  |

[back to top](#toc)

### 6. cv::Matx  <a name="matxtype"></a>

Fixed matrix classes.

| Operation | Example | Comments |
|---|---|---|
| Default constructor | `cv::Matx33f; cv::Matx43d m43d;` |  |
| Copy constructor | `cv::Matx22d m22d(n22d);` |  |
| Value constructor | `cv::Matx21f m(x0, x1); cv::Matx32d m(x0, x1, x2, x3, x4, x5)` |  |
| Matrix of identical elements | `m33f = cv::Matxf::all(x);` |  |
| Matrix of zeros | `m23d = cv::Matx23d::zeros();` |  |
| Matrix of ones | `m16f = cv::Matx16f::ones();` |  |
| Create a unit matrix | `m33f = cv::Matx33f::eye();` |  |
| Matrix that hold a diagonal of another | `m31f = cv::Matx33f::diag();` | create matrix of size 3-by-1 of floats |
| Matrix with uniformly distributed entries | `m33f = cv::Matx33f::randu(min, max);` |  |
| Matris with normally distributed entries | `m33f = cv::Mat33f::nrandn(mean, varinace);` |  |
| Member access | `m(i,j), m(i);` | one arg for one-dimentional matrices only |
| Matrix algebra | `m1 = m0; m0 * m1; m0 + m1; m0 - m1;` |  |
| Singleton algebra | `m * a; a * m; m / a;` |  |
| Comparison | `m1 == m2l m1 != m2;` |  |
| Dot product | `m1.dot(m2);` | sum of element-wise multiplication, precision of m |
| Double dot product | `m1.ddot(m2);` | double precision |
| Reshape a matrix | `m91f = m33f.reshape<9,1>();` |  |
| Cast operators | `m44f = (Mat44f) m44d;` |  |
| Extract `2x2` submatrix at `(i,j)` | `m44f.get_minor<2,2>(i,j);` |  |
| Extract row `i` | `m14f = m44f.row(i);` |  |
| Extract column `j` | `m41f = m44f.col(j);` |  |
| Extract diagonal | `m41f = m44f.diag();` |  |
| Compute transpose | `n44 = m44f.t();` |  |
| Invert matrix | `n44f = m44f.inv(method);` | default is cv::DECOMP_LU |
| Solve linear system | `m31f = m33f.solve(rhs31f, method);  m32f = m33f.solve<2>(rhs32f, method);` | template form, default is DECOMP_LU |
| Per-element multiplication | `m1,mul(m2);` |  |
 
[back to top](#toc)


### Appendix
|  |  |  |

[back to top](#toc)
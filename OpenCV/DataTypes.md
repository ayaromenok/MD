DataTypes
========================
### Table of Content

	- [PointType](#pointtype)
	- 
### Point Type <a name = "pointtype"></a>

Data type for point 2/3

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
|  |  |  |

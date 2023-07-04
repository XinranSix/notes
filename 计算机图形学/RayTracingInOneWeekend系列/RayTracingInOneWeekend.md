![Honeyview_year=2023 month=4 day=15 hour=13 minute=30 second=33 spp=1000 width=1920 height=1080](https://github.com/XinranSix/docs/assets/62458905/d8ca611e-f07c-41c7-ac36-e4e5ff6552f6)

[toc]

## 输出图像

### 介绍 PPM 图像格式 & 输出 PPM 格式的图像

我们需要有一种方式将渲染的图像存储起来，最字节的方法就是将其写入文本文件。`ppm` 是一个纯文本的图像格式，下面是维基百科对其的描绘：

![image](https://github.com/XinranSix/docs/assets/62458905/d139e475-67ad-4d7e-bfa6-31ec245d5107)

让我们编写一些代码输出以下内容：

```cpp
#include <iostream>
#include <fstream>

// Image

const int image_width = 256;
const int image_height = 256;

// Render

std::ofstream ofs("image.ppm");

int main() {
    ofs << "P3\n" << image_width << ' ' << image_height << "\n255\n";
    for (int j = image_height - 1; j >= 0; --j) {
        for (int i = 0; i < image_width; ++i) {
            auto r = double(i) / (image_width - 1);
            auto g = double(j) / (image_height - 1);
            auto b = 0.25;

            int ir = static_cast<int>(255.999 * r);
            int ig = static_cast<int>(255.999 * g);
            int ib = static_cast<int>(255.999 * b);

            ofs << ir << ' ' << ig << ' ' << ib << '\n';
        }
    }

    return 0;
}
```

> 注意：
>
> 1. 像素按行从左到右输出。
> 2. 行从上到下输出。
> 3. 按照惯例，颜色分量范围是 $0.0 \sim 1.0$.
> 4. 红色从左到右从完全关闭（黑色）到完全打开（亮红色），绿色从底部的黑色到顶部完全打开。红色和绿色一起变成黄色，所以我们应该预期右上角是黄色的。

输出得到的内容：

```
P3
256 256
255
0 255 63
1 255 63
2 255 63
3 255 63
4 255 63
5 255 63
6 255 63
7 255 63
8 255 63
9 255 63
...
```

结果如下：

![img](https://raytracing.github.io/images/img-1.01-first-ppm-image.png)

### 添加进度条

进度条是跟踪长时间渲染进度的有效方法，并且可以识别由无限循环或其他问题造成的问题。

我们将图像输出到标准输入流 `std::cout`（我这里为了方便起见输出到了一个文件流），将进度输出到错误流 `std::cerr`：

```cpp
#include <iostream>
#include <fstream>
#include <ostream>

// Image

const int image_width = 256;
const int image_height = 256;

// Render

std::ofstream ofs("image.ppm");

int main() {
    ofs << "P3\n" << image_width << ' ' << image_height << "\n255\n";
    for (int j = image_height - 1; j >= 0; --j) {
        std::cerr << "\rScanlines remaining: " << j << ' ' << std::flush;
        for (int i = 0; i < image_width; ++i) {
            auto r = double(i) / (image_width - 1);
            auto g = double(j) / (image_height - 1);
            auto b = 0.25;

            int ir = static_cast<int>(255.999 * r);
            int ig = static_cast<int>(255.999 * g);
            int ib = static_cast<int>(255.999 * b);

            ofs << ir << ' ' << ig << ' ' << ib << '\n';
        }
    }

    std::cerr << "\nDone.\n";

    return 0;
}
```

## `vec3` 类

> 封装一个 vec3 类

几乎所有的图形程序都要使用存储矢量和颜色的类。在许多系统中，这些矢量是 4D 的（矢量是齐次坐标，颜色是 RGBA）。这里是 3D 矢量来表示颜色、位置、方向、偏移量等。`vec3` 有两个别名：`point3` 和 `color`。

### 变量和方法

下面是 `vec3.h` 文件的前面一部分：

```cpp
/**
 * @file    :   vec3.h
 * @date    :   2023/07/01 10:56:30
 * @author  :   yaojie
 * @version :   1.0
 */

#ifndef VEC3_H
#define VEC3_H

#include <cmath>
#include <iostream>

class vec3 {
public:
    vec3() : e{0, 0, 0} {}
    vec3(double e0, double e1, double e2) : e{e0, e1, e2} {}

    double x() const { return e[0]; }
    double y() const { return e[1]; }
    double z() const { return e[2]; }

    vec3 operator-() const { return vec3(-e[0], -e[1], -e[2]); }
    double operator[](int i) const { return e[i]; }
    double &operator[](int i) { return e[i]; }

    vec3 &operator+=(const vec3 &v) {
        e[0] += v.e[0];
        e[1] += v.e[1];
        e[2] += v.e[2];
        return *this;
    }

    vec3 &operator*=(const double t) {
        e[0] *= t;
        e[1] *= t;
        e[2] *= t;
        return *this;
    }

    vec3 operator/=(const double t) { return *this *= 1 / t; }

    double length() const { return std::sqrt(length_squared()); }

    double length_squared() const {
        return e[0] * e[0] + e[1] * e[1] + e[2] * e[2];
    }

public:
    double e[3];
};

using point3 = vec3;
using color = vec3;

#endif
```

### `vec3` 工具函数

下面是 `vec3.h` 文件的第二部分：

```cpp
// vec3 Utility Functions

inline std::ostream &operator<<(std::ostream &out, const vec3 &v) {
    return out << v.e[0] << ' ' << v.e[1] << ' ' << v.e[2];
}

inline vec3 operator+(const vec3 &u, const vec3 &v) {
    return vec3(u.e[0] + v.e[0], u.e[1] + v.e[1], u.e[2] + v.e[2]);
}

inline vec3 operator-(const vec3 &u, const vec3 &v) {
    return vec3(u.e[0] - v.e[0], u.e[1] - v.e[1], u.e[2] - v.e[2]);
}

inline vec3 operator*(const vec3 &u, const vec3 &v) {
    return vec3(u.e[0] * v.e[0], u.e[1] * v.e[1], u.e[2] * v.e[2]);
}

inline vec3 operator*(double t, const vec3 &v) {
    return vec3(t * v.e[0], t * v.e[1], t * v.e[2]);
}

inline vec3 operator*(const vec3 &v, double t) { return t * v; }

inline vec3 operator/(vec3 v, double t) { return (1 / t) * v; }

inline double dot(const vec3 &u, const vec3 &v) {
    return u.e[0] * v.e[0] + u.e[1] * v.e[1] + u.e[2] * v.e[2];
}

inline vec3 cross(const vec3 &u, const vec3 &v) {
    return vec3(u.e[1] * v.e[2] - u.e[2] * v.e[1],
                u.e[2] * v.e[0] - u.e[0] * v.e[2],
                u.e[0] * v.e[1] - u.e[1] * v.e[0]);
}

inline vec3 unit_vector(vec3 v) { return v / v.length(); }
```

### 颜色功能函数

创建一个函数来将单个像素颜色写入流：

```cpp
#ifndef COLOR_H
#define COLOR_H

#include <iostream>

#include "vec3.h"

void write_color(std::ostream &out, color pixel_color) {
    out << static_cast<int>(255.999 * pixel_color.x()) << ' '
        << static_cast<int>(255.999 * pixel_color.y()) << ' '
        << static_cast<int>(255.999 * pixel_color.z()) << '\n';
}

#endif

```

修改 `main` 函数：

```cpp
#include <iostream>
#include <fstream>

#include "color.h"
#include "vec3.h"

// Image

const int image_width = 256;
const int image_height = 256;

// Render

std::ofstream ofs("image.ppm");

int main() {
    ofs << "P3\n" << image_width << ' ' << image_height << "\n255\n";
    for (int j = image_height - 1; j >= 0; --j) {
        std::cerr << "\rScanlines remaining: " << j << ' ' << std::flush;
        for (int i = 0; i < image_width; ++i) {
            color pixel_color(double(i) / (image_width - 1),
                              double(j) / (image_height - 1), 0.25);
            write_color(ofs, pixel_color);
        }
    }

    std::cerr << "\nDone.\n";

    return 0;
}

```

## 光线、简单的相机、背景

所有的光线追踪器所做的一件事是计算沿着光线方向能看到的颜色。光线可以表示为如下方程：
$$
\mathbf{P}\left(t\right) = \mathbf{A} + t\mathbf{b}
$$
这里 $\mathbf{P}$ 是光线，$\mathbf{A}$ 是原点，$\mathbf{b}$ 是光线方向，$t$ 是一个实数。取不同的 $t$ 可以在光线上移动。对于正 $t$，我们只能看到 $\mathbf{A}$ 前面的部分。

`ray.h` 的代码如下：

```cpp
#ifndef RAY_H
#define RAY_H

#include "vec3.h"

class ray {
public:
    ray() {}
    ray(const point3 &origin, const vec3 &direction)
        : orig(origin), dir(direction) {}

    point3 origin() const { return orig; }
    vec3 direction() const { return dir; }

    point3 at(double t) const { return orig + t * dir; }

public:
    point3 orig;
    vec3 dir;
};

#endif

```

### 将光线发送到场景中


##Name
glViewport — 设置视口。只有绘制在视口区域内的图形才能被显示。

##C Specification

    void glViewport(GLint x, GLint y, GLsizei width, GLsizei height);
 
##Android Specification

    void glViewport (int x, int y, int width, int height)

##Parameters

- ***x, y*** 规定视口矩形左下角顶点在屏幕窗口坐标系中的坐标。初始为(0, 0)。
- ***width, height*** 规定视口的宽、高。在opengl绘制内容第一次attach到窗口上时，视口宽、高会被设置为屏幕窗口的宽、高。

##Description

glViewport specifies the affine transformation of x and y from normalized device coordinates to window coordinates. Let (x[nd],y[nd]) be normalized device coordinates. Then the window coordinates (x[w],y[w]) are computed as follows:

    x[w] = (x[nd] + 1) * width / 2 + x[nd]
    y[w] = (y[nd] + 1) * height / 2 + y[nd]

Viewport width and height are silently clamped to a range that depends on the implementation. To query this range, call `glGet` with argument `GL_MAX_VIEWPORT_DIMS`.

`glViewport`函数导出了“设备”(Device)坐标到窗口(Window)坐标的变化矩阵。令((x[nd],y[nd])为“设备”坐标，那么映射到的窗口坐标(x[w],y[w])将按如下公式计算而成：

    x[w] = (x[nd] + 1) * width / 2 + x[nd]
    y[w] = (y[nd] + 1) * height / 2 + y[nd]

视口的宽、高其实有一个取值范围，它不能超过某个最大值。你可以通过[glGet](1)配合`GL_MAX_VIEWPORT_DIMS`参数来获取这个取值范围。

##Errors

在传入负的宽或高时会触发`GL_INVALID_VALUE`错误。

##Associated Gets

[glGet](1) - `GL_VIEWPORT`参数

[glGet](1) - `GL_MAX_VIEWPORT_DIMS`参数

##See Also

[glDepthRangef](2)

[1]: https://github.com/CodingFish2015/AndroidOpenGLES20Reference_Chinese/blob/master/opengles20reference/glGet.md

[2]: https://github.com/CodingFish2015/AndroidOpenGLES20Reference_Chinese/blob/master/opengles20reference/glDepthRangef.md
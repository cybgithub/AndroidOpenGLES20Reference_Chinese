##Name

`glDrawArrays` — 将当前“状态”中的数据渲染成基本图元。

##C Specification

    void glDrawArrays(GLenum mode, GLint first, GLsizei count);
 
##Android Specification

    void glDrawArrays (int mode, int first, int count)

##Parameters

- ***mode*** 指定渲染的基本图元种类。可以是 `GL_POINTS`, `GL_LINE_STRIP`, `GL_LINE_LOOP`, `GL_LINES`, `GL_TRIANGLE_STRIP`, `GL_TRIANGLE_FAN`, 或 `GL_TRIANGLES` 。

- ***first*** 渲染的顶点数据起始位置。

- ***count*** 渲染的顶点数据个数。

##Description

`glDrawArrays` specifies multiple geometric primitives with very few subroutine calls. Instead of calling a GL procedure to pass each individual vertex attribute, you can use `glVertexAttribPointer` to prespecify separate arrays of vertices, normals, and colors and use them to construct a sequence of primitives with a single call to `glDrawArrays`.

`glDrawArrays` 能够通过简单的几条指令渲染出指定的基本图元。你不需要将顶点属性数据一个个地传入，你只需要调用[glVertexAttribPointer](glVertexAttribPointer.md)指定不同顶点属性（顶点、颜色、一般数据）的数据位置来形成不同顶点属性的数据流，并通过`glDrawArrays`将他们渲染出来。

When `glDrawArrays` is called, it uses count sequential elements from each enabled array to construct a sequence of geometric primitives, beginning with element first. mode specifies what kind of primitives are constructed and how the array elements construct those primitives.

当`glDrawArrays`被调用后，它会从传入的first参数开始，对每个激活的顶点属性数据中进行连续的渲染。mode指定了渲染的基本图元与连续数据组成基本图元的规则。

译者注：关于mode的解释，当有四个顶点(v1,v2,v3,v4)时：

- `GL_POINTS` 每个顶点以独立点的形式渲染，如：v1,v2,v3,v4;
- `GL_LINE_STRIP` 相邻的两个顶点组成连续线段，最后不闭合，如；v1-v2-v3-v4;
- `GL_LINE_LOOP` 相邻的两个顶点组成连续线段，最后闭合，如；v1-v2-v3-v4-v1;
- `GL_LINES` 相邻两个顶点组成两两线段，如：v1-v2, v3-v4;
- `GL_TRIANGLE_STRIP` 相邻三个顶点组成三角形，最后不闭合，如：v1v2v3, v2v3v4;
- `GL_TRIANGLE_FAN` 相邻三个顶点组成三角形，最后闭合，如：v1v2v3,v2v3v4,v3v4v1;
- `GL_TRIANGLES` 相邻三个顶点组成三角形，三角形之间顶点不共用，最后不够组成三角形的顶点不渲染，如：v1v2v3;

To enable and disable a generic vertex attribute array, call `glEnableVertexAttribArray` and `glDisableVertexAttribArray`.

你可以调用[glEnableVertexAttribArray](glEnableVertexAttribArray.md) and [glDisableVertexAttribArray](glDisableVertexAttribArray.md)来激活/反激活一组顶点属性数据。

##Notes

If the current program object, as set by [glUseProgram](glUseProgram.md), is invalid, rendering results are undefined. However, no error is generated for this case.

如果当前的程序对象（通过[glUseProgram](glUseProgram.md)设置）无效，则渲染结果也无效。不过此时不会产生异常。

##Errors

`GL_INVALID_ENUM` 传入的`mode`不是指定的枚举数字类型中的一种。

`GL_INVALID_VALUE` 传入的`count`为负数。

`GL_INVALID_FRAMEBUFFER_OPERATION` 当前的帧缓冲区不完整(当[glCheckFramebufferStatus](glCheckFramebufferStatus.md) 的返回不是 `GL_FRAMEBUFFER_COMPLETE`时这个帧缓冲区就不完整)。

##See Also

[glCheckFramebufferStatus](glCheckFramebufferStatus.md), [glDisableVertexAttribArray](glDisableVertexAttribArray.md), [glDrawElements](glDrawElements.md), [glEnableVertexAttribArray](glEnableVertexAttribArray.md), [glUseProgram](glUseProgram.md), [glVertexAttribPointer](glVertexAttribPointer.md)



##Name

`glGenBuffers` — 生成未使用的缓冲区对象名称。

##C Specification

    void glGenBuffers(  GLsizei n, GLuint *buffers);
 
##Android Specification

    void glGenBuffers (int n, IntBuffer buffers)
    void glGenBuffers (int n, int[] buffers, int offset)

##C Parameters

- ***n*** 需要生成的名称数量。
- ***buffers*** 存储生成的缓冲区对象名称的数组。

##Android Parameters

- ***n*** 需要生成的名称数量。
- ***buffers*** 存储生成的缓冲区对象名称的数组
- ***offset***(可选) 存储起始位置在数组中的偏移量

##Description

`glGenBuffers` returns n buffer object names in buffers. There is no guarantee that the names form a contiguous set of integers; however, it is guaranteed that none of the returned names was in use immediately before the call to glGenBuffers.

`glGenBuffers`会获取n个缓冲区对象名，这n个对象名不一定是连续的，但是一定是没有正在被使用的。

Buffer object names returned by a call to `glGenBuffers` are not returned by subsequent calls, unless they are first deleted with `glDeleteBuffers`.

通过`glGenBuffers`获取到的缓冲区对象名称不会再被接下来的调用的`glGenBuffers`获取，除非调用[glDeleteBuffers](glDeleteBuffers.md)删除与该名称关联的缓冲区对象。

No buffer objects are associated with the returned buffer object names until they are first bound by calling `glBindBuffer`.

生成缓冲区对象名称并不会有缓冲区对象与它关联，除非使用`glBindBuffer`将缓冲区对象与名称绑定。

##Errors

`GL_INVALID_VALUE` - 在输入的参数n为负数时触发。

##Associated Gets

[glIsBuffer](glIsBuffer.md)

##See Also

[glBindBuffer](glBindBuffer.md), [glDeleteBuffers](glDeleteBuffers.md), [glGet](glGet.md)



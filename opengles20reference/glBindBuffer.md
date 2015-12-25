##Name

`glBindBuffer` — 绑定指定名称的服务器缓冲区对象。

##C Specification

    void glBindBuffer(GLenum target, GLuint buffer);
 
##Android Specification

    void glBindBuffer (int target, int buffer)

##Parameters

- ***target*** 被绑定的缓冲区。在gles20中，此选项只能是`GL_ARRAY_BUFFER`（顶点数据）或`GL_ELEMENT_ARRAY_BUFFER`（索引数据）。

- ***buffer*** 缓冲区对象名称。

##Description

`glBindBuffer` lets you create or use a named buffer object. Calling `glBindBuffer` with `target` set to `GL_ARRAY_BUFFER` or `GL_ELEMENT_ARRAY_BUFFER` and `buffer` set to the name of the new buffer object binds the buffer object name to the target. When a buffer object is bound to a target, the previous binding for that target is automatically broken.

`glBindBuffer`允许你创建、使用指定名称的缓冲区对象。调用`glBindBuffer`并设`target`为`GL_ARRAY_BUFFER`或`GL_ELEMENT_ARRAY_BUFFER`可以创建一个指定名称的缓冲区对象，并将其绑定到`target`上。当一个新的对象被绑定到`target`上时，原先绑定到该`target`的对象会自动解绑。

Buffer object names are unsigned integers. The value zero is reserved, but there is no default buffer object for each buffer object target. Instead, buffer set to zero effectively unbinds any buffer object previously bound, and restores client memory usage for that buffer object target. Buffer object names and the corresponding buffer object contents are local to the shared object space of the current GL rendering context.

缓冲区对象名称是无符号整数类型。没有默认名称。这里0是保留字，传入0的话会将之前绑定到`target`的缓存解绑，并停止使用该缓冲区对象。缓冲区对象名称与对应的缓冲区只是当前GL渲染上下文中共享对象区域里的局部变量。

You may use `glGenBuffers` to generate a set of new buffer object names.

你可以使用[glGenBuffers](glGenBuffers.md)来生成一系列未使用的顶点缓存名字。

The state of a buffer object immediately after it is first bound is a zero-sized memory buffer with `GL_STATIC_DRAW` usage.

缓存对象在一开始被绑定时它size被置为0，默认属性是顶点数据一经初始化后不会被修改（`GL_STATIC_DRAW`）。

While a non-zero buffer object name is bound, GL operations on the target to which it is bound affect the bound buffer object, and queries of the target to which it is bound return state from the bound buffer object. While buffer object name zero is bound, as in the initial state, attempts to modify or query state on the target to which it is bound generates an `GL_INVALID_OPERATION` error.

当一个非零名称的缓冲区对象被绑定到某个`target`后，opengl在该`target`上的操作也会影响被绑定的缓冲区对象。查询该`target`的绑定状态时会返回缓冲区对象的状态。如果一个名称为0的缓冲区对象被绑定到`target`上，那么尝试修改或查询该`target`时会触发`GL_INVALID_OPERATION`错误。

When vertex array pointer state is changed by a call to glVertexAttribPointer, the current buffer object binding (`GL_ARRAY_BUFFER_BINDING`) is copied into the corresponding client state for the vertex attrib array being changed, one of the indexed `GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDINGs`. While a non-zero buffer object is bound to the `GL_ARRAY_BUFFER` target, the vertex array pointer parameter that is traditionally interpreted as a pointer to client-side memory is instead interpreted as an offset within the buffer object measured in basic machine units.

当顶点数组指针的状态被[glVertexAttribPointer](glVertexAttribPointer.md)修改之后，当前被绑定的缓冲区对象(可以使用[glGet](glGet.md) with parameter `GL_ARRAY_BUFFER_BINDING`获取)状态会被存为客户端状态(`GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDINGs`)。当一个非0名称的缓冲区对象被绑定到`GL_ARRAY_BUFFER`上时，[glVertexAttribPointer](glVertexAttribPointer.md)的buffer/offset参数会被认为是缓冲区的数据/偏移量，而不是原本的客户机上的内存数据/偏移量。

While a non-zero buffer object is bound to the `GL_ELEMENT_ARRAY_BUFFER` target, the indices parameter of glDrawElements that is traditionally interpreted as a pointer to client-side memory is instead interpreted as an offset within the buffer object measured in basic machine units.

当一个名称非零的缓冲区对象被绑定到`GL_ELEMENT_ARRAY_BUFFER`时，`glDrawElements`的buffer/offset参数会被认为是缓冲区的数据/偏移量，而不是原本的客户机内存数据/偏移量。

A buffer object binding created with `glBindBuffer` remains active until a different buffer object name is bound to the same target, or until the bound buffer object is deleted with glDeleteBuffers.

一个缓存对象会保持激活状态，直至另一个缓存对象名绑定至同一个`target`或者调用[glDeleteBuffers](glDeleteBuffers.md)删除缓存对象。

Once created, a named buffer object may be re-bound to any target as often as needed. However, the GL implementation may make choices about how to optimize the storage of a buffer object based on its initial binding target.

在缓存对象创建之后，它可能会根据需要被反复地绑定到不同的`target`上。不过opengl可能只会根据第一个被绑定的`target`来决定怎么实现这部分缓存存储。

##Errors

`GL_INVALID_ENUM` 在传入的target数值不是合法数值时会触发。

##Associated Gets

[glGet](glGet.md) with argument `GL_ARRAY_BUFFER_BINDING`

[glGet](glGet.md) with argument `GL_ELEMENT_ARRAY_BUFFER_BINDING`

##See Also

[glDeleteBuffers](glDeleteBuffers.md), [glGenBuffers](glGenBuffers.md), [glGet](glGet.md), [glIsBuffer](glIsBuffer.md)


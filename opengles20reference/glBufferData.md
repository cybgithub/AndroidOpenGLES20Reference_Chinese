##Name

`glBufferData` — 创建并初始化缓冲区对象的数据。

##C Specification

    void glBufferData(  GLenum target, GLsizeiptr size, const GLvoid * data, GLenum usage);

##Android Specification

    void glBufferData (int target, int size, Buffer data, int usage)

##C Parameters

- ***target*** Specifies the target buffer object. The symbolic constant must be `GL_ARRAY_BUFFER` or `GL_ELEMENT_ARRAY_BUFFER`.

- ***size*** Specifies the size in bytes of the buffer object's new data store.

- ***data*** Specifies a pointer to data that will be copied into the data store for initialization, or NULL if no data is to be copied.

- ***usage*** Specifies the expected usage pattern of the data store. The symbolic constant must be `GL_STREAM_DRAW`, `GL_STATIC_DRAW`, or `GL_DYNAMIC_DRAW`.

##Android Parameters

- ***target*** 指定缓冲区对象，在OPENGL ES 2.0中，它必须是`GL_ARRAY_BUFFER`或`GL_ELEMENT_ARRAY_BUFFER`。

- ***size*** 创建数据需要分配的空间大小，以字节衡量。

- ***data*** 放进新分配的缓冲区对象数据空间的数据对象，传null则不放进数据。

- ***usage*** 指定新分配的缓冲区对象数据的“用法”。它必须是`GL_STREAM_DRAW`, `GL_STATIC_DRAW`, 或`GL_DYNAMIC_DRAW`。（具体解释见下文）

##Description

`glBufferData` creates a new data store for the buffer object currently bound to target. Any pre-existing data store is deleted. The new data store is created with the specified size in bytes and usage. If data is not NULL, the data store is initialized with data from this pointer.

`glBufferData` 在当前绑定到指定`target`的缓冲区对象中分配了数据空间。这个缓冲区对象中之前的所有数据将会被销毁，会创建一个新的指定字节数与“用法”的数据空间。当传入数据不为空的时候，新创建的数据空间内容会被传入数据初始化。

usage is a hint to the GL implementation as to how a buffer object's data store will be accessed. This enables the GL implementation to make more intelligent decisions that may significantly impact buffer object performance. It does not, however, constrain the actual usage of the data store. usage can be broken down into two parts: first, the frequency of access (modification and usage), and second, the nature of that access. The frequency of access may be one of these:

- `STREAM` The data store contents will be modified once and used at most a few times.
- `STATIC` The data store contents will be modified once and used many times.
- `DYNAMIC` The data store contents will be modified repeatedly and used many times.

“用法”告诉了opengl如何使用这部分缓冲区对象数据。这有助于opengl提升缓冲区对象的使用效率。实际上“用法”并没有限制了数据的使用，它这两方面上做了区分：读取与写入的频率、读取与写入的特征。频率可以分为以下几种：

- `STREAM` 它只会被写入一次，可以读取少数次数。
- `STATIC` 它只会被写入一次，可以读取任意次数。
- `DYNAMIC` 它可以被写入与读取任意次数。

The nature of access must be:

- `DRAW` The data store contents are modified by the application, and used as the source for GL drawing and image specification commands.

读取与写入的特征可以是：(OPENGLES 2.0中只有一项)

- `DRAW` 应用程序(客户机)写入数据，OPENGL(服务机)在绘制、图像处理的时候读取数据。

##Notes

If data is NULL, a data store of the specified size is still created, but its contents remain uninitialized and thus undefined.

当传入的数据为null时，数据空间依然会被创造，但是里面的数据没有被初始化。

Clients must align data elements consistent with the requirements of the client platform, with an additional base-level requirement that an offset within a buffer to a datum comprising N be a multiple of N.

应用程序(客户机)必须自己根据使用平台保证数据偏移量的一致性，数据元的大小为N时相邻数据之间的偏移量也必须是N的倍数。

##Errors

`GL_INVALID_ENUM` - 传入target不是 `GL_ARRAY_BUFFER` 或 `GL_ELEMENT_ARRAY_BUFFER` 时触发。

`GL_INVALID_ENUM` - 传入usage不是 `GL_STREAM_DRAW`,`GL_STATIC_DRAW`或`GL_DYNAMIC_DRAW`时触发。

`GL_INVALID_VALUE` - 传入size为负时触发。

`GL_INVALID_OPERATION` - 当前与target绑定的缓冲区对象名为0时触发。

`GL_OUT_OF_MEMORY` - opengl无法创建指定size的数据空间时触发。

##Associated Gets

[glGetBufferParameteriv](glGetBufferParameteriv.md) with argument `GL_BUFFER_SIZE` or `GL_BUFFER_USAGE`

##See Also

[glBindBuffer](glBindBuffer.md), [glBufferSubData](glBufferSubData.md)



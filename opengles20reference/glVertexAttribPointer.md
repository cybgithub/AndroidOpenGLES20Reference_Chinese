##Name

`glVertexAttribPointer` — 指定顶点属性数组的数据位置。

##C Specification

    void glVertexAttribPointer(GLuint index, GLint size, GLenum type, GLboolean normalized, GLsizei stride, const GLvoid * pointer);
 
##Android Specification

    void glVertexAttribPointer (int index, int size, int type, boolean normalized, int stride, Buffer ptr)

    void glVertexAttribPointer (int index, int size, int type, boolean normalized, int stride, int offset)

##C Parameters

- ***index*** Specifies the index of the generic vertex attribute to be modified.

- ***size*** Specifies the number of components per generic vertex attribute. Must be 1, 2, 3, or 4. The initial value is 4.

- ***type*** Specifies the data type of each component in the array. Symbolic constants `GL_BYTE`, `GL_UNSIGNED_BYTE`, `GL_SHORT`, `GL_UNSIGNED_SHORT`, `GL_FIXED`, or `GL_FLOAT` are accepted. The initial value is `GL_FLOAT`.

- ***normalized*** Specifies whether fixed-point data values should be normalized (`GL_TRUE`) or converted directly as fixed-point values (`GL_FALSE`) when they are accessed.

- ***stride*** Specifies the byte offset between consecutive generic vertex attributes. If stride is 0, the generic vertex attributes are understood to be tightly packed in the array. The initial value is 0.

- ***pointer*** Specifies a pointer to the first component of the first generic vertex attribute in the array. The initial value is 0.

##Android Parameters

- ***index*** 顶点属性数组的索引。
- ***size*** 顶点属性数据的维度，必须是1、2、3、4之一，默认是4。
- ***type*** 顶点属性数据的数据类型，可以是`GL_BYTE`, `GL_UNSIGNED_BYTE`, `GL_SHORT`, `GL_UNSIGNED_SHORT`, `GL_FIXED`, `GL_FLOAT`之一。默认是`GL_FLOAT`。
- ***normalized*** 是否在访问非浮点数据的顶点数据时对它进行归一化。true表示会将非浮点数类型的顶点数据进行归一化 ，false则直接取原值进行强制转换。
- ***stride*** 数组数据之间的偏移量，单位为字节。如果为0，则所有数据将会被认为成“缩在一个点”。默认为0。
- 第五项参数
    + ***offset*** 根据stride分割出的数据单元中，每一项的起始位置到第一个目的数据的偏移量。
    + ***ptr*** 存储上述偏移量的`Buffer`。
  

##Description

`glVertexAttribPointer` specifies the location and data format of the array of generic vertex attributes at index index to use when rendering. size specifies the number of components per attribute and must be 1, 2, 3, or 4. type specifies the data type of each component, and stride specifies the byte stride from one attribute to the next, allowing vertices and attributes to be packed into a single array or stored in separate arrays. If set to `GL_TRUE`, normalized indicates that values stored in an integer format are to be mapped to the range [-1,1]\(for signed values) or [0,1]\(for unsigned values) when they are accessed and converted to floating point. Otherwise, values will be converted to floats directly without normalization.

`glVertexAttribPointer` 指定了对应索引的顶点属性数组将用来渲染的数据位置与类型。`size`指定了数据的维度，必须是1、2、3、4之间的数字。`type`指定了数据的类型。`stride`指定了数据之间的字节偏移量，这允许你将所有数据按照偏移量一致的原则放入同一个数组中。如果`normalized`为true，则整型数据在读取时会被映射到[-1, 1]（有符号整数）或[0, 1]（无符号整数）；如果`normalized`为false，则整型数据会直接被强制转换为浮点数。

If a non-zero named buffer object is bound to the `GL_ARRAY_BUFFER` target (see `glBindBuffer`) while a generic vertex attribute array is specified, pointer is treated as a byte offset into the buffer object's data store. Also, the buffer object binding (`GL_ARRAY_BUFFER_BINDING`) is saved as generic vertex attribute array client-side state (`GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDING`) for index index.

如果一个非0名称的缓冲区对象绑定到`GL_ARRAY_BUFFER`上时（参考[glBindBuffer](glBindBuffer.md)），调用`glVertexAttribPointer`时的`offset`/`Buffer`参数都是根据缓冲区对象里的数据来算的。被绑定的缓冲区对象(可以使用[glGet](glGet.md)并传入参数`GL_ARRAY_BUFFER_BINDING`获取)会被存为索引为index的顶点属性数组的客户机状态(`GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDING`)。

When a generic vertex attribute array is specified, size, type, normalized, stride, and pointer are saved as client-side state, in addition to the current vertex array buffer object binding.

当顶点属性被指定数据后，除了当前被绑定的缓冲区对象，size, type, normalized, stride, index/Buffer这些状态也会被存为客户机状态。

To enable and disable a generic vertex attribute array, call `glEnableVertexAttribArray` and `glDisableVertexAttribArray` with index. If enabled, the generic vertex attribute array is used when `glDrawArrays` or `glDrawElements` is called.

你需要通过[glEnableVertexAttribArray](glEnableVertexAttribArray.md)或[glDisableVertexAttribArray](glEnableVertexAttribArray.md)来激活/取消激活指定索引的属性数组。当属性数组被激活之后它才能够被`glDrawArrays` 或 `glDrawElements`所使用。

##Notes

每个顶点属性数组一开始都是没有激活的，此时他们的数据不能被`glDrawElements` 或 `glDrawArrays`读取。

`glVertexAttribPointer` 是在客户机实现改变数据的典型。

##Errors

`GL_INVALID_ENUM` - 当type不是可接受的类型时。

`GL_INVALID_VALUE` - 当index大于等于`GL_MAX_VERTEX_ATTRIBS`.

`GL_INVALID_VALUE` - 当size不为 1, 2, 3, 或4之一时。

`GL_INVALID_VALUE` - 当stride为负时。

##Associated Gets

[glGet](glGet.md) 配合 `GL_MAX_VERTEX_ATTRIBS`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index and `GL_VERTEX_ATTRIB_ARRAY_ENABLED`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_SIZE`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_TYPE`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_NORMALIZED`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_STRIDE`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDING`

[glGet](glGet.md) 配合 `GL_ARRAY_BUFFER_BINDING`

[glGetVertexAttribPointerv](glGetVertexAttribPointerv.md) 配合 index 与 `GL_VERTEX_ATTRIB_ARRAY_POINTER`

##See Also

[glBindAttribLocation](glBindAttribLocation.md), [glBindBuffer](glBindBuffer.md), [glDisableVertexAttribArray](glDisableVertexAttribArray.md), [glDrawArrays](glDrawArrays.md), [glDrawElements](glDrawElements.md), [glEnableVertexAttribArray](glEnableVertexAttribArray.md), [glVertexAttrib](glVertexAttrib.md)
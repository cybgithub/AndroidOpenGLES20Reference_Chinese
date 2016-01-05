##Name

`glVertexAttrib` — 修改属性变量的值。

##C Specification

    void glVertexAttrib1f(GLuint index, GLfloat v0);
    void glVertexAttrib2f(GLuint index, GLfloat v0, GLfloat v1);
    void glVertexAttrib3f(GLuint index, GLfloat v0, GLfloat v1, GLfloat v2);
    void glVertexAttrib4f(GLuint index, GLfloat v0, GLfloat v1, GLfloat v2, GLfloat v3);

##Android Specification

    void glVertexAttrib1f(int index, float x)
    void glVertexAttrib2f(int index, float x, float y)
    void glVertexAttrib3f(int index, float x, float y, float z)
    void glVertexAttrib4f(int index, float x, float y, float z, float w)

##C Parameters

- ***index*** Specifies the index of the generic vertex attribute to be modified.

- ***v0, v1, v2, v3*** Specifies the new values to be used for the specified vertex attribute.

##Android Parameters

- ***index*** 指定属性变量的索引。

- ***x, y, z, w*** 要写入属性变量的数值。

##C Specification

    void glVertexAttrib1fv(GLuint index, const GLfloat *v);
    void glVertexAttrib2fv(GLuint index, const GLfloat *v);
    void glVertexAttrib3fv(GLuint index, const GLfloat *v);
    void glVertexAttrib4fv(GLuint index, const GLfloat *v);
 
##Android Specification

    void glVertexAttrib1fv (int index, FloatBuffer values)
    void glVertexAttrib1fv (int index, float[] values, int offset)
    void glVertexAttrib2fv (int index, FloatBuffer values)
    void glVertexAttrib2fv (int index, float[] values, int offset)
    void glVertexAttrib3fv (int index, FloatBuffer values)
    void glVertexAttrib3fv (int index, float[] values, int offset)
    void glVertexAttrib4fv (int index, FloatBuffer values)
    void glVertexAttrib4fv (int index, float[] values, int offset)

##C Parameters

- ***index*** Specifies the index of the generic vertex attribute to be modified.

- ***v*** Specifies a pointer to an array of values to be used for the generic vertex attribute.

##Android Parameters

- ***index*** 指定属性变量的索引。

- ***value*** 存储修改的值的对象/数组。

- ***offset（可选）*** 从value的第几位开始应用到属性变量，value的长度必须大于属性变量维度+offset。

##Description

The `glVertexAttrib` family of entry points allows an application to pass generic vertex attributes in numbered locations.

`glVertexAttrib`系列函数允许应用程序修改指定数字索引的顶点属性变量。

Generic attributes are defined as four-component values that are organized into an array. The first entry of this array is numbered 0, and the size of the array is specified by the implementation-dependent symbolic constant `GL_MAX_VERTEX_ATTRIBS`. Individual elements of this array can be modified with a `glVertexAttrib` call that specifies the index of the element to be modified and a value for that element.

四元素的属性变量被放置在一个数组中。数组内第一个属性变量的位置为0，数组的规模不定，根据OpenGL版本对`GL_MAX_VERTEX_ATTRIBS`的实现而定。你可以通过`glVertexAttrib`来修改数组内指定的一个属性变量。

These commands can be used to specify one, two, three, or all four components of the generic vertex attribute specified by index. A 1 in the name of the command indicates that only one value is passed, and it will be used to modify the first component of the generic vertex attribute. The second and third components will be set to 0, and the fourth component will be set to 1. Similarly, a 2 in the name of the command indicates that values are provided for the first two components, the third component will be set to 0, and the fourth component will be set to 1. A 3 in the name of the command indicates that values are provided for the first three components and the fourth component will be set to 1, whereas a 4 in the name indicates that values are provided for all four components.

这些函数可以指定修改1、2、3或4个属性变量内的元素。函数内数字是“1”的只能传1个数，它只能修改变量内第一个元素。这时候第2、3个元素会被设为0，第4个元素为会设为1。类似的，函数内数字为“2”的只能改变属性变量的前两个元素，第3个元素会被设为0，第4个元素会被设为1。函数内数字为“3”的可以改变属性变量的前三个元素，第4个元素会被设为1。函数内数字为“4”的可以改变所有元素。

The letter f indicates that the arguments are of type float. When v is appended to the name, the commands can take a pointer to an array of floats.

函数内的"f"意思是参数为浮点数，如果后缀为"v"则传入数据参数可以为指针。

OpenGL ES Shading Language attribute variables are allowed to be of type mat2, mat3, or mat4. Attributes of these types may be loaded using the `glVertexAttrib` entry points. Matrices must be loaded into successive generic attribute slots in column major order, with one column of the matrix in each generic attribute slot.

OpenGL ES Shading Language(GLSL)的变量类型还可以是mat2, mat3或mat4。这些类型的变量也可以通过`glVertexAttrib`赋值，不过矩阵数值会被以竖向读取连续值。

A user-defined attribute variable declared in a vertex shader can be bound to a generic attribute index by calling glBindAttribLocation. This allows an application to use descriptive variable names in a vertex shader. A subsequent change to the specified generic vertex attribute will be immediately reflected as a change to the corresponding attribute variable in the vertex shader.

用户在顶点着色器中定义的变量可以通过`glBindAttribLocation`绑定索引。这允许用户使用可理解的方式来读取顶点属性变量。通过索引操作属性变量时，顶点着色器内的对应变量同样也会被改变。

The binding between a generic vertex attribute index and a user-defined attribute variable in a vertex shader is part of the state of a program object, but the current value of the generic vertex attribute is not. The value of each generic vertex attribute is part of current state and it is maintained even if a different program object is used.

顶点属性变量与索引是程序对象状态的一部分，但是属性变量的值不是。属性变量的值是当前状态机的一部分，就算另一个程序对象被安装，它也依然存在于这个状态机中。

An application may freely modify generic vertex attributes that are not bound to a named vertex shader attribute variable. These values are simply maintained as part of current state and will not be accessed by the vertex shader. If a generic vertex attribute bound to an attribute variable in a vertex shader is not updated while the vertex shader is executing, the vertex shader will repeatedly use the current value for the generic vertex attribute.

使用`glBindAttribLocation`可以指定没有绑定顶点属性变量的索引。这时传入的数值会作为当前状态的一部分，但是不会被顶点着色器所读取。如果着色器开始渲染之后没有更新顶点属性变量的数值，那么这个数值会被一直读取。

##Notes

It is possible for an application to bind more than one attribute name to the same generic vertex attribute index. This is referred to as aliasing, and it is allowed only if just one of the aliased attribute variables is active in the vertex shader, or if no path through the vertex shader consumes more than one of the attributes aliased to the same location. OpenGL implementations are not required to do error checking to detect aliasing, they are allowed to assume that aliasing will not occur, and they are allowed to employ optimizations that work only in the absence of aliasing.

用户可以将多个用户定义的属性变量绑定到一个索引上。这个操作成为“混淆”。当多个变量被混淆后，除非着色器中没有同时使用多个被混淆的变量，否则其中只有一个变量能够处于激活状态。你可以告知编译器与链接器当前没有被混淆的变量，这样可以提高性能，此时它们就只在非混淆的情况下工作。

##Errors

`GL_INVALID_VALUE` - 索引大于或等于 `GL_MAX_VERTEX_ATTRIBS`。

##Associated Gets

[glGet](glGet.md) 配合`GL_CURRENT_PROGRAM`

[glGetActiveAttrib](glGetActiveAttrib.md) 配合参数`program`与顶点属性变量索引。

[glGetAttribLocation](glGetAttribLocation.md) 配合参数`program`与顶点属性变量名。

[glGetVertexAttrib](glGetVertexAttrib.md) 配合`GL_CURRENT_VERTEX_ATTRIB`与顶点属性变量索引。

##See Also

[glBindAttribLocation](glBindAttribLocation.md), [glVertexAttribPointer](glVertexAttribPointer.md)



##Name

`glLinkProgram` — 链接程序对象中的程序。

##C Specification

    void glLinkProgram(GLuint program);
 
##Android Specification

    void glLinkProgram (int program)

##Parameters

- ***program*** 指定要链接的程序对象句柄。

##Description

`glLinkProgram` links the program object specified by program. A shader object of type `GL_VERTEX_SHADER` attached to program is used to create an executable that will run on the programmable vertex processor. A shader object of type `GL_FRAGMENT_SHADER` attached to program is used to create an executable that will run on the programmable fragment processor.

`glLinkProgram` 对程序对象的程序进行了链接。一个顶点着色器（类型为`GL_VERTEX_SHADER`的着色器）可以生成一个能够在可编程顶点处理器上运行的可执行程序，片段着色器可以生成一个能够再可编程片段处理器上运行的可执行程序。

The status of the link operation will be stored as part of the program object's state. This value will be set to `GL_TRUE` if the program object was linked without errors and is ready for use, and `GL_FALSE` otherwise. It can be queried by calling [glGetProgramiv](glGetProgramiv.md) with arguments program and `GL_LINK_STATUS`.

链接状态会被存在程序对象的状态中。如果程序对象正确链接并可以安装了，则它会被置为true，否则将会被置为false。可以通过[glGetProgramiv](glGetProgramiv.md)并配合`GL_LINK_STATUS`来查看程序对象的链接状态。

As a result of a successful link operation, all active user-defined uniform variables belonging to program will be initialized to 0, and each of the program object's active uniform variables will be assigned a location that can be queried by calling glGetUniformLocation. Also, any active user-defined attribute variables that have not been bound to a generic vertex attribute index will be bound to one at this time.

当程序被成功链接后，其中所有用户定义的一致变量均会被置为0，并且每个被激活的一致变量都会被赋予一个位置。这个位置可以通过[glGetUniformLocation](glGetUniformLocation.md)来获取到。同时，每个被激活的用户定义的属性变量都会被绑定到一个索引上（如果之前没有被绑定的话）。

Linking of a program object can fail for a number of reasons as specified in the OpenGL ES Shading Language Specification. The following lists some of the conditions that will cause a link error.

- A vertex shader and a fragment shader are not both present in the program object.
- The number of active attribute variables supported by the implementation has been exceeded.
- The storage limit for uniform variables has been exceeded.
- The number of active uniform variables supported by the implementation has been exceeded.
- The main function is missing for the vertex shader or the fragment shader.
- A varying variable actually used in the fragment shader is not declared in the same way (or is not declared at all) in the vertex shader.
- A reference to a function or variable name is unresolved.
- A shared global is declared with two different types or two different initial values.
- One or more of the attached shader objects has not been successfully compiled (via glCompileShader) or loaded with a pre-compiled shader binary (via glShaderBinary).
- Binding a generic attribute matrix caused some rows of the matrix to fall outside the allowed maximum of `GL_MAX_VERTEX_ATTRIBS`.
- Not enough contiguous vertex attribute slots could be found to bind attribute matrices.

有很多原因会导致链接程序对象失败（你可以在[glsl语言规范](https://www.opengl.org/documentation/glsl/)中查到），在这里简单列出几个情况：

- 这个程序对象中，顶点着色器与片段着色器中缺少了一种（必须两者都有）；
- 被激活的属性变量数量超过了总数限制（[glGet](glGet.md)配合`GL_MAX_VERTEX_ATTRIBS`查看这个限制）；
- 为一致变量分配的空间超过了限制；
- 被激活的一致变量数量超过了总数限制；（[glGet](glGet.md)配合`GL_MAX_VERTEX_UNIFORM_ATTRIBS`与`GL_MAX_FRAGMENT_UNIFORM_ATTRIBS`查看这个限制）
- 在顶点着色器或片段着色器中缺少了main函数；
- 顶点着色器、片段着色器中对使用到的varying变量声明不一致；
- 无法解析函数/变量名的引用；
- 共享的全局变量被几个地方初始化成不同的变量类型或不同的值；
- 有绑定的着色器对象没有被成功编译（通过[glCompileShader](glCompileShader.md)）并且不是被预编译的着色器二进制文件（通过[glShaderBinary](glShaderBinary.md)）加载的。
- 绑定了一个属性变量矩阵导致其中一些变量超过了属性变量限制（[glGet](glGet.md)配合`GL_MAX_VERTEX_ATTRIBS`查看这个限制）；
- 没有那么多连续的数形变量位置供数形变量矩阵绑定；

When a program object has been successfully linked, the program object can be made part of current state by calling glUseProgram. Whether or not the link operation was successful, the program object's information log will be overwritten. The information log can be retrieved by calling glGetProgramInfoLog.

当一个程序对象被成功链接之后，这个程序对象可以通过[glUseProgram](glUseProgram.md)安装到当前的渲染状态机上。无论是否链接成功，这个程序对象的日志都会被重写。你可以通过[glGetProgramInfoLog](glGetProgramInfoLog.md)来查看日志。

`glLinkProgram` will also install the generated executables as part of the current rendering state if the link operation was successful and the specified program object is already currently in use as a result of a previous call to glUseProgram. If the program object currently in use is relinked unsuccessfully, its link status will be set to GL_FALSE , but the executables and associated state will remain part of the current state until a subsequent call to glUseProgram removes it from use. After it is removed from use, it cannot be made part of current state until it has been successfully relinked.

`glLinkProgram`在链接成功也会在当前程序对象已经被安装上时直接将新生成的可执行文件安装到当前的渲染状态机。如果链接失败，则链接状态会被置为`false`，这时候调用`glUseProgram`会卸载已安装的可执行程序，在被卸载之前这些可执行程序仍然会保留在渲染状态机中。程序被卸载后，除非链接成功，否则无法再安装到当前的渲染状态机中。

The program object's information log is updated and the program is generated at the time of the link operation. After the link operation, applications are free to modify attached shader objects, compile attached shader objects, detach shader objects, delete shader objects, and attach additional shader objects. None of these operations affects the information log or the program that is part of the program object.

当被链接时，程序对象的日志、内部的程序会被更新。当程序对象被链接后，应用程序仍然可以随时修改绑定上去的着色器对象，编译被绑定的着色器对象，绑定新的着色器对象，解绑、删除着色器对象。不过这些都不会影响日志与内部的程序（只当重新链接时才生效）。

##Notes

If the link operation is unsuccessful, any information about a previous link operation on program is lost (i.e., a failed link does not restore the old state of program). Certain information can still be retrieved from program even after an unsuccessful link operation. See for instance glGetActiveAttrib and glGetActiveUniform.

如果链接失败，则之前一次的链接操作信息会丢失。不过程序的具体的信息仍然是保存着的，它们可以通过[glGetActiveAttrib](glGetActiveAttrib.md)，[glGetActiveUniform](glGetActiveUniform.md)获取。

##Errors

`GL_INVALID_VALUE` - 传入的program参数不是openGL所生成的。

`GL_INVALID_OPERATION` - 传入的program指向的不是一个程序对象。

##Associated Gets

[glGet](glGet.md) 配合 `GL_CURRENT_PROGRAM`

[glGetActiveAttrib](glGetActiveAttrib.md) - 配合一个合法的程序对象与被激活的属性变量索引。

[glGetActiveUniform](glGetActiveUniform.md) - 配合一个合法的程序对象与被激活的一致变量索引。

[glGetAttachedShaders](glGetAttachedShaders.md) - 配合一个合法的程序对象。

[glGetAttribLocation](glGetAttribLocation.md) - 配合一个合法的程序对象与属性变量名。

[glGetProgramiv](glGetProgramiv.md) - 配合一个合法的程序对象与要查询的参数。

[glGetProgramInfoLog](glGetProgramInfoLog.md) - 配合一个合法的程序对象。

[glGetUniform](glGetUniform.md) - 配合一个合法的程序对象与一致变量位置。

[glGetUniformLocation](glGetUniformLocation.md) - 配合一个合法的程序对象与一致变量名。

[glIsProgram](glIsProgram.md)

##See Also

[glAttachShader](glAttachShader.md), [glBindAttribLocation](glBindAttribLocation.md), [glCompileShader](glCompileShader.md), [glShaderBinary](glShaderBinary.md), [glCreateProgram](glCreateProgram.md), [glDeleteProgram](glDeleteProgram.md), [glDetachShader](glDetachShader.md), [glUniform](glUniform.md), [glUseProgram](glUseProgram.md), [glValidateProgram](glValidateProgram.md)


##Name

`glUseProgram` — 将程序对象的可执行程序安装到当前OPENGL渲染状态机中。

##C Specification

    void glUseProgram(GLuint program);
 
##Android Specification

    void glUseProgram (int program)

##Parameters

- ***program*** 指定程序对象的句柄。

##Description

`glUseProgram` installs the program object specified by program as part of current rendering state. Executables for each stage are created in a program object by successfully attaching shader objects to it with [glAttachShader](glAttachShader.md), successfully compiling the shader objects with [glCompileShader](glCompileShader.md), and successfully linking the program object with [glLinkProgram](glLinkProgram.md).

`glUseProgram`将指定程序对象的可执行程序安装到当前的渲染状态机中。可执行程序将会由以下步骤产生：

- 通过[glAttachShader](glAttachShader.md)绑定着色器对象到程序对象；
- 通过[glCompileShader](glCompileShader.md)编译着色器对象；
- 通过[glLinkProgram](glLinkProgram.md)链接程序对象。

A program object will contain executables that will run on the vertex and fragment processors if it contains one shader object of type `GL_VERTEX_SHADER` and one shader object of type `GL_FRAGMENT_SHADER` that have both been successfully compiled and linked.

当程序对象绑定了`GL_VERTEX_SHADER`与`GL_FRAGMENT_SHADER`类型的着色器对象并将他们成功编译、链接后，包含的可执行程序会运行在顶点、碎片处理器上。

While a program object is in use, applications are free to modify attached shader objects, compile attached shader objects, attach shader objects, and detach or delete shader objects. None of these operations will affect the executables that are part of the current state. However, relinking the program object that is currently in use will install the program object as part of the current rendering state if the link operation was successful (see [glLinkProgram](glLinkProgram.md) ). If the program object currently in use is relinked unsuccessfully, its link status will be set to `GL_FALSE`, but the executables and associated state will remain part of the current state until a subsequent call to `glUseProgram` removes it from use. After it is removed from use, it cannot be made part of current state until it has been successfully relinked.

当程序对象被安装后，应用程序仍然可以随时修改绑定上去的着色器对象，编译被绑定的着色器对象，绑定新的着色器对象，解绑、删除着色器对象。不过注意，这些操作不会修改当前渲染状态机内的可执行程序，但是调用[glLinkProgram](glLinkProgram.md)成功重新链接程序后就会将这些可执行程序添加到渲染状态机中。如果链接失败，则链接状态会被置为`false`，这时候调用`glUseProgram`会卸载已安装的可执行程序，在被卸载之前这些可执行程序仍然会保留在渲染状态机中。程序被卸载后，除非链接成功，否则无法再安装到当前的渲染状态机中。

If program is 0, then the current rendering state refers to an invalid program object, and the results of vertex and fragment shader execution due to any glDrawArrays or glDrawElements commands are undefined.

如果程序句柄为0，则当前渲染状态机使用了一个无效的程序对象。当调用[glDrawArrays](glDrawArrays.md) 或 [glDrawElements](glDrawElements.md)执行的顶点着色器、片段着色器操作都是无效的。

##Notes

Like texture objects and buffer objects, the name space for program objects may be shared across a set of contexts, as long as the server sides of the contexts share the same address space. If the name space is shared across contexts, any attached objects and the data associated with those attached objects are shared as well.

就像纹理对象、缓冲区对象一样，只要服务机有多个上下文共享了命名空间，则程序对象的命名空间有可能被多个上下文共享。如果命名空间被多个上下文共享，那么它们所绑定的对象、对象中的数据都会被共享。

Applications are responsible for providing the synchronization across API calls when objects are accessed from different execution threads.

应用程序（客户机）应该在多线程访问OPENGL ES的API时自己处理好线程之间的同步。

##Errors

`GL_INVALID_VALUE` - 传入的program不是0也不是opengl生成的值时。

`GL_INVALID_OPERATION` - 传入的program不指向一个程序对象时。

`GL_INVALID_OPERATION` - 该程序对象无法成为渲染状态机的一部分时。

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

[glAttachShader](glAttachShader.md), [glBindAttribLocation](glBindAttribLocation.md), [glCompileShader](glCompileShader.md), [glCreateProgram](glCreateProgram.md), [glDeleteProgram](glDeleteProgram.md), [glDetachShader](glDetachShader.md), [glLinkProgram](glLinkProgram.md), [glUniform](glUniform.md), [glValidateProgram](glValidateProgram.md), [glVertexAttrib](glVertexAttrib.md)



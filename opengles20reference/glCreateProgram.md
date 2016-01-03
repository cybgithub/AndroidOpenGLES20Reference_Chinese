##Name

`glCreateProgram` — 创建程序对象。

##C Specification

    GLuint glCreateProgram(void);
 
##Android Specification

    int glCreateProgram()

##Description

`glCreateProgram` creates an empty program object and returns a non-zero value by which it can be referenced. A program object is an object to which shader objects can be attached. This provides a mechanism to specify the shader objects that will be linked to create a program. It also provides a means for checking the compatibility of the shaders that will be used to create a program (for instance, checking the compatibility between a vertex shader and a fragment shader). When no longer needed as part of a program object, shader objects can be detached.

`glCreateProgram`创建了一个空的程序对象，并返回一个非零数作为指向它的句柄。程序对象可以绑定着色器对象。它实现了创建可供着色器绑定的程序对象的机制，同时也作为检查着色器对象之间兼容性的仲裁者（比如检查顶点着色器与片段着色器之间的兼容性）。当着色器对象不需要再在程序中使用时，它可以从程序对象上解绑。

One or more executables are created in a program object by successfully attaching shader objects to it with glAttachShader, successfully compiling the shader objects with glCompileShader, and successfully linking the program object with glLinkProgram. These executables are made part of current state when glUseProgram is called. Program objects can be deleted by calling glDeleteProgram. The memory associated with the program object will be deleted when it is no longer part of current rendering state for any context.

你可以通过[glAttachShader](glAttachShader.md)绑定着色器对象到程序对象上，通过[glCompileShader](glCompileShader.md)编译着色器对象，并调用[glLinkProgram](glLinkProgram.md)链接程序对象。这个操作会生成一些opengl可执行的二进制对象，通过[glUseProgram](glUseProgram.md)安装program中的可执行对象作为opengl渲染状态机的一部分。程序对象能够通过[glDeleteProgram](glDeleteProgram.md)删除。

##Notes

Like texture objects, the name space for program objects may be shared across a set of contexts, as long as the server sides of the contexts share the same address space. If the name space is shared across contexts, any attached objects and the data associated with those attached objects are shared as well.

像纹理对象一样，如果服务机的多个上下文之间共享一个命名空间，则程序对象的命名空间也可能被几个不同的上下文共享。如果命名空间被共享，则所有绑定的对象、绑定对象中的数据也会被共享。

Applications are responsible for providing the synchronization across API calls when objects are accessed from different execution threads.

应用程序（客户机）应该在多线程访问OPENGL ES的API时自己处理好线程之间的同步。

##Errors

This function returns 0 if an error occurs creating the program object.

创建程序对象失败时，返回的句柄为0。

##Associated Gets

[glGet](glGet.md) - 配合`GL_CURRENT_PROGRAM`

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

[glAttachShader](glAttachShader.md), [glBindAttribLocation](glBindAttribLocation.md), [glCreateShader](glCreateShader.md), [glDeleteProgram](glDeleteProgram.md), [glDetachShader](glDetachShader.md), [glLinkProgram](glLinkProgram.md), [glUniform](glUniform.md), [glUseProgram](glUseProgram.md), [glValidateProgram](glValidateProgram.md)



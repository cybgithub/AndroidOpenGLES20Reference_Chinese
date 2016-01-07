##Name

`glBindAttribLocation` — 为顶点属性变量绑定索引。

##C Specification

    void glBindAttribLocation(GLuint program, GLuint index, const GLchar *name);
 
##Android Specification

    void glBindAttribLocation (int program, int index, String name)

##Parameters

- ***program*** 包含顶点属性变量的程序对象句柄；

- ***index*** 指定要绑定的索引；

- ***name*** 指定要绑定的顶点属性变量名字。

##Description

`glBindAttribLocation` is used to associate a user-defined attribute variable in the program object specified by program with a generic vertex attribute index. The name of the user-defined attribute variable is passed as a null terminated string in name. The generic vertex attribute index to be bound to this variable is specified by index. When program is made part of current state, values provided via the generic vertex attribute index will modify the value of the user-defined attribute variable specified by name.

`glBindAttribLocation` 通常用来为用户在glsl程序中定义的属性变量绑定索引。在C语言中这个属性变量名必须以null结尾。顶点属性变量的索引是唯一的。当程序对象安装到当前的渲染状态机上后，通过索引修改顶点属性变量就能够修改对应名字的顶点属性变量。

If name refers to a matrix attribute variable, index refers to the first column of the matrix. Other matrix columns are then automatically bound to locations index+1 for a matrix of type mat2; index+1 and index+2 for a matrix of type mat3; and index+1, index+2, and index+3 for a matrix of type mat4.

如果这个顶点属性变量是一个矩阵变量，那么索引指向的是该矩形中的第一列。矩阵的其他列会自动向后绑定索引（如在2x2的矩阵中第二列是index+1；在3x3的矩阵中第二列是index+1，第三列是index+2；在4x4的矩阵中第二列是index+1，第三列是index+2，第四列是index+3）。

This command makes it possible for vertex shaders to use descriptive names for attribute variables rather than generic variables that are numbered from 0 to `GL_MAX_VERTEX_ATTRIBS` - 1. The values sent to each generic attribute index are part of current state, just like standard vertex attributes such as color, normal, and vertex position. If a different program object is made current by calling `glUseProgram`, the generic vertex attributes are tracked in such a way that the same values will be observed by attributes in the new program object that are also bound to index.

这个函数可以让用户以可辨识的方式来索引顶点属性变量，而不是通过机器定义的[0, `GL_MAX_VERTEX_ATTRIBS` - 1]之间的随机数字来索引。当你用`glBindAttribLocation`绑定属性变量后，如果使用[glUseProgram](glUseProgram.md)安装另一个程序对象到渲染状态机中时，与另一程序中相同的属性变量会被绑定到相同索引中。

Attribute variable name-to-generic attribute index bindings for a program object can be explicitly assigned at any time by calling `glBindAttribLocation`. Attribute bindings do not go into effect until `glLinkProgram` is called. After a program object has been linked successfully, the index values for generic attributes remain fixed (and their values can be queried) until the next link command occurs.

通过`glBindAttribLocation`进行的属性变量绑定可以在任何时候调用，它只会在[glLinkProgram](glLinkProgram.md)中生效。当程序被链接之后，被绑定的索引在下次链接之前不会再改变。

Applications are not allowed to bind any of the standard OpenGL vertex attributes using this command, as they are bound automatically when needed. Any attribute binding that occurs after the program object has been linked will not take effect until the next time the program object is linked.

但是需要注意，`glBindAttribLocation`不可以绑定OpenGL自有的属性变量，它们会在需要的时候自动绑定。在程序链接之后的任何绑定操作都只会在下次链接成功时生效。

##Notes

`glBindAttribLocation` can be called before any vertex shader objects are bound to the specified program object. It is also permissible to bind a generic attribute index to an attribute variable name that is never used in a vertex shader.

`glBindAttribLocation`可以在顶点着色器被绑定到程序对象之前调用，它可以作用于顶点着色器内的任何用户定义的属性变量。

If name was bound previously, that information is lost. Thus you cannot bind one user-defined attribute variable to multiple indices, but you can bind multiple user-defined attribute variables to the same index.

如果准备绑定的属性变量已经被绑定过了，那么之前的绑定信息会丢失。所以你无法将用户定义的属性变量绑定到多个索引上，不过你可以将多个用户定义的属性变量绑定到一个索引上。

Applications are allowed to bind more than one user-defined attribute variable to the same generic vertex attribute index. This is called aliasing, and it is allowed only if just one of the aliased attributes is active in the executable program, or if no path through the shader consumes more than one attribute of a set of attributes aliased to the same location. The compiler and linker are allowed to assume that no aliasing is done and are free to employ optimizations that work only in the absence of aliasing. OpenGL implementations are not required to do error checking to detect aliasing. Because there is no way to bind standard attributes, it is not possible to alias generic attributes with conventional ones (except for generic attribute 0).

用户可以将多个用户定义的属性变量绑定到一个索引上。这个操作成为“混淆”。当多个变量被混淆后，除非着色器中没有同时使用多个被混淆的变量，否则其中只有一个变量能够处于激活状态。你可以告知编译器与链接器当前没有被混淆的变量，这样可以提高性能，此时它们就只在非混淆的情况下工作。OpenGL中没有检查混淆的机制，因为没有方法去绑定自有变量，并且无法将自有变量与用户定义的变量进行混淆。

Active attributes that are not explicitly bound will be bound by the linker when `glLinkProgram` is called. The locations assigned can be queried by calling `glGetAttribLocation`.

如果被激活的属性变量没有被手动绑定，则在调用[glLinkProgram](glLinkProgram.md)时链接器会帮它绑定。绑定的索引可以通过[glGetAttribLocation](glGetAttribLocation.md)查找。

OpenGL copies the name string when `glBindAttribLocation` is called, so an application may free its copy of the name string immediately after the function returns.

OpenGL会在`glBindAttribLocation`时保存变量名，所以应用程序在调用这个函数之后就可以释放掉存储变量名的这部分空间。

##Errors

`GL_INVALID_VALUE` - index大于或等于`GL_MAX_VERTEX_ATTRIBS`。

`GL_INVALID_OPERATION` - 被绑定的属性变量前缀是"_gl"时（这是OPENGL的保留字，说明该变量为OPENGL的自有变量）。

`GL_INVALID_VALUE` - 传入的`program`不是OPENGL生成的数字。

`GL_INVALID_OPERATION` - 传入的`program`指向的不是程序对象。

##Associated Gets

[glGet](glGet.md) 配合`GL_MAX_VERTEX_ATTRIBS`

[glGetActiveAttrib](glGetActiveAttrib.md) 配合参数`program`

[glGetAttribLocation](glGetAttribLocation.md) 配合参数`program`与`name`

[glIsProgram](glIsProgram.md)

##See Also

[glDisableVertexAttribArray](glDisableVertexAttribArray.md), [glEnableVertexAttribArray](glEnableVertexAttribArray.md), [glUseProgram](glUseProgram.md), [glVertexAttrib](glVertexAttrib.md), [glVertexAttribPointer](glVertexAttribPointer.md)



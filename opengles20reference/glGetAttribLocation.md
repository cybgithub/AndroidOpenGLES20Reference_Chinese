##Name

`glGetAttribLocation` — 获取顶点属性变量的位置。

##C Specification

    GLint glGetAttribLocation(GLuint program, const GLchar *name);

##Android Specification

    int glGetAttribLocation (int program, String name)

##Parameters

- ***program*** 含有顶点属性变量的程序对象句柄；

- ***name*** 要查看的顶点属性变量名；

##Description

`glGetAttribLocation` queries the previously linked program object specified by program for the attribute variable specified by name and returns the index of the generic vertex attribute that is bound to that attribute variable. If name is a matrix attribute variable, the index of the first column of the matrix is returned. If the named attribute variable is not an active attribute in the specified program object or if name starts with the reserved prefix "gl_", a value of -1 is returned.

`glGetAttribLocation` 可以获取**已链接的程序对象**中的顶点属性变量的绑定位置。如果这是一个矩阵属性变量，则它会返回矩阵第一行变量的位置。如果指定的变量名在程序对象内没有被激活或者它以OPEN GL的保留字"gl_"开头，则会返回-1。

The association between an attribute variable name and a generic attribute index can be specified at any time by calling `glBindAttribLocation`. Attribute bindings do not go into effect until `glLinkProgram` is called. After a program object has been linked successfully, the index values for attribute variables remain fixed until the next link command occurs. The attribute values can only be queried after a link if the link was successful. `glGetAttribLocation` returns the binding that actually went into effect the last time `glLinkProgram` was called for the specified program object. Attribute bindings that have been specified since the last link operation are not returned by `glGetAttribLocation`.

你可以随时通过[glBindAttribLocation](glBindAttribLocation.md)为顶点属性变量绑定索引位置，但是绑定只有在程序对象调用[glLinkProgram](glLinkProgram.md)并成功链接时才生效。绑定生效后的索引位置直到下次链接成功之前都不会改变。顶点属性变量只有在程序正确链接后才能被查询，[glGetAttribLocation](glGetAttribLocation.md)获取的也是最近一次成功链接的程序对象中的变量位置，在最近一次成功链接之后的索引绑定不会生效。

##Errors

`GL_INVALID_VALUE` - program不是Open GL 生成的数字时。（译者注：原文此处是`GL_INVALID_OPERATION`，实际上是`GL_INVALID_VALUE`）

`GL_INVALID_OPERATION` - program指向的不是程序对象时。

`GL_INVALID_OPERATION` - program指向的程序对象没有被链接时。

##Associated Gets

[glGetActiveAttrib](glGetActiveAttrib.md) 配合program与顶点属性变量的位置。

[glIsProgram](glIsProgram.md)

##See Also

[glBindAttribLocation](glBindAttribLocation.md), [glLinkProgram](glLinkProgram.md), [glVertexAttrib](glVertexAttrib.md), [glVertexAttribPointer](glVertexAttribPointer.md)

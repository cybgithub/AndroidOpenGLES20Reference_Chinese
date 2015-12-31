##Name

`glGetUniformLocation` — 获取一致变量的位置。

##C Specification

    GLint glGetUniformLocation(GLuint program, const GLchar *name);
 
##Android Specification

    int glGetUniformLocation (int program, String name)

##Parameters

- ***program*** 指定程序对象句柄。

- ***name*** 一致变量的名字。

##Description

`glGetUniformLocation` returns an integer that represents the location of a specific uniform variable within a program object. name must be a null terminated string that contains no white space. name must be an active uniform variable name in program that is not a structure, an array of structures, or a subcomponent of a vector or a matrix. This function returns -1 if name does not correspond to an active uniform variable in program or if name starts with the reserved prefix "gl_".

`glGetUniformLocation`返回了在指定程序中指定名字的一致变量位置。一致变量的名字中不可以有空格。它在这个程序对象中的类型不可以是structure（或structure数组）、vector或matrix的子元素。当你查询的一致变量不可用或者它不是由"gl_"开头的话会返回-1。

Uniform variables that are structures or arrays of structures may be queried by calling `glGetUniformLocation` for each field within the structure. The array element operator "[]" and the structure field operator "." may be used in name in order to select elements within an array or fields within a structure. The result of using these operators is not allowed to be another structure, an array of structures, or a subcomponent of a vector or a matrix. Except if the last part of name indicates a uniform variable array, the location of the first element of an array can be retrieved by using the name of the array, or by using the name appended by "[0]".

类型为structure（或structure数组）的一致变量可以通过`glGetUniformLocation`查询其中每一个域的变量位置。你可以使用数组操作符"[]"来指定数组中的structure，使用域操作符"."指定一个structrue中的一致变量。使用这些操作符获取的一致变量位置，无法用于其他structrue（或structure数组）、vector或matrix的子元素。当获取的是数组第一个元素时，你可以通过数组名获取它的位置，也可以通过数组名后面加上"[0]"来获取。

The actual locations assigned to uniform variables are not known until the program object is linked successfully. After linking has occurred, the command `glGetUniformLocation` can be used to obtain the location of a uniform variable. This location value can then be passed to `glUniform` to set the value of the uniform variable or to `glGetUniform` in order to query the current value of the uniform variable. After a program object has been linked successfully, the index values for uniform variables remain fixed until the next link command occurs. Uniform variable locations and values can only be queried after a link if the link was successful.

在程序对象被链接上之前，一致对象的位置都是未知的。在链接成功之后，你才能使用`glGetUniformLocation`来获取一致对象的位置。这个位置可以用于`glUniform`系列函数指定一致变量的数值，也可以用于`glGetUniform`来获取一致变量的状态。当程序被链接上之后，每个一致变量的位置都是固定的，直到下次链接上之后才会被改变。

##Errors

`GL_INVALID_VALUE` - program不是被opengl生成的句柄。

`GL_INVALID_OPERATION` - program指向的对象不是一个程序对象。

`GL_INVALID_OPERATION` - program指向的程序对象没有被链接。

##Associated Gets

[glGetActiveUniform](glGetActiveUniform.md) 配合程序句柄与一致变量的索引。

[glGetProgramiv](glGetProgramiv.md) 配合程序句柄与 `GL_ACTIVE_UNIFORMS` 或 `GL_ACTIVE_UNIFORM_MAX_LENGTH`

[glGetUniform](glGetUniform.md) 配合程序对象句柄与一致变量的位置。

[glIsProgram](glIsProgram.md)

##See Also

[glLinkProgram](glLinkProgram.md), [glUniform](glUniform.md)



##Name

`glIsProgram` — 查看指定句柄是否是程序对象

##C Specification

    GLboolean glIsProgram(GLuint program);
 
##Android Specification

    boolean glIsProgram (int program);

##Parameters

- ***program*** 传入要检查的句柄。

##Description

`glIsProgram` returns `GL_TRUE` if program is the name of a program object previously created with [glCreateProgram](glCreateProgram.md) and not yet deleted with [glDeleteProgram](glDeleteProgram.md). If program is zero or a non-zero value that is not the name of a program object, or if an error occurs, `glIsProgram` returns GL_FALSE.

`glIsProgram`会在传入句柄指向程序对象的时候返回true。这个程序对象必须由[glCreateProgram](glCreateProgram.md)创建，并且仍未被[glDeleteProgram](glDeleteProgram.md)删除。如果程序对象为0或者为负数，或者指向的不是程序对象，或者有异常产生，`glIsProgram`都会返回负数。

##Notes

No error is generated if program is not a valid program object name.

当句柄指向程序对象的时候不会产生异常。

A program object marked for deletion with glDeleteProgram but still in use as part of current rendering state is still considered a program object and `glIsProgram` will return `GL_TRUE`.

程序对象被[glDeleteProgram](glDeleteProgram.md)删除但是仍然存在于当前的渲染状态中时它也会被认为是一个合法的程序对象，并且`glIsProgram`会返回true。

##See Also

[glCreateProgram](glCreateProgram.md), [glDeleteProgram](glDeleteProgram.md), [glUseProgram](glUseProgram.md)



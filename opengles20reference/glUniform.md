##Name

glUniform — 指定当前程序中指定一致变量的值。它一共有三种类型：`glUniform{1|2|3|4}{f|i}`，`glUniform{1|2|3|4}{f|i}v`，`glUniformMatrix{2|3|4}fv`。

##C Specification

    void glUniform1f(GLint location, GLfloat v0);
    void glUniform2f(GLint location, GLfloat v0, GLfloat v1);
    void glUniform3f(GLint location, GLfloat v0, GLfloat v1, GLfloat v2);
    void glUniform4f(GLint location, GLfloat v0, GLfloat v1, GLfloat v2, GLfloat v3);
    void glUniform1i(GLint location, GLint v0);
    void glUniform2i(GLint location, GLint v0, GLint v1);
    void glUniform3i(GLint location, GLint v0, GLint v1, GLint v2);
    void glUniform4i(GLint location, GLint v0, GLint v1, GLint v2, GLint v3);

##Android Specification

    void glUniform1f (int location, float x)
    void glUniform1i (int location, int x)
    void glUniform2f (int location, float x, float y)
    void glUniform2i (int location, int x, int y)
    void glUniform3f (int location, float x, float y, float z)
    void glUniform3i (int location, int x, int y, int z)
    void glUniform4f (int location, float x, float y, float z, float w)
    void glUniform4i (int location, int x, int y, int z, int w)

##Parameters

- ***location*** 一致变量的位置。
- ***x, y, z, w*** 改变的目标值。

##C Specification

    void glUniform1fv(GLint location, GLsizei count, const GLfloat *value);
    void glUniform2fv(GLint location, GLsizei count, const GLfloat *value);
    void glUniform3fv(GLint location, GLsizei count, const GLfloat *value);
    void glUniform4fv(GLint location, GLsizei count, const GLfloat *value);
    void glUniform1iv(GLint location, GLsizei count, const GLint *value);
    void glUniform2iv(GLint location, GLsizei count, const GLint *value);
    void glUniform3iv(GLint location, GLsizei count, const GLint *value);
    void glUniform4iv(GLint location, GLsizei count, const GLint *value);

##Android Specification

    void glUniform1fv (int location, int count, FloatBuffer v)
    void glUniform1iv (int location, int count, IntBuffer v)
    void glUniform2fv (int location, int count, FloatBuffer v)
    void glUniform2iv (int location, int count, IntBuffer v)
    void glUniform3fv (int location, int count, FloatBuffer v)
    void glUniform3iv (int location, int count, IntBuffer v)
    void glUniform4fv (int location, int count, FloatBuffer v)
    void glUniform4iv (int location, int count, IntBuffer v)

    void glUniform1fv (int location, int count, float[] v, int offset)
    void glUniform1iv (int location, int count, int[] v, int offset)
    void glUniform2fv (int location, int count, float[] v, int offset)    
    void glUniform2iv (int location, int count, int[] v, int offset)
    void glUniform3fv (int location, int count, float[] v, int offset)
    void glUniform3iv (int location, int count, int[] v, int offset)
    void glUniform4fv (int location, int count, float[] v, int offset)
    void glUniform4iv (int location, int count, int[] v, int offset)

##Parameters

- ***location*** 一致变量的位置。
- ***count*** 需要改变的变量数，如果要修改的一致变量不是一个数组(`glUniform1*`)时，它必须是1。
- ***v*** 存储改变目标值的数组。
- ***offset***（可选） 数组v的第一位相对一致变量数组第一位的偏移量。

##C Specification

    void glUniformMatrix2fv(GLint location, GLsizei count, GLboolean transpose, const GLfloat *value);
    void glUniformMatrix3fv(GLint location, GLsizei count, GLboolean transpose, const GLfloat *value);
    void glUniformMatrix4fv(GLint location, GLsizei count, GLboolean transpose, const GLfloat *value);

##Android Specification

    void glUniformMatrix2fv (int location, int count, boolean transpose, FloatBuffer value)
    void glUniformMatrix2fv (int location, int count, boolean transpose, float[] value, int offset)
    void glUniformMatrix3fv (int location, int count, boolean transpose, float[] value, int offset)
    void glUniformMatrix3fv (int location, int count, boolean transpose, FloatBuffer value)
    void glUniformMatrix4fv (int location, int count, boolean transpose, float[] value, int offset)
    void glUniformMatrix4fv (int location, int count, boolean transpose, FloatBuffer value)

##Parameters

- ***location*** 一致变量矩阵的位置。

- ***count*** 要修改的矩阵数量。如果一致变量不是矩阵列，那么它必须是1；如果是矩阵列，则可以是大于等于1的数字。

- ***transpose*** 是否传入数据时对矩阵进行转置（若为true，则相当于每个矩阵中纵向放入数据）。在OPENGL ES 2.0中，它必须是`false`。

- ***value*** 要写入一致变量的目标值。

##Description

`glUniform` modifies the value of a uniform variable or a uniform variable array. The location of the uniform variable to be modified is specified by location, which should be a value returned by `glGetUniformLocation`. `glUniform` operates on the program object that was made part of current state by calling `glUseProgram`.

`glUniform` 可以修改一致变量或一致变量数组。要修改的一致变量通过location来判定（可以通过`glGetUniformLocation`获取）。通过`glUseProgram`链接程序对象，才可以调用`glUniform`来修改这个程序对象中的一致变量。

The commands `glUniform{1|2|3|4}{f|i}` are used to change the value of the uniform variable specified by location using the values passed as arguments. The number specified in the command should match the number of components in the data type of the specified uniform variable (e.g., 1 for float, int, bool; 2 for vec2, ivec2, bvec2, etc.). The suffix f indicates that floating-point values are being passed; the suffix i indicates that integer values are being passed, and this type should also match the data type of the specified uniform variable. The i variants of this function should be used to provide values for uniform variables defined as int, ivec2, ivec3, ivec4, or arrays of these. The f variants should be used to provide values for uniform variables of type float, vec2, vec3, vec4, or arrays of these. Either the i or the f variants may be used to provide values for uniform variables of type bool, bvec2, bvec3, bvec4, or arrays of these. The uniform variable will be set to false if the input value is 0 or 0.0f, and it will be set to true otherwise.

函数`glUniform{1|2|3|4}{f|i}`直接要写入的值作为参数传入指定一致变量。函数中的数字必须与一致变量的数据维度相对应（比如：1 对应float, int, bool; 2对应vec2, ivec2, bvec2 诸如此类）。后缀f说明这写入的是浮点数，后缀i说明传入的是整型数，传入数据必须与一致变量的数据类型一致。int, ivec2, ivec3, ivec4（或者这些类型的数组）对应整型数，float, vec2, vec3, vec4（或者这些类型的数组）对应浮点数，同时整型数、浮点数都可以用在bool, bvec2, bvec3, bvec4（或者这些类型的数组）。

All active uniform variables defined in a program object are initialized to 0 when the program object is linked successfully. They retain the values assigned to them by a call to `glUniform` until the next successful link operation occurs on the program object, when they are once again initialized to 0.

被激活的一致变量在成功连接上程序对象之后的初始值为0。它们将会一致保持`glUniform`设置的值，直到下一次被连接上程序对象（这时候被重新初始化为0）。

The commands `glUniform{1|2|3|4}{f|i}v` can be used to modify a single uniform variable or a uniform variable array. These commands pass a count and a pointer to the values to be loaded into a uniform variable or a uniform variable array. A count of 1 should be used if modifying the value of a single uniform variable, and a count of 1 or greater can be used to modify an entire array or part of an array. When loading n elements starting at an arbitrary position m in a uniform variable array, elements m + n - 1 in the array will be replaced with the new values. If m + n - 1 is larger than the size of the uniform variable array, values for all array elements beyond the end of the array will be ignored. The number specified in the name of the command indicates the number of components for each element in value, and it should match the number of components in the data type of the specified uniform variable (e.g., 1 for float, int, bool; 2 for vec2, ivec2, bvec2, etc.). The data type specified in the name of the command must match the data type for the specified uniform variable as described previously for `glUniform{1|2|3|4}{f|i}`.

函数`glUniform{1|2|3|4}{f|i}v`可以修改指定一致变量或者一致变量数组的值。它传入count参数标识着要改变的值的数量，v参数存储着要写入的值。当指定一致变量不是数组时，count必须是1。当offset=m时，从数组第m个元素开始，写入n个元素，即m ~ m + n - 1的元素会被改变。如果m + n - 1大于数组长度，则超出部分的数据会被无视。函数名中的数字指定了一致变量的数据维度（如 1 对应 float, int, bool；2对应vec2, ivec2, bvec2， 诸如此类）。像`glUniform{1|2|3|4}{f|i}`一样，函数中传入的数据类型必须与一致变量的数据类型对应。

For uniform variable arrays, each element of the array is considered to be of the type indicated in the name of the command (e.g., `glUniform3f` or `glUniform3fv` can be used to load a uniform variable array of type vec3). The number of elements of the uniform variable array to be modified is specified by count.

对于一致变量数组，数组中的每个元素的维度都必须与函数名中的数字对应（如`glUniform3f` 或 `glUniform3fv` 必须对应vec3, ivec3, bvec3类型组成的数组）。数组中要修改的元素数量由count指定。

The commands `glUniformMatrix{2|3|4}fv` are used to modify a matrix or an array of matrices. The numbers in the command name are interpreted as the dimensionality of the matrix. The number 2 indicates a 2 × 2 matrix (i.e., 4 values), the number 3 indicates a 3 × 3 matrix (i.e., 9 values), and the number 4 indicates a 4 × 4 matrix (i.e., 16 values). Each matrix is assumed to be supplied in column major order. The count argument indicates the number of matrices to be passed. A count of 1 should be used if modifying the value of a single matrix, and a count greater than 1 can be used to modify an array of matrices.

`glUniformMatrix{2|3|4}fv` 用来修改矩阵或者矩阵数组。函数中的数字是矩阵的维度（2对应2x2的4元素矩阵，3对应3x3的9元素矩阵，4对应4x4的16元素矩阵）。每个矩阵都默认是横向读取的矩阵。count指定了要修改的矩阵数量，为1说明只修改一个矩阵，大于1说明要矩阵数组中的多个矩阵。

##Errors

`GL_INVALID_OPERATION` - 当前没有程序对象被链接。

`GL_INVALID_OPERATION` - 一致变量的维度与函数名中指定的维度不同。

`GL_INVALID_OPERATION` - 一致变量的数据类型与传入数据类型不同（如对类型为float, vec2, vec3, vec4的一致变量传入了整型数据）。

`GL_INVALID_OPERATION` - location不是-1且在当前程序中不存在此location的一致变量时。

`GL_INVALID_VALUE` - count为负数。

`GL_INVALID_VALUE` - transpose不是false。

`GL_INVALID_OPERATION` - 对非数组的一致变量传入了count>1。

`GL_INVALID_OPERATION` - 对sampler赋值时使用了除`glUniform1i`或`glUniform1iv`之外的函数。

##Associated Gets

[glGet](glGet.md) 配合 `GL_CURRENT_PROGRAM`

[glGetActiveUniform](glGetActiveUniform.md) 配合程序对象句柄与一致变量的索引。

[glGetUniform](glGetUniform.md) 配合程序对象句柄与一致变量的位置。

[glGetUniformLocation](glGetUniformLocation.md) 配合程序对象句柄与一致变量的名字。

##See Also

[glLinkProgram](glLinkProgram.md), [glUseProgram](glUseProgram.md)

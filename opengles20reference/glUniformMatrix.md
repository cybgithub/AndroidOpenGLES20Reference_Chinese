##Name

`glUniformMatrix` — specify the value of a uniform variable for the current program object

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

- ***location*** Specifies the location of the uniform value to be modified.

- ***count*** Specifies the number of matrices that are to be modified. This should be 1 if the targeted uniform variable is not an array of matrices, and 1 or more if it is an array of matrices.

- ***transpose*** Specifies whether to transpose the matrix as the values are loaded into the uniform variable. Must be GL_FALSE.

- ***value*** Specifies a pointer to an array of count values that will be used to update the specified uniform variable.

##Description

The commands `glUniformMatrix{2|3|4}fv` are used to modify a matrix or an array of matrices. The numbers in the command name are interpreted as the dimensionality of the matrix. The number 2 indicates a 2 × 2 matrix (i.e., 4 values), the number 3 indicates a 3 × 3 matrix (i.e., 9 values), and the number 4 indicates a 4 × 4 matrix (i.e., 16 values). Each matrix is assumed to be supplied in column major order. The count argument indicates the number of matrices to be passed. A count of 1 should be used if modifying the value of a single matrix, and a count greater than 1 can be used to modify an array of matrices.

##Errors

`GL_INVALID_OPERATION` is generated if there is no current program object.

`GL_INVALID_OPERATION` is generated if the size of the uniform variable declared in the shader does not match the size indicated by the glUniform command.

`GL_INVALID_OPERATION` is generated if one of the integer variants of this function is used to load a uniform variable of type float, vec2, vec3, vec4, or an array of these, or if one of the floating-point variants of this function is used to load a uniform variable of type int, ivec2, ivec3, or ivec4, or an array of these.

`GL_INVALID_OPERATION` is generated if location is an invalid uniform location for the current program object and location is not equal to -1.

`GL_INVALID_VALUE` is generated if count is less than 0.

`GL_INVALID_OPERATION` is generated if count is greater than 1 and the indicated uniform variable is not an array variable.

`GL_INVALID_OPERATION` is generated if a sampler is loaded using a command other than glUniform1i and glUniform1iv.

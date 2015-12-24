void glVertexAttribPointer (int indx, int size, int type, boolean normalized, int stride, Buffer ptr)
void glVertexAttribPointer (int indx, int size, int type, boolean normalized, int stride, int offset)

##Name

glVertexAttribPointer — define an array of generic vertex attribute data

##C Specification

    void glVertexAttribPointer( GLuint index, GLint size, GLenum type, GLboolean normalized, GLsizei stride, const GLvoid * pointer);
 
##Android Specification

    void glVertexAttribPointer (int indx, int size, int type, boolean normalized, int stride, Buffer ptr)


    void glVertexAttribPointer (int indx, int size, int type, boolean normalized, int stride, int offset)

##Parameters

- ***index*** Specifies the index of the generic vertex attribute to be modified.
- ***size*** Specifies the number of components per generic vertex attribute. Must be 1, 2, 3, or 4. The initial value is 4.
- ***type*** Specifies the data type of each component in the array. Symbolic constants GL_BYTE, GL_UNSIGNED_BYTE, GL_SHORT, GL_UNSIGNED_SHORT, GL_FIXED, or GL_FLOAT are accepted. The initial value is GL_FLOAT.
- ***normalized*** Specifies whether fixed-point data values should be normalized (GL_TRUE) or converted directly as fixed-point values (GL_FALSE) when they are accessed.
-  ****stride*** Specifies the byte offset between consecutive generic vertex attributes. If stride is 0, the generic vertex attributes are understood to be tightly packed in the array. The initial value is 0.
- ***pointer*** Specifies a pointer to the first component of the first generic vertex attribute in the array. The initial value is 0.

##Description

glVertexAttribPointer specifies the location and data format of the array of generic vertex attributes at index index to use when rendering. size specifies the number of components per attribute and must be 1, 2, 3, or 4. type specifies the data type of each component, and stride specifies the byte stride from one attribute to the next, allowing vertices and attributes to be packed into a single array or stored in separate arrays. If set to GL_TRUE, normalized indicates that values stored in an integer format are to be mapped to the range [-1,1] (for signed values) or [0,1] (for unsigned values) when they are accessed and converted to floating point. Otherwise, values will be converted to floats directly without normalization.

If a non-zero named buffer object is bound to the GL_ARRAY_BUFFER target (see glBindBuffer) while a generic vertex attribute array is specified, pointer is treated as a byte offset into the buffer object's data store. Also, the buffer object binding (GL_ARRAY_BUFFER_BINDING) is saved as generic vertex attribute array client-side state (GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDING) for index index.

When a generic vertex attribute array is specified, size, type, normalized, stride, and pointer are saved as client-side state, in addition to the current vertex array buffer object binding.

To enable and disable a generic vertex attribute array, call glEnableVertexAttribArray and glDisableVertexAttribArray with index. If enabled, the generic vertex attribute array is used when glDrawArrays or glDrawElements is called.

##Notes

Each generic vertex attribute array is initially disabled and isn't accessed when glDrawElements or glDrawArrays is called.

glVertexAttribPointer is typically implemented on the client side.

##Errors

GL_INVALID_ENUM is generated if type is not an accepted value.

GL_INVALID_VALUE is generated if index is greater than or equal to GL_MAX_VERTEX_ATTRIBS.

GL_INVALID_VALUE is generated if size is not 1, 2, 3, or 4.

GL_INVALID_VALUE is generated if stride is negative.

##Associated Gets

glGet with argument GL_MAX_VERTEX_ATTRIBS

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_ENABLED

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_SIZE

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_TYPE

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_NORMALIZED

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_STRIDE

glGetVertexAttrib with arguments index and GL_VERTEX_ATTRIB_ARRAY_BUFFER_BINDING

glGet with argument GL_ARRAY_BUFFER_BINDING

glGetVertexAttribPointerv with arguments index and GL_VERTEX_ATTRIB_ARRAY_POINTER

##See Also

glBindAttribLocation, glBindBuffer, glDisableVertexAttribArray, glDrawArrays, glDrawElements, glEnableVertexAttribArray, glVertexAttrib
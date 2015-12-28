##Name

`glEnableVertexAttribArray` - 激活一个顶点属性数组。

`glDisableVertexAttribArray` - 取消一个顶点属性数组的激活状态。

##C Specification

    void glEnableVertexAttribArray(GLuint index);
 
    void glDisableVertexAttribArray(GLuint index);
 
##Android Specification

    void glEnableVertexAttribArray (int index)

    void glDisableVertexAttribArray (int index)

##Parameters

- ***index*** 指定顶点属性数组的索引。

##Description

`glEnableVertexAttribArray` enables the generic vertex attribute array specified by index. `glDisableVertexAttribArray` disables the generic vertex attribute array specified by index. By default, all client-side capabilities are disabled, including all generic vertex attribute arrays. If enabled, the values in the generic vertex attribute array will be accessed and used for rendering when calls are made to vertex array commands such as `glDrawArrays` or `glDrawElements`.

`glEnableVertexAttribArray` 可以激活指定索引的顶点属性数组。 `glDisableVertexAttribArray` 可以取消激活指定索引的顶点属性数组。所有应用程序(客户机)上的容器一开始都是没有被激活的，包括顶点属性数组。当它们被激活之后才可以被`glDrawArrays`或`glDrawElements`这类函数所读取、渲染。

##Errors

`GL_INVALID_VALUE` - 当索引大于等于`GL_MAX_VERTEX_ATTRIBS`时触发

##Associated Gets

[glGet](glGet.md) 配合`GL_MAX_VERTEX_ATTRIBS`

[glGetVertexAttrib](glGetVertexAttrib.md) 配合index与`GL_VERTEX_ATTRIB_ARRAY_ENABLED` 

[glGetVertexAttribPointerv](glGetVertexAttribPointerv.md) 配合index与`GL_VERTEX_ATTRIB_ARRAY_POINTER`

##See Also

[glBindAttribLocation](glBindAttribLocation.md), [glDrawArrays](glDrawArrays.md), [glDrawElements](glDrawElements.md), [glVertexAttrib](glVertexAttrib.md), [glVertexAttribPointer](glVertexAttribPointer.md)

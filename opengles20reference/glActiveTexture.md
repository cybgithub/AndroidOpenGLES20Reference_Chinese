## Name

***glActiveTexture*** — select active texture unit

选择一个活动的（Active）纹理（Texture）单元。

## C Specification

`void glActiveTexture(GLenum texture);`

## Android Specification

`void glActiveTexture (int texture)`

## Parameters

* ***C texture***  Specifies which texture unit to make active. The number of texture units is implementation dependent, but must be at least 8. texture must be one of GL_TEXTUREi, where i ranges from 0 to (GL_MAX_COMBINED_TEXTURE_IMAGE_UNITS - 1). The initial value is GL_TEXTURE0.
* ***Android Texture*** 指定要激活的纹理单元。系统中纹理单元（Texture Unit）的数量由具体的 OpenGL ES  的实现而决定，但是必须保证其不少于8个。**texture**的值为`GL_TEXTURE0`到`GL_TEXTURE31`中的一个，其默认值为`GL_TEXTURE0`。

## Description

`glActiveTexture`  selects which texture unit subsequent texture state calls will affect. The number of texture units an implementation supports is implementation dependent, but must be at least 8.

`glActiveTexture`  确定了后续的纹理状态（Texture State）改变时将会影响到的纹理单元（Texture Unit）。系统中纹理单元（Texture Unit）的数量由具体的 OpenGL ES 的实现而决定，但是不会少于8个。Texture Unit 的数量，从 OpenGL ES 1.0版时的至少一个，到 OpenGL ES 1.1时变为至少两个，一直到 OpenGL ES 2.0版本时的至少八个。

## Errors

GL_INVALID_ENUM is generated if texture is not one of GL_TEXTUREi , where i ranges from 0 to (GL_MAX_COMBINED_TEXTURE_IMAGE_UNITS - 1).

如果传入的`texture`值不在`GL_TEXTURE0`到`GL_TEXTURE31`的范围之内，则会产生`GL_INVALID_ENUM` 错误。
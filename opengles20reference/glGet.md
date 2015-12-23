##Name

glGet — return the value or values of a selected parameter

##C Specification

void glGetBooleanv( GLenum pname,
    GLboolean * params);
 
##C Specification

void glGetFloatv(   GLenum pname,
    GLfloat * params);
 
##C Specification

void glGetIntegerv( GLenum pname,
    GLint * params);
 
##Parameters

- ***pname*** Specifies the parameter value to be returned. The symbolic constants in the list below are accepted.

- ***params***
Returns the value or values of the specified parameter.

###Description

These four commands return values for simple state variables in GL. pname is a symbolic constant indicating the state variable to be returned, and params is a pointer to an array of the indicated type in which to place the returned data.

Type conversion is performed if params has a different type than the state variable value being requested. If glGetBooleanv is called, a floating-point (or integer) value is converted to GL_FALSE if and only if it is 0.0 (or 0). Otherwise, it is converted to GL_TRUE. If glGetIntegerv is called, boolean values are returned as GL_TRUE or GL_FALSE, and most floating-point values are rounded to the nearest integer value. Floating-point colors and normals, however, are returned with a linear mapping that maps 1.0 to the most positive representable integer value and -1.0 to the most negative representable integer value. If glGetFloatv is called, boolean values are returned as GL_TRUE or GL_FALSE, and integer values are converted to floating-point values.

The following symbolic constants are accepted by pname:

`GL_ACTIVE_TEXTURE`
params returns a single value indicating the active multitexture unit. The initial value is GL_TEXTURE0. See glActiveTexture.

`GL_ALIASED_LINE_WIDTH_RANGE`
params returns two values, the smallest and largest supported widths for aliased lines. The range must include width 1.

`GL_ALIASED_POINT_SIZE_RANGE`
params returns two values, the smallest and largest supported sizes for aliased points. The range must include size 1.

`GL_ALPHA_BITS`
params returns one value, the number of alpha bitplanes in the color buffer of the currently bound framebuffer.

`GL_ARRAY_BUFFER_BINDING`
params returns a single value, the name of the buffer object currently bound to the target GL_ARRAY_BUFFER. If no buffer object is bound to this target, 0 is returned. The initial value is 0. See glBindBuffer.

`GL_BLEND`
params returns a single boolean value indicating whether blending is enabled. The initial value is GL_FALSE. See glBlendFunc.

`GL_BLEND_COLOR`
params returns four values, the red, green, blue, and alpha values which are the components of the blend color. See glBlendColor.

`GL_BLEND_DST_ALPHA`
params returns one value, the symbolic constant identifying the alpha destination blend function. The initial value is GL_ZERO. See glBlendFunc and glBlendFuncSeparate.

`GL_BLEND_DST_RGB`
params returns one value, the symbolic constant identifying the RGB destination blend function. The initial value is GL_ZERO. See glBlendFunc and glBlendFuncSeparate.

`GL_BLEND_EQUATION_ALPHA`
params returns one value, a symbolic constant indicating whether the Alpha blend equation is GL_FUNC_ADD, GL_FUNC_SUBTRACT, or GL_FUNC_REVERSE_SUBTRACT. See glBlendEquationSeparate.

`GL_BLEND_EQUATION_RGB`
params returns one value, a symbolic constant indicating whether the RGB blend equation is GL_FUNC_ADD, GL_FUNC_SUBTRACT, or GL_FUNC_REVERSE_SUBTRACT. See glBlendEquationSeparate.

`GL_BLEND_SRC_ALPHA`
params returns one value, the symbolic constant identifying the alpha source blend function. The initial value is GL_ONE. See glBlendFunc and glBlendFuncSeparate.

`GL_BLEND_SRC_RGB`
params returns one value, the symbolic constant identifying the RGB source blend function. The initial value is GL_ONE. See glBlendFunc and glBlendFuncSeparate.

`GL_BLUE_BITS`
params returns one value, the number of blue bitplanes in the color buffer of the currently bound framebuffer.

`GL_COLOR_CLEAR_VALUE`
params returns four values: the red, green, blue, and alpha values used to clear the color buffers. Integer values, if requested, are linearly mapped from the internal floating-point representation such that 1.0 returns the most positive representable integer value, and -1.0 returns the most negative representable integer value. The initial value is (0, 0, 0, 0). See glClearColor.

`GL_COLOR_WRITEMASK`
params returns four boolean values: the red, green, blue, and alpha write enables for the color buffers. The initial value is (GL_TRUE, GL_TRUE, GL_TRUE, GL_TRUE). See glColorMask.

`GL_COMPRESSED_TEXTURE_FORMATS`
params returns a list of symbolic constants of length GL_NUM_COMPRESSED_TEXTURE_FORMATS indicating which compressed texture formats are available. See glCompressedTexImage2D.

`GL_CULL_FACE`
params returns a single boolean value indicating whether polygon culling is enabled. The initial value is GL_FALSE. See glCullFace.

`GL_CULL_FACE_MODE`
params returns one value, a symbolic constant indicating which polygon faces are to be culled. The initial value is GL_BACK. See glCullFace.

`GL_CURRENT_PROGRAM`
params returns one value, the name of the program object that is currently active, or 0 if no program object is active. See glUseProgram.

`GL_DEPTH_BITS`
params returns one value, the number of bitplanes in the depth buffer of the currently bound framebuffer.

`GL_DEPTH_CLEAR_VALUE`
params returns one value, the value that is used to clear the depth buffer. Integer values, if requested, are linearly mapped from the internal floating-point representation such that 1.0 returns the most positive representable integer value, and -1.0 returns the most negative representable integer value. The initial value is 1. See glClearDepthf.

`GL_DEPTH_FUNC`
params returns one value, the symbolic constant that indicates the depth comparison function. The initial value is GL_LESS. See glDepthFunc.

`GL_DEPTH_RANGE`
params returns two values: the near and far mapping limits for the depth buffer. Integer values, if requested, are linearly mapped from the internal floating-point representation such that 1.0 returns the most positive representable integer value, and -1.0 returns the most negative representable integer value. The initial value is (0, 1). See glDepthRangef.

`GL_DEPTH_TEST`
params returns a single boolean value indicating whether depth testing of fragments is enabled. The initial value is GL_FALSE. See glDepthFunc and glDepthRangef.

`GL_DEPTH_WRITEMASK`
params returns a single boolean value indicating if the depth buffer is enabled for writing. The initial value is GL_TRUE. See glDepthMask.

`GL_DITHER`
params returns a single boolean value indicating whether dithering of fragment colors and indices is enabled. The initial value is GL_TRUE.

`GL_ELEMENT_ARRAY_BUFFER_BINDING`
params returns a single value, the name of the buffer object currently bound to the target GL_ELEMENT_ARRAY_BUFFER. If no buffer object is bound to this target, 0 is returned. The initial value is 0. See glBindBuffer.

`GL_FRAMEBUFFER_BINDING`
params returns a single value, the name of the currently bound framebuffer. The initial value is 0, indicating the default framebuffer. See glBindFramebuffer.

`GL_FRONT_FACE`
params returns one value, a symbolic constant indicating whether clockwise or counterclockwise polygon winding is treated as front-facing. The initial value is GL_CCW. See glFrontFace.

`GL_GENERATE_MIPMAP_HINT`
params returns one value, a symbolic constant indicating the mode of the mipmap generation filtering hint. The initial value is GL_DONT_CARE. See glHint.

`GL_GREEN_BITS`
params returns one value, the number of green bitplanes in the color buffer of the currently bound framebuffer.

`GL_IMPLEMENTATION_COLOR_READ_FORMAT`
params returns one value, the format chosen by the implementation in which pixels may be read from the color buffer of the currently bound framebuffer in conjunction with GL_IMPLEMENTATION_COLOR_READ_TYPE. In addition to this implementation-dependent format/type pair, format GL_RGBA in conjunction with type GL_UNSIGNED_BYTE is always allowed by every implementation, regardless of the currently bound render surface. See glReadPixels.

`GL_IMPLEMENTATION_COLOR_READ_TYPE`
params returns one value, the type chosen by the implementation with which pixels may be read from the color buffer of the currently bound framebuffer in conjunction with GL_IMPLEMENTATION_COLOR_READ_FORMAT. In addition to this implementation-dependent format/type pair, format GL_RGBA in conjunction with type GL_UNSIGNED_BYTE is always allowed by every implementation, regardless of the currently bound render surface. See glReadPixels.

`GL_LINE_WIDTH`
params returns one value, the line width as specified with glLineWidth. The initial value is 1.

`GL_MAX_COMBINED_TEXTURE_IMAGE_UNITS`
params returns one value, the maximum supported texture image units that can be used to access texture maps from the vertex shader and the fragment processor combined. If both the vertex shader and the fragment processing stage access the same texture image unit, then that counts as using two texture image units against this limit. The value must be at least 8. See glActiveTexture.

`GL_MAX_CUBE_MAP_TEXTURE_SIZE`
params returns one value. The value gives a rough estimate of the largest cube-map texture that the GL can handle. The value must be at least 16. See glTexImage2D.

`GL_MAX_FRAGMENT_UNIFORM_VECTORS`
params returns one value, the maximum number of four-element floating-point, integer, or boolean vectors that can be held in uniform variable storage for a fragment shader. The value must be at least 16. See glUniform.

`GL_MAX_RENDERBUFFER_SIZE`
params returns one value. The value indicates the largest renderbuffer width and height that the GL can handle. The value must be at least 1. See glRenderbufferStorage.

`GL_MAX_TEXTURE_IMAGE_UNITS`
params returns one value, the maximum supported texture image units that can be used to access texture maps from the fragment shader. The value must be at least 8. See glActiveTexture.

`GL_MAX_TEXTURE_SIZE`
params returns one value. The value gives a rough estimate of the largest texture that the GL can handle. The value must be at least 64. See glTexImage2D.

`GL_MAX_VARYING_VECTORS`
params returns one value, the maximum number four-element floating-point vectors available for interpolating varying variables used by vertex and fragment shaders. Varying variables declared as matrices or arrays will consume multiple interpolators. The value must be at least 8.

`GL_MAX_VERTEX_ATTRIBS`
params returns one value, the maximum number of 4-component generic vertex attributes accessible to a vertex shader. The value must be at least 8. See glVertexAttrib.

`GL_MAX_VERTEX_TEXTURE_IMAGE_UNITS`
params returns one value, the maximum supported texture image units that can be used to access texture maps from the vertex shader. The value may be 0. See glActiveTexture.

`GL_MAX_VERTEX_UNIFORM_VECTORS`
params returns one value, the maximum number of four-element floating-point, integer, or boolean vectors that can be held in uniform variable storage for a vertex shader. The value must be at least 128. See glUniform.

`GL_MAX_VIEWPORT_DIMS`
params returns two values: the maximum supported width and height of the viewport. These must be at least as large as the visible dimensions of the display being rendered to. See glViewport.

`GL_NUM_COMPRESSED_TEXTURE_FORMATS`
params returns a single integer value indicating the number of available compressed texture formats. The minimum value is 0. See glCompressedTexImage2D.

`GL_NUM_SHADER_BINARY_FORMATS`
params returns a single integer value indicating the number of available shader binary formats. The minimum value is 0. See glShaderBinary.

`GL_PACK_ALIGNMENT`
params returns one value, the byte alignment used for writing pixel data to memory. The initial value is 4. See glPixelStorei.

`GL_POLYGON_OFFSET_FACTOR`
params returns one value, the scaling factor used to determine the variable offset that is added to the depth value of each fragment generated when a polygon is rasterized. The initial value is 0. See glPolygonOffset.

`GL_POLYGON_OFFSET_FILL`
params returns a single boolean value indicating whether polygon offset is enabled for polygons in fill mode. The initial value is GL_FALSE. See glPolygonOffset.

`GL_POLYGON_OFFSET_UNITS`
params returns one value. This value is multiplied by an implementation-specific value and then added to the depth value of each fragment generated when a polygon is rasterized. The initial value is 0. See glPolygonOffset.

`GL_RED_BITS`
params returns one value, the number of red bitplanes in the color buffer of the currently bound framebuffer.

`GL_RENDERBUFFER_BINDING`
params returns a single value, the name of the currently bound renderbuffer. The initial value is 0, indicating no renderbuffer is bound. See glBindRenderbuffer.

`GL_SAMPLE_ALPHA_TO_COVERAGE`
params returns a single boolean value indicating if the fragment coverage value should be ANDed with a temporary coverage value based on the fragment's alpha value. The initial value is GL_FALSE. See glSampleCoverage.

`GL_SAMPLE_BUFFERS`
params returns a single integer value indicating the number of sample buffers associated with the currently bound framebuffer. See glSampleCoverage.

`GL_SAMPLE_COVERAGE`
params returns a single boolean value indicating if the fragment coverage value should be ANDed with a temporary coverage value based on the current sample coverage value. The initial value is GL_FALSE. See glSampleCoverage.

`GL_SAMPLE_COVERAGE_INVERT`
params returns a single boolean value indicating if the temporary coverage value should be inverted. See glSampleCoverage.

`GL_SAMPLE_COVERAGE_VALUE`
params returns a single positive floating-point value indicating the current sample coverage value. See glSampleCoverage.

`GL_SAMPLES`
params returns a single integer value indicating the coverage mask size of the currently bound framebuffer. See glSampleCoverage.

`GL_SCISSOR_BOX`
params returns four values: the x and y window coordinates of the scissor box, followed by its width and height. Initially the x and y window coordinates are both 0 and the width and height are set to the size of the window. See glScissor.

`GL_SCISSOR_TEST`
params returns a single boolean value indicating whether scissoring is enabled. The initial value is GL_FALSE. See glScissor.

`GL_SHADER_BINARY_FORMATS`
params returns a list of symbolic constants of length GL_NUM_SHADER_BINARY_FORMATS indicating which shader binary formats are available. See glShaderBinary.

`GL_SHADER_COMPILER`
params returns a single boolean value indicating whether a shader compiler is supported. GL_FALSE indicates that any call to glShaderSource, glCompileShader, or glReleaseShaderCompiler will result in a GL_INVALID_OPERATION error being generated.

`GL_STENCIL_BACK_FAIL`
params returns one value, a symbolic constant indicating what action is taken for back-facing polygons when the stencil test fails. The initial value is GL_KEEP. See glStencilOpSeparate.

`GL_STENCIL_BACK_FUNC`
params returns one value, a symbolic constant indicating what function is used for back-facing polygons to compare the stencil reference value with the stencil buffer value. The initial value is GL_ALWAYS. See glStencilFuncSeparate.

`GL_STENCIL_BACK_PASS_DEPTH_FAIL`
params returns one value, a symbolic constant indicating what action is taken for back-facing polygons when the stencil test passes, but the depth test fails. The initial value is GL_KEEP. See glStencilOpSeparate.

`GL_STENCIL_BACK_PASS_DEPTH_PASS`
params returns one value, a symbolic constant indicating what action is taken for back-facing polygons when the stencil test passes and the depth test passes. The initial value is GL_KEEP. See glStencilOpSeparate.

`GL_STENCIL_BACK_REF`
params returns one value, the reference value that is compared with the contents of the stencil buffer for back-facing polygons. The initial value is 0. See glStencilFuncSeparate.

`GL_STENCIL_BACK_VALUE_MASK`
params returns one value, the mask that is used for back-facing polygons to mask both the stencil reference value and the stencil buffer value before they are compared. The initial value is all 1's. See glStencilFuncSeparate.

`GL_STENCIL_BACK_WRITEMASK`
params returns one value, the mask that controls writing of the stencil bitplanes for back-facing polygons. The initial value is all 1's. See glStencilMaskSeparate.

`GL_STENCIL_BITS`
params returns one value, the number of bitplanes in the stencil buffer of the currently bound framebuffer.

`GL_STENCIL_CLEAR_VALUE`
params returns one value, the index to which the stencil bitplanes are cleared. The initial value is 0. See glClearStencil.

`GL_STENCIL_FAIL`
params returns one value, a symbolic constant indicating what action is taken when the stencil test fails for front-facing polygons and non-polygons. The initial value is GL_KEEP. See glStencilOp and glStencilOpSeparate.

`GL_STENCIL_FUNC`
params returns one value, a symbolic constant indicating what function is used to compare the stencil reference value with the stencil buffer value for front-facing polygons and non-polygons. The initial value is GL_ALWAYS. See glStencilFunc and glStencilFuncSeparate.

`GL_STENCIL_PASS_DEPTH_FAIL`
params returns one value, a symbolic constant indicating what action is taken when the stencil test passes, but the depth test fails for front-facing polygons and non-polygons. The initial value is GL_KEEP. See glStencilOp and glStencilOpSeparate.

`GL_STENCIL_PASS_DEPTH_PASS`
params returns one value, a symbolic constant indicating what action is taken when the stencil test passes and the depth test passes for front-facing polygons and non-polygons. The initial value is GL_KEEP. See glStencilOp and glStencilOpSeparate.

`GL_STENCIL_REF`
params returns one value, the reference value that is compared with the contents of the stencil buffer for front-facing polygons and non-polygons. The initial value is 0. See glStencilFunc and glStencilFuncSeparate.

`GL_STENCIL_TEST`
params returns a single boolean value indicating whether stencil testing of fragments is enabled. The initial value is GL_FALSE. See glStencilFunc and glStencilOp.

`GL_STENCIL_VALUE_MASK`
params returns one value, the mask that is used to mask both the stencil reference value and the stencil buffer value before they are compared for front-facing polygons and non-polygons. The initial value is all 1's. See glStencilFunc and glStencilFuncSeparate.

`GL_STENCIL_WRITEMASK`
params returns one value, the mask that controls writing of the stencil bitplanes for front-facing polygons and non-polygons. The initial value is all 1's. See glStencilMask and glStencilMaskSeparate.

`GL_SUBPIXEL_BITS`
params returns one value, an estimate of the number of bits of subpixel resolution that are used to position rasterized geometry in window coordinates. The value must be at least 4.

`GL_TEXTURE_BINDING_2D`
params returns a single value, the name of the texture currently bound to the target GL_TEXTURE_2D for the active multitexture unit. The initial value is 0. See glBindTexture.

`GL_TEXTURE_BINDING_CUBE_MAP`
params returns a single value, the name of the texture currently bound to the target GL_TEXTURE_CUBE_MAP for the active multitexture unit. The initial value is 0. See glBindTexture.

`GL_UNPACK_ALIGNMENT`
params returns one value, the byte alignment used for reading pixel data from memory. The initial value is 4. See glPixelStorei.

`GL_VIEWPORT`
params returns four values: the x and y window coordinates of the viewport, followed by its width and height. Initially the x and y window coordinates are both set to 0, and the width and height are set to the width and height of the window into which the GL will do its rendering. See glViewport.

Many of the boolean parameters can also be queried more easily using glIsEnabled.

##Errors

GL_INVALID_ENUM is generated if pname is not one of the values listed previously.

##See Also

glGetActiveAttrib, glGetActiveUniform, glGetAttachedShaders, glGetAttribLocation, glGetBufferParameteriv, glGetError, glGetFramebufferAttachmentParameteriv, glGetProgramiv, glGetProgramInfoLog, glGetRenderbufferParameteriv, glGetShaderiv, glGetShaderInfoLog, glGetShaderSource, glGetString, glGetTexParameter, glGetUniform, glGetUniformLocation, glGetVertexAttrib, glGetVertexAttribPointerv, glIsEnabled